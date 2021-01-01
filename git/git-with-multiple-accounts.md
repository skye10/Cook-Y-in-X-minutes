# Git with multiple accounts

### Problem

You have multiple Git accounts (e.g. one for work, another for play) and want to organize your local system to keep things separate.

### Strategy

Create a separate private/public key pair for each Git account. Add each Git account in your local ~/.ssh/config file.

### How to do it

These steps have been verified on OS X, should work similarly for a windows / linux system.

#### On Local

* Generate a ssh key for each of your accounts (for example, one for your work Git account, another for personal account). Example below shows ssh key generation for your work account. 
  
```
$ ssh-keygen -t rsa -b 4096 -c “me@work” -f "id_work"
             -------1------    ----2----    -----3---

Notes:
1. Options ("use algorithm RSA with key size 4096 bits")
2. -c ("comment") good practice: tag with your persona email
3. -f (file) file that stores the key
```
* The above command will generate two files containing private and the public keys:
  * 	`~/.ssh/id_work`, the private key
  * 	`~/.ssh/id_work.pub`, the public key
* As next step, add this key to `~/.ssh/config`. If this file doesn't exist, create one.

```
Host github-at-work               ...1
    HostName bitbucket.org        ...2
    User git                      ...3
    IdentityFile ~/.ssh/id_work   ...4
    UseKeychain yes               ...5

Notes:
1. Provide a string to use for this Git account ("github-at-work" in this case)
2. Hostname domain ("bitbucket.org", "github.com", etc)
3. User is always "git"
4. The ssh key you created for this Host
5. UseKeychain is always "yes"
```

#### On Git
* Log on to your git account
* Copy the ssh key you created on local (you will need to do this for every local machine you want to connect to your git account)
  * Copy to clipboard `cat ~/.ssh/id_work.pub | pbcopy .`
* Add the ssh key to this account (paste from clipboard)
  * Bitbucket.org: Login page > BitBucketSettings > SSH Keys
  * Github.com: Settings > SSG and GPG keys > Click button “New SSH Key”

You are all set and ready to clone and use your Git repository.

#### Git clone
To clone the repository, use this command:

     git clone git@github-at-work:path/to/repository.git
               ---------1-------- ---------2------------
     
     1. Host string specified in ~/.ssh/config file for this account
     2. Path to the repository you want to clone
     
