# Terminal Grepping for Gold

The questions:

```text
Howdy howdy!  Mind helping me with this homew- er, challenge?
Someone ran nmap -oG on a big network and produced this bigscan.gnmap file.
The quizme program has the questions and hints and, incidentally,
has NOTHING to do with an Elf University assignment. Thanks!

Answer all the questions in the quizme executable:
- What port does 34.76.1.22 have open?
- What port does 34.77.207.226 have open?
- How many hosts appear "Up" in the scan?
- How many hosts have a web port open?  (Let's just use TCP ports 80, 443, and 8080)
- How many hosts with status Up have no (detected) open TCP ports?
- What's the greatest number of TCP ports any one host has open?

Check out bigscan.gnmap and type quizme to answer each question.
```

## To get the first question:
`grep 34.76.1.22 ./bigscan.gnmap`

```sh
elf@7781f0dee573:~$ grep 34.76.1.22 ./bigscan.gnmap 
Host: 34.76.1.22 ()     Status: Up
Host: 34.76.1.22 ()     Ports: 62078/open/tcp//iphone-sync///      Ignored State: closed (999)
```

## Second question
```sh
elf@7781f0dee573:~$ grep 34.77.207.226 ./bigscan.gnmap 
Host: 34.77.207.226 ()     Status: Up
Host: 34.77.207.226 ()     Ports: 8080/open/tcp//http-proxy///      Ignored State: filtered (999)
```

## Third question

```sh
elf@7781f0dee573:~$ grep "Status: Up" ./bigscan.gnmap | sort | uniq | wc -l
26054
```

## Fourth question
```sh
elf@0e70aef3f715:~$ egrep '(80\/|443\/|8080\/)' ./bigscan.gnmap  | wc -l
14372
```
Logic above needs a trailing slash because otherwise 80 can be part of an IP address.

## Fifth question (I am a Linux GOD)

```sh
elf@6728125b0666:~$ grep "Host:" ./bigscan.gnmap | cut -f1 -d'(' | sort| uniq -c | grep -E '^ *1 ' | wc -l
402
```

The logic to the above: Grep everything that has the word "Host:" in the line, since if it is listed here at least once it is detected.

Then, split the results by cutting it from the '(' character in the '()'. Remeber that the results look like this:

```sh
Host: 34.76.1.22 ()     Status: Up
Host: 34.76.1.22 ()     Ports: 62078/open/tcp//iphone-sync///      Ignored State: closed (999)
```

Since if no ports are detected, the new instance of the host IP will not appear twice. So I only care about it if the `Host:` line appears ONLY ONCE.

Pipe the results to `sort`, then `uniq -c` to prepend a count number. I only care about it if the count is 1. So use `grep` again to ONLY look for a count of 1! Then get a wordcount!

## Sixth (and final) question

```sh
elf@70ebc5c42816:~$ for i in $(grep Ports: ./bigscan.gnmap | cut -f3 -d: | sed -e 's/Ignored State//g' | sed -e 's/ //g'); do echo -n $i | awk -F',' "{ print NF }"; done | sort -n | uniq | tail
3
4
5
6
7
8
9
10
11
12
```

Answer is `12`! Logic here:

`for i in $(...)` -- Loop over the result of...

`grep Ports: ./bigscan.gnmap` -- Any line that mentions "Ports:"

`cut -f3 -d:` -- Show only field 3 when delimiting the line by `:`'s.
`sed -e 's/Ignored State//g'` -- Remove the line about "Ignored State"
`sed -e 's/ //g')` -- remove any whitespace

Take the results of that, then loop over each line. On each line, run:

`echo -n $i` -- Print the line for each loop iteration
`awk -F',' "{ print NF }"` -- Print the number of fields delimited by the `,` character

Take the results of the above loop, then...
`sort -n` -- sort numerically
`uniq` -- show only unique numbers
`tail` -- Only show the last 10 lines.