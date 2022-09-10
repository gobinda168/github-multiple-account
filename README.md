# Github-multiple-account

## Problem
I have 2 different github account one for work and other one for personal. I want to use both on same pc

## Solution
Use ssh keys and define host aliases in ssh config file (each alias for an account).

## Solution
Use ssh keys and define host aliases in ssh config file (each alias for an account).

## How to?
1. [Generate ssh key pairs for accounts](https://help.github.com/articles/generating-a-new-ssh-key/) and [add them to GitHub accounts](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/).
2. Edit/Create ssh config file (`~/.ssh/config`):

   ```conf
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
   ```
   
3. [Add ssh private keys to your agent](https://help.github.com/articles/adding-a-new-ssh-key-to-the-ssh-agent/):

   ```shell
   $ ssh-add ~/.ssh/gobinda_private_key
   $ ssh-add ~/.ssh/gobinda_work_private_key
   ```

4. Test your connection

   ```shell
   $ ssh -T git@gobinda
   $ ssh -T git@gobinda-work
   ```

   With each command, you may see this kind of warning, type `yes`:

   ```shell
   The authenticity of host 'github.com (192.30.252.1)' can't be established.
   RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:
   Are you sure you want to continue connecting (yes/no)?
   ```

   If everything is OK, you will see these messages:

   ```shell
   Hi gobinda! You've successfully authenticated, but GitHub does not provide shell access.
   ```
   
   ```shell
   Hi gobinda-work! You've successfully authenticated, but GitHub does not provide shell access.
   ```

5. Now all are set, just clone your repositories

   ```shell
   $ git clone git@gobinda-work:org2/project2.git /path/to/project2
   $ cd /path/to/project
   $ git config user.email "gobinda@org.com"
   $ git config user.name  "gobinda-work"
