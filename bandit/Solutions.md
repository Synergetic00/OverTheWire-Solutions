# Level -1

## Goal: log onto an SSH server with a username and port

Commands used: `ssh`

The syntax for an SSH command is as follows:
`ssh <username>@<hostaddress> -p <portnumber>`

Thus for our purposes we need to write it as:
`ssh bandit0@bandit.labs.overthewire.org -p 2220`

# Level 0

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

```
bandit0@bandit:~$ ls
readme

bandit0@bandit:~$ cat readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

# Level 1

The password for the next level is stored in a file called - located in the home directory

```
bandit1@bandit:~$ ls
-

bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

# Level 2

The password for the next level is stored in a file called spaces in this filename located in the home directory

```
bandit2@bandit:~$ ls
spaces in this filename

bandit2@bandit:~$ cat "spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

## Level 3

The password for the next level is stored in a hidden file in the inhere directory.

```
bandit3@bandit:~$ ls
inhere

bandit3@bandit:~$ cd inhere

bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden

bandit3@bandit:~/inhere$ cat ./.hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## Level 4

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

### Solution

Using the `find` command we can search the directory. Since we need human readable text we need to examine what is in ASCII, so we can run the `-exec <command> {} +`, for the command section we can use file, which tells what the metadata's header matches to. So can combine these using all of the above to list the file types in the directory.

Then we can use a technique in shells called the pipe, delimiting commands with `|` which allows for the passing out the outputs to the next command instead of the stdin of the user or the file system. If the list was alot longer or has multiple results, we can use the `grep` command with a string to search on each individual line.

```
bandit4@bandit:~$ ls
inhere

bandit4@bandit:~$ cd inhere

bandit4@bandit:~/inhere$ ls -a
.  ..  -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

bandit4@bandit:~/inhere$ find -exec file {} +
.:         directory
./-file01: data
./-file00: data
./-file06: data
./-file03: data
./-file05: data
./-file08: data
./-file04: data
./-file07: ASCII text
./-file02: data
./-file09: data

bandit4@bandit:~/inhere$ find -exec file {} + | grep "ASCII"
./-file07: ASCII text

bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## Level 5

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

* human-readable
* 1033 bytes in size
* not executable

### Solution

```
bandit5@bandit:~$ ls
inhere

bandit5@bandit:~$ cd inhere

bandit5@bandit:~/inhere$ ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19

bandit5@bandit:~/inhere$ find -size 1033c ! -executable -exec file {} + | grep "ASCII"
./maybehere07/.file2: ASCII text, with very long lines

bandit5@bandit:~/inhere$ cat "./maybehere07/.file2"
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

However, since there is only one file with 1033 bytes, you can use just `find -size 1033c`

## Level 6

find / -user bandit7 -group bandit6 -size 33c 2>/dev/null

## Level 7

cat data.txt | grep "millionth"

## Level 8

cat data.txt | sort | uniq -u

## Level 9

strings data.txt | grep "="

## Level 10

strings data.txt | grep "=" | base64 -d

## Level 11

cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'

## Level 12

file (to find what type it is), then unpack it

## Level 13
## Level 14
## Level 15
## Level 16
## Level 17
## Level 18
## Level 19
## Level 20
## Level 21
## Level 22
## Level 23
## Level 24
## Level 25
## Level 26
## Level 27
## Level 28
## Level 29
## Level 30
## Level 31
## Level 32
## Level 33
## Level 34