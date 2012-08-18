#### Requirements ####
 * The following classes is required.

    * \phpSec\Common\Core

Authy is a simple API to add two-factor authentication to your website or app. Before you start implementing Authy please read trough the documentation at [their website](https://authy.com/).

### Getting Started ###
First of all you need to create a user on the [Authy website](https://authy.com/) and create an API key. Afther doing this, you need to tell phpSec about your API key.

    <?php
    \phpSec\Auth\Authy::$_apiKey = '0fc9b66ef2132aab01b3d7d9055b00ea';
    
### Adding users ###
To add Authy users to your application and get their Authy ID we use \phpSec\Auth\Authy::userNew(). This method takes three arguments.
 *  User e-mail
 *  User cellphone
 *  User countrycode

    <?php
    \phpSec\Auth\Authy::$_apiKey = '0fc9b66ef2132aab01b3d7d9055b00ea';
    $authyID = \phpSec\Auth\Authy::userNew($user['email'], $user['cellphone'], $user['countrycode']);
    
We then need to store the *$authyID* for the user in our database.

### Validating Authy tokens ###
To validate a Authy token we forst need to get the Authy ID from our user database. Then we call \phpSec\Auth\Authy::verify() with the Authy ID and the Authy token entered by the user.

    <?php
    \phpSec\Auth\Authy::$_apiKey = '0fc9b66ef2132aab01b3d7d9055b00ea';
    /* Fetch $authyID from user database. */
    if(\phpSec\Auth\Authy::verify($authyID, $_POST['authy']) === true) {
      /* Valid Authy token. */
    } else {
      /* Invalid token. */
      echo \phpSec\Auth\Authy::$lastError;
    }

### Error Codes ###
If something goes wrong you can find out what, by looking at *\phpSec\Auth\Authy::$lastError*. The following list explains what you might expect.

 *  AUTHY_SERVER_INVALID_API_KEY
    API key provided not valid.
 *  AUTHY_SERVER_ERROR
    Could not reach Authy servers.
 *  AUTHY_SERVER_INVALID_DATA
    Data provided with request not accepted.
 *  AUTHY_SERVER_SAYS_NO
    Unknown error returned by server.
 *  AUTHY_SERVER_BAD_OTP
    Authy token provided not valid.

