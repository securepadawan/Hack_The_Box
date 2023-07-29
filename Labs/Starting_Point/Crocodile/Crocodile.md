![croc](https://github.com/securepadawan/Hack_The_Box/assets/66234098/05e06719-34e7-42ac-b708-723afecfc4d0)

# About Crocodile

- Starting point machine

# Categories

- Web
- Network
- Custom Applications
- Protocols
- Apache
- FTP

# Area of Interest

- Reconnaissance
- Web Site Structure Discovery

# Vulnerabilities

- Clear Text Credentials
- Anonymous / Guest Access

# Languages

- N/A

# Hints

1. What Nmap scanning switch employs the use of default scripts during a scan?
    - When checking Nmap's help menu, the description for this switch describes how using it can be considered intrusive to the target host.
2. What service version is found to be running on port 21?
    - In the output of our Nmap scan, there is a column called VERSION.
3. What FTP code is returned to us for the "Anonymous FTP login allowed" message?
    - The code is a 3 digit number which is output both in the nmap scan and when successfully logging into the FTP service.
4. After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?
5. After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?
    - Typing the "help" command inside the FTP service shell can yield you the result.
6. What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?
    - The answer is at the end of the username list.
7. What version of Apache HTTP Server is running on the target host?
    - In the output of our Nmap scan, there is a column called VERSION.
8. What switch can we use with Gobuster to specify we are looking for specific filetypes?
    - Using Gobuster's help menu for the "dir" mode can yield you the answer.
9. Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?
    - Make sure to include the filetype as well in your answer. For example: image.jpg, game.exe, script.php.
10. Submit root flag

# Solution

1. `-sC`
2. Within Terminal, `nmap -sC -sV [Machine IP Address]` and under “Version” shows `vsftpd 3.0.3`
3. `220`
4. `anonymous`
5. `get`
6. Within the terminal, used commands `get allowed.userlist` and `get allowed.userlist.passwd`. After both had successfully downloaded, used the command `exit` and then `cat allowed.userlist`. The last account on the list is `admin`
7. `Apache httpd 2.4.41`
8. `-x`
9. `login.php`
10. Logged in using the `Username: admin` and `Password: rKXM59ESxesUFHAd` that was pulled from the allowed.userlist and allowed.userlist.passwd. Using the browser, went to `http://[Machine IP Address]/login.php` and then it showed the flag.

# Flag

`c7110277ac44d78b6a9fff2232434d16`
