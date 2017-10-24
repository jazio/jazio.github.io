---
layout: default
title:  "Taming Composer"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---

# Composer.

Composer is not a package manager. Yes, it deals with "packages" or libraries, but it manages them on a per-project basis, installing them in a directory (e.g. vendor) inside your project. By default it will never install anything globally. Thus, it is a dependency manager.

This idea is not new and Composer is strongly inspired by node's npm and ruby's bundler. But there has not been such a tool for PHP.

$ curl -s http://getcomposer.org/installer | php

sudo mv composer.phar /usr/bin/composer

This moves the file into your bin, which allows you to access all commands with the much shorter example:
1

$ composer about

Composer uses a composer.json file to specify settings and package requirements for your application.

$ composer install

You'll now notice files being downloaded and placed into a new vendors/ folder within the root of your application.

Composer bundles with a PSR-0 autoloader, which you can include in your project with only a single line:

If you run composer global install, it will install it globally.


include_once './vendor/autoload.php';



Composer and Drush
-------------------
Since Drush is distributed as a PEAR package, it can be installed as project dependencies via Composer. This allow you to install Drush on a per-project basis, to ensure the proper version of is used. This is especially useful when using Drush in a build script run through a CI server such a Jenkins.

composer.json

{
  // ...
  "repositories": [
    {
      "type": "pear",
      "url": "pear.drush.org"
    }
  ],
  "config": {
    "bin-dir": "bin"
  },
  "require-dev": {
    "pear-drush/drush": "6.*"
  }
}

or from git
    "require": {
        "drush/drush": "6.*"
    }
After running composer install Drush will be available in the bin directory in your project dir. In order to use it from you shell, you need to add your the bin directory to your path and set the DRUSH_PHP environement variable. This can be done running the following commands from you project directory.

export PATH=`pwd`/bin:$PATH;
export DRUSH_PHP=`dirname $(which drush)`/composer-php;

Can you install multiple packages globally?
------------------------------------------
You can't install multiple versions of the same package.
If you want to install all Drush versions (e.g 6 and 7) you cannot install them globally
The files are installed in ~/.composer/vendor/ there you


vendor/{vendor}/{product}/{version}/
and in require
"vendor/product": ["version","version"...]

more on: http://www.jpstacey.info/blog/2014-04-07/switching-between-drush-major-versions