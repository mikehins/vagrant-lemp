# Vagrant LEMP stack

[![Tested on Vagrant 2.2.x](https://img.shields.io/badge/Vagrant-2.2.x-0E7EFF.svg)](https://www.vagrantup.com/)
[![Tested on VirtualBox 6.0.x](https://img.shields.io/badge/VirtualBox-6.0.x-183861.svg)](https://www.vagrantup.com/)
[![Version 2.0](https://img.shields.io/badge/Version-2.0-success.svg)](#)

This script will automate the setup of a PHP developement box.

## Includes

- Ubuntu 18.04 (LTS)
- Nginx 1.14+
- PHP 7.2+
- MariaDB 10.1+ (~MySQL 5.7+)
- Redis 5.0+
- Memcached
- Composer

## Requirements

- MacOS (Windows and Linux might work but aren't covered here)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](http://www.vagrantup.com/)

## Install

You clone this repo in a folder called `Vagrant` in your home directory. 

```bash
git clone https://github.com/milhouse1337/vagrant-lemp.git ~/Vagrant
cd ~/Vagrant
```

You need to remove the `.git` folder, it will cause conflicts with your own Git repos later.

```bash
rm -rf .git
```

Open the following file:

> ~/Vagrant/_install/bootstrap.sh

- Update the MySQL root password around lines 38 and 39.
- Validate if the rest of the script feels right for you and update as needed.

When everything seems fine you launch it. 🚀

```bash
vagrant up
```

You will have to wait a few seconds (minutes) ☕️ for the script to complete. When everything is done you have a complete [LEMP](https://lemp.io/) setup to play with. 🤓

## Test your setup

Create the following folders and PHP file: 

```bash
mkdir -p ~/Vagrant/test.127.0.0.1.xip.io/public
echo "<?php phpinfo(); ?>" > ~/Vagrant/test.127.0.0.1.xip.io/public/index.php
```

Open the link on your browser:

> [http://test.127.0.0.1.xip.io:8080](http://test.127.0.0.1.xip.io:8080)

You should see a `phpinfo()` output. 👍

> Note: If you want Vagrant to listen on port 80 (or 443 for TLS) you might have to forward the ports with [pfctl](https://man.openbsd.org/pfctl) (the built-in MacOS firewall). More information [on this Stack Overflow](https://stackoverflow.com/questions/17437137/vagrant-wont-forward-only-port-80) if you want to know why and how to fix it.

### How does it work ? I didn't changed my hosts file or anything and it works. 🤔

- The DNS part is handled by [xip.io](http://xip.io) which is a free service that is ment exactly for this purpose. It resolves any subdomain to the IP address you specify.
- We use a wildcard for the default Nginx vhost so the document root is `/var/www/{$host}/public` for the VM and `~/Vagrant/{$host}/public` on your local machine.

## Vagrant cheat sheet

```bash
vagrant up # Boot. (install if not already provisioned)
vagrant ssh # Login as user "vagrant".
vagrant reload # Reboot.
vagrant halt # Poweroff.
vagrant destroy # Delete.
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
