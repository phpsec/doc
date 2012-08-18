The phpSec session handler is an advanced session handler that changes the way session data is handled by the web server. The phpSec session handler has a number of advantages over the regular PHP session handler.

### Hard to guess session ID ###
The same session ID is only used once. This makes session hijacking harder. The session ID is a 128 byte string, that makes it just about impossible to guess a session ID.

### Safe storage ###
All session data is encrypted using a user specific encryption key that is stored in a cookie on the users computer. This key is changed each 30 seconds. The data is saved in the phpSec store, allowing for storage in databases or flat files.

### Easy to use ###
To enable the phpSec session handler all you have to do is to configure the phpSec store (described in chapter 1) and add the following line where you usually would put `session_start();`

    \phpSec\Common\Session::init(true);

The argument passed to Session::init() tells phpSec to regenerate the session ID. This feature can cause problems on Ajax requests, and could be set to false if you want.
Please note that you should *not* call `session_start()`, since this will cause problems.
