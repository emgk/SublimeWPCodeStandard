## Configure Code Standard in Sublime using PEAR

### 1. Install PEAR 

To install the PEAR, you can use the following provisional way:

````
$ wget http://pear.php.net/go-pear.phar
$ php go-pear.phar
$ sudo apt-get install wget
````

### 2. Install PHP_Codesniffer

We're using PEAR, so we can install PHP_CodeSniffer using the PEAR installer. This will make the phpcs and phpcbf commands immediately available for use. To install PHP_CodeSniffer using the PEAR installer, first ensure you have installed PEAR and then run the following command:


- install PHP_CodeSniffer
````
$ sudo pear install PHP_CodeSniffer
````

- To get the list of all standard installed by default 
````
$ phpcs -i
should return : The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz and Zend
````

- if it return 
````
Warning: include_once(PHP/CodeSniffer/CLI.php): failed to open stream: No such file or directory in /usr/bin/phpcs on line 22
Warning: include_once(): Failed opening 'PHP/CodeSniffer/CLI.php' for inclusion (include_path='.:') in /usr/bin/phpcs on line 22
Fatal error: Class 'PHP_CodeSniffer_CLI' not found in /usr/bin/phpcs on line 25
````
-- Must include pear path
-- Modify php.ini
````
$ sudo vim /etc/php.ini
````
````
include_path = ".:/usr/share/pear"
````

### 3. Configure WordPress coding standard to PHPCS using this commands

* Clone WordPress standards repository

````
$ git clone git://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards.git $(pear config-get php_dir)/PHP/CodeSniffer/Standards/WordPress
````

* Add its path to PHP_CodeSniffer configuration

````
$ phpcs --config-set installed_paths $(pear config-get php_dir)/PHP/CodeSniffer/Standards/WordPress
````

* Set default standard to PHP_CodeSniffer

````
$ phpcs --config-set default_standard WordPress
````

### 4. Sublime Text

sublime-phpcs package

Install the [sublime-phpcs package](https://github.com/benmatselby/sublime-phpcs), then use the "Switch coding standard" command in the Command Palette to switch between coding standards.

#### now in sublime 

Go to 
````
Preference-> Package Settings>PHP Codesniffer>user
````
Add this code 
````
{
	"phpcs_executable_path": "phpcbf",
	"phpcs_linter_run": true
}
````

All Done !
