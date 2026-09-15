# Solution
[THM - Pickle Rick](https://tryhackme.com/room/picklerick) - Challege URL

Get OVPN connection and do an nmap on the target machine's IP: 10.65.189.212
```bash
stacy@stacy:~$ sudo nmap -sC -sS 10.65.189.212
[sudo: authenticate] Password:           
Starting Nmap 7.98 ( https://nmap.org ) at 2026-09-15 01:06 +0300
Nmap scan report for 10.65.189.212
Host is up (0.25s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
| ssh-hostkey: 
|   3072 04:1b:43:33:ab:39:33:d5:57:88:4d:28:a6:4c:fe:f5 (RSA)
|   256 d0:b2:56:e1:2b:0e:bb:e8:6a:93:9b:99:44:fd:ef:95 (ECDSA)
|_  256 aa:6b:83:25:e3:dc:8d:1c:0a:32:8d:7c:d2:1c:5a:ea (ED25519)
80/tcp open  http
|_http-title: Rick is sup4r cool

Nmap done: 1 IP address (1 host up) scanned in 16.29 seconds
```
Open ports are 22(SSH) and 80(HTTP)
Cause it's a web app, go to target IP and in this case: http://10.65.189.212
![WebPage](/images/10.65.189.212.png)

Not much on there so we have to inspect the page.
We got the username: `R1ckRul3s`
![Q](/images/username.png)

Running nikto and we found a robots.txt file. 
A robots.txt file tells search engine crawlers which URLs the crawler can access on your site. 

```bash
stacy@stacy:~$ nikto -h 10.65.189.212
- Nikto v2.1.5
---------------------------------------------------------------------------
+ Target IP:          10.65.189.212
+ Target Hostname:    10.65.189.212
+ Target Port:        80
+ Start Time:         2026-09-15 01:48:07 (GMT3)
---------------------------------------------------------------------------
+ Server: Apache/2.4.41 (Ubuntu)
+ Server leaks inodes via ETags, header found with file /, fields: 0x426 0x5818ccf125686 
+ The anti-clickjacking X-Frame-Options header is not present.
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ "robots.txt" retrieved but it does not contain any 'disallow' entries (which is odd).
+ Allowed HTTP Methods: OPTIONS, HEAD, GET, POST 
+ Cookie PHPSESSID created without the httponly flag
-C all
- STATUS: Completed 3160 tests (~48% complete, 19.0 minutes left: currently in plugin 'Nikto Tests')
```
The `robots.txt` has the word `Wubbalubbadubdub` which could be the password.

Next is to try and get all files available on the site using Gobuster with the command:
```bash
gobuster dir -u http://10.65.189.212 -w /home/stacy/Downloads/quick-list.txt -x php,html,txt
# Searching for php cause we know the server runs php plus the rest
```
The output is:
```bash
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.65.189.212
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/stacy/Downloads/quick-list.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              php,html,txt
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
robots.txt           (Status: 200) [Size: 17]
portal.php           (Status: 302) [Size: 0] [--> /login.php]
login.php            (Status: 200) [Size: 882]
index.html           (Status: 200) [Size: 1062]
assets               (Status: 301) [Size: 315] [--> http://10.65.189.212/assets/]
Progress: 24 / 24 (100.00%)
===============================================================
Finished
===============================================================
```
Some good stuff cause we can see there's a login page `login.php` and we can try the text in robots.txt: `Wubbalubbadubdub` as the password.

It actually IS the password and we got access to Rick's computer.
![Files](/images/ls-la.png)

Let's `cat Sup3rS3cretPickl3Ingred.txt`
![cat disabled](/images/image.png)
and oopsies, the cat command is disabled so we have to try everything in the books.

Using `less`, we get our first ingredient **mr. meeseek hair**
![Sup3rS3cretPickl3Ingred.txt](/images/image-1.png)

So what's the second ingredient????

Tried to `tac denied.php` and OMG XD the output felt violent.
![picklerick](/images/image-2.png)

So let's check the `portal.php` and we got some interesting code. With the commands we can't use.
![portal.php](/images/image-3.png)

For some admin activities, `sudo` isn't in the blocked commands list so we can `sudo -l` to get allllll the commands that aren't blocked, just to make the testing easy, no trial and error and we get:
![sudo -l](/images/image-4.png)
That means we can use all commands without a password except the listed ones.
So.....
![root](image-5.png)
THen check the home directory. We got two directories `rick` and `ubuntu` then got into rick with `ls ../../../home/rick` and got: ![alt text](/images/image-7.png)
Opening the file we get:
![alt text](/images/image-8.png)
The second ingredient. Now for the third.
Looked around and couldn't find anything so we should check the root directory and ofc with `sudo`
![alt text](/images/image-11.png)

Then we open the `3rd.txt`
THIRD INGREDIENT
![alt text](/images/image-9.png)