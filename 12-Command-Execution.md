Command Execution
=================

The Exec class allows you to execute commands in a PDO like way.
It also provides more detailed output from the executed command, and allows you to pass data to the command after it is executed.
The Exec class only has one public method: [run()](https://phpseclib.com/api/phpsec/lib--phpSec--Common--Exec.php/function/Exec%3A%3Arun).

    Exec::run($cmd, $arg, $stdin);

* **$cmd** Command to execute. If you need to pass arguments to a command. A PDO like syntax can be used. For example: "ls -lsa %path". 
* **$arg** An associative array containing the arguments to pass to $cmd. For example: array('%path' => '/home');
* **$stdin** If the command requests input (e.g. a passphrase) this can be passed here. Note that if a command requires multiple feedbacks from a user this method can not be used.

Exec::run() will return an array containing three values:

* **STDOUT** Normal output from the command.
* **STDERR** Error output from the command.
* **return** [Exit status](http://en.wikipedia.org/wiki/Exit_status).

### Simple example ###

    <?php
    print_r(\phpSec\Common\Exec::run('ls -lsa %path',
      array(
        '%path' => '/home/',
      )
    ));

Thsi example will output something like this:

    Array
    (
        [STDOUT] => total 12
        4 drwxr-xr-x  3 root  root  4096 May 29 22:44 .
        4 drwxr-xr-x 27 root  root  4096 Jul 22 02:44 ..
        4 drwxr-xr-x 57 xqus  xqus  4096 Nov  6 14:19 xqus
    
    [STDERR] => 
    [return] => 0
    )

### Passing input to command ###
You can pass data to a command using the $stdin parameter. 

    print_r(\phpSec\Common\Exec::run('php', array(), "<?php echo 'Hello World!';"));

This example would output:

    Array
    (
        [STDOUT] => Hello World!
        [STDERR] => 
        [return] => 0
    )

