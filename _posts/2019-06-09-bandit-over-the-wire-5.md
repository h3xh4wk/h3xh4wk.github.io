### Level 25 -> Level 26


1. login

```bash
ssh bandit25@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

The password is the key for the next level and stored in the home directory. I
came to know when I found it using the `ls` command after logging in. The trick
was to get the file to my local and change its permissions using the below
command.

```bash
chmod 400 bandit26.sshkey # the file should only be visible to me

```

Now I could log into the next level using the downloaded key.

### Level 26 -> Level 27

Logging into the level 26 is now fairly easy after changing the file
permissions of the file as stated in the previous level

1. login

```bash
ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

This one was really tricky, logging in was leading to immediate logout. Well..
finding out the shell was possible only by using the below command.

```bash
cat /etc/passwd | grep bandit26
# instead of bash there was some custom text file that was being used.

```
The contents of the custom shell were as shown below:

```bash
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

Even after reading the content of the custom shell, there was no way I could
think of to get the content of `/etc/bandit_pass/bandit27`. Also I didn't know
what kind of a file was `~/text.txt`. There was some trick which could help me
open the editor and see the contents of `/etc/bandit_pass/bandit27`. I googled
and found that I had to minimise the console so that the more command could be
used to open the editor. Please note that once the content hangs inside the
more command, we can press `v` to open up the default editor i.e. `vim`. and
then in its command mode need to be used for setting the shell to `bash` as show
```bash
:set shell=/bin/bash
```
This did not give any error and now just to see whether I will be able to get
the output of any command I tried `ls -la` as shown below. 

```bash
:! ls -la
```

Output of this command lists the files inside the home directory. Now here I
had to take care if at all privellege escalation was required by bandit26 so
that this use could `cat` the contents of `/etc/bandit_pass/bandit27` to see
the password. However, I did not check the file ownership and directly used the
below shown command to see the password for the next level.

```bash
:! ./bandit27-do cat /etc/bandit_pass/bandit27

```

### Level 27 -> Level 28


1. login

```bash
ssh bandit27@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

This step was not that tough. I just had to use the below commands to get the
password.

```bash

mkdir /tmp/tmpuser
cd /tmp/tmpuser
git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
# as password I gave bandit27 password
cat repo/README
```


### Level 28 -> Level 29


1. login

```bash
ssh bandit28@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

Cloning the repo from the given git url 

```bash
# make a directory under /tmp and change into it
git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
cat repo/README.md
```

The content given has password as `xxxxxxxxxx`. I tried to create the password
by generating `md5sum` and `sha256sum` and tried logging in for the next level
but it did not work. It means that passwords are strings that persist and are
not dynamic. Always !

I changed into `repo` directory and issue the below command.

```bash

git log

```

After looking at the output, when I used the below command, it gave me the
password which was replaced by `xxxxxxxxxx` in the latest commit.

```bash

git diff <checksum~1> <checksum~2>

```

So now I have reached level 29 and can log in as bandit29.


### Level 29 -> Level 30


1. login

```bash
ssh bandit29@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

This step was similar to the one in the previous level, however I had to
checkout the `dev` branch and `cat` the `README.md` for the password.

```bash

cat README.md
```
I have reached level 30.



### Level 30 -> Level 31


1. login

```bash
ssh bandit30@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

There was no commit history, but there were some packed refs when I used the
below command

```bash
cat .git/packed-refs
```
Or to use the below command and pressing <TAB> also lists the packed-refs.

```bash
git show --name-only # <Press TAB> twice-thrice
```

And after these I was able to see the value in packed-ref called secret.

```bash
git show --name-only secret
```
Now I have the password for the next level.


### Level 31 -> Level 32


1. login

```bash
ssh bandit31@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

I just followed the instructions in README.md and when I pushed into the repository, I got
the password on my console.


### Level 32 -> Level 33


1. login

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

I really did not have any idea on what I could do to escape from the uppercase
shell that I logged into. Then I googled and found that using `$0`, which has
the path of shell, we can drop into the normal shell and after that we can
`cat` the password file for the next level if bandit32 the permission for the
same.

```bash
>> $0
$ cat /etc/bandit_pass/bandit33
```

The above commands were used to get the password for the next level.


### Level 33 -> Level 34


1. login

```bash
ssh bandit33@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password from the previous level

```
2. find password

After reaching this level, which I `cat` the `README.txt` in the home
directory, I get the below output.

```bash
bandit33@bandit:~$ cat README.txt
Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!
```

I feel awesome and happy to have come to this level. I learnt so many things
and really I was missing on so much of valuable stuff over the internet.

I hope I start with another CTF challenge soon !!.

Thanks to people who have created such environments to whet the appetite of
learners like me. 
