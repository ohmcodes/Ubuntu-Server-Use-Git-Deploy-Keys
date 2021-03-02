# Ubuntu-Server-Use-Git-Deploy-Keys

This guide will teach you how to use Github Deploy keys in your Hosting server here Im gonna use AWS lightsail Ubuntu 20

## Creating Keygen
```
ssh-keygen -t rsa -b 4096 -C "your-email@email.com"

this will appear

Generating public/private rsa key pair.
Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa):

just press ENTER or for advance user you can put a name on it and it will save to current directory you are on.

Enter passphrase (empty for no passphrase):

Enter (bypass) or put passphrase for more security

if you put passphrase it will ask you to do it again

Enter same passphrase again:

Your identification has been saved in <if_you_rename_the_key> or else it will save to /home/ubuntu/.ssh/id_rsa
Your public key has been saved in <if_you_rename_the_key>.pub or /home/ubuntu/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:ciEKjS5LaC76asdqwesqweqweqwxcwerqweqwdasdas ubuntu@ip-<your-hosting-ip-address>
The key's randomart image is:
+---[RSA 3072]----+
|8====D . oo..+o. |
|   o  . . o.o.o.o|
|  o ...... o . oo|
|.. . .+.o.. + .  |
|oo.o.+.+So o o   |
|+o+ E =o  o . .  |
|o. o   .   + . . |
|oo.         + .  |
|ooo 8======D .   |
+----[SHA256]-----+

```

## Create config file
```
sudo nano ~/.ssh/config

Host gitreponame
Hostname github.com
IdentityFile "~/.ssh/id_rsa"

Note: 
"Host" will be your <change_this_with_your_host_in_config_file> later on
"IdentityFile" will be your id_rsa (default) if you change it and changed its location you must indicate here

Note: to be sure change the file permission of id_rsa to 400

sudo chmod 400 ~/.ssh/id_rsa

Change the config file to 644

sudo chmod 644 ~/.ssh/config

```

## Opening Pub file and Copy/Paste for Deploy Keys
```
type in:
cat ~/.ssh/id_rsa.pub
```
#### then copy the keygen and go to your repo (note: not in your account settings) and navigate to settings find Deploy Keys tab
then create new Deploy keys name a title and paste the keygen 


#### Go back to your console and type in:
```
eval `ssh-agent`
```

#### Make sure you use the backquote (`), located under the tilde (~), rather than the single quote (').

```
type in:
ssh-add

Enter passphrase (empty for no passphrase):
```
#### this will save your ssh passphrase so whenever you run git pull it will not ask for passphrase


#### Navigate to your repo and check the remote URL
```
git remote -v

if its...
origin https://github.com/USERNAME/REPOSITORY.git

if its under your account
git remote set-url origin git@<change_this_with_your_host_in_config_file>:USERNAME/REPOSITORY.git

if its under an organization
git remote set-url origin git@<change_this_with_your_host_in_config_file>:ORGANIZATION/REPOSITORY.git

```

### Enjoy! :)
