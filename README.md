# WordPress development environment with one command (Vagrant+Ansible)

This is a Vagranfile plus Ansible recipe to get a WordPress development server installed with a single command. 

This is the list of software installed:

- Ubuntu precise64 (should work with other Ubuntu versions) 
- Nginx
- Php5-fpm
- Mysql
- WordPress
- Various system software (likve Vim and Git)

PLEASE DON'T USE THIS SOFTWARE ON A PRODUCTION ENVIRONMENT, IT'S A SERIOUS SECURITY RISK!


## Requirements

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads). Tested on 4.3.x, but 4.2.x should also work.
- [Vagrant](http://www.vagrantup.com/downloads.html). Tested on 1.6.5
- [Vagrant hostupdater](https://github.com/cogitatio/vagrant-hostsupdater).
- [Vagrant bindfs](https://github.com/gael-ian/vagrant-bindfs)
- [Ansible](http://docs.ansible.com/intro_installation.html). Tested on 1.5.5.

## Installation

1. First of all install all the required software.

2. Clone this repo and launch Vagrant.

    ```
    git clone https://github.com/nballotta/one-command-wordpress.git
    cd one-command-wordpress
    ```

3. Configure ansible variables in `ansible/group_vars/all` and launch Vagrant
    
    ```
    vagrant up
    ```

4. You will find your WordPress installation under `wordpress.dev/`.

### Synced folders

This Vagrantfile uses bindfs to manage synced folders. This is done to avoid permission problem and to give a developer the ability to write code directly into the WordPress folder. 


### Change local domain name

To change the default local domain name (the one to reach WordPress), simply modify these lines in Vagrantfile.

```
config.hostsupdater.aliases = [
    "wordpress.dev"
]
```

### Todo

- [ ] Add vhost configurations
- [ ] Improve app templates
- [ ] Add WordPress Network toggle
- [ ] Add default plugins installation
- [ ] Add WP-CLI

## License

Copyright (c) 2014 Nicola Ballotta

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE
