# Git for dummies using multiple accounts


### Linking a Git account to local machine

#### On Local
* Generate a ssh key for each of your personas (for example, 1 for your work persona, 1 for personal)
  
```
ssh-keygen -t rsa -b 4096 -C “rsec@work.com” -f "id_rsec_work"
--------------1---------- -------2----------    -----3-------

1. Command
2. Comment - tag with your persona email
3. id file name (if not provided, you will be prompted)
```
* Add this key to `~/.ssh/config`

```
Host bitbucket.org-rsec                (1)
    HostName bitbucket.org             (2)
    User git                           (3)
    IdentityFile ~/.ssh/id_rsec_work   (4)
    UseKeychain yes                    (5)

1. Provide a string to use for Host (for git clone)
2. Hostname domain ("bitbucket.org", "github.com", etc)
3. User is always "git"
4. The ssh key you created for this Host
5. UseKeychain is always "yes"
```

#### On Git
* Log on to your git account (on bitbucket.org here, following this example)
* Copy the ssh key you created on local (you will need to do this for every local machine you want to connect to your git account)
  * Copy to clipboard `cat ~/.ssh/id_rsec_work.pub | pbcopy .`
* Add the ssh key to this account (paste from clipboard)
  * Bitbucket.org: Login page > BitBucketSettings > SSH Keys
  * Github.com: Settings > SSG and GPG keys > Click button “New SSH Key”
* Save
* You can move on to cloning your Git repository

### Git clone

     git clone git@bitbucket.org-rsect:saas21/testdriven.io.git
     -------1----- ---------2--------- ---3-- -------4---------
     
     1. Does not change
     2. Host string specified in ~/.ssh/config file for this account
     3. Workspace
     4. Repository
