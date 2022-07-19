# Steps to set up SSH keys for github

- ### _*STEP 1*_ : Generate SSH keys 

    ```
    ssh-keygen
    ```
    
    The public and private keys will be stored in the directory _home/.ssh_ 

- ### _*STEP 2*_ : Move to the directory .ssh and create a folder github 

    ```
    cd ~/.ssh   
    mkdir -p github   
    ```

- ### _*STEP 3*_ : Move the generated key files to github folder

    ```
    mv id* github/ 
    ```
    Since the key files start with 'id', both the files are moved to the github folder

- ### _*STEP 4*_ : Rename the key files to something which is readble

    ```
    cd github 
    mv id_ed25519 <some filename>
    mv id_ed25519.pub <some filename>.pub 
    ```

- ### _*STEP 5*_ : Create 'config' file in vsc from .ssh directory

    ```
    cd ..           # going to parent directory of github which is .ssh  
    code config 
    ```
    Save the file with required configurations

    Eg :
    ```
    Host github.com-<key filename>
    HostName github.com
    User git
    IdentityFile /home/<user>/.ssh/github/<key filename>


    Host *
        ServerAliveInterval 240
    ```

- ### _*STEP 6*_ : Create .gitconfig file in vsc from home directory 

    ```
    cd 
    code ~/.gitconfig 
    ```

    Save the file with required global configurations common to all repos

    Eg :
    ```
    [user]
	name = <your name>
	email = <your email id>

    [includeIf "gitdir:/home/<user>/clients/git/<your folder>/"]
        path = /home/<user>/clients/git/gitconfig.ofm

    [core]
        excludesfile = ~/.gitignore
    [cola]
        spellcheck = false
        icontheme = dark
        theme = flat-dark-red
        boldheaders = true
        statusshowtotals = true
        statusindent = true
    [init]
        defaultBranch = ""
    ```

- ### _*STEP 7*_ : Create the directory clients/git/< some foldername> in home

    ```
    mkdir -p clients/git/<some folder name> 
    ```

- ### _*STEP 8*_ : Open gitconfig.< ssh key file name> from the above directory 

    ```
    code gitconfig.<ssh key file name>
    ```
    Add the contents in vsc and exit 

    Eg :
    ```
    [user]
    email = <your email id>
    name = <your github acc name>
    
    [github]
    user = <github username>

- ### _*STEP 9*_ : Copy the the public ssh key and add it to your github acc 

    ```
    cd ~/.ssh/github 
    cat <sshkey filename>.pub 
    ```

- ### _*STEP 10*_ : Add the identity 

    ```
    ssh-add <ssh key filename> 
    ```

- ### _*STEP 11*_ : Move to clients/git/< your foldername>; add known hosts

    ```
    cd ~/clients/git/<some folder name of ur choice>
    ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts 
    ```

- ### _*STEP 12*_ : Try to Clone a repo 

    ```
    git clone git@github.com-<ssh key filename>:......git
    ```

## NOTE :

CONFIGURATION FILES :

1) .gitconfig 
    - global configuration file common for all repos of that github acc
    - Directory : home

2) config 
    - to connect with github host via ssh keys
    - Directory : home/.ssh 

3) gitconfig.ps 
    - to save github acc credentials 
    - Directory: home/clients/git/< your folder name>

## REFERENCES :

- [Set up SSH Keys for Github](https://youtu.be/8X4u9sca3Io)

- [Multiple SSH keys for multiple Github accounts](https://gist.github.com/jexchan/2351996)

