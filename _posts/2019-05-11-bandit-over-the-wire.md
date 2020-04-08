# wargames at OTW ( Over the Wire ) - Bandit

I came to know about this website from a friend named Arushit. I have
been lucky to get a mentor at owasp workspace. They have a channel called
`#mentor`. 

## Exploration

One first time scan of the website, I find that there is a suggested order to
play the games. I have picked up Bandit to start with. The game is to search
for password at a given location in the machine by using tips and commands
given and log into same machine on a different port by using the acquired
information.

### Level 0
Log into the machine using the given details using `ssh`.

```bash

ssh bandit0@bandit.labs.overthewire.org -p 2220 
#give username as the password

```
You get a nice banner and welcome as a player. It was quite exiting to log into
a machine that has been placed for learning. However, in real scenarios getting
into a machine might not be this easy. Here at evey level we need to search for
the password and log in using username made for the corresponding level.

    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit0@bandit.labs.overthewire.org's password: 
    Linux bandit 4.18.12 x86_64 GNU/Linux
                
        ,----..            ,----,          .---. 
        /   /   \         ,/   .`|         /. ./|
        /   .     :      ,`   .'  :     .--'.  ' ;
    .   /   ;.  \   ;    ;     /    /__./ \ : |
    .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
    ;   |  ; \ ; | |    :     | /___/ \ |    ' ' 
    |   :  | ; | ' ;    |.';  ; ;   \  \;      : 
    .   |  ' ' ' : `----'  |  |  \   ;  `      |
    '   ;  \; /  |     '   :  ;   .   \    .\  ; 
    \   \  ',  /      |   |  '    \   \   ' \ |
        ;   :    /       '   :  |     :   '  |--"  
        \   \ .'        ;   |.'       \   \ ;     
    www. `---` ver     '---' he       '---" ire.org     
                
                
    Welcome to OverTheWire!

    If you find any problems, please report them to Steven or morla on
    irc.overthewire.org.

    --[ Playing the games ]--

    This machine might hold several wargames. 
    If you are playing "somegame", then:

        * USERNAMES are somegame0, somegame1, ...
        * Most LEVELS are stored in /somegame/.
        * PASSWORDS for each level are stored in /etc/somegame_pass/.

    Write-access to homedirectories is disabled. It is advised to create a
    working directory with a hard-to-guess name in /tmp/.  You can use the
    command "mktemp -d" in order to generate a random and hard to guess
    directory in /tmp/.  Read-access to both /tmp/ and /proc/ is disabled
    so that users can not snoop on eachother. Files and directories with 
    easily guessable or short names will be periodically deleted!
        
    Please play nice:
        
        * don't leave orphan processes running
        * don't leave exploit-files laying around
        * don't annoy other players
        * don't post passwords or spoilers
        * again, DONT POST SPOILERS! 
        This includes writeups of your solution on your blog or website!

    --[ Tips ]--

    This machine has a 64bit processor and many security-features enabled
    by default, although ASLR has been switched off.  The following
    compiler flags might be interesting:

        -m32                    compile for 32bit
        -fno-stack-protector    disable ProPolice
        -Wl,-z,norelro          disable relro 

    In addition, the execstack tool can be used to flag the stack as
    executable on ELF binaries.

    Finally, network-access is limited for most levels by a local
    firewall.

    --[ Tools ]--

    For your convenience we have installed a few usefull tools which you can find
    in the following locations:

        * pwndbg (https://github.com/pwndbg/pwndbg) in /usr/local/pwndbg/
        * peda (https://github.com/longld/peda.git) in /usr/local/peda/
        * gdbinit (https://github.com/gdbinit/Gdbinit) in /usr/local/gdbinit/
        * pwntools (https://github.com/Gallopsled/pwntools)
        * radare2 (http://www.radare.org/)
        * checksec.sh (http://www.trapkit.de/tools/checksec.html) in /usr/local/bin/checksec.sh

    --[ More information ]--

    For more information regarding individual wargames, visit
    http://www.overthewire.org/wargames/

    For support, questions or comments, contact us through IRC on
    irc.overthewire.org #wargames.

    Enjoy your stay!


### Level 0 -> Level 1

At this level, I need to read `readme` file located in the home directory. File
name and location are known. I can `cat` a file and read it for password to get
on to the next level. 

```bash
cat ~/readme

```
The above command gave me the password. I consider myself to be on level1. I
hope so.


### Level 1 -> Level 2

Using the password that I got from the previous level, I want to reach level 2.
I exited from the terminal and logged in again using the below command.

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
So now I am on level 2 but to go up one more level up, I need to find the
password on this stage. 

Again the filename and the location is given, but the file name starts with a
`-` and such files are dangerous for `shell`. I came to know about it from the
help links given on the website. The below commands and options are there for
the rescue. 

```bash

cat -- ~/- # -- I have used while using git checkout single files too.

cat ./-

# still I don't know but which one of the above command is better. 
# TODO: I will ask other guys and read more about it.

```
Anyways, I am up for the next level.

### Level 2 -> Level 3

I exited from the last session and logged in using the below command.

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
Here I need to find the password from the next level. I have been writing a
lot. From now onwards, I will mark my step as 1(login) and 2(find password).

```bash
cat spaces\ in\ this\ filename
# clicking on TAB key autocompletes the file name.

cat "spaces in this filename" # this command too gives the result

```
Exit from the 2nd level.

### Level 3 -> Level 4

1. login

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
2. find password

```bash
# find password
# list the type of files using the below command
find ./inhere -exec file {} \;
# ./inhere: directory
# ./inhere/.hidden: ASCII text

cat ./inhere/.hidden # gave the password

```

Exit from the shell.

### Level 4 -> Level 5

1. login

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
2. find password

```bash
# find password
bandit4@bandit:~$ find ./inhere/ -exec file {} \;
./inhere/: directory
./inhere/-file09: data
./inhere/-file06: data
./inhere/-file01: data
./inhere/-file02: data
./inhere/-file05: data
./inhere/-file03: data
./inhere/-file08: data
./inhere/-file07: ASCII text
./inhere/-file04: data
./inhere/-file00: data
bandit4@bandit:~$ cat -- ./inhere/-file07 


```
### Level 5 -> Level 6

1. login

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
2. find password

```bash
# find password
find inhere/ -size 1033c ! -executable
# I learnt that size and not executable could be passed as options to the find
# command.

bandit5@bandit:~$ cat inhere/maybehere07/.file2

```
Exit the shell.

### Level 6 -> Level 7


1. login

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
2. find password

```bash
# find password
bandit6@bandit:~$ find / -size 33c -user bandit7 -group bandit6
find: ‘/run/lvm’: Permission denied
find: ‘/run/screen/S-bandit13’: Permission denied
....

# I had to scroll through the output to see which file to cat
cat /var/lib/dpkg/info/bandit7.password

# there must be a way to redirect stdrr to /dev/null
find / -size 33c -user bandit7 -group bandit6 2>/dev/null
# the above command gives only one line and doesn't fill my terminal

```
exit the shell. Well I am left with one more level and there is a sense of
achievement already.

### Level 7 -> Level 8


1. login

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password.

```
2. find password

```bash
# find password
bandit7@bandit:~$ find / -name 'data.txt' 2>/dev/null -exec grep 'millionth' {} \;

```


I am planning only these many levels for today, I am not sure when will I reach
the level. Solving for these challenges looks like reinforcement learning; the
technique I came across while reading about neural networks used in abstractive
summarisation problems. RL is about taking appropriate action in order to
maximize the reward in a particular situation. 

## What did I learn ?


- find command and it various options to make file search better.
- I can redirect the `stderr` to `/dev/null`.
- I can use `exec` to execute a command on the output of the previous command
    in line.
- about the dashed files and their significance and how they can be used as
    input to commands such as `cat` and `file`.
