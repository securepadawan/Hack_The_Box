# About

- Starting point machine

# Categories

- Redis
- Vulnerability Assessment
- Databases

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Anonymous / Guest Access

# Languages

- N/A

# Hints

1. Which TCP port is open on the machine?
    - Use Nmap to run a port scan, scanning all ports with '-p-'. This can be really slow, so consider adding '--min-rate 5000' or '-T5' to speed it up.
2. Which service is running on the port that is open on the machine?
    - Analyse the result of the Nmap scan.
3. What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database
    - Use Google.
4. Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments.
    - Do a simple Google search about "command-line utility for Redis".
5. Which flag is used with the Redis command-line utility to specify the hostname?
    - Refer to the help page of the utility to understand its usage.
6. Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?
    - Do a Google search about "Redis commands”
7. What is the version of the Redis server being used on the target machine?
    - Use the Redis command-line utility to obtain the Redis version or refer to the output of the Nmap scan.
8. Which command is used to select the desired database in Redis?
    - Use Google.
9. How many keys are present inside the database with index 0?
10. Which command is used to obtain all the keys in a database?
11. Submit root flag

# Solution

1. Within the terminal, I typed `nmap -p- -sV [Machine IP Address]` . This output `6379/tcp open`. The `-p-` command lists the ports. 
2. Again, using the same command ask the solution above `nmap -p- -sV [Machine IP Address]` it shows the server as `redis`.
3. `In-memory Database`
4. `redis-cli`
5. When running command `redis-cli --help` you can see that `-h` is for the hostname.
6. `info`
7. Within the terminal, type `redis-cli -h [Machine IP Address]` . Once it connects to the machine, type `info` . This will give the “redis_version” `5.0.7`
8. `select`
9. When using the command `info` and scrolling to the bottom, under “Keyspace” you can see `keys=4`
10. `keys *`
11. After typing `keys *` , it shows four keys : “numb”, “stor”, “flag”, and “temp”. When typing `get flag` it shows the flag.

# Flag

03e1d2b376c37ab3f5319922053953eb
