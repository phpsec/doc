phpSec is now a PSR-0 compatible library. this means that it can easilly be installed and loaded using [Composer](http://getcomposer.org/doc/00-intro.md).
You can also install phpSec manually, or using Git.

### Installing using [Composer](http://getcomposer.org/doc/00-intro.md)
To install using Composer just add phpSec to your composer.json file in your project directory.
```
{
    "require": {
        "phpsec/phpsec":"dev-master"
    },
    "minimum-stability": "dev"
}
```

Then all you need to do is to run `$ php composer.phar install` .
phpSec can then be loaded using the Composer autoloader.

`require 'vendor/autoload.php';`

### Installing manually/Git
Download, checkout or peferrably add phpSec as a Git submodule. Then you can autoload the required files using a
[PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) compatible autoloader, or manually require the files you need.

It you want to add an autoloader to your project there is [one example here](http://gist.github.com/221634).
This can be initialized like this:

```php
<?php
require_once 'SplClassLoader.php';
$classLoader = new SplClassLoader('phpSec', '/var/www/vendor/phpsec/phpsec/lib');
$classLoader->register();
```
