# Deployment scripts

Scripts for fast user, site configs, database and git autodeployment creating on VPS/VDS

## Script for initial site deploying

This script can be using when you need to fast create your vps/vds linux user,
site directory structure, database and git repo for autodeployment.

### Common usage
```shell
./init site|git|db|setup options
```

### Making site
```shell
./init site <site_domain>[:<site_ip>] <template> <ssh_username> [<ssh_password>]
```
Where `<site_domain>` is web domain, which would be placed at nginx config for listenting connections.

Where `<site_ip>` is server ip, which would be placed at nginx config for listenting connections.

Where `<template>` is config template preset. Can be one of simple, yii.

`<site_ip>` can be omitted, but it can be required on some server configurations.

If `<ssh_password>` not set it would be generated.

Examples:
```shell
./init site example.com simple user1 1234567890
./init site example.com yii user1
```

### Making git bare repo autodeployment set
```shell
./init git <path_to_project> <username> [<branch_name>]
```
Where `<project_path>` is path to your project where git repo will be created.

Where `<username>` is the user that will be set as the owner for the .git directory.

If `<branch_name>` not set it would be "master".

Examples:
```shell
./init git "/var/www/user1/www/example.com" user1 main
./init git "/var/www/user1/www/example.com" user1
```

### Making database
```shell
./init db <dbname> [ <dbuser> [<dbpass>] ]
```
If `<dbuser>` not set it would be equal to dbname.

If `<dbpass>` not set it would be generated.

Examples:
```shell
./init db database1 dbuser1 1234567890
./init db database1 dbuser1
./init db database1
```

### Making project setup
```shell
./init setup <project_path> <username> [options]
```
Where `<project_path>` is path to your project within which commands will be executed.

Where `<username>` is the user that will be set as the owner for the project directory and its content.

Where options:
- `composer-install` - composer install
- `yii-init` - yii init production
- `yii-config` - yii database config file
- `yii-migrate` - yii database migrations

If no options used - all of them will be applied.

Examples:
```shell
./init setup /var/www/user1/www/example.com user1 composer-install yii-init yii-config yii-migrate npm
./init setup /var/www/user1/www/example.com user1
```

### Making npm-project setup
```shell
./init npm <npm_project_path> <username> [options]
```
Where `<npm_project_path>` is path to your npm-project files within which commands will be executed.

Where `<username>` is the user that will be set as the owner for the npm-project directory and its content.

Where options:
- `install` - instal npm dependencies
- `build` - run build script

If no options used - all of them will be applied.

Examples:
```shell
./init npm /var/www/user1/www/example.com/vuejs user1 install build
./init npm /var/www/user1/www/example.com/vuejs user1
```

### Additional script params
You can edit script params in section `# Script params` of `./init` file.

#### Defaults are:
- is_mariadb=true
- php_executable="/usr/bin/php81"
- composer_executable="/usr/bin/composer"
- npm_executable="/usr/bin/npm"
- nginx_conf_dir="/etc/nginx/conf.d"
- php_fpm_conf_dir="/etc/opt/remi/php81/php-fpm.d"
- nginx_service="nginx"
- php_fpm_service="php81-php-fpm"