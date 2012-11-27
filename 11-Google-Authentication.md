Google Authenticator
====================

[Google Authenticator](http://en.wikipedia.org/wiki/Google_Authenticator) is a Time based One Time Password (TOTP) based on RFC 4226 which is initialised using a 16 digit Base32 (RFC 4648) encoded secret.
The secret can be entered into the Google Authenticator app manually by keyboard, or by scanning a QR code.
To use Google authentiator you need to have [configured a store](http://phpseclib.com/manual/gettingstarted) for phpSec.

phpSec is able to:

* Generate Base32 encodeed secrets
* Create links for adding secrets to Google Authenticator
* Validating OTP

phpSec also includes additional security features that prevents a user from using the same OTP multiple times, and that a token
is newer than the last token used.

### Generating keys ###
To generate a key to use with Google Authenticator you can use the newKey() method.
This method will generate the 16 digit Base32 encoded secret that you will need to add to the Google Auth application.
You will also need to save this secret in your user database, as you need it when validating OTPs entered by the user.

    <?php
    $secret = \phpSec\Auth\Google::newKey();

You can add this to your Google Authenticator manually, or you can use the getUrl() method to create links to add it.

    <?php
    $secret = \phpSec\Auth\Google::newKey();
    
    $url = getUrl('Account name', $secret);
    
    /* Mobile use. */
    echo $url['url'];
    
    /* QR code */
    echo $url['qr'];

### Verifying an OTP ###
To verify a OTP you use the verify() method. The first parameter is the OTP as entered by the user. This should be a 6 digit number.
The second argument is the user secret that was added to the Google Auth application before.

    <?php
    if(\phpSec\Auth\Google::verify($_POST['otp'], $secret) === true) {
        /* Valid OTP. */
    } else {
        /* Invalid OTP. */
    }

