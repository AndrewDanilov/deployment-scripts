# Deployment scripts

Scripts for fast user, site configs, database and git autodeployment creating on VPS/VDS

## Script for initial site deploying

This script can be using when you need to fast create your vps/vds linux user,
site directory structure, database and git repo for autodeployment.

### Common usage
```shell
./deploy site|git|db|setup options
```

### Making site
```shell
./deploy site <site_domain> <template> <ssh_username> [<ssh_password>]
```
Where `<template>` is config template preset. Can be one of simple, yii.
If `<ssh_password>` not set it would be generated
Examples:
```shell
./deploy site example.com simple user1 1234567890
./deploy site example.com yii user1
```

### Making git bare repo autodeployment set
```shell
./deploy git <path_to_project> [<branch_name>]
```
If `<branch_name>` not set it would be "master"
Examples:
```shell
./deploy git "/var/www/user1/www/example.com" main
./deploy git "/var/www/user1/www/example.com"
```

### Making database
```shell
./deploy db <dbname> <dbuser> [<dbpass>]
```
If `<dbpass>` not set it would be generated
Examples:
```shell
./deploy db database1 dbuser1 1234567890
./deploy db database1 dbuser1
```

### Making project setup
```shell
./deploy setup <project_path> [options]
```
Where `<project_path>` is path to your project within which commands will be executed.
Where options:
- `composer-install` - composer install
- `yii-init` - yii init production
- `yii-config` - yii database config file
- `yii-migrate` - yii database migrations
If no options used - all of them will be applied
Examples:
```shell
./deploy setup /var/www/user1/www/example.com composer-install yii-init yii-config yii-migrate npm
./deploy setup /var/www/user1/www/example.com
```

### Making npm-project setup
```shell
./deploy npm <npm_project_path> [options]
```
Where `<npm_project_path>` is path to your npm-project files within which commands will be executed.
Where options:
- `install` - instal npm dependencies
- `build` - run build script
If no options used - all of them will be applied
Examples:
```shell
./deploy npm /var/www/user1/www/example.com/vuejs install build
./deploy npm /var/www/user1/www/example.com/vuejs
```

### Additional script params
You can edit script params in section `# Script params` of `deploy` file.

#### Defaults are:
- is_mariadb=true
- php_executable="/usr/bin/php81"
- composer_executable="/usr/bin/composer"
- npm_executable="/usr/bin/npm"
- nginx_conf_dir="/etc/nginx/conf.d"
- php_fpm_conf_dir="/etc/opt/remi/php81/php-fpm.d"
- nginx_service="nginx"
- php_fpm_service="php81-php-fpm"