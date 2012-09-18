To use Google authentiator you need to have [configured a store](http://phpseclib.com/manual/gettingstarted) for phpSec.


### Generating keys ###
To generate a secret key to use with Google authenticator you can use the newKey() method.

    <?php
    $secret = \phpSec\Auth\Google::newKey();

You can add this to your Google authenticator manually, or you can use the getUrl() method.

    <?php
    $secret = \phpSec\Auth\Google::newKey();
    
    $url = getUrl('Account name', $secret);
    
    /* Mobile use. */
    echo $url['url'];
    
    /* QR code */
    echo $url['qr'];

### Verifying an OTP ###
To verify a one tme token you can use the verify() method.

    <?php
    if(\phpSec\Auth\Google::verify($_POST['otp'], $secret) === true) {
        /* Valid OTP. */
    }

