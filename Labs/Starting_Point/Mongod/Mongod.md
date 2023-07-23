![mongo_icon](https://github.com/securepadawan/Hack_The_Box/assets/66234098/f7a0509b-3085-41d2-a1f0-deddb755fbf7)

# About Mongod

- Starting point machine

# Categories

- MongoDB
- Web
- Databases

# Area of Interest

- Reconnaissance

# Vulnerabilities

- Misconfiguration
- Anonymous / Guest Access

# Languages

- N/A

# Hints

1. How many TCP ports are open on the machine?
    - Use Nmap to run a port scan scanning all ports with -p-. This can be really slow, so consider adding --min-rate 5000 or -T4 to speed it up.
2. Which service is running on port 27017 of the remote host?
    - The -sV flag on nmap can attempt to pull version information from services.
3. What type of database is MongoDB? (Choose: SQL or NoSQL)
    - A Google search along the keywords "What type of database is MongoDB?".
4. What is the command name for the Mongo shell that is installed with the mongodb-clients package?
    - A Google search for the package name and the term "Mongo shell".
5. What is the command used for listing all the databases present on the MongoDB server? (No need to include a trailing ;)
6. What is the command used for listing out the collections in a database? (No need to include a trailing ;)
7. What is the command used for dumping the content of all the documents within the collection named flag in a format that is easy to read?
8. Submit root flag

# Solution

1. Ran command `nmap -p- -sV [Machine IP Address]` and found 2 tcp ports open.
2. When using the command above, it showed `MongoDB 3.6.8` running on `port 27017`
3. `NoSQL`
4. `mongo`
5. `show dbs`
6. `show collections`
7. `db.flag.find().pretty()`
8. First had to install MongoDB using the following command `curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.7.tgz` , then ran `tar xvf mongodb-linux-x86_64-3.4.7.tgz` , then ran `cd mongodb-linux-x86_64-3.4.7/bin` and lastly used command `./mongo mongodb://[Machine IP Address]:27017` to connect to the MongoDB server. After connecting used `show dbs;` to show the databases. I then used `use sensitive_information;` and then `show collections;` . This showed `flag` . To read the flag, I used command `db.flag.find().pretty();`

# Flag

`1b6e6fb359e7c40241b6d431427ba6ea`
