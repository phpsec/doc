Altough phpSec is pretty plug and play there are some small steps you need to take before you are ready to harness the power of phpSec. First of all make sure all the required
files are loaded, either manually or using an autoloader.

Preparing the data storage if needed
------------------------------------
phpSec saves data in something called *the store*. Everything from session data to cache and one time passwords are saved there. Configuring the store is optional if you only want to use the basic functionality of phpSec.
The following modules require a configured store:
  * Cache
  * Otp
  * OtpCard
  * Session
  * Token

If you want full phpSec functionality you need to configure the store. This is done with the *phpSec\Common\Core::setStore()* method. The store is defined as a string with the storage method followed by a colon (:), and the storage destination. So if you want to save your data using flat files to */var/www/phpSec/data* the following example would be correct.

    phpSec\Common\Core::setStore('filesystem:/var/www/phpSec/data');

The target directory needs to be writeable by PHP, and should not be accessible trough your web server. Setting up phpSec to use mySQL is a bit more complex, but is [well described here](/node/7595). Be sure to come back here to complete your set-up.

After this, you are ready to harness the power of phpSec.
