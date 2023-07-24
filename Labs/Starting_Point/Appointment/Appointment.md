![appointment_icon](https://github.com/securepadawan/Hack_The_Box/assets/66234098/baa6c4f6-37f3-4aad-84d6-8107640a0314)

# About Appointment

- Starting point machine

# Categories

- Web
- Database
- Injection

# Area of Interest

- Apache

# Vulnerabilities

- Reconnaissance
- SQL Injection

# Languages

- MariaDB
- PHP
- SQL

# Hints

1. What does the acronym SQL stand for?
    - A simple Google search will yield the answer. Use Camel Case.
2. What is one of the most common type of SQL vulnerabilities?
    - Mentioned in the write-up's Introduction section.
3. What does PII stand for?
    - It's a common term found in user data protection. Use camel case.
4. What is the 2021 OWASP Top 10 classification for this vulnerability?
    - It holds first place in the OWASP Top 10 2021 list of most commonly met web vulnerabilities. Use the complete classification name.
5. What does Nmap report as the service and version that are running on port 80 of the target?
    - Exact string under the VERSION column of the scan results.
6. What is the standard port used for the HTTPS protocol?
    - It's different from the unsecured version.
7. What is a folder called in web-application terminology?
    - Whenever I'm a bad employee, I get called to the "director's" office.
8. What is the HTTP response code is given for 'Not Found' errors?
    - Look up HTTP response codes.
9. Gobuster is one tool used to brute force directories on a webserver. What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?
    - Shorthand name for directories.
10. What single character can be used to comment out the rest of a line in MySQL?
    - -- also makes a comment, but that's two characters.
11. If user input is not handled carefully, it could be interpreted as a comment. Use a comment to login as admin without knowing the password. What is the first word on the webpage returned?
    - Try adding a comment at the end of the username.
12. Submit root flag

# Solution

1. `Structured Query Language`
2. `SQL Injection`
3. `Personally Identifiable Information`
4. `A03:2021-Injection`
5. Ran `nmap -p- -sV 10.129.39.74` and found the service `Apache httpd 2.4.38 ((Debian))`
6. `443`
7. `directory`
8. `404`
9. `dir`
10. `#`
11. Went to the webpage on the target machine. It requested the login credentials. `Username: admin'#` and `Password:admin`. The first word on the webpage was `Congratulations`
12. When using the command above, it also provided the flag.

# Flag

`e3d0796d002a446c0e622226f42e9672`
