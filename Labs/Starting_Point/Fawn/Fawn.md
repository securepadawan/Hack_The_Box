# About

- Starting point machine

# Categories

- FTP
- Network
- Protocol

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Anonymous / Guest Access

# Languages

- N/A

# Hints

1. What does the 3-letter acronym FTP stand for?
    - It's always good practice to associate the purpose of the `protocol` with the meaning of the acronym in order to remember them better. The IT domain has a lot of acronyms you will need to remember, FTP being one of the more basic ones. In this case, it has something to do with `file transfer`. When using acronyms, remember that the first letter of each word is always capitalized as standard. This is called Camel Case (or Medial Capitals).
2. Which port does the FTP service listen on usually?
    - Googling things like "FTP default port" should get you there.
3. What acronym is used for the secure version of FTP?
    1. The difference between the normal 'FTP' service and the secured version is that the secured version runs under the SSH protocol. SSH stands for "Secure Shell". Following this logic, your new protocol would be "Secure FTP". What would the acronym for this new protocol be?
4. What is the command we can use to send an ICMP echo request to test our connection to the target?
    - It's a simple protocol you might've used before to troubleshoot your router at home. It's also an "onomatopoeia".
5. From your scans, what version is FTP running on the target?
    - Remember to use the '-sV' flag in nmap to find out the answer to this!
6. From your scans, what OS type is running on the target?
    - Remember to use the '-sV' flag in 'nmap' to find out the answer to this!
7. What is the command we need to run in order to display the 'ftp' client help menu?
    - This is a typical command argument, or 'flag' that we add to most of the commands we run in the terminal to display their help menus. Usually, the structure of the command is '{command} {-x}' where 'x' is the 'flag' we need to use. A more detailed alternative is the 'man' command.
8. What is username that is used over FTP when you want to log in without having an account?
    - When your name is not known, you are…
9. What is the response code we get for the FTP message 'Login successful'?
    - Response codes are important because we can tell what the service is reporting back to us at a glance. For example, we're all acquainted with the '404' code. We can even use it as a casual joke nowadays. '404' is the web protocol response code for 'Not Found', telling us that the resource we are trying to reach could not be found by the web server. In our case as well, the response code is made of '3' digits.
10. There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system.
    - Try running help from within FTP to see the possible commands.
11. What is the command used to download the file we found on the FTP server?
    - Using the 'help' command within the 'ftp service' will reveal this command. Its' meaning is straight-forward.

# Solution

1. `file transfer protocol`
2. `21`
3. `SFTP`
4. `ping`
5. Within the terminal, type `nmap -sV [Machine IP address]`. The `-sV` refers to the “service” and “version”. This outputs `ftp vsftpd 3.0.3`
6. `Unix`
7. `ftp -h`
8. Due to the misconfiguration of ftp, you are able to login with username `anonymous` . For the password, you can use any passwords as it doesn’t matter.
9. `230`
10. `ls`
11. `get` You can type `help get` to give details for the command
12. (flag) Type `get flag.txt`. This will download the flag. Once you have downloaded the flag, type `bye` to disconnect the ftp connection. Type `ls` to verify you have the `flag.txt` file. To read it, type `cat flag.txt`

# Flag

035db21c881520061c53e0536e44f815
