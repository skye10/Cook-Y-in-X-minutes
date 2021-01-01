# Git with multiple accounts

### Problem

You have multiple Git accounts (e.g. one for work, another for play) and want to organize your local system to keep things separate.

### Strategy

Create a separate private/public key pair for each Git account. Add each Git account in your local ~/.ssh/config file.

### How to do it

These steps have been verified on OS X, should work similarly for a windows / linux system.

#### On Local

Generate a ssh key for each of your accounts (for example, one for your work Git account, another for personal account). Example below shows ssh key generation for your work account. 

```
$ ssh-keygen -t rsa -b 4096 -c “me@work” -f "id_work"
             -------1------    ----2----    -----3---
```
* Guide:
  1. Options ("use algorithm RSA with key size 4096 bits")
  2. `-c` option is a comment. As a matter of practice, I tag it with my email (work email in this case)
  3. `-f` option is the filename that stores the private/public keys (the public key has an extension `.pub`)

The following files containing private/public keys are created as a result of the above command:

* 	`~/.ssh/id_work`, the private key
* 	`~/.ssh/id_work.pub`, the public key

As next step, add the private key to the config file `~/.ssh/config`. If the config file doesn't exist, create one.

```
Host github-at-work               ...1
    HostName bitbucket.org        ...2
    User git                      ...3
    IdentityFile ~/.ssh/id_work   ...4
    UseKeychain yes               ...5
```

* Guide:
  1. Provide a string to use for this Git account ("github-at-work" in this case)
  2. Hostname domain ("bitbucket.org", "github.com", etc)
  3. User is always "git"
  4. The ssh key you created for this Host
  5. UseKeychain is always "yes"

Save the above file. Now you are ready to set up your Git account to synchronize with your local system, and clone a repository.

#### On Git

* Log on to your git account
* Copy the ssh key you created on local (you will need to do this for every local machine you want to connect to your git account)
  * Copy to clipboard `cat ~/.ssh/id_work.pub | pbcopy .`
* Add the ssh key to this account (paste from clipboard)
  * Bitbucket.org: BitBucketSettings > SSH Keys
  * Github.com: Settings > SSG and GPG keys > Click button “New SSH Key”

You are now ready to clone your Git repository.

#### Clone your repository
To clone a repository, use this command on your local system:

     git clone git@github-at-work:path/to/repository.git
               ---------1-------- ---------2------------

* Guide:
  1. Host string specified in ~/.ssh/config file for this account
  2. Path to the repository you want to clone

