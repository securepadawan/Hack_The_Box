![sequel](https://github.com/securepadawan/Hack_The_Box/assets/66234098/0ebfdb75-4829-49d7-9032-19c783ea33db)

# About Sequel

- Starting point machine

# Categories

- Vulnerability Assessment
- Databases

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Weak Credentials

# Languages

- SQL
- MySQL

# Hints

1. During our scan, which port do we find serving MySQL?
    - The answer is under the PORT column of the nmap scan of our target host.
2. What community-developed MySQL version is the target running?
    - Typically '-sV' is used with Nmap to determine versions, but that's not always enough. In this case, try adding '-sC' to run safe scripts, which is another good way to get things like versions.
3. When using the MySQL command line client, what switch do we need to use in order to specify a login username?
    - The answer can be found in MySQL's help menu.
4. Which username allows us to log into this MariaDB instance without providing a password?
    - The root of all evil.
5. In SQL, what symbol can we use to specify within the query that we want to display everything inside a table?
    - This will make you starry-eyed.
6. In SQL, what symbol do we need to end each query with?
    - You can find the answer by reading the write-up carefully.
7. There are three databases in this MySQL instance that are common across all MySQL instances. What is the name of the fourth that's unique to this host?
    - Try 'show databases;' to list the databases, and then read about default databases in the MySQL documentation.
8. Submit root flag

# Solution

1. Within the terminal, ran `nmap -sC -sV [Machine IP Address]` and showed me `3306 mysql port open`.
2. `MariaDB`
3. `-u`
4. `root`
5. `*`
6. `;`
7. Ran `show databases;` and showed `htb`
8. Ran `USE htb;` , `SHOW tables;` , `SELECT * FROM config;` . When looking at the output, id 5 shows flag and the value.

# Flag

`7b4bec00d1a39e3dd4e021ec3d915da8`
