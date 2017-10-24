

# Apache.


## Configuration [see above].

In bash_profile:
```
alias apache2.conf="sudo subl /etc/apache2/apache2.conf"
alias apache2.errors="subl /var/log/apache2/error.log"
alias apache2.access="subl /var/log/apache2/access.log"
```

### Configuration file.
`/etc/apache2/apache2.conf`

### Find out apache user (normally www-data)
`ps aux | egrep '(apache|http)'`

### Make Apache2 owner of file folder
`sudo chown -R www-data:www-data files/`

## Cookbook

### Problem: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName
### Solution. Run this in command prompt. This will write the line in the file servername.conf
```
echo "ServerName localhost" | sudo tee /etc/apache2/conf-available/servername.conf
```

### Change DocumentRoot in Ubuntu distribution. Found in /etc/apache2/000-default.conf and /etc/apache2/default-ssl.conf
```
DocumentRoot /var/www
```

### Restart apache2
```
sudo server apache2 reload
```

### Enable mode rewrite module

```
sudo a2enmod rewrite
```

### Determine the domain name

```
$ apache2ctl -S
AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message
VirtualHost configuration:
*:80                   127.0.1.1 (/etc/apache2/sites-enabled/000-default.conf:1)
ServerRoot: "/etc/apache2"
Main DocumentRoot: "/var/www/html"
Main ErrorLog: "/var/log/apache2/error.log"
Mutex watchdog-callback: using_defaults
Mutex default: dir="/var/lock/apache2" mechanism=fcntl 
PidFile: "/var/run/apache2/apache2.pid"
Define: DUMP_VHOSTS
Define: DUMP_RUN_CFG
User: name="www-data" id=33 not_used
Group: name="www-data" id=33 not_used
```

### I get all pages 404 Not found except homepage.

Open up apache.conf

```
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
```

And change to 
```
AllowOverride All
```

### How to create virtual hosts

```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/clima.conf
```

Then look into clima.conf
```
<VirtualHost *:80>
   
  ServerName clima     
  DocumentRoot /var/www/html/clima/platform


    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

```
sudo a2ensite clima.conf
sudo a2dissite 000-default.conf
sudo service apache2 reload
sudo subl /etc/hosts
```

```
sudo a2enmod rewrite
```

Edit .htaccess
```
RewriteBase /
```

```
/etc/hosts

127.0.0.1   localhost
127.0.1.1   T410
127.0.0.1 clima
```

now access http://clima




# PHP

## Installation.

Install PHP extentions.
Locate the ini file [phpinfo].
```
/etc/php5/apache2/php.ini.
```
Locate the extension dir: extension_dir /usr/lib/php5/20121212. It contains extensions in .so format.
Use synaptic to install all php extentions.

# PHP Performance.

php.ini // slow localhost
```
realpath_cache_size = 24M
```

# MySQL/Mariadb


#Replace mysql with mariadb

Mariadb is mysql compatible. Faster faster complex queries. Virtual columns which allow for on-the-fly calculation and updating of columns.

A number of large sites have changed to MariaDB from MySQL or are in the process of doing so

>“Taking the times of 100% of all queries over regular sample windows, the average query time across all enwiki slave queries is about 8% faster with MariaDB vs. our production build of 5.1-fb. Some queries types are 10-15% faster, some are 3% slower, and nothing looks aberrant beyond those bounds. Overall throughput as measured by qps queries per second has generally been improved by 2-10%. “

Purge current mysql installation
```
sudo apt-get purge mysql-server mysql-client mysql-common mysql-server-core-5.7 mysql-client-core-5.7
sudo rm -rf /etc/mysql /var/lib/mysql
sudo apt-get autoremove
sudo apt-get autoclean
sudo apt-get install mariadb-server
```


### Problem: mysql is only reachable by sudo

```
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'admin'@'localhost';
FLUSH PRIVILEGES;
```

## Phpmyadmin
In ubuntu by default, phpmyadmin is installed in /usr/share/phpmyadmin
`$ ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin`

You also have to include 
`Include /etc/phpmyadmin/apache.conf` in the `file /etc/apache2/apache2.conf`.

###Troubleshooting

###Problem: Message in phpmyadmin ```Connection for controluser as defined in your configuration failed phpmyadmin```

`sudo dpkg-reconfigure phpmyadmin`

#2. Problem: WSOD

Added this in the root `index.php`
```
error_reporting(E_ALL);
ini_set('display_errors', TRUE);
ini_set('display_startup_errors', TRUE);
```
and revealed
```
PHP Fatal error:  require_once(): Failed opening required '/usr/share/php/php-gettext/gettext.inc' (include_path='.:/usr/share/php') in /usr/share/phpmyadmin/libraries/select_lang.lib.php on line 477
```

Obvious missing module `php-gettext`

```
sudo apt-get install php-gettext
sudo service apache2 restart
```


v.1.0