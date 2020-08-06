# Laravel Setup

## Install PHP

```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php7.4
```

### Verify the installation with `php -v`

## Install MySQL

```bash
sudo apt install php7.4-mysql
sudo apt install mysql-server
sudo mysql_secure_installation
```

### Perform MySQL installation as per the following

- Skip the `Validate Password Plugin`
- Choose a password for `root` user
- Remove the anonymous users, disallow the `root` user from remote access, and remove the test database
- When asked to reload privilege tables select `yes`

### Create a non-root user with root privileges

```sql
# Log into MySQL as root
sudo mysql -u root -p 

# Create a user - admin with a blank password
CREATE USER 'admin'@'localhost' IDENTIFIED BY '';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;

# Exit MySQL
exit
```

### Verify that you can login via `admin` by: `mysql -u admin`

## Install Composer

```bash
sudo apt update

# Download some required dependencies (use php7.4-x if required)
sudo apt install curl php-cli php-mbstring git unzip

# Refer to the Composer Documentation for #1 and #2
[https://getcomposer.org/download/](https://getcomposer.org/download/)

#1 Download the installer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

#2 Verify the installer
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e5325b19b381bfd88ce90a5ddb7823406b2a38cff6bb704b0acc289a09c8128d4a8ce2bbafcd1fcbdc38666422fe2806') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

# Install Composer
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# Update permissions to the composer directory
sudo chown -R $USER ~/.composer/
```

### Verify the installation with `composer`

## Install Laravel

```bash
# Download some required dependencies
sudo apt install php7.4-zip
sudo apt install php7.4-xml

# Download Laravel using composer
composer global require laravel/installer

# Update the $PATH env
export PATH="~/.composer/vendor/bin:$PATH"
```

## First Laravel Project

### Create a database in MySQL

```sql
// Log into MySQL as admin
mysql -u admin

// Create a new database - blog
CREATE DATABASE blog;
```

### Initiate the Laravel Project

```php
// Initiate a new laravel project - blog. This will create a directory named blog
laravel new blog

// To initiate the project with authentication
laravel new blog --auth

// Open the .env file
nano .env

// Change the database settings to this:
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=blog
DB_USERNAME=admin
DB_PASSWORD=
```

### Run the server: `php artisan serve`

### Activate the built-in authentication (in an existing project without auth)

```php
// Install the required dependency
composer require laravel/ui

// Generate the authentication system
php artisan ui vue --auth
```

# Using Laravel Valet

## Install dependencies

```bash
sudo apt-get install php7.4-curl
sudo apt-get install jq
sudo apt-get install xsel
sudo apt-get install libnss3-tools
```

## Download Valet

```bash
composer global require cpriego/valet-linux
```

## Install Valet

```bash
valet install
```

## Configure Valet

```bash
# Create a directory wherein you can store all your projects
mkdir sites
cd sites

# Park the directory so that valet can serve the projects inside it
valet park
```

## Using Valet

Now you can access all your laravel projects inside `sites` at `blog.test` or `<app-name>.test` 

If you don't want to `park` an entire directory, you can `link` a specific project like: `valet link blog`

# Resources

Laravel setup

[https://dev.to/andrewbrooks/setting-up-laravel-local-dev-environment-on-ubuntu-51kp](https://dev.to/andrewbrooks/setting-up-laravel-local-dev-environment-on-ubuntu-51kp)

Laravel Valet

[https://dev.to/andrewbrooks/using-laravel-valet-on-linux-ubuntu-2bcf](https://dev.to/andrewbrooks/using-laravel-valet-on-linux-ubuntu-2bcf)

[https://cpriego.github.io/valet-linux/index](https://cpriego.github.io/valet-linux/index)

Stackoverflow

[https://stackoverflow.com/questions/28597648/laravel-5-installation-in-ubuntu-laravel-command-not-found](https://stackoverflow.com/questions/28597648/laravel-5-installation-in-ubuntu-laravel-command-not-found)

Laravel Documentation

[https://laravel.com/docs/7.x](https://laravel.com/docs/7.x)

Composer Documentation

[https://getcomposer.org/](https://getcomposer.org/)
