# Initial

Access to the site:

![Access](/img/obj8-2/img1.png)

```text
username: nfjhsxqtcz
password: Anuakviba@

ssh nfjhsxqtcz@grades.elfu.org -p 2222
```

??? note "Continuity Disclaimer"
    You may see me interchangeably using different randomly-generated usernames and passwords. This is because I had to log in at a later date and get screenshots or documentation on this challenge after the fact and a new username/password combination was randomly assigned in the process. Apologies for the confusion.

Connecting via SSH as it instructs you gives you access to a menu:

```sh
===================================================
=      Elf University Student Grades Portal       =
=          (Reverts Everyday 12am EST)            =
===================================================
1. Print Current Courses/Grades.
e. Exit
: 
```

If I type `1` to read my current courses and grades, it refreshes the screen and displays:

```sh
0  Shortname                  Description  Grade
================================================
1    NPAR101  North Pole Art Appreciation     C+
2    REIH201           Reindeer Husbandry     C 
3    WHOL201     World Holiday Literature     C+
4    CACH301              Candy Chemistry     C+
Press Enter to continue...

```

Man, I didn't realize what a C student I was. Especially disappointing in the Candy Chemistry category. I really like candy.

After a fair a bit of hemming and hawing over how much of a C student I was, I discovered that this particular menu situation was simply a python intepreter. If I hit ++ctrl+c++ it would complain that I could exit by typing in `exit`. So it traps the SIGKILL signal, but what about the EOF statement? What happens if I hit ++ctrl+d++? Well of course it kills the application but leaves me in an interactive python prompt!

```sh
===================================================
=      Elf University Student Grades Portal       =
=          (Reverts Everyday 12am EST)            =
===================================================
1. Print Current Courses/Grades.
e. Exit
: Traceback (most recent call last):
  File "/opt/grading_system", line 41, in <module>
    main()
  File "/opt/grading_system", line 26, in main
    a = input(": ").lower().strip()
EOFError
>>> 
```

So, to dump to a shell:

```python
import pty
pty.spawn("/bin/bash")
```

Finally, after obtaining shell access, I changed my shell to something more sensible than this python script:

```sh
nfjhsxqtcz@grades:~$ chsh
Password: 
Changing the login shell for nfjhsxqtcz
Enter the new value, or press ENTER for the default
    Login Shell [/opt/grading_system]: /bin/bash
nfjhsxqtcz@grades:~$ 
```

Now with that out of the way, I logged out and logged back in, because with the python shell trapping my SIGINT and SIGSTOP signals it became annoying if I ran something that took so long it needed to be killed. Plus I now had the ability to `scp` files up and down, so it worked out for the best.

Just for funsies, I snagged the code used to create the interactive prompt:

```python
#!/usr/bin/python3 -i
# Created by:
# Alabaster Snowball
import signal
import os
import grades
from pandas import *
from termcolor import colored, cprint

def signal_handler(sig, frame):
    print("You may only type 'exit' to leave the exam!")

signal.signal(signal.SIGINT, signal_handler)
signal.signal(signal.SIGTSTP, signal_handler)

def main():
    os.umask(7)
    os.system('/usr/bin/clear')
    while True:
        cprint("===================================================", "cyan")
        cprint("=      Elf University Student Grades Portal       =", "cyan")
        cprint("=          (Reverts Everyday 12am EST)            =", "cyan")
        cprint("===================================================", "cyan")
        cprint("1. Print Current Courses/Grades.", "green")
        cprint("e. Exit", "green")
        a = input(": ").lower().strip()
        if a.startswith("1"):
            os.system('/usr/bin/clear')
            user_grades = grades.get_grades()
            formatted_user_grades = [[user_grades[key][0], user_grades[key][1], user_grades[key][2]] for key in user_grades.keys()]
            formatted_user_grades.insert(0,["Shortname","Description","Grade"])
            lines = str(DataFrame(formatted_user_grades)).split('\n')[1:]
            lines.insert(1,"="* len(lines[0]))
            cprint('\n'.join(lines), 'yellow')
            a = input("Press Enter to continue...").lower().strip()
        elif a.startswith("e"):
            os.kill(os.getpid(), 9)
        os.system('/usr/bin/clear')

if __name__ == "__main__":
    main()
```

And since it's calling the `grades` module, looking through the OS I was able to find the module itself in `/usr/lib/python3.8/grades.py`. Here's the source code!

```python
#!/usr/bin/env python3
import getpass
import os
import random
import ast

def get_grades():
    possible_class_titles = [
        ['REIH','Reindeer Husbandry'],
        ['SLPE','Sleigh Propulsion Engineering'],
        ['GEOG','Geometry of Gift-Wrapping'],
        ['CACH','Candy Chemistry'],
        ['WHOL','World Holiday Literature'],
        ['NPAR','North Pole Art Appreciation'],
        ['ELFS','Elf Studies'],
        ['ESCV','Escape vim'],
        ['PRDL','Present Delivery Logistics'],
        ['NNLM','Naughty Nice List Mathematics']
    ]
    possible_class_numbers = ['101','201','301']
    possible_grades = ['F','D','C','B','A']
    possible_modifiers = ['-','+',' ']
    home = f"/home/{getpass.getuser()}"
    gfile = f"{home}/.grades"
    final_grades = {}
    for i in range(random.randrange(4,6)):
        c = random.choice(possible_class_titles)
        while c[0] in final_grades:
            c = random.choice(possible_class_titles)
        final_grades[ c[0] ] = [c[0] + random.choice(possible_class_numbers), c[1], (random.choice(possible_grades) + random.choice(possible_modifiers)).replace("F-",'F ').replace("F+",'F ')]
        # Shortname, Descr, Grade
    if os.path.isfile(gfile):
        try:
            final_grades = ast.literal_eval(open(gfile,'r').read())
        except:
            pass
    else:
        try:
            gf = open(gfile,'w')
            gf.write(repr(final_grades))
            gf.close()
        except:
            pass
    return final_grades
```

Just some fun 4th-wall-breaking stuff. Anyway, onto the challenge!

Noticed that according to `/etc/shells`, `powershell` is a valid shell.

Routing tables shows a particularly interesting set of routes:

```sh
PS /home/nfjhsxqtcz> route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         172.17.0.1      0.0.0.0         UG    0      0        0 eth0
10.128.1.0      172.17.0.1      255.255.255.0   UG    0      0        0 eth0
10.128.2.0      172.17.0.1      255.255.255.0   UG    0      0        0 eth0
10.128.3.0      172.17.0.1      255.255.255.0   UG    0      0        0 eth0
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 eth0
```

From this point, I started to perform a host lookup scan. To accomplish this, I ran the following: `nmap -sn -oG ping-sweep 10.128.1-3.1-255`

And it returned:

```text
Nmap scan report for 10.128.2.3
Host is up (0.00046s latency).
Nmap scan report for 10.128.2.4
Host is up (0.00039s latency).
Nmap scan report for 10.128.2.5
Host is up (0.00035s latency).
Nmap scan report for 10.128.2.6
Host is up (0.00031s latency).
Nmap scan report for 10.128.2.7
Host is up (0.00028s latency).
Nmap scan report for 10.128.2.8
Host is up (0.00023s latency).
Nmap scan report for 10.128.2.9
Host is up (0.00018s latency).
Nmap scan report for 10.128.2.10
Host is up (0.00013s latency).
Nmap scan report for 10.128.2.11
Host is up (0.000079s latency).
Nmap scan report for 10.128.2.12
Host is up (0.0010s latency).
Nmap scan report for 10.128.2.13
Host is up (0.00094s latency).

 << snipped in the interest of space >>

Nmap scan report for 10.128.3.58
Host is up (0.0015s latency).
Nmap scan report for 10.128.3.59
Host is up (0.0014s latency).
Nmap scan report for 10.128.3.60
Host is up (0.0013s latency).
```

So...a bunch of hosts. I'm going to have to narrow this down some. Gotta see if there's an AD server to interrogate!