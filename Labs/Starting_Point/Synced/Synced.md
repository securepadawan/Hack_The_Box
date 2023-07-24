![synced_icon](https://github.com/securepadawan/Hack_The_Box/assets/66234098/41a6e632-453c-4452-b50e-d579f4a63b81)

# About Synced

- Starting point machine

# Categories

- Rsync
- Network
- Protocols

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Anonymous / Guest Access

# Languages

- N/A

# Hints

1. What is the default port for rsync?
    - Googling things like "rsync default port" should get you there.
2. How many TCP ports are open on the remote host?
3. What is the protocol version used by rsync on the remote machine?
4. What is the most common command name on Linux to interact with rsync?
    - Usually the commands used to interact with such protocols have the same name as the protocol.
5. What credentials do you have to pass to rsync in order to use anonymous authentication? anonymous:anonymous, anonymous, None, rsync:rsync
    - Anonymous authentication for rsync is more minimalistic than that of FTP.
6. What is the option to only list shares and files on rsync? (No need to include the leading -- characters)
    - Look at the official manual page of rsync by executing "man rsync" in your terminal
7. Submit root flag

# Solution

1. `873`
2. Within Terminal, `nmap -p- -sV [Machine IP Address]` and displayed `1` tcp port open.
3. Using the same command above, it shows the protocol version for rsync as `31`
4. `rsync`
5. `none`
6. `list-only`
7. I first ran `rsync --list-only [Machine IP Address]::` and that provided `public Anonymous Share` . I then ran this command to see what was inside public `rsync --list-only [Machine IP Address]::public` . After seeing the `flag.txt` file, I downloaded it by running `rsync [Machine IP address]::public/flag.txt flag.txt` and then `cat flag.txt` to read it.

# Flag

`72eaf5344ebb84908ae543a719830519`
