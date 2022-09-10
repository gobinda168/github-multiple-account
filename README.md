# Github-multiple-account

## Problem
I have 2 different github account one for work and other one for personal. I want to use both on same pc

## Solution
Use ssh keys and define host aliases in ssh config file (each alias for an account).

How to?
Generate ssh key pairs for accounts and add them to GitHub accounts.

Edit/Create ssh config file (~/.ssh/config):

# Default github account: gobinda
Host github.com
   HostName gobinda
   IdentityFile ~/.ssh/gobinda_private_key
   IdentitiesOnly yes
   
# Other github account: gobinda-work
Host gobinda-work
   HostName github.com
   IdentityFile ~/.ssh/gobinda_work_private_key
   IdentitiesOnly yes
Add ssh private keys to your agent:

$ ssh-add ~/.ssh/gobinda_private_key
$ ssh-add ~/.ssh/gobinda_work_private_key
Test your connection

$ ssh -T git@github.com
$ ssh -T git@github-superman
With each command, you may see this kind of warning, type yes:

The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:
Are you sure you want to continue connecting (yes/no)?
If everything is OK, you will see these messages:

Hi gobinda! You've successfully authenticated, but GitHub does not provide shell access.
Hi gobinda-work! You've successfully authenticated, but GitHub does not provide shell access.
Now all are set, just clone your repositories

$ git clone git@github-gobinda-work:org/project2.git /path/to/project2
$ cd /path/to/project2
$ git config user.email "gobinda-work@org.com"
$ git config user.name  "gobinda-work"
Thats it! All Set!
