# Etalik - test

The project run with Symfony 5.4 (Lts) with the following requirement : 

- php v8.3 or higher
- Mariadb v10

### - Clone the project
git clone https://github.com/randrianantenaina8/etalik-test.git




### - install the vendor libraries
get into your project root directory and execute the following command :
Run composer install to download the suitable vendors.  


```shell
$ composer install
```

### - Update the database schema (if already exists)
```shell
$ docker exec jarvis-php-fpm php bin/console doctrine:schema:update --force --complete 
$ docker exec jarvis-php-fpm php bin/console cache:clear
```
or inside your jarvis-php-fpm container cmd (for wsl user with docker desktop)
```shell
$ php bin/console doctrine:schema:update --force --complete 
$ php bin/console cache:clear
```

### - Create the database schema (if not exist only) 
```shell
$ docker exec jarvis-php-fpm php bin/console doctrine:migrations:migrate
$ docker exec jarvis-php-fpm php bin/console cache:clear
```
or inside your jarvis-php-fpm container cmd (for wsl user with docker desktop)
```shell
$ php bin/console doctrine:migrations:migrate
$ php bin/console cache:clear
```



### - Test every webservice on browser
- Test on http://127.0.0.1:9088 for web test,
- for mysql: http://127.0.0.1:9086,

## If you don't use docker

### - Install php 8.2, mysql and any webserver you are comfortable with on your host
### You are on your own for the details about the server configurations :-)
- see the activation of xdebug, curl extension on the webserver 

### - Create a local environment file
```shell
$ cp ./.env ./.env.local
```
### - Customize .env.local for mysql accesses according to your installations

## Using Xdebug for PhpStorm user with Postman

Jarvis use xdebug v3.3.4 for php 8.2 as a debugger, you can use the configuration below in case it is not created automatically on build up.
- Go to settings > Php > Cli interpreter and add a new CLI interpreter by using the "from docker, Vagrant, VM, WSL ...', select as source the php jarvis fpm image.
- Go to settings > Php > Servers and if the Server "jarvis" is missing from your list, add a new server with a serverName "jarvis"
- follow the mapping from the docker compose image as "/var/www/html" as main entry, and point the public dir as "/var/www/html/public"

## To Enable xdebug on postman
- add "XDEBUG_SESSION=PHPSTORM; Path=/; Expires=<Expiry time>;" as a cookie of your host

## Validate code with grumphp
To keep code quality, readability and scalability. This project use phpro/grumphp as a tool to improve the codebase with a set of common tasks on pre-commit. 
- php-cs-fixer : 
  * cs rules can be edited in php-cs-fixer.php and based on the documentation from https://cs.symfony.com/doc/rules/index.html
  * using phpstorm php-cs-fixer can be activated from Settings > Quality tools > php cs fixer,  use the the same configuration as the project do to limit conflict.
- php-unit :
  * make sure all the unit test pass after any update on the code
  * !!! Important !!! make sure your test database is different from other environment, since it will restored to empty after each test session.

## Commit Validation
make sure to use the following command to validate your code before before you commit your modification : 
```shell
$ php ./vendor/bin/grumphp run
```
 