---
layout: post
title:  "Silex, Symfony's Prodigal Brother"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---


# Silex, Symfony's Prodigal Brother



You can use Composer to create new projects from an existing package. This is the equivalent of doing a git clone/svn checkout followed by a composer install of the vendors.



.HTACCESS


 RewriteRule ^(.*) index.php

 it will redirect everything entered from http://www.sample-domain.com to index.php so that you can parse the URI.

RewriteEngine on
RewriteBase /

RewriteCond %{REQUEST_FILENAME} -f
RewriteRule ^ %{REQUEST_FILENAME} [L]

RewriteCond %{REQUEST_FILENAME} -d
RewriteCond %{REQUEST_FILENAME}/index.php -f
RewriteRule ^ %{REQUEST_FILENAME}/index.php [L]

RewriteCond %{REQUEST_FILENAME} -d
RewriteCond %{REQUEST_FILENAME}/index.php !-f
RewriteRule ^ 404/ [L]

RewriteRule ^(.*[^/]) index.php?var=$1 [QSA,L]


RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

... means that if the file with the specified name in the browser doesn't exist, or the directory in the browser doesn't exist then procede to the rewrite rule below


.htaccess in the views folder

Prevent anyone to retrieve files inside templates folder




Silex for sublime
https://sublime.wbond.net/packages/Silex%20Snippets
<?php

# Error Handling
use Symfony\Component\HttpFoundation\Response;

```
$app->error(function (\Exception $e) use ($app) {
    return new Response('Wooops, page not found!');
});
```
or with Twig
```
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\HttpKernel\Exception\HttpException;
use Symfony\Component\HttpKernel\Exception\NotFoundHttpException;

// Register error handlers
$app->error(
    function (\Exception $e) use ($app) {
        if ($e instanceof NotFoundHttpException) {
            return $app['twig']->render('error.twig', array('code' => 404));
        }

        $code = ($e instanceof HttpException) ? $e->getStatusCode() : 500;
        return $app['twig']->render('error.twig', array('code' => $code));
    }
);
```

# How to add menu 

Need to add bind to paths,
```
$app->get('/blog', function () use ($blogPosts) {
...
// Optional nameroutes to be used with UrlGenerator Provider 
})->bind('blog');
```

then

```
use Silex\Provider\UrlGeneratorServiceProvider;
$app->register(new UrlGeneratorServiceProvider());
```

then in twig template
```
<li><a href="{{ path('blog') }}">blog</a></li>
```

If you don't want to use UrlGenerator

            <nav class="grid_3">
                <a href="{{ app.request.baseUrl }}">Inicio</a>
                <a href="{{ app.request.baseUrl }}/noticia">Notícias</a>
                <a href="{{ app.request.baseUrl }}/galeria">Galerias</a>
                {% for item in menu %}
                <a href="{{ app.request.baseUrl ~ item.uri }}">{{ item.titulo }}</a>
                {% endfor %}
                <a href="{{ app.request.baseUrl }}/mapa">Mapa do Site</a>
            </nav>


Add basic layout
```
// Add layout
$app->before(function () use ($app) {
    $app['twig']->addGlobal('layout', $app['twig']->loadTemplate('layout.twig'));
});
```


# Register forms

```
// Exceptions
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

use Silex\Provider\FormServiceProvider;
// mandatory for using forms
use Silex\Provider\TranslationServiceProvider;

// Contact
$app->match('/contact', function (Request $request) use ($app) {
    try {
        $data = array(
            'name' => 'Your name', 
            'email' => 'Your email',
            'message' => 'Message',
            );

    $form = $app['form.factory']->createBuilder('form', $data)
        ->add('name', 'text')
        ->add('email', 'email')
        ->add('message', 'textarea')
        ->getForm();
    $form->handleRequest($request);
        
    } catch (Exception $e) {
        return '<pre>'.$e.'</pre>';
    }
    

    return $app['twig']->render('contact.twig',array(
        'pageTitle' => 'Contact',
        'form' => $form->createView()
        ));
})->bind('contact');
```

Templates

```
{% extends 'layout.twig' %}
{% set active = 'contact' %}
{% block content %}
    <h1>{{ pageTitle }}</h1>
    {{ form_widget(form) }}
    <input type="submit" name="submit" />
{% endblock %}
```

Form template improved

    <form method="post" action="{{ app.url_generator.generate('contact') }}" enctype="application/x-www-form-urlencoded">
 

                  {{ form_errors(form) }}
    {{ form_row(form.name) }}
      {{ form_row(form.email) }}
        {{ form_row(form.message) }}
    </form>




##Organizing our routes

Even on a static website you should have a lot of really static webpages, resulting in many actions. Here is a snippet showing a way to avoid code duplication:

```
$routes = array(
    'home' => array('url' => '/', 'template' => 'home.html.twig'),
    'references' => array('url' => 'references', 'template' => 'references.html.twig'),
    'contact' => array('url' => 'contact', 'template' => 'contact.html.twig'),
    // ...
);

foreach ($routes as $routeName => $data) {
    $app->get($data['url'], function() use($app, $data) {
        return $app['twig']->render($data['template']);
    })->bind($routeName);
}
```




```
use Symfony\Component\HttpFoundation\Response;
// path() usage in twig
use Silex\Provider\TwigServiceProvider;
use Silex\Provider\UrlGeneratorServiceProvider;
// configuration, data storage and parsing
use Symfony\Component\Yaml\Yaml;
// 
use Silex\Provider\FormServiceProvider;
// mandatory for using forms
use Silex\Provider\TranslationServiceProvider;
```



application/x-www-form-urlencoded   Default. All characters are encoded before sent (spaces are converted to "+" symbols, and special characters are converted to ASCII HEX values)
multipart/form-data No characters are encoded. This value is required when you are using forms that have a file upload control
text/plain  Spaces are converted to "+" symbols, but no special characters are encoded

{{ form_widget(form) }}


SwiftMailer
headers
http://swiftmailer.org/docs/headers.html

## Debugging Silex 
###How to debug templates

Use dump()
```
{% if posts %}
    {% for post in posts %}
    {{ dump(post) }}
        <li>{{ post['title'] }}</li>
    {% endfor %}
{% else %}
    <p>No posts found.</p>
{% endif %}
```


https://github.com/symfony/Debug

```
"symfony/debug": "~2.3",
```

Debug provides tools to make debugging easier.
Enabling all debug tools is as easy as calling the enable() method on the main Debug class:
```
use Symfony\Component\Debug\Debug;

Debug::enable();
You can also use the tools individually:
use Symfony\Component\Debug\ErrorHandler;
use Symfony\Component\Debug\ExceptionHandler;

error_reporting(-1);

ErrorHandler::register($errorReportingLevel);
if ('cli' !== php_sapi_name()) {
    ExceptionHandler::register();
} elseif (!ini_get('log_errors') || ini_get('error_log')) {
    ini_set('display_errors', 1);
}
```
Note that the Debug::enable() call also registers the debug class loader from the Symfony ClassLoader component when available.

