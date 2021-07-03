# Level -1

## Goal: log onto an SSH server with a username and port

The syntax for an SSH command is as follows:
`ssh <username>@<hostaddress> -p <portnumber>`

Thus for our purposes we need to write it as:
`ssh bandit0@bandit.labs.overthewire.org -p 2220`

# Level 0

-
-
-
-
find -exec file {} + | grep ASCII
find -size 1033c
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat data.txt | grep "millionth"
cat data.txt | sort | uniq -u
strings data.txt | grep "="
strings data.txt | grep "=" | base64 -d
cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
file (to find what type it is), then unpack it