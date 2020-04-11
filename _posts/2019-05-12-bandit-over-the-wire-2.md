# wargames at OTW ( Over the Wire ) - Bandit - Part 2

I am here again to whet my appetite on learning some more while reaching higher
level in the game. If you are not sure what is going on here, please read my
previous post on starting with bandit on OTW.


### Level 8 -> Level 9


1. login

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

```bash
# find password
bandit8@bandit:~$ find / -name 'data.txt' 2>/dev/null -exec file {} \;

bandit8@bandit:~$ sort /home/bandit8/data.txt | uniq -c
# the above command list the count lines and the counts of strings in the file.
# selected the password as the line for which the count was 1

```

### Level 9 -> Level 10


1. login

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

```bash
# find password
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ strings data.txt | grep ^=
```

### Level 10 -> Level 11


1. login

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

```bash
# find password

bandit10@bandit:~$ base64 -d data.txt

```

### Level 11 -> Level 12


1. login

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

```bash
# find password
bandit11@bandit:~$ cat data.txt | tr '[a-zA-Z]' '[n-za-mN-ZA-M]'

```
Translating using regular expression and doing rot(13) was awesome and felt
like a relevation. Cheated this one from web.

### Level 12 -> Level 13


1. login

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```

For this one I had to create a temp directory and copy data.txt to it. I
renamed it and un-hexdumed it using `xxd`. After that it was a seies of steps
using various zip utitlies to extract the files. `file` command was very
helpful in determining that which zip utility is required for unzipping a file.

2. find password

```bash
# find password

bandit12@bandit:/tmp/h3xh4wk$ xxd -r hexdumped.txt > mydata.bin

data3: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/h3xh4wk$ bzip2 -d data3 -c > data4
bandit12@bandit:/tmp/h3xh4wk$ file data
data3  data4  
bandit12@bandit:/tmp/h3xh4wk$ file data
data3  data4  
bandit12@bandit:/tmp/h3xh4wk$ file data4 
data4: gzip compressed data, was "data4.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/h3xh4wk$ gzip -d data4 -c > data5
bandit12@bandit:/tmp/h3xh4wk$ file data5
data5: POSIX tar archive (GNU)
bandit12@bandit:/tmp/h3xh4wk$ tar xf data5

bandit12@bandit:/tmp/h3xh4wk$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/h3xh4wk$ tar xf data5.bin
bandit12@bandit:/tmp/h3xh4wk$ ls
data3  data4  data5  data5.bin  data6.bin  data7  hexdumped.txt  mydata.bin
bandit12@bandit:/tmp/h3xh4wk$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/h3xh4wk$ bzip2 -d data6.bin -c > data7
bandit12@bandit:/tmp/h3xh4wk$ ls
data3  data4  data5  data5.bin  data6.bin  data7  hexdumped.txt  mydata.bin
bandit12@bandit:/tmp/h3xh4wk$ file data7
data7: POSIX tar archive (GNU)
bandit12@bandit:/tmp/h3xh4wk$ tar xf data7
bandit12@bandit:/tmp/h3xh4wk$ ls
data3  data4  data5  data5.bin  data6.bin  data7  data8.bin  hexdumped.txt  mydata.bin
bandit12@bandit:/tmp/h3xh4wk$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/h3xh4wk$ gzip -d data8.bin -c > data9
bandit12@bandit:/tmp/h3xh4wk$ file data9
data9: ASCII text
bandit12@bandit:/tmp/h3xh4wk$ cat data9 


```

I am ready to log into level 13.

### Level 13 -> Level 14


1. login

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```

2. find password

```bash
# find password
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost
# I jumped to level 14 without a password

```

### Level 14 -> Level 15


1. login

```bash
# already logged in .. using the bandit14's private key as identity

```

2. find password

```bash
# find password - need to send the pass 14 level password to 30000
bandit14@bandit:~$ nc -v localhost < /etc/bandit_pass/bandit14
```


### Level 15 -> Level 16


1. login

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220

```

2. find password

```bash
# find password
bandit15@bandit:~$ cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
# I tried ncat command too with --ssl option but could not get the result

```
### Level 16 -> Level 17


1. login

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220

```

2. find password

```bash
# find password
nmap --script=ssl-enum-ciphers -p 31000-32000 --reason localhost

# the above command gave me only 1 port in the result and the below commands

cat /etc/bandit_pass/bandit16

ncat -v --ssl localhost <port>
# then Ineed to pass the password from the password file of this level


```

I saved the RSA key to a file from the previous step.


### Level 17 -> Level 18


1. login

```bash
ssh bandit17@bandit.labs.overthewire.org -p 2220

```

2. find password

```bash
# find password
diff passwords.old passwords.new 


```
Using the password from the previous step, when I try to log in to the next
level. I come out. trying to send `ls -lh` command while logging in.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 ls -lh

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
total 4.0K
-rw-r----- 1 bandit19 bandit18 33 Oct 16  2018 readme


```

`ls -lh` command lists the `readme` file. This time I will send `cat readme`
along with the login attempt.



```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

```

