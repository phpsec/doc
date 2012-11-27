Getting started
===============

Altough phpSec is pretty plug and play there are some small steps you need to take before you are ready to harness the power of phpSec. First of all make sure all the required
files are loaded, either manually or using an autoloader.

### Preparing the data storage if needed ###

phpSec saves data in something called *the store*. Everything from session data to cache and one time passwords are saved there. Configuring the store is **optional** if you only want to use the basic functionality of phpSec.
**The following modules require a configured store:**

* Cache
* Otp
* OtpCard
* Session
* Token

If you want full phpSec functionality you need to configure the store. This is done with the *\phpSec\Common\Core::setStore()* method. The store is defined as a string with the storage method followed by a colon (:), and the storage destination. So if you want to save your data using flat files to */var/www/phpSec/data* the following example would be correct.

    <?php
    \phpSec\Common\Core::setStore('filesystem:/var/www/phpSec/data');

The target directory needs to be writeable by PHP, and should *not* be accessible trough your web server. 

#### Using mySQL for storage ####
If you want, you can also use mySQL for storing phpSec data. phpSec will not create any tables for you, but it will check the table structure. the following table is required for phpSec. you can call it anything you want:

    --
    -- Table structure for table `phpsec`
    --
    
    CREATE TABLE IF NOT EXISTS `phpsec` (
      `type` varchar(255) NOT NULL COMMENT 'Type of data.',
      `id` varchar(255) NOT NULL COMMENT 'Item ID.',
      `mac` binary(32) NOT NULL COMMENT 'Message Authentication Message.',
      `time` int(11) unsigned NOT NULL COMMENT 'Unix time stamp of creation time.',
      `data` text NOT NULL COMMENT 'Serialized object.',
      UNIQUE KEY `id` (`id`),
      KEY `type` (`type`)
    ) ENGINE=MyISAM DEFAULT CHARSET=utf8;

To tell phpSec to use mySQL, you will have to call the *\phpSec\Common\Core::setStore()* method with the database details in a special string. This can look something like this:

    <?php
    
    $dsn = 'mysql:' .
      'dbname=mydb;' .
      'table=phpsec;' .
      'host=localhost;' .
      'username=myuser;' .
      'password=mypass';
    
    \phpSec\Common\Core::setStore($dsn);

The above is an example of how your string may look like. The string consists of several configuration opions and their values. The following options are available and all of them are required. The order is not important.

<table>
  <thead>
    <tr>
      <th scope="col">Variable</th>
      <th scope="col">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>dbname</td>
      <td>Name of your database.</td>
    </tr>
    <tr>
      <td>table</td>
      <td>Name of the table. Should be phpsec if you didn&#39;t change it when creating the table.</td>
    </tr>
    <tr>
      <td>host</td>
      <td>Hostname to your mySQL server. Usually localhost.</td>
    </tr>
    <tr>
      <td>username</td>
      <td>Your database username.</td>
    </tr>
    <tr>
      <td>password</td>
      <td>Your database password.</td>
    </tr>
  </tbody>
</table>


