# Bonus! Blue Log4Jack

A bonus Blue Team event appears surrounding the Log4j debacle!

Starts out with:

![RU Ready?](img/bonus_blue/img1.png)

After hitting yes

![After hitting yes](img/bonus_blue/img2.png)

After typing `next`

![After typing next](img/bonus_blue/img3.png)

After running `ls`

![After running ls](img/bonus_blue/img4.png)

After running `cd vulnerable`

![After running cd vulnerable](img/bonus_blue/img5.png)

Listing files in that directory: `ls`

![Listing files](img/bonus_blue/img6.png)

Displaying the contents of `DisplayFilev1.java`

![Display contents of java file](img/bonus_blue/img7.png)

Compiled the java with `javac DisplayFilev1.java`

![Compiling java](img/bonus_blue/img8.png)

Running the program with `java DisplayFilev1 testfile.txt`:

![Running the program](img/bonus_blue/img9.png)

Now trying to read a file that isn't there, forcing an exception:

![Forcing Exception](img/bonus_blue/img10.png)

Running `next`

![Running next](img/bonus_blue/img11.png)

Displaying the contents of a java program that properly utilizes the `log4j` utility.

![Display contents of java program](img/bonus_blue/img12.png)

Running `next`

![Running next](img/bonus_blue/img13.png)

Compling the new code with `javac DisplayFilev2.java`

![Compiling again](img/bonus_blue/img14.png)

Forcing it to fail by reading a file that doesn't exist:

![Forcing it to fail](img/bonus_blue/img15.png)

Running `next`

![Running next](img/bonus_blue/img16.png)

Injecting code via Log4j and displaying the java version

![Injecting code via log4j](img/bonus_blue/img17.png)

Even more scary stuff you can do with this vulnerability

![Even more scary stuff](img/bonus_blue/img18.png)

After typing `next`

![After typing next](img/bonus_blue/img19.png)

After running `startserver.sh`

![Running startserver.sh](img/bonus_blue/img20.png)

Exploiting and showing how an LDAP lookup can be created

![Exploiting via ldap](img/bonus_blue/img21.png)

Hitting ++ctrl+c++ backs out of everything

![Back out of everything](img/bonus_blue/img22.png)

`cd` into `~/patched`

![cd into patched](img/bonus_blue/img23.png)

Listing the contents of the directory

![Listing contents](img/bonus_blue/img24.png)

After sourcing the new classpath with `source claspath.sh`

![Sourcing new classpath](img/bonus_blue/img25.png)

Compiling the code with `javac DisplayFilev2.java`

![Compiling the code](img/bonus_blue/img26.png)

Now it doesn't work:

![it don't work](img/bonus_blue/img27.png)

Running `cd` to return to the home dir

![cd to return to home dir](img/bonus_blue/img28.png)

Running `log4j2-scan ./vulnerable` from the home dir

![Running log4j2-scan](img/bonus_blue/img29.png)

Running the same command on the `~/patched` dir

![Running same command in patched](img/bonus_blue/img30.png)

Running the command under `/var/log/solr`

![Running the command under /var/log/solr](img/bonus_blue/img31.png)

After running `next`

![After running next](img/bonus_blue/img32.png)


After running `ls /var/log/www` and seeing only one file there, `access.log`

![After running ls /var/log/www](img/bonus_blue/img33.png)


After examining `log4shell-search.sh`

![After examining log4shell-search.sh](img/bonus_blue/img34.png)


After running `log4shell-search.sh /var/log/www/access.log`

![After running log4shell-search.sh /var/log/www/access.log](img/bonus_blue/img35.png)


After running `./logshell-search.sh /var/log/www | sed '1!d'`

![After getting one line of output](img/bonus_blue/img36.png)


After running `./logshell-search.sh /var/log/www | sed '2!d'`

![After getting second line of output](img/bonus_blue/img37.png)


After running  `./logshell-search.sh /var/log/www | sed '3!d`

![After getting 3rd line of output](img/bonus_blue/img38.png)


After hitting `next`

![After hitting next](img/bonus_blue/img39.png)

