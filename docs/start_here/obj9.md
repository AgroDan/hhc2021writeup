# Chapter IX

Ah yes, wouldn't be a Holiday Hack Challenge without a Splunk exercise! Good thing I have the experience for this from elsewhere. I am instructed to help Angel Candysalt to solve a Splunk challenge. Before that however, I should first visit Fitzy Shortstack in Santa's lobby, as he knows a thing or two about Splunk. So on to the lobby!

## Yara Analysis

![Fitzy Shortstack](../img/start/img27.png)

Fitzy stands beside a lovely Christmas tree and a "Yara Analysis" terminal challenge.

!!! quote "Fitzy Shortstack"
    Hiya, I'm Fitzy Shorstack!

    I was just trying to learn a bit more about YARA with this here Cranberry Pi terminal.

    I mean, I'm not saying I'm worried about attack threats from that other con next door, but...

    OK. I AM worried. I've been thinking a bit about how malware might bypass YARA rules.

    If you can help me solve the issue in this terminal, I'll understand YARA so much better! Would you please check it out so I can learn?

    And, I'll tell you what -- if you help me with YARA, I'll give you some tips for Splunk!

    I think if you make small, innocuous changes to the executable, you can get it to run in spite of the YARA rules.

Okay Fitzy, you're on. Time to complete the [Yara Analysis Terminal Challenge](../term_ya.md)

## Splunk!

Upon completing that, I get some new dialogue!

!!! quote "Fitzy Shortstack"
    Thanks - you figured it out!

    Let me tell you what I know about Splunk.

    Did you know Splunk recently added support for new data sources includeing Sysmon for linux and GitHub Audit Log data?

    Between Github audit log and webhook event recording, you can monitor all activity in a repository, including common git commands such as `git add`, `git status`, and `git commit`.

    You can also see cloned GitHub projects. There's a lot of interesting stuff out there. Did you know there are repositories of code that are Darn Vulnerable?

    Sysmon provides a lot of valuable data, but sometimes correlation across data types is still necessary.

    Sysmon network events don't reveal the process parent ID for example. Fortunately, we can pivot with a query to investigate process creation events once you get a process ID.

    Sometimes Sysmon data collection is awkward. Pipelining multiple commands generates multiple Sysmon events, for example.

    Did you know there are multiple versions of the Netcat command that can be used maliciously? `nc.openbsd` for example.

Alrighty. Well, on to visiting Angel Candysalt in Santa's Great Room!

![Angel Candysalt](../img/start/img28.png)

!!! quote "Angel Candysalt"
    Greetings North Pole visitor! I'm Angel Candysalt!

    A euphamism? No, that's my name. Why do people ask me that?

    Anywho, I'm back at Santa's Splunk terminal again this year.

    There's always more to learn!

    Take a look and see what you can find this year.

    With who-knows-what going on next door, it never hurts to have sharp SIEM skills!

Okay Angel, time to finish [the Splunk Objective](../obj9.md)!

Upon completing that, Angel is happy and celebrates my victory with a "Yay! You did it!"

Sorry Angel, no time to celebrate. Christmas isn't going to save itself. Onto [Objective 10!](obj10.md)!