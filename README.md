# Vagrant-Debian-Ansible-LEMP

[![Build Status](https://travis-ci.org/neikei/vagrant-debian-ansible-lemp.svg?branch=master)](https://travis-ci.org/neikei/vagrant-debian-ansible-lemp)

This is a development environment for Symfony projects on a Debian based Vagrantbox.

## Included components

| Software | Debian Jessie | Debian Stretch | Tested   |
|----------|---------------|----------------|----------|
| Debian   | 8.10          | 9.4            | &#10003; |
| Nginx    | 1.12.2        | 1.12.2         | &#10003; |
| MariaDB  | -             | 10.3           | &#10003; |
| Redis    | 2.8.17        | 3.2.6          | &#10003; |
| PHP      | 7.2           | 7.2            | &#10003; |
| PHPUnit  | 7.0.2         | 7.0.2          | &#10003; |
| Composer | 1.6.3         | 1.6.3          | &#10003; |
| Node.js  | 8.10.0        | 8.10.0         | &#10003; |
| Symfony  | 4.0.8         | 4.0.8          | &#10003; |

## Requirements

- Hypervisor
  - Virtualbox >= 5.2.4 (do not use it with MacOS)
  - Parallels >= 10 (use it with MacOS)
- Vagrant >= 2.0.1
- Vagrant Plugins:
  - vagrant-hostmanager # necessary for host entries
  - vagrant-vbguest # recommended for virtualbox users
  - vagrant-winnfsd # only for Windows

## Getting started

1. git clone https://github.com/neikei/vagrant-debian-ansible-lemp.git
2. cd vagrant-debian-ansible-lemp
3. vagrant up --provider=virtualbox OR vagrant up --provider=parallels
4. ... wait ...
5. Check the initial webpage: http://lemp.test/

## Default access

- Default project: http://lemp.test/
- Default web root: /vagrant/web
- Symfony projects: http://example.lemp.test
- Symfony web root: /vagrant/example
- MySQL: 192.168.56.111:3306
  - user: admin
  - password: changeme
  - root is allowed to access the database from localhost without a password
- Redis: 127.0.0.1:6379

## Symfony3 Debugging

The app_dev.php file of your application has to allow the first IP of the configured network. In the config.yaml example you have to allow the IP '192.168.56.1' in your app_dev.php to use http://example.lemp.test/app_dev.php for debugging.

```php
if (isset($_SERVER['HTTP_CLIENT_IP'])
    || isset($_SERVER['HTTP_X_FORWARDED_FOR'])
    || !(in_array(@$_SERVER['REMOTE_ADDR'], ['127.0.0.1', '::1', '192.168.56.1'], true) || PHP_SAPI === 'cli-server')
) {
    header('HTTP/1.0 403 Forbidden');
    exit('You are not allowed to access this file. Check '.basename(__FILE__).' for more information.');
}
```

## xDebug

xDebug is available on port 9000 from your local machine to debug your application with tools like PHPStorm.

## Configuration

Check the config.yml if you want to modify the following settings.

```yaml
configs:
    os: "9.4"                       # Choose between 8.10 and 9.4 (change requires: vagrant destroy & vagrant up)
    private_ip: "192.168.56.111"    # VM IP in your host-only-network
    vmname: "symfony-development"   # VM name for Virtualbox
    servername: "lemp.test"         # Servername and domain for your projects
    projectnames:                   # Comma-separated list with your symfony projectnames (change requires: vagrant provision & vagrant hostmanager)
      - foo                         # Generated URLs => foo.lemp.test
      - bar                         # Generated URLs => bar.lemp.test
    symfony_version: 4.0            # Symfony version like 4.0 or 3.4
```

Every servername or projectname change needs an update of your local hostfile.

```bash
vagrant hostmanager
```

## Feedback, Issues and Pull-Requests

Feel free to report issues, fork this project and submit pull requests.

## Changelog
19 June 2018

- add ansible role for yarn js packes manager

25 May 2018

- Update to install Percona Version of MySQL instead of MariaDB

16 May 2018

- Update MariaDB to 10.3 (similar with MySQL 5.7)

13 April 2018

- Updated Ansible to version 2.5

28 March 2018

- Updated Debian to version 9.4

23 March 2018

- Improved the ansible installation to prevent breaking version changes
- Disabled node-sass installation again

12 March 2018

- Re-enabled node-sass installation

09 March 2018

- Added Symfony 4 support
- Updated PHP to version 7.2
- Ansible YAML improvements
- Updated nodejs to version 8

1 February 2017

- Updated Ansible to version 2.4.3

26 January 2018

- Updated Debian version to 9.3 and 8.10

25 December 2017

- Updated Vagrant version to 2.0.1
- Documentation improvements

08 December 2017

- Documentation improvements

30 November 2017

- Updated Ansible version to 2.4.2.0

07 November 2017

- Added php-apcu and php-memcache packages
- Improved Ansible installation
- Pinned Ansible version to 2.4.1.0

06 November 2017

- Removed Varnish
- Updated Debian to version 9.2

04 October 2017

- Fixed Nginx vhost include configuration

06 September 2017

- Changed Nginx installation source to the official repository
- Fixed Nodejs installation

30 August 2017

- Modifications for Debian Stretch
- Improved xDebug configuration

08 August 2017

- Modifications for Debian Stretch
- Added os switcher to the config.yaml
- Updated Readme.md

09 July 2017

- xDebug configuration improvements
- Added check of minimum Vagrant version

28 June 2017

- Updated Debian to version 8.8

14 June 2017

- Configurable symfony version
- Improved service start after vagrant up

06 June 2017

- Added basic xDebug configuration

02 June 2017

- Improved service start and autostart
- Updated Readme.md
- Updated .gitignore
- Added imagemagick

02 May 2017

- Update local hostfile instead of re-build the whole box

31 March 2017

- Documentation improvements

21 March 2017

- Improved multi-project handling
- Added Redis
- Added Varnish

16 March 2017

- Node.js installation improvements
- Updated Nginx to version 1.10.3 from dotdeb

14 March 2017

- Added hostmanger for local hostfile management
- Improved PHP, Nginx and Nodejs installation
- Added Symfony 3.2 compatibility

27 February 2017

- Updated Debian to version 8.7

22 February 2017

- Added PHPUnit
- Added tests for the Vagrantbox
- Added Travis CI builds

21 February 2017

- Added nodejs

17 February 2017

- Improved the PHP provisioning

16 February 2017

- Changed PHP repository from dotdeb.org to sury.org
- Updated PHP to version 7.1

14 February 2017

- Initial Commit
- Debian 8.6, Nginx, PHP 7.0, MySQL
