# 1. LEVEL 0

The goal of this level is to log into the game using `SSH`. The host to which you need to connect is `bandit.labs.overthewire.org`, on port `2220`. The username is `bandit0` and the password is `bandit0`.

**Commands you may need to solve this level:**

```bash
ssh
```

The default SSH port is `22`. When using `ssh user@host`, SSH will try to connect through port `22`. Since this challenge uses port `2220`, we must specify the port number using `-p`.

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

Using the given password:

```text
bandit0
```

After running the command, we get access to the Bandit remote server.

---

# 2. LEVEL 0 - 1

### Level Goal

The password for the next level is stored in a file called `readme` located in the home directory.

Use this password to log in as username `bandit1` using SSH.

Whenever you find a password for a level, use SSH on port `2220` to log into that level and continue the game.

**Commands you may need to solve this level:**

```bash
ls
cd
cat
file
du
find
```

In the remote server, I used `ls -la` to list the files in the home directory and find the `readme` file.

```bash
ls -la
```

Then I used `cat` to read the contents of the file:

```bash
cat readme
```

This gave me:

```text
The password you are looking for is: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

I then connected to the host `bandit.labs.overthewire.org` using the username `bandit1` on port `2220`.

```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

Password:

```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

---

# 3. LEVEL 1 - 2

### Level Goal

The password for the next level is stored in a file called `-` (a dashed filename) located in the home directory.

**Commands you may need to solve this level:**

```bash
ls
cd
cat
file
du
find
```

In the home directory, I used `ls` to see the files:

```bash
ls
```

One of the files was named:

```text
-
```

I initially tried:

```bash
cat -
```

However, this did not work as expected because `cat -` interprets `-` as standard input (`stdin`) rather than as the filename.

I then used:

```bash
cat ./-
```

The `./` tells the shell that `-` is the name of a file in the current directory.

This gave me the password for the next level.

### PASS

**Password for Level 2 → 3:**

```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

I then connected to the next level using:

```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```

---

# 4. LEVEL 2 - 3

### Level Goal

The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory.

**Commands you may need to solve this level:**

```bash
ls
cd
cat
file
du
find
```

Spaces in filenames can cause issues in the terminal because the shell treats spaces as separators between arguments.

For example:

```bash
cat my text.txt
```

The terminal will interpret `my` and `text.txt` as two different arguments rather than one filename.

These issues can be avoided by using a backslash `\` or quotation marks `""` in the terminal XD.

I used `find` to confirm the exact filename:

```bash
bandit2@bandit:~$ find "./--spaces in this filename--"

./--spaces in this filename--
```

I then used quotation marks around the filename so that the entire filename would be treated as a single argument:

```bash
bandit2@bandit:~$ cat "./--spaces in this filename--"

7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

### PASS

**Password for Level 3 - 4:**

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

---

# 5. LEVEL 3 - 4

### Level Goal

The password for the next level is stored in a hidden file in the `inhere` directory.

**Commands you may need to solve this level:**

```bash
ls
cd
cat
file
du
find
```

I first SSH'd into `bandit3` using:

```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```

Using the password from the previous level:

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

After logging in, I used:

```bash
ls -la
```

to list all files and directories, including hidden ones.

This revealed the `inhere` directory.

I then entered the directory:

```bash
cd inhere
```

and used:

```bash
ls -la
```

to list all the files, including hidden files.

One of the files was:

```text
...Hiding-From-You
```

I then read the file using:

```bash
cat ./...Hiding-From-You
```

This gave me the password for the next level.

### PASS

**Password for Level 4 - 5:**

```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

---

# 6. LEVEL 4 - 5

### Level Goal

The password for the next level is stored in the only human-readable file in the `inhere` directory.

**Tip:** If your terminal is messed up, try the `reset` command.

**Commands you may need to solve this level:**

```bash
ls
cd
cat
file
du
find
```

 first SSH'd into `bandit4` using:

```bash
ssh -p 2220 bandit4@bandit.labs.overthewire.org
```

Using the password from the previous level:

```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

After logging into the bandit4 host `inhere` directory, I typed in `ls -la` to get info on the files and got nine files. Reading each file then got the password in `-file07`:
```bash
cat -- -file07
```
Getting the password for the next level
```
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

# 7. LEVEL 5 - 6
### Level Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
1. human-readable
2. 1033 bytes in size
3. not executable

**Commands you may need to solve this level:**

```bash
ls
cd
cat
file
du
find
```
SSH into bandit5 using:
```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org
```
Using the password we got from the previous level:
```text
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```
After logging into bandit5 host `inhere` directory, I type din `ls -la` to get details on the available directories and files.

The level goal was to find the `bandit6` password in a human-readable file that is 1033 bytes and non-executable. IN the terminal I specified these features by typing in"
```bash
find . -type f -size 1033c
```
and the output was `./maybehere07/.file2`. I then checked what type of file it was with the file command and the output was `./maybehere07/.file2: ASCII text, with very long lines (1000)` which tells us that the file is human-readable because it's ASCII text. I used the cat command to get the password.

Level 6 - 7 password:

```text
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```
# LEVEL 6 - 7
### Level Goal
The password for the next level is stored somewhere on the server and has all of the following properties:

    owned by user bandit7
    owned by group bandit6
    33 bytes in size

**Commands you may need to solve this level:**
```bash
ls
cd
cat
file
du
find
grep
```
I first ssh to `bandit6` using:
```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org
```
With the password we got from level 5 - 6:
```text
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```
I got into the user directory and input `ls -la` to get the contents of the `bandit6` host"
```bash
bandit6@bandit:~$ ls -la
total 20
drwxr-xr-x   2 root root 4096 Jun 24 14:58 .
drwxr-xr-x 150 root root 4096 Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root root 3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13  2026 .profile
```
There wasn't any clues so I typed in `ls /` to go back to root directory and used the `find` command to searched for one of the goal specifications which was a file sized 33 bytes.
```bash
find / -type f -size -33c
```
I got a huge output of files and looked through them and found `/var/lib/dpkg/info/bandit7.password`
I then input `cat /var/lib/dpkg/info/bandit7.password` and got the level 7 - 8 password.

Password for level 7 - 8:
```text
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

# LEVEL 7 - 8
### Level Goal
The password for the next level is stored in the file `data.txt` next to the word `millionth`.

**Commands you may need to solve this level"**
```bash
man
grep
sort
uniq
strings
base64
tr
tar
gzip
bzip2
xxd
```
First tash is to `SSH` into the bandit7 host:
```bash
ssh -p 2220 bandit7@bandit.labs.overthewire.org
```
Uisng the password we got  from the previos level:
```text
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```
I got into the host and input `ls -la` getting the output:
```bash
bandit7@bandit:~$ ls -la
total 4108
drwxr-xr-x   2 root    root       4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root       4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root        220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root    root       3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root        807 Feb 13  2026 .profile
-rw-r-----   1 bandit8 bandit7 4184396 Jun 24 14:59 data.txt
```
I then used the `grep` command to search for the word `millionth` in the `data.txt` file and the output was `millionth	VR1ljMayciFxbnUokuQmJFw6QC9VKtub`, giving us the password. Which was way easier than I anticipated.

Password for level 8 - 9:
```text
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

# LEVEL 8 - 9
### Level Goal
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.

**Commands you may need to solve this level:**
```
grep
sort
uniq
strings
base64
tr
tar
gzip
bzip2
xxd
```
As usual, we `SSH` into the host on port 2220:
```bash
ssh -p 2220 bandit8@bandit.labs.overthewire.org
```
With the password from the previous level:
```text
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```
Got into the host user `bandit8` and input `ls -la` seeing the `data.txt`. I then used the command `uniq data.txt` and got a hugeeee output and obviously I can't look through all of them to find the one that **occurs only once** as per the level goal.

Used the `sort` command and got a sorted output that makes it easy to identify instances of the same text in a file. I found the password after looking through the output results but I'm sure there's an easier way cause what if there was millions of instances??

So I used the command:
```bash
sort data.txt | uniq -c
```
With `-c` showing the count of the instances in the file. The output had the password having only 1 instance.

Password for level 9 - 10:
```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```
# LEVEL 9 - 10
### Level Goal
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

**Commands you may need to solve this level:**
```bash
grep
sort
uniq
strings
base64
tr
tar
gzip
bzip2
xxd
```
As usual again, `SSH` into `bandit9' host with"
```bash
ssh -p 2220 bandit9@bandit.labs.overthewire.org
```
With the password we got from the previous level:
```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```
This was easy peasy hhh.
I got into the host and `ls -la` getting the usual output with the target file being `data.txt`.

I then used the command `strings` to print out the sequence of printable character in the file. THe password was supposed to be found alongside `=` characters. 
```bash
strings data.txt
```

Password for level 10 - 11:
```text
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```
# LEVEL 10 - 11
### Level Goals
The password for the next level is stored in the file data.txt, which contains base64 encoded data.

**Commands you may need to solve this level:**
```bash
grep
sort,
uniq,
strings
base64
tr
tar
gzip
bzip2
xxd
```
Ofc, you know the usual:
```bash
ssh -p 2220 bandit10@bandit.labs.overthewire.org
```
With the password we got from the previos level
```text
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```
Got in `ls -la` and used the `base64` command to decode the password in the data.txt file.
```bash
base64 data.txt
```
To get the encoded text:
```text
VkdobElIQmhjM04zYjNKa0lHbHpJSEJaWms5Wk5raDNWWE5FYWpWeVREbFZkbmxvVlRkTlEyMTJP
SFpPTlZKdkNnPT0K
```
We now decode it using:
```bash
bandit10@bandit:~$ base64 -d data.txt
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
bandit10@bandit:~$ 
```
The decoded password for level 11 - 12 is therefore:
```text
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

# LEVEL 11 - 12
### Level Goals
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

**Commands you may need to solve this level:**
```bash
grep
sort
uniq
strings
base64
tr
tar
gzip
bzip2
xxd
```
Again, `SSH` into bandit11 host:
```bash
ssh -p 2220 bandit11@bandit.labs.overthewire.org
```
With the password from the previous level:
```text
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```
Got into data.txt
```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
bandit11@bandit:~$ 
```

* `**cat data.txt:` Reads the contents of the file.
* `| (pipe):` Sends the text output into the next command.
* `tr:` Translates or replaces specific characters.
* `'A-Za-z' 'N-ZA-Mn-za-m':` Shifts every uppercase and lowercase letter by 13 positions back to its normal readable form.

Password for the next level is:
```text
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

# LEVEL 12 - 13
### Level Goals
