# wargames at OTW ( Over the Wire ) - Bandit - Part 3

I am enjoying learning so many things about linux commands and tricks to log
into the systems. `openssl` and `nmap` scan steps were awesome. Using `ncat` to
arbitrarily connect to ports was also awesome and passing commands to machine
while logging in also was new for me. 

I haved reached level 19.


### Level 19 -> Level 20


1. login

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

```bash
# find password
# below command lists the UID's of owner and the group
ls -n bandit20-do

# find the password files for which owner is bandit20
find /etc/bandit_pass/ -uid 11020

# we get the file path
# as given on the page of the current level the below command should give us
# the password for the next level
cat /etc/bandit_pass/bandit20

```

I used the `cat` command with the filepath, but the permission to view the file
was denied. `./bandit20-do` is the file that can be used to execute this
command with the privelleges of `bandit20`. The below command helps in reading
the contents of the file, which has the password for the next level.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20

```

### Level 20 -> Level 21


1. login

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

This step needs that we listen on a port of our choice for the setuid binary to
connect to. This binary connects to the port and if the correct previous level
password is given the next stage password will be sent. 

To setup the communication, I had to use `tmux`, which helps in creating
multiple windows in same session. In one window I used the below command to
listen for `suconnect`.

```bash
# find password
nc -l -p 4445 < /etc/bandit_pass/bandit20

```
Then to get the password for the next level in another windows, I executed the
below command.

```bash
./suconnect 4445
```
The output from the above command prompted me to go to previous window to look
for the response. The password for the next level was printed on the console.


### Level 21 -> Level 22


1. login

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

I used below commands to find the password

```bash
# find password
ls -la /etc/cron.d

cat /etc/cron.d/cronjob_bandit22

cat /usr/bin/cronjob_bandit22.sh

# the script had a step of redirecting content of password file

tail -f /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```


### Level 22 -> Level 23


1. login

```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

Below are the sequence of commands that I followed to know the password. These
steps are left for self-understanding.

```bash
# find password
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget

```
Now here we need to pay attention to the below line :

`mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)` .

The `$myname` variable is the username. replace that with bandit23 and md5sum
it to get the file name in the tmp directory to read the password. Here is the
command below.

```bash
bandit22@bandit:~$ echo "I am user bandit23" | md5sum
8ca319486bfbbc3663ea0fbe81326349  -
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```


### Level 23 -> Level 24


1. login

```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

I could not figure this out for a very long time. However, there are some
observations about the same. I know that I can `cd` or `cp` i.e. copy to a
directory even when I do not have permission. A `777` persmision given to an
executable file can be executed by a cron from directory which is permitted for
a particular user. I learnt how to create a shell script. 

```bash
#!/bin/sh
cat /etc/bandit_pass/bandit24 > /tmp/bandit24pass
```
The above show script I saved as `test.sh` , modified its mode to `+x` i.e.
executable and copied it to the spool of `bandit24` i.e. to
`/var/spool/bandit24`. and then used the below command to get the password for
the next level. We need to note that it is mandatory to create your own
directory inside `tmp` if you want to create a file there. As I did while
creating `test.sh`. 


```bash
cat /tmp/bandit24pass

```

I will write about next levels in my next post. So far the experience of
playing bandit has been awesome.


