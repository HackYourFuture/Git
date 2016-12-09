Tutorial for HackYourFuture Git basics. This tutorial has three sections:
1. Git
2. GitHub
3. Using Git

# 1. Git: 

## 1.1 What is Git, Etymology and a short history.
———————————————————————---------------------------
Distributed version control system
Linus Torvalds, 2005
GIT: Global Information Tracker or the stupid content tracker or unpleasant person in British slang

## 1.2 Installing Git
 ————————------------
 For Windows,
 install Git for Windows:
 https://github.com/git-for-windows/git/releases/tag/v2.10.2.windows.1

 For Linux, open gnome-terminal for GNome desktops  or Konsole for KDE desktops and type the command to install git based on your Linux distribution. 

 For a RedHat based Linux (Like CEntOS)
 sudo yum install git

 For Fedora
 sudo yum install git-core

 For a Debian based Linux (like Ubuntu)
 sudo apt-get install git 

 For Arch Linux
 sudo paceman -Sy git

 For Gentoo Linux
 sudo emerge ask —verbose dev-util/git

 For a MAC, open Terminal and execute following command
 brew install git

# 2. GitHub: 

## 2.1 What is GitHub 
 —————————-----------
 GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

 Registering/Creating the account on GitHub
 You need
* A valid Email address
* An SSH key-pair

 For you to be able to communicate with Github securely, you have to generate an ssh keypair, and then register it on the Github website.

## 2.2 Generating the ssh keypair
 ———————————————-----------------

 For Windows MSysGit/GitBash command prompt use
```
ssh-keygen.exe -C "username@email.com" -t rsa
```

```
 For Linux/MAC, use
ssh-keygen -C "username@email.com" -t rsa
```

Supply your Github email address instead of this fake one. 
Accept the default location storage (default file) for the keys. When prompted for a passphrase, make up one, and don't forget it ! This is your private key, do not share it with anyone.
You will have id_rsa and id_rsa.pub files in the directory at the following path /c/Users/<your_user_name>/.ssh/

 You want to copy the contents of the id_rsa.pub (open it with a simple text editor or use the command cat in the Bash)
 After you copy the contents of the id_rsa.pub file, Go to the GitHub account, settings and SSH/GPG keys and add this key.


# 3. Using Git

## 3.1 Creating the repository
-—————————————----------------
 create a new directory
 `mkdir hello-world`
 Enter it 
 `cd hello-world`
 and perform a 
 `git init`
 to create a new git repository.

## 3.2 Workflow
 ————————------
 Working Directory -> Index -> HEAD
 your local repository consists of three "trees" maintained by git. the first one is your Working Directory which holds the actual files. the second one is the Index which acts as a staging area and finally the HEAD which points to the last commit you've made.

 configure your email and username of Github in the git
 ```
 git config --global user.email "username@email.com"
 git config --global user.name "username"
```

 Make sure that the username is the one you used for the github account.

## 3.3 add and commit
 ——————————----------
 You can propose changes (add it to the Index) using
 git add <filename>
 git add *
 This is the first step in the basic git workflow. To actually commit these changes use
 git commit -m "Commit message"

## 3.4 Pushing changes
 ——————————-----------
 If you have not cloned (Our case) an existing repository and want to connect your repository to a remote server, you need to add it with
 git remote add origin <server>
 where
 <server> : https://github.com/user/repo.git
 Now you are able to push your changes to the selected remote server i.e. your remote repository on GitHub.
 Your changes are now in the HEAD of your local working copy. To send those changes to your remote repository, execute 
 git push -u origin master


