Safe storage of your users password is an important step to increase the security of your web-application. phpSec implements [bcrypt](http://en.wikipedia.org/wiki/Bcrypt), [sha2](http://en.wikipedia.org/wiki/SHA-2) and [pbkdf2](http://en.wikipedia.org/wiki/PBKDF2) to protect your users passwords from rainbow tables and brute force attacks in case they are compromised. You can read more about this [here](http://codahale.com/how-to-safely-store-a-password/).

phpSec creates salted hashes using the very well prooven [crypt()](http://en.wikipedia.org/wiki/Crypt_(Unix)) function. The crypt() function is available on virtually any platform. This means that a password hashed with phpSec could be validated on almost any system without any effort at all.

*Note: There is one exception. The [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2) implementation in phpSec is only supported in phpSec. If you need portability configure phpSec to use Bcrypt.*

Creating hashes
---------------

To create a salted hash we use \phpSec\Crypt\Hash::create(). It takes just one argument and that is the password you wish to create an hash from.

    <?php
    $hash = \phpSec\Crypt\Hash::create('password');
    echo $hash;

The above code will output something like: *$pbkdf2$c=8192&dk=128&f=sha256$cSgQjF7RNrc0c(...)3ZHdrug0kd/ttLCbiH8fh4sucFK+GEI9ITYBXvNt3oYepK0MXxzjGxhcUg4UxE1yA1pRhuIhZ2KamDduyz+A==*

This value can then be stored in a database for validation at a later time.

Validating passwords
--------------------

When validating password we use \phpSec\Crypt\Hash::check(). This method takes two arguments. The first is the password we want to check, and the second is the hash we created before. \phpSec\Crypt\Hash::check() will atomatically detect the method used to create the hash.

    <?php
    if(\phpSec\Crypt\Hash::check($_POST['password'], $hash)) {
      echo "Valid password";
    }

Changing hash method
--------------------

phpSec enables you to change hashing method without making old hashes unusable. So if you started using PBKDF2 and later decides to use bcrypt, you can just tell phpSec to use bcrypt when creating new hashes. Since phpSec automatically detects the hash type when callingn \phpSec\Crypt\Hash::check(), the old PBKDF2 hashes would still work.

If you want to create a hash using bcrypt all you need to do is to set *\phpSec\Crypt\Hash::$_method* to *\phpSec\Crypt\Hash::BCRYPT*.

    <?php
    \phpSec\Crypt\Hash::$_method = \phpSec\Crypt\Hash::BCRYPT;
    
    $hash = \phpSec\Crypt\Hash::make('password');
    echo $hash;

This will produce a hash that looks like this *$2a$12$1r4Sv3VuunDtN9sbjWSgfOO6wfM9vnwE9U4fZGhBaJVVgwtz3IsI6*.

Advanced settings
------------------
There are several options you could use to tune phpsecHash to work the way you want it to work. You can find a complete list [here](https://phpseclib.com/api/phpsec/lib--phpSec--Crypt--Hash.php/class/Hash/dev).
Please note that as shown in the example above you need to set *\phpSec\Crypt\Hash::$_method* to either:

* \phpSec\Crypt\Hash::BCRYPT
* \phpSec\Crypt\Hash::PBKDF2
* \phpSec\Crypt\Hash::SHA256
* \phpSec\Crypt\Hash::SHA512

