# Izzat you, AD Server?

Typically, an AD server has port `88` open.

Since I knew the general range of ports here, I ran:

`nmap -PS88 -p 88 10.128.1-3.1-255 -oG - | grep open`

And the output:

```sh
nfjhsxqtcz@grades:~$ nmap -PS88 -p 88 10.128.1-3.1-255 -oG - | grep open
Host: 10.128.1.53 (hhc21-windows-dc.c.holidayhack2021.internal) Ports: 88/open/tcp//kerberos-sec///
Host: 10.128.3.30 ()    Ports: 88/open/tcp//kerberos-sec///

```

Two potential active directory servers! Or at least two servers that have Kerberos listening anyway.

Scanning all ports on the machines: note that I had to add the `-Pn` flag to `10.128.1.53` because it was blocking ping. Took a while to scan but the results were:

```sh
nfjhsxqtcz@grades:~$ nmap -Pn -sC -sV 10.128.1.53
Starting Nmap 7.80 ( https://nmap.org ) at 2021-12-27 15:51 UTC
Nmap scan report for hhc21-windows-dc.c.holidayhack2021.internal (10.128.1.53)
Host is up (0.00035s latency).
Not shown: 988 filtered ports
PORT     STATE SERVICE       VERSION
53/tcp   open  domain?
| fingerprint-strings: 
|   DNSVersionBindReqTCP: 
|     version
|_    bind
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2021-12-27 15:51:45Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: elfu.local0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: elfu.local0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: ELFU
|   NetBIOS_Domain_Name: ELFU
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: elfu.local
|   DNS_Computer_Name: DC01.elfu.local
|   DNS_Tree_Name: elfu.local
|   Product_Version: 10.0.17763
|_  System_Time: 2021-12-27T15:54:00+00:00
| ssl-cert: Subject: commonName=DC01.elfu.local
| Not valid before: 2021-10-28T19:21:37
|_Not valid after:  2022-04-29T19:21:37
|_ssl-date: 2021-12-27T15:54:40+00:00; 0s from scanner time.
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.80%I=7%D=12/27%Time=61C9E116%P=x86_64-pc-linux-gnu%r(DNS
SF:VersionBindReqTCP,20,"\0\x1e\0\x06\x81\x04\0\x01\0\0\0\0\0\0\x07version
SF:\x04bind\0\0\x10\0\x03");
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-12-27T15:54:04
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 238.48 seconds
```

And finally, scanning the second AD server I didn't have to use the `-Pn` flag so I could get a quicker scan result back:

```sh
nfjhsxqtcz@grades:~$ nmap -sC -sV 10.128.3.30
Starting Nmap 7.80 ( https://nmap.org ) at 2021-12-15 20:48 UTC
Nmap scan report for 10.128.3.30
Host is up (0.00022s latency).
Not shown: 966 closed ports
PORT     STATE SERVICE      VERSION
22/tcp   open  ssh          OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 9b:3f:f6:9b:fa:21:9d:77:cd:69:be:85:98:28:ff:a7 (RSA)
|   256 77:90:ab:a9:07:a9:23:c4:d4:52:83:b3:fd:20:1e:9c (ECDSA)
|_  256 58:3c:f3:ee:82:02:cc:89:51:87:da:83:11:07:74:24 (ED25519)
53/tcp   open  domain       (generic dns response: NOTIMP)
| fingerprint-strings: 
|   DNSVersionBindReqTCP: 
|     version
|_    bind
80/tcp   open  http         Werkzeug httpd 2.0.2 (Python 3.8.10)
|_http-server-header: Werkzeug/2.0.2 Python/3.8.10
| http-title: Site doesn't have a title (text/html; charset=utf-8).
|_Requested resource was http://10.128.3.30/register
88/tcp   open  kerberos-sec Heimdal Kerberos (server time: 2021-12-15 20:48:16Z)
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Samba smbd 3.X - 4.X (workgroup: ELFU)
389/tcp  open  ldap         (Anonymous bind OK)
| ssl-cert: Subject: commonName=SHARE30.elfu.local/organizationName=Samba Administration
| Not valid before: 2021-10-29T19:30:08
|_Not valid after:  2023-09-29T19:30:08
|_ssl-date: 2021-12-15T20:46:12+00:00; -3m00s from scanner time.
445/tcp  open  netbios-ssn  Samba smbd 4.3.11-Ubuntu (workgroup: ELFU)
464/tcp  open  kpasswd5?
636/tcp  open  ssl/ldap     (Anonymous bind OK)
| ssl-cert: Subject: commonName=SHARE30.elfu.local/organizationName=Samba Administration
| Not valid before: 2021-10-29T19:30:08
|_Not valid after:  2023-09-29T19:30:08
|_ssl-date: 2021-12-15T20:46:46+00:00; -2m26s from scanner time.
1024/tcp open  msrpc        Microsoft Windows RPC
1025/tcp open  tcpwrapped
1026/tcp open  tcpwrapped
1027/tcp open  tcpwrapped
1028/tcp open  tcpwrapped
1029/tcp open  tcpwrapped
1030/tcp open  tcpwrapped
1031/tcp open  tcpwrapped
1032/tcp open  tcpwrapped
1033/tcp open  tcpwrapped
1034/tcp open  tcpwrapped
1035/tcp open  tcpwrapped
1036/tcp open  tcpwrapped
1037/tcp open  tcpwrapped
1038/tcp open  tcpwrapped
1039/tcp open  tcpwrapped
1040/tcp open  tcpwrapped
1041/tcp open  tcpwrapped
1042/tcp open  tcpwrapped
1043/tcp open  tcpwrapped
1044/tcp open  tcpwrapped
2222/tcp open  ssh          OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
3268/tcp open  ldap         (Anonymous bind OK)
| ssl-cert: Subject: commonName=SHARE30.elfu.local/organizationName=Samba Administration
| Not valid before: 2021-10-29T19:30:08
|_Not valid after:  2023-09-29T19:30:08
|_ssl-date: 2021-12-15T20:48:08+00:00; -1m04s from scanner time.
3269/tcp open  ssl/ldap     (Anonymous bind OK)
| ssl-cert: Subject: commonName=SHARE30.elfu.local/organizationName=Samba Administration
| Not valid before: 2021-10-29T19:30:08
|_Not valid after:  2023-09-29T19:30:08
|_ssl-date: 2021-12-15T20:49:17+00:00; +5s from scanner time.
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.80%I=7%D=12/15%Time=61BA5495%P=x86_64-pc-linux-gnu%r(DNS
SF:VersionBindReqTCP,2B,"\0\)\0\x06\x81\x80\0\x01\0\0\0\0\0\x01\x07version
SF:\x04bind\0\0\x10\0\x03\0\0\)\x02\0\0\0\0\0\0\0")%r(DNSStatusRequestTCP,
SF:E,"\0\x0c\0\0\x90\x04\0\0\0\0\0\0\0\0");
Service Info: Host: SHARE30; OSs: Linux, Windows; CPE: cpe:/o:linux:linux_kernel, cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -54s, deviation: 1m18s, median: 0s
|_nbstat: NetBIOS name: SHARE30, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: share30
|   NetBIOS computer name: SHARE30\x00
|   Domain name: elfu.local
|   FQDN: share30.elfu.local
|_  System time: 2021-12-15T20:49:04+00:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-12-15T20:49:04
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 63.34 seconds
```

Two AD servers! Let's do a bit more enumeration here!