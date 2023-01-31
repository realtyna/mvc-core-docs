---
layout: default
title: Testing
nav_order: 6
---
# Testing
We use WordPress plugin unit test to write and run our tests.

Read more on [Plugin Integration Test](https://make.wordpress.org/cli/handbook/misc/plugin-unit-tests/) and install it's
dependencies on your system: PHPUnit, curl, svn, git, php and apache

## Install temporary WordPress and it's database
There is a bash script located in ```bin/install-wp-tests.sh```,
This script will install a WordPress in your system temp folder.

You should run this script to be able to run your tests.
Based on it`s documentation this how it works:

```
usage: ./bin/install-wp-tests.sh <db-name> <db-user> <db-pass> [db-host] [wp-version] [skip-database-creation]
```

so in my example it would be:
```bash
./bin/install-wp-tests.sh realtyna-test root admin 127.0.0.1 6.1.1
```


after you ran this command in your terminal you can use phpunit. you have 2 options
to do so:

- using ```phpunit``` in terminal
- using ```vendor/bin/phpunit``` in terminal

### bootstrap tests
Go on and take a look at ```tests/bootstap.php```.

this file is responsible to load WordPress before running your tests. feel free to dig deeper
in this file.

if you look at line 31-33 you see that it's loading your plugin.
So if you need to include another plugin in your test you should enter it`s path in this function.

## Test Naming

Take a look at ```phpunit.xml.dist```, you can see on line 12 
that PHPUnit will look for files that ends with ```Test.php``` in ```tests``` folder.

You can change that if you want.