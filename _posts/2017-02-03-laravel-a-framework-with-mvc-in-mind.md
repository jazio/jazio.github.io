---
layout: post
title:  "Laravel"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---

Laravel

Install

Add the laravel executable

```
# Added for laravel excutable.
export PATH=$PATH:/home/jazio/.composer/vendor/bin
```

Start Project

```
laravel new
```

$ php artisan make:migration stocman
Created Migration: 2017_03_11_202314_stocman

You need to edit this file with tables schema then:

```
$ php artisan migrate:status
+------+------------------------------------------------+
| Ran? | Migration                                      |
+------+------------------------------------------------+
| Y    | 2014_10_12_000000_create_users_table           |
| Y    | 2014_10_12_100000_create_password_resets_table |
| N    | 2017_03_11_202314_stocman                      |
+------+------------------------------------------------+


$ artisan migrate

```


#Routing

Create routes.php

For me the routes didn't work until I added
```
require app_path('Http/routes.php');
```

in the Providers\RouteServiceProviders

```
    public function map()
    {
        $this->mapApiRoutes();

        $this->mapWebRoutes();

        require app_path('Http/routes.php');
        //
    }
```