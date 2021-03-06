# Config Ubuntu

This is for a [Ubuntu](http://ubuntu.com/desktop), I have run this on `14`, `15`, and `16`
as a Desktop and a Server.


Terminal Help Has been moved: [https://github.com/JREAM/ubuntu-cheatsheet](https://github.com/JREAM/ubuntu-cheatsheet)

### Script Files
There are two main script files:

- `./desktop.sh` Options to install desktop items.
- `./server.sh` Options to install server items, you can do this on your desktop too.

***

# Table of Contents
- [Order of Grub](#order-of-grub)
- [Dot Files](#dot-files)
- [Tweaking the UI](#tweaking-the-ui)
- [Utilities](#utilities)
    - [Convert PPK to SSH Key](#convert-ppk-to-ssh-key)
    - [RedShift For Eye Strain](#redshift-for-eye-strain)
    - [Numix Theme](#numix-theme)
    - [Wine](#wine)
    - [USB Maker for Windows ISO on Linux](#usb-maker-for-windows-on-linux)
- [LAMP](#lamp)
    - [PHP5](#php5)
    - [Apache](#apache)
    - [Nginx](#nginx)
    - [MySQL](#mysql)
    - [MyCLI](#mycli) Terminal MySQL Utility
    - [Redis](#redis)
    - [Phalcon](#phalcon)
    - [Phalcon Dev Tools](#phalcon-dev-tools)
    - [Secure Permissions](#secure-permissions)
- [Python](#python)
- [Ruby](#ruby)
- [NodeJS](#nodejs)
- [Java](#java)
- [Google Chrome](#google-chrome)
- [Ubuntu Fixes](#ubuntu-fixes)
    - [Sound Indicator Not Showing](#sound-indicator-not-showing)
- [Install Gnome 3](#install-gnome-3)
    - [Easy Window Resize](#easy-window-resize)
    - [Left or Right Close Buttons](#left-or-right-close-buttons)
    - [Fix Gnome Lockscreen](#fix-gnome-lockscreen)
    - [My Gnome Extensions](#my-gnome-extensions)
    - [Reload Gnome Freeze](#reload-gnome-freeze)
- [Adjust Mouse and Devices](#adjust-mouse-and-devices)
- [Virtual Machine Related](#virtual-machine-related)
    - [Fix Mouse Side Buttons in VMWare](#fix-mouse-side-buttons-in-vmware)
    - [Vagrant VBGuest Fix](#vagrant-vbguest-fix)
    - [Windows 8 VirtualBox Fix](#windows-8-virtualbox-fix)
    - [Install ATI Drivers](#install-ati-drivers)
    - [Remove ATI Drivers](#remove-ati-drivers)
- [Chrome Addons](#chrome-addons)
- [Other Applications](#other-applications)

***

[(Back to top)](#table-of-contents)

# Order of Grub
If you are running Grub as your default boot-loader, you can use this application to make it easier to change the order.

    sudo add-apt-repository ppa:danielrichter2007/grub-customizer
    sudo apt-get update && sudo apt-get install grub-customizer

Load the application either with `<Super>` and look for grub customizer or terminal `gksudo grub-customizer`.

Go to the `General Settings` tab, and you'll see *default entry*.

- Click the drop-down list and you can either select Entry By Order (Left Column) Or a specific Item (Right Column).
- If you are dual booting Windows and want Windows the default, Select the right column for Windows.
- The reason is if more items are added, perhaps new kernels, then if Position 5 which held Windows will no longer be the default.

***

[(Back to top)](#table-of-contents)

# Dot Files
Here are some shortcuts for the dotfiles if you use them:

| Shortcut | Action |
|----------|--------|
| mkproject &lt;name&gt; | virtualenv in ~/projects/&lt;name&gt; |
| workon &lt;name> | load virtualenv in ~/projects/&lt;name&gt; |
| l  | ls -la |
| la | ls -la |
| .. | cd .. |
| ... | cd ../../ |
| .... | cd ../../../ |
| ffile | find . name &lt;your_file&gt; (Searches for file in current folder) |
| ftext | ftext () { grep -rnwi &lt;your_text&gt; . ;} (Searches for text in file of current folder) |
| ip | current IP address |
| ports | see open ports |
| update | apt update |
| updatey | apt update && install -y |
| ngmake <name> | vim etc/nginx/sites-available/&lt;name&gt; |
| ngenable <name> | enable nginx &lt;name&gt; |
| ngdisable <name> | disable nginx &lt;name&gt; |
| h | history |
| codi python test.py | interactive scratch pad, See: [Codi](https://github.com/metakirby5/codi.vim)  |

| Git Alias | Command (See ~/.gitconfig) |
|----------|--------|
| git lg | git log --graph --pretty=format:'long-string' |
| git co | git checkout |
| git ci | git commit |
| git aa | git add --all |
| git st | git status |
| git di | git diff |
| git dc | git diff --cached |

# Tweaking the UI
This is for tweaking the UI

    sudo apt-get install -y\
        unity-tweak-tool\
        compizconfig-settings-manager\
        compiz-plugins\
        dconf-editor\
        synaptic
        
- The Tweak Tool works great for Applying the Numix theme
- Compiz is good for customizing everything, make sure to save a profile when you make your UI how you like.

# Utilities
These are some common items I enjoy using

    sudo apt-get install -y\
        vim\
        git\
        mercurial\
        meld\
        curl\
        htop\
        xclip\
        unzip\
        terminator\
        gdebi\
        preload\
        bleachbit\
        ubuntu-restricted-extras

## Convert PPK to SSH Key
Already included in the utils is `putty-tools`. To convert a `*.ppk` (Putty Key) to an SSH or EC2 valid key do the following.

```
puttygen your_key.ppk -O private-openssh -o id_dsa
puttygen your_key.ppk -O public-openssh -o id_dsa.pub
```

Then move it to your SSH folder with proper permissions:
```
mv -i ~/id_dsa* ~/.ssh
chmod 600 ~/.ssh/id_dsa
chmod 644 ~/.ssh/id_dsa.pub
```

## RedShift For Eye Strain

    sudo apt-get install redshift

Create your configuration file:

    sudo vim ~/.config/redshift.conf

Adjust the temperatures you prefer. I like mine to be very yellow and dim. (The lower the dimmer)

    [redshift]
    temp-day=3500
    temp-night=3500
    ; Set the screen brightness. Default is 1.0.
    ;brightness=0.9
    ; It is also possible to use different settings for day and night
    ;brightness-day=0.7
    ;brightness-night=0.4
    ; There are more settings for Gamma, Location Provider, Manual Location, etc.

Close and reload redshift. If you cannot find the icon anywhere run this in terminal:

    pkill redshift-gtk && pkill redshift

If RedShift gives you a `Geoclue2` error do this:

    sudo vim /etc/geoclue/geoclue.conf

Append these lines at the bottom:

    [redshift]
    allowed=true
    system=false
    users=

A newer version of redshift will install a desktop file so a Geoclue2 warning won't happen
on newer systems.

## Numix Theme

Use the **Unity Tweak Tool** to set these. *(Apply Icon & Themes)*

    sudo add-apt-repository ppa:numix/ppa
    sudo apt-get update
    sudo apt-get install -y numix-gtk-theme numix-icon-theme numix-icon-theme-circle

Turn it on using **Tweak UI**

## Wine
To run windows applications Wine is the best option. I often use HeidiSQL with Wine.

    sudo add-apt-repository ppa:ubuntu-wine/ppa
    sudo apt-get install -y wine1.7-amd64

If you need a 32bit installation:

    sudo apt-get install -y wine1.7-i386

## USB Maker for Windows ISO on Linux
You can easily use `Startup Disk Creator` and `UNetbootin` to create Linux to USB. But if you need Windows to USB from your Linux OS use Win USB:

    sudo add-apt-repository ppa:colingille/freshlight
    sudo sh -c "sed -i 's/trusty/saucy/g' /etc/apt/sources.list.d/colingille-freshlight-trusty.list"
    sudo apt-get update && sudo install -y winusb

We replace the sources.list back to saucy in order to get it to work for ubuntu 14, that is the purpose of the `sed` command.

***
[(Back to top)](#table-of-contents)

# LAMP
Linux Apache MySQL PHP

**- Installation for the following:**
- PHP 5.5+ (and Modules)
- Apache 2 (and Modules)
- Nginx *(Optional)*
- MySQL
- Redis
- and Header Files.

## PHP5
**PHP7 Ships with Ubuntu 16**

It's important to install **php5-dev** if you want to compile any add-ons later. We also want composer (PHP Package Manager) to be installed globally and accessible via `$ composer`

    sudo apt-get install -y php5 php5-dev php5-curl libpcre3-dev

    curl -sS https://getcomposer.org/installer | php && sudo mv composer.phar /usr/local/bin/composer

If you are looking for more PHP modules try:

    sudo apt-cache search php5-

## Apache

    sudo apt-get install -y apache2 libapache2-mod-php5

If you are looking for more Apache modules try:

    sudo apt-cache search libapache2-mod

## Nginx
Or if you prefer to use nginx

    sudo apt-get install -y nginx

## MySQL

    sudo apt-get install -y mysql-server mysql-client php5-mysql
    sudo sed -i 's/bind-address/bind-address = 0.0.0.0#/' /etc/mysql/my.cnf

The last line simply allows you to connect from outside of the machine. A good example of wanting that is if you had a Vagrant Box.

## MyCLI
This is a very nice utility in Python [https://github.com/dbcli/mycli](https://github.com/dbcli/mycli)

    pip install mycli

Usage (See the documents from the git link above for more example):

    mycli -h localhost -u root
    mycli -h localhost -u root -p

## Redis

    sudo apt-get install -y redis-server

## Phalcon

    sudo apt-add-repository ppa:phalcon/stable
    sudo apt-get update
    sudo apt-get install -y php5-phalcon

## Phalcon Dev Tools
This is an easy to use install script that will cleanup after itself. It can also be used for updating:

    sudo bash install_phalcon_devtools.sh

To test it run: `$ phalcon`

## Secure Permissions
We will use the Access Control Lists (ACL) or (Filesystem Access Control List). We will use group permissions for folders so you don't have to make the public writable, because `777` is dangerous.

    # Make sure you have ACL installed
    sudo apt-get install acl

Look for your main partition with:

    $ df


Mine happens to be `dev/root`, yours may be `dev/sda` or something. Make sure to replace that below:

    sudo /sbin/tune2fs -o +acl /dev/root

To see what file system you are using `ext3`, `ext4`, etc, use the partition:

    sudo file -sL /dev/root

We have to put the partition in read-only mode, then remount it:

    sudo /bin/mount -o remount /dev/root

Apply Group

    # This sets the Defaults
    setfacl -Rd g:www-data:rw /var/www
    # This sets future file
    setfacl -Rm g:www-data:rw /var/www

To Modify

    setfacl -Rm g:www-data:rw /var/www

Otherwise you could always set up a crontab such as:

    crontab -e

Then append this to run every five minutes.

    */5 * * * * /home/ramesh/backup.sh chgrp -R www-data /var/www && chmod g+rw /var/www

Lastly, you could have a deploy script that does this for you, such as Python `Fabfile`, but that's another topic.


***

[(Back to top)](#table-of-contents)

## Python

Python is installed by default on Ubuntu, version 2.7 is suitable. I strongly recommend installing `python-dev` for headers to compile certain PIP packages.

    sudo apt-get install -y python-dev
    sudo apt-get install -y python-pip
    sudo pip install fabric virtualenv virtualenvwrapper
    
If you plan on using SSL or PIL(Pillow) for Image manipulation,  I'd have these dependencies pre-installed:

    sudo apt-get install -y\
        libssl-dev\
        libffi-dev\
        libjpeg8-dev\
        libjpeg-dev

Note: Some programs use `libffi` (Foreign Functions Interface) and need the dev headers to build from it, as well as the other dev packages, yet FFI just looks funny to read.

***
[(Back to top)](#table-of-contents)

## Ruby
Install Ruby 2.X with header files in `ruby2.3-dev`, this will keep your gems from having issues.

    sudo apt-get install -y\
        ruby2.3\
        ruby2.3-dev\
        gems

For Ruby RVM (Version Management)

    gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
    \curl -sSL https://get.rvm.io | bash -s stable

***
[(Back to top)](#table-of-contents)

## NodeJS
I am using a PPA to fix the nodejs path issue(s)

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

## Java
I use the default JRE/JDK, the others are up to you. 

#### To insteall Default JRE/JDK

    sudo apt-get install -y\ 
        default-jre\ 
        default-jdk

#### To install OpenJDK (7, 8, or 9)

    sudo apt-get install -y\
        openjdk-8-jdk
        openjdk-8-jre
        
#### To install Oracle JDK (7, 8, or 9)
    
    sudo add-apt-repository ppa:webupd8team/java
    
    sudo apt-get install oracle-java7-installer
    sudo apt-get install oracle-java8-installer
    sudo apt-get install oracle-java9-installer

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

# Ubuntu Fixes
These are solutions to fix problems I've encountered.

### Sound Indicator Not Showing
This appears in the top-right menu on Unity. Tested in 14/15.

This will also fix Tweak UI if a sound item is missing.

    sudo apt-get install indicator-sound

For Unity (Default)

   killall unity-panel-service

For Gnome

    killall gnome-panel

# Install Gnome 3
If you prefer Gnome 3 over the Unity desktop it's easy to install:

    sudo apt-get install ubuntu-gnome-desktop
    sudo service gdm restart (Or a reboot is easier)

Unity uses `lightdm` and Gnome uses `gdm`, it's easiest to stick with lightdm.

If you want the default login a certain one select either lightdm or gdm. If you want to change it later run:

    sudo dpkg-reconfigure gdm

### Easy Window Resize
Without Compiz, you can resize windows very nicely:
- Focus on a window
- Hold <kbd>ALT</kbd> + Middle Mouse Click + Drag
- Note: Depending on where you position your mouse to will resize up/down/left/right

### Left or Right Close Buttons
Run this simple command in the terminal and you will see the positions change right away.

Move to right (terminal)

    gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

Move to left (terminal)

    gsettings set org.gnome.desktop.wm.preferences button-layout 'close,minimize,maximize:'


### Fix Gnome Lockscreen
In terminal make sure this is false, then try your hotkey `ctrl+alt+l` or if you set it like min `super+l` in the settings:

    gsettings set org.gnome.desktop.lockdown disable-lock-screen 'false'

### My Gnome Extensions
You need to use **Firefox** or **IceWeasle** at https://extensions.gnome.org/ to toggle these items. I suggest creating an account so you have a record.

You can use **TweakUI** to toggle Extensions when they are installed.

- **Extensions I use**
- All Windows
- Alt tab lift first window
- Alternatetab
- [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
- [Force Quit](https://extensions.gnome.org/extension/770/force-quit/)
- Frippery move clock
- Gno-menu
- Lock screen
- Netspeed
- [No Topleft Hot Corner](https://extensions.gnome.org/extension/118/no-topleft-hot-corner/)
- Quick app launcher
- Workspace Indicator
- [Workspaces to Dock](https://extensions.gnome.org/extension/427/workspaces-to-dock/)
- Windownavigator
- **Nice Extensions**
- [Applications Menu](https://extensions.gnome.org/extension/6/applications-menu/)
- [Taskbar](https://extensions.gnome.org/extension/584/taskbar/)
- [Small Panel Icon](https://extensions.gnome.org/extension/861/small-panel-icon/)
- [Top Icons](https://extensions.gnome.org/extension/495/topicons/)
- [MMOD Panel](https://extensions.gnome.org/extension/898/mmod-panel/)
- [Keyboard Modifiers Status](https://extensions.gnome.org/extension/975/keyboard-modifiers-status/)
- [Laine](https://extensions.gnome.org/extension/937/laine/)
- [Disable Workspace Switcher Popup](https://extensions.gnome.org/extension/959/disable-workspace-switcher-popup/)
- [Refresh Wifi Connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)
- [Disconnect Wifi](https://extensions.gnome.org/extension/904/disconnect-wifi/)
- [Toggle Touchpad](https://extensions.gnome.org/extension/935/toggle-touchpad/) (For Laptops)

### Reload Gnome Freeze
This is a rare things for me, it happens much more in unity and requires a lot more "damaging" things. To fix a gnome that seems frozen do the following:

<kbd>ALT + F2</kbd> enter in <kbd>r</kbd> (lowecase) and press <kbd>Enter</kbd>


***
[(Back to top)](#table-of-contents)

# Adjust Mouse and Devices
When using a USB mouse sometimes the speed is just not right, in my case it's too slow often. Here is how to adjust it:

    xinput --list

I get something like this:

    ⎡ Virtual core pointer                      id=2    [master pointer  (3)]
    ⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
    ⎜   ↳ ETPS/2 Elantech Touchpad                  id=15   [slave  pointer  (2)]
    ⎜   ↳ Logitech Unifying Device. Wireless PID:101b   id=12   [slave  pointer  (2)]
    ⎣ Virtual core keyboard                     id=3    [master keyboard (2)]
        ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
        ↳ Power Button                              id=6    [slave  keyboard (3)]
        ↳ Video Bus                                 id=7    [slave  keyboard (3)]
        ↳ Power Button                              id=8    [slave  keyboard (3)]
    ...

The ID of my mouse is `12`.
You can see all the properties with:

    $ xinput --list-props 12

Then you can adjust the settings the String value and a value at the end:

    $ xinput --set-prop 12 "Device Accel Constant Deceleration" 2

## Preserve Settings

To keep the settings in Gnome, do the following:

    $ cd ~
    $ touch gnome-boot.sh && chmod +x gnome-boot.sh

Example of `gnome-boot.sh` file (Note: You can call it whatever you like):

    #!/bin/bash
    xinput --set-prop 12 "Device Accel Constant Deceleration" 4


Then Add the Bash script the Gnome Session:

    $ gnome-session-properties


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

# Chrome Addons

- [Chroma Color Picker](https://chrome.google.com/webstore/detail/chroma/gefgglgjdlddcpcapigheknbacbmmggp?utm_source=chrome-app-launcher-info-dialog)
- [Postman Rest Client](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?utm_source=chrome-app-launcher-info-dialog)

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

[(Back to top)](#table-of-contents)
