# LDAP Enumeration

First, forwarding the port so I can do some ldap enumeration. To get to this fancy menu, I can reference [this handy reference](https://www.sans.org/blog/using-the-ssh-konami-code-ssh-control-sequences/), and by hitting `Enter` on the command line to make sure I'm at a blank line, I then hit `~C` to get a `ssh> ` prompt. From there I can forward a port!

![Start Forwarding](/img/obj8-4/img1.png)

Then, using `ldapsearch` on my tunnel

![Using ldapsearch](/img/obj8-4/img2.png)

Just to get the naming contexts! Now I know the domain! Unfortunately that was all the information I could glean from this LDAP server, as anonymous binds were not allowed. Oh well, onto more enumeration!