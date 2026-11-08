A structured walk-through of the OverTheWire Bandit wargame.(as I did it) {#! DONT COPY PASTE COMMANDS UNTIL YOU UNDERSTAND SOME FRACTION OF THINGS WHAT'S THE LEVEL IS DEMANDING !#}

Tools needed - tmux(just to have split window of terminal), git, ssh, (I used wsl UBUNTU), vim (or you can use nano built in editor of terminal), nmap 

!!- Use sshpass to pass the password file instead of writing password every time (sshpass -p `cat bandit1` ssh  bandit1@bandit.labs.overthewire.org -p 2220 )

0 -
make a connection by ssh on port 2220   
>ssh bandit0@bandit.labs.overthewire.org -p 2220

0-1 -
ssh operates over port 22 -p tag make it to 2220
>cat readme 

1-2 -
'-' is seen as a command options in UNIX systems so use relative pathing 
cat ./-

2-3 -
Quoting will treat the spaces as single argument 
> cat ./"--spaces in this filename--"  

3-4 -
files with prefix '.' are hidden in unix systems 
>cd inhere
>ls -la
>cat .hidden

4-5 -
inspect file siganture or look for strings   
>strings./*  or file./*

5-6 -
\! negates the permission
>find . \! -executable -size 1033c

6-7 -
2>/dev/null  (/dev/null is black hole of Linux and 2 is for errors)
> find | grep bandit7     or   find -user bandit7 -group bandit6 -size 33c 2>/dev/null

7-8 -
>cat data.txt | grep "millionth"   or   grep "millionth" data.txt

8-9 - 
unique isolate the non repeated entry 
>9- cat data.txt | sort | uniq -u

9-10 - 
> strings -a data.txt | grep ==

10-11 -
binary to text encoding scheme 
>cat data.txt | base64 -d

11-12 - 
ROT 13 cypher rotate every alphabet to 13 position
>cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

12-13 - 
uncompressed the hex dumped binary 
> 13- cp data.txt something.txt
xxd -reverse data.txt > something1
mv something1 something.gz
gunzip something.gz
 mv somemething.out something.gz
gunzip something.gz
tar xf something
 tar xvf data5.bi
bunzip2 data6.bin
 tar xvf data6.bin.out
mv data8.bin data8.bin.gz
 cat data8.bin

13-14 -
making a connection using private key  
>ssh -i sshkey.private bandit14@localhost -p 2220
cat /etc/bandit_pass/bandit14

14-15 - 
net cat for TCP UDP connections 
> cat  /etc/bandit_pass/bandit14 | nc localhost 30000      nc(netcat)

15-16 -
openssl exposes interactive pipeline (search about sockets)
> cat /etc/bandit_pass/bandit15 | openssl s_client -ign_eof localhost:30001

16-17 -
SSH refuses to use private keys that have loose read/write permissions. chmod 600 ensures that only the current user can access the key file.
> nmap localhost -p 31000-32000 --script ssl-enum-ciphers

17-18 - 
>diff passwords.old passwords.new

18-19 -
pass the commands with ssh to execute it immediately 
> sshpass -p `cat bandit18` ssh  bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"

19-20 -
SUID lets you run commands temporarily runs command with owner privileged 
> ./bandit20-do id    
 ./bandit20-do cat /etc/bandit_pass/bandit20
 
20-21 - 
use tmux , make one session listening using netcat and other triggering 
>echo -n "<bandit20_password>" | nc -l -p 44444
>./suconnect 44444

21-22 - 
cron jobs often write's output to /tmp directory 
>cd /etc/cron.d/    cat cronjob_bandit22  cat /usr/bin/cronjob_bandit22.sh  

22-23 - 
>echo I am user bandit23 | md5sum | cut -d ' ' -f 1
>cat/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv 

23-24 -
>cat cronjob_bandit24  
cat /usr/bin/cronjob_bandit24.sh   
myname=bandit24
cd /var/spool/"$myname"/foo
nano get.sh(script to redirect password to password.txt)   
chmod +x get.sh      
cat /tmp/john3/password.txt

24-25 -
>mkdir /tmp/bf_b24 && cd /tmp/bf_b24

Generate all 10,000 combinations into a single payload buffer
for pin in {0000..9999}; do
  echo "<bandit24_password> $pin"
done > wordlist.txt

Pipe the dictionary directly into the daemon port
nc localhost 30002 < wordlist.txt | grep -v "Wrong"

25-26 -
shrink your terminal it will give you a window to prompt more 
>more   
v for vim  
:r to read the password file   

26-27 - 
prompt in vim for jail breaking
>:set shell=/bin/bash   
shell  

27-28 -
clone git repo using absolute path on port 2220
>git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo      
cat README

28-29 -
>git log    
git show 26663cf19bf4014c5f9dc845b9e8feef90a84660   

29-30 - 
always inspect all branches (git never forgets)
>git checkout remotes/origin/dev     
git show 6a3b86581f1c4ba92a2ae86b3d62f95dd20b284f

30-31 - 
tag dereferencing 
>git tag
git show secret

31-32 -
Check repository instructions
>cat README.md

Create the requested file
echo "May I come in?" > key.txt

Bypass the existing .gitignore constraint
git add -f key.txt
git commit -m "Add authentication token"
git push origin master

32-33 -
$0 evaluates the currently executing process  
>$0     
cat /etc/bandit_pass/bandit33



