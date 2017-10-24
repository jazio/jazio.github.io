---
layout: post
title:  "Some thoughts on frontend"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---

# Some thoughts on frontend


## Configuration

All npm installed modules: bower, generator-angular, generator-karma, grunt-cli, grunt-init, yo
/home/jazio/npm/lib/node_modules  

You can run them from /home/jazio/npm/bin (added to PATH): bower, grunt, grunt-init, yo

### grunt-init templates

Read ```http://gruntjs.com/project-scaffolding```

Install grunt-init templates: ```/home/jazio/npm/lib/node_modules/grunt-init/templates```

## Build a yeoman generator

http://yeoman.io/authoring/

```
yo doctor
```

## Markdown

- **Compile**: ```markdown roadmap > roadmap.html```
- Markdown for Sublime: ```Ctrl+Shift+P``` then type ```Markdown```. To enable preview select from syntax or  ```Ctrl+Shift+P``` then type ```ss Markdown```

## node
n is a tool to install different versions of node.

Updated nodejs - 
$ npm cache clean -f
$ npm install -g n
# Install latest
$ n latest
# nodejs -v // version 7 is not the best for ionic so I downgraded to 6.9.1
$ sudo n 6.9.1



## AngularJS

###Kickstart AngularJS using Yeoman, Grunt and Bower.

Install the 3 tools

```
sudo npm install -g yo grunt-cli bower
```
Deal with an error related to changing the node to nodejs command.

```
sudo apt-get install nodejs-legacy
```
Install Angular generator

```
sudo npm install -g generator-angular
```
Scafold your app. You will be asked if need to include Bootstrap, Sass, Sass for bootstrap. Then will trigger the angular generator and will be asked which angular component to install.

```
yo angular
```
If running into permission errors, chown the folder


---
layout: post
title:  "Frontent"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---
# Frontend


## Configuration

All npm installed modules: bower, generator-angular, generator-karma, grunt-cli, grunt-init, yo
/home/jazio/npm/lib/node_modules  

You can run them from /home/jazio/npm/bin (added to PATH): bower, grunt, grunt-init, yo

### grunt-init templates

Read ```http://gruntjs.com/project-scaffolding```

Install grunt-init templates: ```/home/jazio/npm/lib/node_modules/grunt-init/templates```

## Build a yeoman generator

http://yeoman.io/authoring/

```
yo doctor
```



## AngularJS

###Kickstart AngularJS using Yeoman, Grunt and Bower.

Install the 3 tools

```
sudo npm install -g yo grunt-cli bower
```
Deal with an error related to changing the node to nodejs command.

```
sudo apt-get install nodejs-legacy
```
Install Angular generator

```
sudo npm install -g generator-angular
```
Scafold your app. You will be asked if need to include Bootstrap, Sass, Sass for bootstrap. Then will trigger the angular generator and will be asked which angular component to install.

```
yo angular
```
If running into permission errors, chown the folder




