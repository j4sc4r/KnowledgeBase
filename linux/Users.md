# Users

> create user
```bash
useradd <name>
```

>change password
```bash
passwd <name>
```

>create group
```bash
groupadd <name>
```

>modify user with a group
```bash
usermod -aG <groupname> <username>
```

>user password informations
```bash
chage -l <username>
```

>set a user expiredate
```bash
chage -E $(date -d +90days +%Y-%m-%d) <username>
```

>better way to set passwords 
```bash 
echo <password> | passwd --stdin tony
```

>locking user account
```bash
passwd -l <username>
OR
usermod -L <username>
```

>delete a user with "-R" you will delete user home directory 
```bash
userdel <username>
OR 
userdel -R <username>
```


