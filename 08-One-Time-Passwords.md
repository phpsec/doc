[One time passwords (OTP)](http://en.wikipedia.org/wiki/One-time_password) is a password that is valid for only one login session or transaction. It can be used for [multi-factor authentication](http://en.wikipedia.org/wiki/Multi-factor_authentication) or lost password recovery. phpSec provides a class (\phpSec\Auth\Otp) for creating and validating passwords, but the [delivery method](http://en.wikipedia.org/wiki/One-time_password#Methods_of_delivering_the_OTP) must be implemented separately.

### Generating a OTP ###
You should only generate a OTP when you require the user to supply one. \phpSec\Auth\Otp::generate() takes several parameters that allows you to specify what the OTP will be used for. This way you ensure that the OTP is only used for the intended action.

    <?php
    $action ='login';
    $data['user'] = $_POST['username'];
    
    $otp = \phpSec\Auth\Otp::generate($action, $data);

The *$action* string specifies the action that the OTP will be used for. This is required. The *$data* array allows you to specify additional data about the request, making sure the OTP is used with the correct parameters. This is an optional setting.

The next step is to deliver the OTP to the user, using a trusted channel. For example an encrypted e-mail, SMS or a pidgin. For now phpSec does not contain any methods for doing this.

### Validating a OTP ###
When validating a OTP all you need is a simple call to the \phpSec\Auth\Otp::validate() method.

    <?php
    $action ='login';
    $data['user'] = $_POST['username'];
    
    if(\phpSec\Auth\Otp::validate($_POST['otp'], $action, $data)) {
      // Success. Do the rest of the login stuff here.  
    } else {
      echo 'Login failed.';
    }

The *$action* and *$data* parameters must be identical to the one used when creating the OTP or else the validation will fail.

