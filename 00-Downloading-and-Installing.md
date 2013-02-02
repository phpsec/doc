/*
Title: Downloading and installing
*/

Downloading and installing
==========================

phpSec is now a PSR-0 compatible library. this means that it can easilly be installed and loaded using [Composer](http://getcomposer.org/doc/00-intro.md).
You can also install phpSec manually, or using Git.

### Installing using [Composer](http://getcomposer.org/doc/00-intro.md)
To install using Composer just add phpSec to your composer.json file in your project directory.

    {
      "require": {
        "phpsec/phpsec":"0.5.*"
      }
    }


Then all you need to do is to run `$ php composer.phar install` .
phpSec can then be loaded using the Composer autoloader.

`require 'vendor/autoload.php';`

### Installing manually/Git
Download, checkout or peferrably add phpSec as a Git submodule. Then load the *lib/phpSec/bootstrap.php* file.
This is a really simple autoloader that will load phpSec classes when needed.

`require_once 'lib/phpSec/bootstrap.php';`

If you already have a PSR-0 compatible autoloader for your project there is no need to call the *bootstrap.php* file.
All you have to do is to register the *phpSec* namespace to the *phpSec/lib* folder.

If you want to add an autoloader to your project there is [one example here](http://gist.github.com/221634).
This can be initialized like this:


    <?php
    require_once 'SplClassLoader.php';
    $classLoader = new SplClassLoader('phpSec', '/var/www/vendor/phpSec/lib');
    $classLoader->register();

