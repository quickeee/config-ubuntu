# Config Ubuntu

This is primarily a __Debian__ based OS, such as __Debuan__, __Ubuntu__, __Mint__, and __Elementary OS__.

# Table of Contents
- [OS Downloads](#os-downloads)
- [Optional Configurations](#optional-configurations)
- [VIM Customization](#vim-customization)
- [Installation Packages](#installation-packages)
	- [Use 32Bit on 64bit](#use-32bit-on-64bit)
	- [Enable PPA](#enable-ppa)
	- [System Tools](#system-tools)
		- [Numix Theme](#numix-theme)
		- [Utilities](#utilities)
		- [Wine](#wine)
	- [LAMP](#lamp)
		- [PHP5](#php5)
		- [Apache](#apache)
		- [Nginx](#nginx)
		- [MySQL](#mysql)
		- [Redis](#redis)
		- [Phalcon](#phalcon)
		- [Phalcon Dev Tools](#phalcon-dev-tools)
	- [Python](#python)
	- [Ruby](#ruby)
	- [NodeJS](#nodejs)
	- [Google Chrome](#google-chrome)
- [Virtual Machine Related](#virtual-machine-related)
	- [Fix Mouse Side Buttons in VMWare](#fix-mouse-side-buttons-in-vmware)
	- [Vagrant VBGuest Fix](#vagrant-vbguest-fix)
	- [Windows 8 VirtualBox Fix](#windows-8-virtualbox-fix)
	- [Install ATI Drivers](#install-ati-drivers)
	- [Remove ATI Drivers](#remove-ati-drivers)
- [Other Applications](#other-applications)

***

[(Back to top)](#table-of-contents)

# OS Downloads  

- [Ubuntu Desktop](http://ubuntu.com/desktop)
- [Elementary Desktop](http://elementaryos.org/)
- [Linux Mint](http://www.linuxmint.com/)

***

[(Back to top)](#table-of-contents)

# Optional Configurations  
- Some items (`termatinator`, `virtualenvs`) copied from [Dan Sackett](https://github.com/dansackett/dotfiles).

***
[(Back to top)](#table-of-contents)

# VIM Customization  

**Setup VIM**

	git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim

	$ vim
	:PluginInstall

**Set Capslock key to Esc**

	$ dconf write /org/gnome/desktop/input-sources/xkb-options "['caps:escape']

***

[(Back to top)](#table-of-contents)

# Installation Packages  

Login to your Linux user and go to your **home** directory, 
 
	cd ~

Run these commands and tweak them as needed. The `-y` flag installs without a prompt. Run these commands from the terminal.

    sudo apt-get update && sudo apt-get upgrade

## Use 32Bit on 64bit  

You can use 32Bit applications if you like, sometimes this is useful.

    sudo apt-get update && sudo apt-get install -y unetbootin

## Enable PPA 
PPA's are provided within cateogories below, I highly recommend using PPA's or atleast installing this package incase you ever use them.

    sudo apt-get install -y python-software-properties

## System Tools  
This is for tweaking the UI

    sudo apt-get install -y unity-tweak-tool compizconfig-settings-manager dconf-editor

### Numix Theme  

Use the **Unity Tweak Tool** to set these. *(Apply Icon & Themes)*

    sudo add-apt-repository ppa:numix/ppa
    sudo apt-get update
    sudo apt-get install -y numix-gtk-theme numix-icon-theme numix-icon-theme-circle

### Utilities  
I prefer Git 2.X, so I'll use a PPA. Otherwise you can simply install git by default.

    sudo add-apt-repository ppa:git-core/ppa -y
    
**Install the Utilities:**
    
    sudo apt-get install -y vim git mercurial meld curl htop xclip terminator gdebi preload bleachbit ubuntu-restricted-extras

To setup the git defaults *(Omit the `push.default` if you are using below 2.X)*

    git config --global push.default simple
    git config --global user.name your name
    git config --global user.email your@email.com
    
That will create a `~/.gitconfig` with:

 	[user]
    	email = aniyishay@gmail.com
    	name = Jesse Boyer
	[push]
		default = simple


### Wine
To run windows applications Wine is the best option. I often use HeidiSQL with Wine.

    sudo add-apt-repository ppa:ubuntu-wine/ppa
    sudo apt-get install -y wine1.7-amd64

If you need a 32bit installation:

    sudo apt-get install -y wine1.7-i386

***
[(Back to top)](#table-of-contents)

## LAMP  
Linux Apache MySQL PHP

**- Installation for the following:**
- PHP 5.5+ (and Modules)
- Apache 2 (and Modules)
- Nginx *(Optional)*
- MySQL
- Redis
- and Header Files.

### PHP5  
It's important to install **php5-dev** if you want to compile any add-ons later. We also want composer (PHP Package Manager) to be installed globally and accessible via `$ composer`

    sudo apt-get install -y php5 php5-dev php5-curl libpcre3-dev
    
    curl -sS https://getcomposer.org/installer | php && sudo mv composer.phar /usr/local/bin/composer

If you are looking for more PHP modules try:

    sudo apt-cache search php5-
    
### Apache

    sudo apt-get install -y apache2 libapache2-mod-php5

If you are looking for more Apache modules try:

    sudo apt-cache search libapache2-mod

### Nginx  
Or if you prefer to use nginx

    sudo apt-get install -y nginx

### MySQL

    sudo apt-get install -y mysql-server mysql-client php5-mysql
    sudo sed -i 's/bind-address/bind-address = 0.0.0.0#/' /etc/mysql/my.cnf

### Redis 

    sudo apt-get install -y redis-server

### Java Runtime

    sudo apt-get install -y default-jre

### Phalcon  

    sudo apt-add-repository ppa:phalcon/stable
    sudo apt-get update
    sudo apt-get install -y php5-phalcon

### Phalcon Dev Tools 
This is an easy to use install script that will cleanup after itself. It can also be used for updating:

    sudo bash install_phalcon_devtools.sh

To test it run: `$ phalcon`

***

[(Back to top)](#table-of-contents)

## Python  

Python is installed by default on Ubuntu, version 2.7 is suitable. I strongly recommend installing `python-dev` for headers to compile certain PIP packages.

    sudo apt-get install -y python-dev 
    sudo apt-get install -y python-pip
    sudo pip install fabric virtualenv virtualenvwrapper

***
[(Back to top)](#table-of-contents)

## Ruby
Install Ruby 2.X with header files in `ruby2.0-dev`, this will keep your gems from having issues.

    sudo apt-get install -y ruby2.0 ruby2.0-dev

For Ruby RVM (Version Management)

    gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
    \curl -sSL https://get.rvm.io | bash -s stable

***
[(Back to top)](#table-of-contents)

## NodeJS
I am using a PPA to fix the nodejs path issue(s)

    sudo add-apt-repository ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install nodejs
    sudo chown -R $(whoami) ~/.npm
    sudo npm install bower gulp grunt-cli -g

If installing coffee-script and typing `$ coffee` produces an error, make sure coffee is not within the $PATH

    echo $PATH

**Upgrade NodeJS**

Clear NPM's cache:

    sudo npm cache clean -f
    
Install a helper called `n`

    sudo npm install -g n
    
Install latest stable NodeJS version

    sudo n stable
  
Or pick a specific version:

    sudo n 0.8.20

***
[(Back to top)](#table-of-contents)

## Google Chrome
Version 41 has some annoying issues. It's best to revert to version 40, and Ubuntu does not auto update Chrome without you doing a update.

Stable versions at at: http://mirror.pcbeta.com/google/chrome/deb/pool/main/g/google-chrome-stable/

If you have chrome installed, I'd backup anything if you need it, and remove it *(If you are sync'd, you won't lose anything)*:

    sudo apt-get purge google-chrome-stable
    rm -rf ~/.config/google-chrome

Then install an older version -- This is **40** for a 64-bit OS:

	wget http://mirror.pcbeta.com/google/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_40.0.2214.95-1_amd64.deb
	
    sudo dpkg -i google-chrome-stable_40.0.2214.95-1_amd64.deb

Then launch it with `$ google-chrome` and you can pin it to a unity bar.

***
[(Back to top)](#table-of-contents)

# Virtual Machine Related  

This has to do with VirtualBox, not VMWare even though I favor it.

## Fix Mouse Side Buttons in VMWare 
Append the following to `yourbox.vmx` with the machine off.

    mouse.vusb.enable = "TRUE"
    mouse.vusb.useBasicMouse = "FALSE"
    usb.generic.allowHID = "TRUE"

## Vagrant VBGuest Fix: 

    vagrant plugin install vagrant-vbguest

    vagrant ssh
    sudo ln -s /opt/VBoxGuestAdditions-4.3.10/lib/VBoxGuestAdditions /usr/lib/VBoxGuestAdditions


## Windows 8 VirtualBox Fix 
Running Windows 8 in Virtualbox has an odd error, run this in `cmd` or `powershell`, or `terminal` on linux.

    vboxmanage list vms
    vboxmanage setextradata "The Box Name" VBoxInternal/CPUM/CMPXCHG16B 1

## Install ATI Drivers  

    sudo apt-add-repository ppa:xorg-edgers/ppa
    sudo apt-get update

    sudo apt-get install fglrx
    sudo amdconfig --initial
    sudo apt-get install gksu

**To Edit Catalyst Settings**; Type the following in the Global Launcher *(Super Key/Windows Key)*:

    gksu amdcccle

## Remove ATI Drivers
 
    sudo apt-get remove --purge fglrx fglrx_* fglrx-amdcccle* fglrx-dev*
    sudo rm /etc/X11/xorg.conf
    sudo apt-get install --reinstall xserver-xorg-core libgl1-mesa-glx libgl1-mesa-dri libgl1-mesa-glx libgl1-mesa-dri
    sudo dpkg-reconfigure xserver-xorg

***
[(Back to top)](#table-of-contents)

# Other Applications
- [Chrome](https://www.google.com/intl/en-US/chrome/browser/)
- [Sublime Text 3](http://www.sublimetext.com/3)
- [Skype](http://www.skype.com/en/download-skype/skype-for-computer/)
- [Virtualbox](https://www.virtualbox.org/wiki/Downloads)
  - Preferred: [Debian-based Linux distributions](https://www.virtualbox.org/wiki/Linux_Downloads)
- [Vagrant](http://www.vagrantup.com/)
- [DragonDisk](http://www.dragondisk.com/) S3
- Kazam (Screen Recorder)
- Shutter
- Compiz Config
- gnome-system-tools
- Terminator
- Gdeb
- MySQL Workbench
- Synaptic Package Manager
- Bleachbit (Trash Cleaner)
- Preload (Intelligent Bootup Time)
- [DBeaver](http://dbeaver.jkiss.org/)
- Numix Theme & Numix Circle Icons
- PIP
    - fabric
    - virtualenv
    - virtualenvwrapper

***

By [JREAM](http://jream.com) 2014-2015
