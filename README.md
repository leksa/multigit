# Setting Multi Git Account in Your Local Machine

## Step 1 - Create a new SSH Key
Generate new SSH key for our second or more GitHub/another Git account. In your computer, open the terminal and type: 

`ssh-keygen -t rsa -C "your-email-address`

>This command will ask you to provide the name of this RSA key. Be careful that you don't over-write your existing key for your
> personal account. You can use unique name at the end of the name like `~/.ssh/id_rsa_MYKEYFORYOU`. Please make user you have the .ssh folder in your $HOME . You can make one if this is your new SSH key process.

## Step 2 - Add your SSH Key to github (or another git platform)
In this example we use Github. Login to your target GitHub account, browse to "Account Overview," and add the new key, within the "SSH Public Keys" section. 
To retrieve the value of the key that you just created, return to the Terminal, and type: 

`cat ~/.ssh/id_rsa_UNIQUE.pub`

Copy the entire string that is displayed, and paste this into the GitHub textarea. Give a specific name so you know this key is yours.

## Step 3 - SSH-add the unique RSA key
Because we saved our key with a unique name, we need to tell our SSH about it. Within the Terminal, type: 

`ssh-add ~/.ssh/id_rsa_UNIQUE`. 

Follow the process and if successful, you'll see a response of "Identity Added."

## Step 4 - Create a config file inside .ssh folder
Make config file with this command.

    touch ~/.ssh/config
    nano config

> I use nano here. You can use vim or else.

Write this configuration in the file 
	
    #Default GitHub
    Host github.com
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_rsa

    #UNIQUE GitHub
    Host github-UNIQUE
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_rsa_UNIQUE

We make two configuration here. The first one is for caution if you have the default github account before. The second one is your UNIQUE SSH access to another repository account. Remember we have change the HOST to github-UNIQUE.

## Step 4 - Try it Out
Make a repository in your new Github account. Let say your new account is NARNIA.  And your new repository is "Test".  

Because this is just a test, try to make a new file inside the repository. You can do this by thick "*Initialize this repository with a README* " or "*Add a LICENSE*".  After successfully  create the repository, You'll have a "Test" repository with a file inside it.

Please check the clone button. You will get the link for SSH clone

`git@github.com:narnia/test.git`

Copy this remote SSH clone. 

Back to your computer, make a new folder for test repo. Do your git init in the folder, so you're ready to work with Git.

`git init`

And then the important part is connect your test repo folder to remote git repository. Remember you need to use the UNIQUE HOST that we have set before. Change the "github.com" to the "github-UNIQUE".

`git remote add origin git@github-UNIQUE:narnia/test.git`

## Step 5 - Run your first pull

`git pull origin master`

Congrats! You have connected to the new repo and success to pull the README file (or a LICENSE file).
