#### Requirements ####
 * The following classes is required.

    * \phpSec\Common\Core

Random isn't always random enough. The built in [random functions in PHP](http://php.net/manual/en/function.mt-rand.php) may be good enough for displaying a random quote, or a random image. But when it comes to generating random data for use in encryption keys or other security related things the pseudo random generator provided by phpSec is preferable.

phpSec provides you with a number of different methods of collecting random data. All of them uses the same pseudo random generator, the only difference is how they return the data.

### Random numbers ###
Getting random numbers with phpSec is done with \phpSec\Crypt\Rand::int(). This method takes two arguments. The first is the lowest possible number, and the second is the highest possible number. The following example will produce a random number between 1 and 10.

    <?php
    echo \phpSec\Crypt\Rand::int(1, 10);


### Random strings ###
Random strings can be used for example to create new passwords to users in case they have lost the current password.
Random strings are created with \phpSec\Crypt\Rand::str(). This method takes only one argument, the length of the string to be generated. The following example will produce a random string of 10 characters.

    <?php
    echo \phpSec\Crypt\Rand::str(10);

It is also possible to define what characters to use when generating the string.

    \phpSec\Crypt\Rand::$_charset = 'abcdef';
    echo \phpSec\Crypt\Rand::str(10);


### Random array keys ###
phpSec can also select random keys from an array. This is done with the <a href="/api/phpsec/phpsec--phpsec.rand.php/function/phpsecRand%3A%3AarrayRand">phpsecRand::arrayRand()</a> This method takes two arguments, the first one is the array to pick random keys from, and the second is the number of keys to pick. If only one key is picked this method returns a string. If multiple keys are picked it will return an array.

    <?php
    $array = array(
     'key' => 'foo',
     'bar'
    );

    print_r(\phpSec\Crypt\Rand::arrayRand($array, 1));


### Random data ###
It is also possible to collect random bytes from phpSec. This can be used if you don't need data that is printable. A good example is if you need an encryption key. Binary data is collected using \phpSec\Crypt\Rand::bytes().
This method only takes one argument, how many bytes to produce.

    <?php
    echo \phpSec\Crypt\Rand::bytes(32);
