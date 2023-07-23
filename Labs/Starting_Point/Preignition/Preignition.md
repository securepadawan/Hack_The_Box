![preignition_icon](https://github.com/securepadawan/Hack_The_Box/assets/66234098/18582026-f6cf-4cbb-86d9-b1e1b472c133)

# About Preignition

- Starting point machine

# Categories

- Network
- Programming
- RDP

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Weak Credentials

# Languages

- N/A

# Hints

1. What does the 3-letter acronym RDP stand for?
    - A quick Google search can yield you the results. Use Camel Case
2. What is a 3-letter acronym that refers to interaction with the host through a command line interface?
    - You can abbreviate the last three words of the question.
3. What about graphical user interface interactions?
    - You can use the same concept as in the previous question.
4. What is the name of an old remote access tool that came without encryption by default and listens on TCP port 23?
    - Definition: The prefixes (tel- and telo-) mean end, terminus, extremity, or completion. They are derived from the Greek telos - meaning an end or goal. The prefixes (tel- and telo-) are also variants of (tele-), which means distant!
5. What is the name of the service running on port 3389 TCP?
    - This can be found from the output of our Nmap scan.
6. What is the switch used to specify the target host's IP address when using xfreerdp?
    - In the help menu, its description is "Server hostname".
7. What username successfully returns a desktop projection to us with a blank password?
8. Submit root flag

# Solution

1. `remote desktop protocol`
2. `CLI`
3. `GUI`
4. `telnet`
5. `ms-wbt-server` . Found this answer by typing in the terminal `nmap -sV [Machine IP Address]`
6. `/v:`
7. `Administrator`
8. Within the terminal, typed `xfreerdp /v:10.129.1.13 /cert:ignore /u:Administrator` . When it prompted for a password, I just hit enter. It then remoted into a Windows machine. On the desktop was the `flag.txt` file. 

# Flag

`951fa96d7830c451b536be5a6be008a0`
