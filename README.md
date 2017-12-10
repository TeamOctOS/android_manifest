![Github Logo](https://i.imgflip.com/1we6lo.jpg)

TeamOctOS Android Source 2017
=========================

Getting Started
---------------

To get started with the TeamOctOS sources, you'll need to get
familiar with [Git and Repo](http://source.android.com/source/using-repo.html).


Creating Your SSH Keys
----------------------

Check to see if you already have existing SSH Keys.

    ls ~/.ssh

By default, SSH Keys are saved as: id_rsa and id_rsa.pub

If you do NOT have these files, continue.  If you DO have these, skip the next
step!

Note: If you already have existing SSH Keys, doing this will overwrite them! 

    cd ~
    ssh-keygen -t rsa

It will ask you where to store the key (defaults to ~/.ssh/id_rsa) and will ask if you
wish to enter a password.  If you enter a password, you will need to enter this EVERY
TIME.


Registering Your SSH Keys
-------------------------

We recommend (and will assume) that you are using your SSH Keys for GitHub and Gerrit
review.

    cat ~/.ssh/id_rsa.pub

This will display your PUBLIC SSH Key.  This is what you will put on GitHub and Gerrit,
and will be used to identify you to those services.

Please see GitHub's [Step 3: Add your SSH key to GitHub](https://help.github.com/articles/generating-ssh-keys/#step-3-add-your-ssh-key-to-github)
to add your key to your account.


Creating your SSH Config File
-----------------------------

After creating your SSH Key, you will need to create a configuration file so the system
will know to use these keys automatically.

Open your ~/.ssh/config file in your favorite editor (nano, gedit, vim, etc).

    nano ~/.ssh/config

and add the following code blocks.

    Host review.teamoctos.com
        User <Gerrit_UserName>
        IdentityFile ~/.ssh/id_rsa
        StrictHostKeyChecking no
        UserKnownHostsFile /dev/null
    Host github.com
        User <GitHub_Registered_Email>
        IdentityFile ~/.ssh/id_rsa
        StrictHostKeyChecking no
        UserKnownHostsFile /dev/null

and then save.  This will allow your system to automatically supply your SSH key when
connecting to these hosts.


Create the Directories
----------------------

You will need to set up some directories in your build environment.

To create them run:

    mkdir -p ~/bin
    mkdir -p ~/octos


Install the Repository Binary
-----------------------------

Enter the following to download the "repo" binary and make it executable:

    curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo

You may need to reboot for these changes to take effect. 
Now enter the following to initialize the repository:


Initialize the Repositories
---------------------------

    cd ~/octos
    repo init -u https://github.com/TeamOctOS/android_manifest.git -b oreo && repo sync

This will initialize the new repository and begin the initial sync.  This will take a while!