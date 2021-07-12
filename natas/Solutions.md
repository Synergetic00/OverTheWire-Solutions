## Level 0

```
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

### Solution

We can view the source code of a website in Chrome by adding the prefix `view-source:` to the URL to view the HTML program, and in the page there is a comment with the password.

## Level 1

```
Username: natas1
Password: gtVrDuiDfck831PqWsLEZy5gyDz1clto
URL:      http://natas1.natas.labs.overthewire.org
```

### Solution

Although normally, on Chrome you can right click on text and select `View page source`, but again using the method above we can find the source code again with a comment, additionally you can use the shortcut `Ctrl + U`.

## Level 2

```
Username: natas2
Password: ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi
URL:      http://natas2.natas.labs.overthewire.org
```

### Solution

By viewing the source again we see no comments that give clues, just an image with a source from a `files` folder: `<img src="files/pixel.png">`. We can then go to the directory that contains this image and see that there is another file called `users.txt` with the password in it.

## Level 3

```
Username: natas3
Password: sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
URL:      http://natas3.natas.labs.overthewire.org
```

### Solution

This is a tricky one, but the clue lies in the comment "Not even Google will find it this time", since Google uses webcrawlers, developers use `robots.txt` on the root directory of the website to store relevant information for the search engine.

From this file, we can see this line `Disallow: /s3cr3t/` This means they're blocking the folder called `s3cr3t` from being indexed by the search engine, this directory contains `users.txt`.

## Level 4

```
Username: natas4
Password: Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
URL:      http://natas4.natas.labs.overthewire.org
```

### Solution

This one requires an external program for my solution called `Insomnia`, which is used for writing your own custom web requests and getting a detailed response back, from the text of the website when we first visit, there is no text in the quotes, but when we hit the `Refresh page` button we load this page from a page link and , if we open the `Network` panel by pressing `F12` or right-clicking, selecting `Inspect` and going to the tab, hitting the refresh button and finding the entry for `index.php` we can open the request headers, which is the metadata being sent to the web server and there is a field called `Referer`, which from looking up the documentation is "The address of the previous web page from which a link to the currently requested page was followed.", so if we use Insomnia to create a request with `header = Referer` and `value = http://natas5.natas.labs.overthewire.org/` and a `GET` type request to the website, we can trick the web server into thinking we came from natas5 and get the password. Also if you're getting an authentication error, go to the `Auth` tab, select `Basic Auth` from the drop down menu and put in the username and password.

## Level 5

```
Username: natas5
Password: iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
URL:      http://natas5.natas.labs.overthewire.org
```

### Solution

When we first visit the website, we get this message "Access disallowed. You are not logged in", we can setup the request to the website again with the authentication fields filled like before, but now there is a tab called cookies, which could also be seen in the Network tab in the browser, there is a cookie called `loggedin` with a value of `0`, we can manage and edit this cookie to have the value set to 1 instead: `loggedin=1; Path=/; Domain=natas5.natas.labs.overthewire.org`.

## Level 6

```
Username: natas6
Password: aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
URL:      http://natas6.natas.labs.overthewire.org
```

### Solution

After reviewing the source code there is a PHP script in the HTML file with a references file: `include "includes/secret.inc";`, navigating to this file gives the secret key as `FOEIUWGHFEEUHOFUOIU`, we then can put this into the text box input on the page for our password.

## Level 7

```
Username: natas7
Password: 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
URL:      http://natas7.natas.labs.overthewire.org
```

### Solution

From the source code we can see that other pages can be accessed using a query string parameter `<url>?page=<pagename>` and it returns different text for either home or about, looking at the comments on the source code, it says "stuff in the header has nothing to do with the level" and "password for webuser natas8 is in /etc/natas_webpass/natas8" as hints. So if we put this as the argument in the query string like `index.php?page=/etc/natas_webpass/natas8` we get the password.

## Level 8

```
Username: natas8
Password: DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
URL:      http://natas8.natas.labs.overthewire.org
```

### Solution

This requires another key, but looks like they've encrypted the key now, but, they left the encryption algorithm in the code, so we can use similar functions to undo the encodings to find the original password. The code for encrypting is `bin2hex(strrev(base64_encode($secret)))`, which go as follows: plain text -> base64 -> reversed -> binary to hex, thus we can undo it by using these PHP commands `base64_decode(strrev(hex2bin($secret)))`, thus getting our key for this stage: `oubWYf2kBq`, putting this in the input gives us the password.

## Level 9

```
Username: natas9
Password: W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
URL:      http://natas9.natas.labs.overthewire.org
```

### Solution

From examining the source code we can see something very interesting, there is a command used call `passthru()` with a `grep` command, these appear to be running commands on the shell through the browser input, thus since it doesn't seem to be filtered we can do remote code execution. They setup the function like this `passthru("grep -i $key dictionary.txt");`, so our input will go where the `$key` is, so we can put some junk data where the grep is looking and terminate the command with `;` and append another command after, thus we can test this by running just `test; ls` and the Output field on the website is connected to the console's stdout. We know the passwords are in `/etc/natas_webpass/natas10` for this level, then we can use the `cat` command to view the contents of the file. So the final input will be `test; cat /etc/natas_webpass/natas10`

## Level 10

```
Username: natas10
Password: nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
URL:      http://natas10.natas.labs.overthewire.org
```

### Solution

From viewing the source code again, we see that the author has included another check to filter his inputs with `preg_match('/[;|&]/',$key)`, this means we cannot have a semi-colon in the input, thus we will have to use the feature in grep, so that we can check multiple files like `grep -i <term> <file1> <file2> <file3>`, thus we can find our password in `/etc/natas_webpass/natas11` and then it'll search the `dictionary.txt`, we can use regex to search for any input with `.*`, which means match any character an abritrary number of times. So combining all of these we can input `.* /etc/natas_webpass/natas11`

## Level 11

```
Username: natas11
Password: U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
URL:      http://natas11.natas.labs.overthewire.org
```

### Solution

## Level 12

```
Username: natas12
Password: 
URL:      http://natas12.natas.labs.overthewire.org
```

### Solution

## Level 13

```
Username: natas13
Password: 
URL:      http://natas13.natas.labs.overthewire.org
```

### Solution

## Level 14

```
Username: natas14
Password: 
URL:      http://natas14.natas.labs.overthewire.org
```

### Solution

## Level 15

```
Username: natas15
Password: 
URL:      http://natas15.natas.labs.overthewire.org
```

### Solution

## Level 16

```
Username: natas16
Password: 
URL:      http://natas16.natas.labs.overthewire.org
```

### Solution

## Level 17

```
Username: natas17
Password: 
URL:      http://natas17.natas.labs.overthewire.org
```

### Solution

## Level 18

```
Username: natas18
Password: 
URL:      http://natas18.natas.labs.overthewire.org
```

### Solution

## Level 19

```
Username: natas19
Password: 
URL:      http://natas19.natas.labs.overthewire.org
```

### Solution

## Level 20

```
Username: natas20
Password: 
URL:      http://natas20.natas.labs.overthewire.org
```

### Solution

## Level 21

```
Username: natas21
Password: 
URL:      http://natas21.natas.labs.overthewire.org
```

### Solution

## Level 22

```
Username: natas22
Password: 
URL:      http://natas22.natas.labs.overthewire.org
```

### Solution

## Level 23

```
Username: natas23
Password: 
URL:      http://natas23.natas.labs.overthewire.org
```

### Solution

## Level 24

```
Username: natas24
Password: 
URL:      http://natas24.natas.labs.overthewire.org
```

### Solution

## Level 25

```
Username: natas25
Password: 
URL:      http://natas25.natas.labs.overthewire.org
```

### Solution

## Level 26

```
Username: natas26
Password: 
URL:      http://natas26.natas.labs.overthewire.org
```

### Solution

## Level 27

```
Username: natas27
Password: 
URL:      http://natas27.natas.labs.overthewire.org
```

### Solution

## Level 28

```
Username: natas28
Password: 
URL:      http://natas28.natas.labs.overthewire.org
```

### Solution

## Level 29

```
Username: natas29
Password: 
URL:      http://natas29.natas.labs.overthewire.org
```

### Solution

## Level 30

```
Username: natas30
Password: 
URL:      http://natas30.natas.labs.overthewire.org
```

### Solution

## Level 31

```
Username: natas31
Password: 
URL:      http://natas31.natas.labs.overthewire.org
```

### Solution

## Level 32

```
Username: natas32
Password: 
URL:      http://natas32.natas.labs.overthewire.org
```

### Solution

## Level 33

```
Username: natas33
Password: 
URL:      http://natas33.natas.labs.overthewire.org
```

### Solution

## Level 34

```
Username: natas34
Password: 
URL:      http://natas34.natas.labs.overthewire.org
```

### Solution
