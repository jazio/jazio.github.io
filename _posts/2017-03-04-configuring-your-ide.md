#PhpStorm.
-------------------------------------------------------------------------------------------------
tar xvf your-archive.tar.gz. mv to /opt.
firefox  google  phpstorm8  sublime_text  vagrant.
All are there too.

Create a Desktop Shortcut. From IDE > Tools > Create Desktop Entry

Useful Shortcuts
Access menu from keyboard: Ctrl+Shift+A
Generate GenDoc Alt+ Enter
Jump to another part Ctrl+F12
Terminal Alt+F12
Surround with Ctr+Alt+T
Lines: Duplicates Ctrl+D, Delete Ctrl+Y, Move Up, Ctrl+Shift+Up or Ctrl+Shift+Down.



#Sublime Text 3.
-------------------------------------------------------------------------------------------------
Download .deb. $sudo dpkg -i whatever.deb. No need for aliasing.
Launch $subl filename

Regular Expression Search: Alt+R then e.g. add a * in the beginning of lines: find \n replace \n * 





#XDebug for Linux.
-------------------------------------------------------------------------------------------------

jazio@jazio /etc/php5/mods-available $ ls
curl.ini  gd.ini  json.ini  mcrypt.ini  mysqli.ini  mysql.ini  mysqlnd.ini  opcache.ini  pdo.ini  pdo_mysql.ini  xdebug.ini
jazio@jazio /etc/php5/mods-available $ gksudo gedit xdebug.ini

zend_extension=xdebug.so
Then paste

xdebug.remote_enable=on
xdebug.remote_handler=dbgp
xdebug.remote_host=localhost
xdebug.remote_port=9000

In PhpStorm

Go to PHP HTTP Request and add the local server
Go to PHP Web Application and add the path to your current drupal installation.
