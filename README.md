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
