Get started building your Bolt Extentions

```
composer create-project --no-install bolt/bolt-extension-starter:^3.0 <newextname>
```

Only the folder public/ needs to be accessible in the browser.

```
chown -R www-data:www-data public
```


The file .bolt.yml is outside public (that is /var/www/blog)

 paths:
    cache: app/cache
    config: app/config
    database: app/database
    web: public
    themebase: public/theme
    files: public/files
    view: public/bolt-public/view


I also created a virtual server blog.jazio.eu to point to public folder.

```
sudo a2ensite yoursite
sudo service apache2 reload
```

For vernisaj.ro the .htaccess has RewriteBase /

```
database:
    driver: mysql
    databasename: vernisaj
    username: root
    password: oceanograf2020
    host: localhost
```

jazio/Mnaspreas...

