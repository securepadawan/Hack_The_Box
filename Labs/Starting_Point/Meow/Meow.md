![Screenshot 2023-07-19 000950](https://github.com/securepadawan/Hack_The_Box/assets/66234098/f829fa20-4d62-487c-8cf6-3cd87804f81d)

# About Meow

- Starting point machine

# Categories

- Telnet
- Network
- Protocol

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Weak Credentials
- Misconfiguration

# Languages

- N/A

# Hints

1. What does the acronym VM stand for?
2. What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It’s also known as a console or shell.
3. What service do we use to form our VPN connection into HTB labs?
4. What is the abbreviated name for a ‘tunnel interface’ in the output of your VPN boot-up sequence output?
5. What tool do we use to test our connection to the target with an ICMP echo request?
6. What is the name of the most common tool for finding open ports on a target?
7. What service do we identify on port 23/tcp during our scans? Use nmap scan to find all available services on your machine.
8. What username is able to log into the target over telnet with a blank password?
9. Submit root flag-We want to find the flag in the machine. So we will connect the telnet service to connect the machine

# Solution

1. `virtual machine`
2. `terminal`
3. `openvpn`
4. `tun`
5. `ping`
6. `nmap`
7. Within the terminal, `nmap -v [Machine IP address]` . This will provide you with the service `telnet`
8. `root`
9. Within the terminal, `telnet [Machine IP address]` . When prompting for login `root` . Type `ls` to list all files. To view flag.txt, need to input `cat flag.txt` . 

# Flag

b40abdfe23665f766f9c61ecba8a4c19
