## SSH Login to Router using SSH Private/Public Key 

**Project description:** Instructions to setup SSH between Server and Router using Public/Private Key 

### 1. Generate Public and Private Key

``` sh
regress@r6:~$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/regress/.ssh/id_rsa): my_rsa
Enter passphrase (empty for no passphrase):   ===> No phrase used in this example
Enter same passphrase again: 
Your identification has been saved in my_rsa.
Your public key has been saved in my_rsa.pub.
The key fingerprint is:
SHA256:JxZ6Ls4wglfr8L/neLzMo0UljpUvyAMY/HSX9M5Q9Cc regress@r6
The key's randomart image is:
+---[RSA 2048]----+
| ..    ..oo      |
|  .o. . o+ .     |
|  .o.. .* o E .  |
|    .o * O   o   |
|    . * S =      |
| . . . * +       |
|. + + ..o        |
| . = = *=        |
|    o.B*=o       |
+----[SHA256]-----+

regress@r6:~$ ls -ltr
total 28
-rw-r--r-- 1 regress regress  392 Jun 20 02:15 my_rsa.pub  ==> public key
-rw------- 1 regress regress 1675 Jun 20 02:15 my_rsa  ===> private key

```

### 2. Copy the public key to Router;

```sh
** this method copies the public key to /var/home/<username>/.ssh/authorized_keys  in router

regress@r6:~$ ssh-copy-id -i ~/my_rsa.pub regress@10.49.167.137   
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/regress/my_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
Password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'regress@10.49.167.137'"
and check to make sure that only the key(s) you wanted were added.
```

### 3. Login to Router without password (if no phrase was entered during key generation)

```sh

==> Login from Server to Router 

regress@r6:~$ ssh -i my_rsa regress@10.49.167.137
Last login: Fri Jun 19 13:44:25 2020 from 10.49.167.14
--- JUNOS 18.2X75-D24.11 Kernel 64-bit  JNPR-11.0-20190316.df99236_buil
% 
root@IER:/var/home/regress # cd .ssh/
root@IER:/var/home/regress/.ssh # ls
authorized_keys.old
root@IER:/var/home/regress/.ssh # cat authorized_keys.old 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDIi0D9J0+65lxXDE1xk2c+4Pn4ej9zLTV7sQ4x0AgpOjS71JTHS+88------
------8tAyNKvvTTaMpIgrRGlBCpCxMJHiCrme3Ozxlsri65/Q0+9aMMXWxRT3GhNG9UY5H64YFOL regress@r6
root@IER:/var/home/regress/.ssh # 
```
