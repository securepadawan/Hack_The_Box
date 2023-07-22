
![Screenshot 2023-07-19 155549](https://github.com/securepadawan/Hack_The_Box/assets/66234098/430efa25-7033-46fa-9a4c-f9cdc4117bc5)

# About Dancing

- Starting point machine

# Categories

- Network
- Protocol
- SMB

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Anonymous / Guest Access

# Languages

- N/A

# Hints

1. What does the 3-letter acronym SMB stand for?
2. What port does SMB use to operate at?
    - A simple portscan using version detection can get you this result. Also, Googling the port value will return the services used for that port in most cases.
3. What is the service name for port 445 that came up in our Nmap scan?
    - You will need to use the -sV switch during your nmap scan in order to see this in your results! The answer creates a ? at the end, so remember to include it!
4. What is the 'flag' or 'switch' we can use with the SMB tool to 'list' the contents of the share?
    - The acronym of this flag stands for 'list', and is precedes by a '-'.
5. How many shares are there on Dancing?
    - Use "smbclient -L" to list them.
6. What is the name of the share we are able to access in the end with a blank password?
    - It's the one that doesn't terminate with the '$' symbol. This is a custom share, made by a system administrator during the configuration phase.
7. What is the command we can use within the SMB shell to download the files we find?
    - This is the same command used during the interaction with the FTP shell in the previous box!
8. Submit root flag

# Solution

1. `server message block`
2. `445`
3. `microsoft-ds`
4. `-L`
5. `4`
6. `WorkShares`
7. `get`
8. Within the terminal, type `smbclient \\\\[Machine IP Address]\\WorkShares` . Then type `ls` to view files. There are two directories (`Amy.J` and `James.P`). You can access them by typing `cd [Directory Name]` . Once in the directory, you can type again `ls` to see what is located in the folder. The `flag.txt` file is located in the `James.P` directory. Then type `get flag.txt`. Once the file is downloaded, you can type `exit`. Then type `cat flag.txt` to get the flag.

# Flag

5f61c10dffbc77a704d76016a22f1664
