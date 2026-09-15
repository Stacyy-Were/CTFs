# LEVEL 0 - 1
### Level Info
Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

`S1JZUFRPTklTR1JFQVQ=`


Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/

## Solution

I created a file `password.txt` and pasted the given encoded string. I then used the command `base64 -d password.txt` to decode the string and got the password:
```bash
# tr command 
stacy@stacy:~$ base64 -d flag.txt
KRYPTONISGREAT
```
With this password, I got access to `krypton1@krypton.labs.overthewire.org` with the given password" `KRYPTONISGREAT` using port 2231.

# LEVEL 1 - 2
### Level Info
The password for level 2 is in the file ‘krypton2’. It is ‘encrypted’ using a simple rotation. It is also in non-standard ciphertext format. When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. This helps obfuscate any patterns. This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!

### SOLUTION
Got into the krypton1 user directory