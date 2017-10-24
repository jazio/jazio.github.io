---
layout: post
title:  "Get Productive with Linux"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---

# LINUX.
# Certifications Linux Enterprise: http://www.lpi.org/our-certifications/summary-of-certifications


# Find what version you use
$ uname
#37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016

# Folder structure.


/bin #contains executables which are required by the system for emergency repairs, booting, and single user mode.
/usr/bin #contains any binaries that aren't required.
/usr/local/ #Tertiary hierarchy for local data, specific to this host.

# Home folder.
 # contains useful .dor files

 .gitconfig
 .bash_history
 .vim_history  #useful as it contains latest files accessed, commands used

Put all your aliases and environment variables in either .bashrc (which only
gets loaded in non-login shells) and .bash_profile (for login shells).

Executing files containing commands:
$ source your_file_name


#/////////////////////////////////////////////////////////////////////////////////////////////////

 #DASH AND DASH COMMANDS.

#/////////////////////////////////////////////////////////////////////////////////////////////////
# On Ubuntu and Mint, /bin/sh is dash, not bash. Dash and bash both have the same core features,
# but dash sticks to these core features in order to be fast and small whereas bash adds a lot of features at the cost of requiring more resources.
# It is common to use dash for scripts that don't need the extra features and bash for interactive use (though zsh has a lot of nicer features).
# So put your environment variable definitions in ~/.profile. Make sure to use only syntax that dash supports.

.profile # place your aliases here.
alias php.ini="sudo subl /etc/php5/apache2/php.ini" # please remember the php plugin ini settings are in ../apache2/config.d/*.ini

alias php.ini="sudo subl /etc/php5/apache2/php.ini"
alias apache2.conf="sudo subl /etc/apache2/apache2.conf"
alias apache2.errors="subl /var/log/apache2/error.log"
alias apache2.access="subl /var/log/apache2/access.log"

# Add git info to the prompt.
source ~/.git-prompt.sh
GIT_PS1_SHOWDIRTYSTATE=true
GIT_PS1_SHOWSTASHSTATE=true
GIT_PS1_SHOWUNTRACKEDFILES=true
GIT_PS1_SHOWUPSTREAM=auto

# bold green user@host full path git information $ normal yellow
PS1='\e[1;32m \u@\h \w$(__git_ps1 " (%s)") \$ \e[0;33m'
# To restart
. ~/.profile


# cd.
#-------------------------------------------------------------------------------------------------

cd ~ # change to home
cd / # change to root
cd - # change to last used

# makedirs
```
$ mkedir
// Set permission mode -m, or -p no error if existing.
$ mkdir -p
```
# Symlinks.
# -------------------------------------------------------------------------------------------------
# Symlinks. Create hard links by default, symbolic links with --symbolic.
# By default, each destination (name of new link) should not already exist.
# When creating hard links, each TARGET must exist.  Symbolic links
# can hold arbitrary text; if later resolved, a relative link is
# interpreted in relation to its parent directory.
# Create symbolic links with option -s

# Create symlinks:
ln -s /path/to/file /path/to/symlink

# Delete symlinks:
rm -rm /path/to/symlink/file. #recommended
#or
ulink link

# Display files
$ ls
$ ll

# search // find // replace
#-------------------------------------------------------------------------------------------------
find /path -iname "folder/file name"
# Reverse i-search
Ctrl+R
# Linux Mint Rebecca+
search in folder for string


# Replace a file

```
sed -i 's|composer.phar|/usr/local/bin/composer|g' build.properties.local
```
=======
# Replace a string (e.g. composer path) with another one in a file.

sed -i 's|composer.phar|/usr/bin/composer|g' your_file_name

#//////////////////////////////////////////////////////////////////////////////


# tmux.
# -------------------------------------------------------------------------------------------------
# Every command is preceded by Ctrl+B. Split screen. " to split the screen vertically, % horizontally

Every command is preceded by ```Ctrl+B```.

Split screen. " vertically, % horizontally."
 Swap panes: o
 display numeric values: q
 show commands: ?
 dettach: d
 kill the current pane: x
 next layout: space
 shift + arrows = move to other pane




# kill processes.
# -------------------------------------------------------------------------------------------------

```
ps aux | grep whatever. Identify pid. kill pid.
```

# hosts.
# -------------------------------------------------------------------------------------------------
/etc

host.conf
hostname # change hostname
hosts
hosts.allow
hosts.deny

# Proxies.
#-------------------------------------------------------------------------------------------------
Set them in /etc/environment
http_proxy
https_proxy
#
# PATH variables.
# -------------------------------------------------------------------------------------------------

#Display them
```
echo $PATH
```
#Where
place your variables in ```~/.profile``` for your per-user PATH setting or ```/etc/environment``` for global settings.

Do something like export PATH=$PATH:/your/new/path/here

Reload
```
source /etc/environment
```
#See all environment variables

$ env

# tee
#
```
./install.sh -f -k -i multisite_drupal_standard multisite_drupal_rey2  2>&1 | tee log.txt
```

Search inside the package names
apt-cache search sublime

## Wifi configuration

# See and configure wifi interface. Similar to ipconfig but specialized to wifi interface
$ iwconfig

restart the wifi
```
sudo service network-manager restart
```
# List hardware in your computer
$ lspci -nn




# Edit exit node in TorBrowser, {za} is country code for South Africa.
sudo vim ./Browser/TorBrowser/Data/Tor/torrc
Add these 2 lines
ExitNodes {za} 
StrictNodes 1



VPN
azirevpn / jazio/Nsv
expresVPN

Update repository

apt-get update

2.2 Install OpenVPN

apt-get install openvpn

2.3 Prevent DNS-leak by adding these 3 lines to the end of your .ovpn file

script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf