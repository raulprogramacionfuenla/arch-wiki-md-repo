[PHPUnit](https://phpunit.de/) is a programmer-oriented testing framework for PHP.

## Contents

*   [1 Installing](#Installing)
    *   [1.1 DbUnit](#DbUnit)
*   [2 Example](#Example)
*   [3 References](#References)

## Installing

By far the easiest way to install is using the PHP Archive ([PHAR](http://php.net/phar)) package provided by the project. The PHAR package contains all dependencies as well as some of the optional dependencies for PHPUnit. The latest version can be retrieved from the project's site:

```
wget [https://phar.phpunit.de/phpunit.phar](https://phar.phpunit.de/phpunit.phar)

```

**Note:** PHPUnit is also avalible from the [AUR](/index.php/AUR "AUR") as [phpunit](https://aur.archlinux.org/packages/phpunit/).

You can then run PHPUnit using `php phpunit.phar`. You can also make the PHP Archive executable (`chmod +x phpunit.phar`) and move it to /usr/local/bin or ~/bin or somewhere else you have in your `$PATH`.

### DbUnit

Since version 7, the DbUnit extension for database interaction testing is no longer supplied as part of the base PHAR, and needs to be installed separately. Download it from the project site:

```
wget [https://phar.phpunit.de/dbunit.phar](https://phar.phpunit.de/dbunit.phar)

```

Place it in a suitable directory, and then configure PHPUnit to load extensions in that directory as described in the [DbUnit readme](https://github.com/sebastianbergmann/dbunit/blob/master/README.md).

## Example

This section gives beginners a very brief introduction to how to use PHPUnit to run test cases. It won't explain how to write them but if you want to get more information about this have a look at the references.

As the application to be tested we use in this example a [JSON schema validator](https://github.com/hasbridge/php-json-schema%7C). In the directory *tests* you'll see the directory *mock* and three files.

*   mock
*   JsonValidatorTest.php
*   bootstrap.php
*   phpunit.xml

*mock* contains JSON schemas which have nothing to do with PHPUnit itself, it's application-specific here, you won't find it in other applications.

*phpunit.xml is a [configuration file](http://www.phpunit.de/manual/current/en/appendixes.configuration.html) where you*

*   configure PHPUnit's core functionality,
*   compose a test suite out of test suites and test cases,
*   select groups of tests from a suite of tests that should (not) be run,
*   configure the blacklist and whitelist for the code coverage reporting,
*   configure the logging of the test execution,
*   attach additional test listeners to the test execution,
*   configure PHP settings, constants, and global variables or
*   configure a list of Selenium RC servers.

In *bootstrap.php* you put code to be run before tests are executed. Here you could register your autoloading functions or include other php scripts. Though there's one limitation, only one bootstrap can be defined per PHPUnit configuration file.

*JsonValidatorTest.php* is the PHP file with the test cases. It's beyond the scope to explain the content of this file in depth. As a beginner you are most likely interested in how to run the test cases so what you need to execute is simply

 `phpunit JsonValidatorTest JsonValidatorTest.php` 

You pass it the class with the test cases and the file where they're defined. That's it.

## References

*   [Official PHPUnit Manual](http://www.phpunit.de/manual/current/en/index.html)
*   [Introduction to Unit Testing with PHPUnit](http://www.slideshare.net/DragonBe/introduction-to-unit-testing-with-phpunit-presentation-705447)