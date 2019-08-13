
# Laravel Forge + Visual Studio Remote
Connect Visual Studio Remote to a Laravel Forge Managed Server on Windows 10.

## About
This is a setup guide on how to connect Visual Studio Code (SSH) to a Laravel Forge Managed Server.

## Requirements

 1. [Laravel Forge](https://forge.laravel.com)
 2. [Visual Studio Code](https://code.visualstudio.com/)
 3. [Remote Development Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
 4. Windows 10 (This guide was made for windows 10)

## Guide
### Step 1: Provision your Laravel Server
This guide will not be going over how to provision a laravel forge server. For information on this I recommend this serires form LaraCasts: [Learn Forge](https://laracasts.com/series/learn-laravel-forge).
### Step 2: Install Visual Studio Code + Remote Development Extension
Install [Visual Studio Code](https://code.visualstudio.com/), [Remote Development Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack).
### Step 3: Activate OpenSSH in Windows Features
Go to *Apps & Features* in windows, click *Manage optional features* then *Add a feature*, then find *OpenSSH Client* and *OpenSSH Server* and activate them. If they do not appear in the list, check and see if they were already installed by backing out and looking for them inside the list.

<img src="https://github.com/pkeogan/laravel-forge-visual-studio-remote-setup/blob/master/act-openssh.GIF">
### Step 4: Create a Private + Public Keypair with OpenSSH
Open *Command Prompt* and run 
```
ssh-keygen -t rsa -b 4096
```
this will create the needed private and public key's on your computer in the folder `C:/users/{username}/.ssh/`
**PLEASE NOTE: if you use an existing generated key pair, or putty, you will run into permissions errors.**
### Step 5: Add the public key to Forge Managed Server
Open up the public key that was created @ `C:/users/{username}/.ssh/id_rsa.pub` with note pad or visual studio code, copy then contents and paste into the SSH Keys on Forge. Then click *Apply*.

<img src="https://github.com/pkeogan/laravel-forge-visual-studio-remote-setup/blob/master/paste-ssh-into-forge.png">

### Step 6: Add connection to Visual Studio Code.
Launch Visual Studio Code, then click on the *Remote-SSH* tab, then click the gear icon to the right of *connections* then click the first file the appears in the dropdown.

Replace the file with the following template: 
```
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config
Host {host}
	HostName {insert-ip}
	User forge
	IdentityFile C:\Users\{insert-username}\.ssh\id_rsa
	StrictHostKeyChecking no
```

**Host:** is used just for reference
**HostName :**  public IP of the forge server you created.
**IdentityFile :** points to the private key you made in step 4. just place your desktops username in the curly bracket.

Click save once done.

<img src="https://github.com/pkeogan/laravel-forge-visual-studio-remote-setup/blob/master/config-paste.png">

### Step 7: Connect to your Forge Server
click on the *Remote-SSH* tab, then right click on the host you just created and launch the connection. Your all done!
<img src="https://github.com/pkeogan/laravel-forge-visual-studio-remote-setup/blob/master/connect.gif">

