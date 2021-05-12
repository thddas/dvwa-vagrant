# DVWA Vagrant

This project uses [Vagrant](https://www.vagrantup.com/) to automate the installation and configuration of [Damn Vulnerable Web App (DVWA)](https://dvwa.co.uk/) application in a Linux VM.

## Quick Start

### Requirements

The Package dependencies: `Vagrant` and `Virtualbox`.

### Instructions

With Vagrant and Virtualbox installed, just run the following commands to start the application install/config process:

```bash
$ git clone https://github.com/thddas/dvwa-vagrant.git
$ cd dvwa-vagrant
$ vagrant up
```

The `vagrant up`command will create a Linux VM in Virtualbox, install the application's dependencies (like Apache, PHP and MySQL) and install DVWA. Finally, it will configure the web application and its database.

Done! The web application is up! Access this address in your browser: `http://192.168.50.50/setup.php` to open the application and click in `Create / Reset Database`. After that, you will redirected to login page (username/password: `admin` / `password`). Good Studies!

## Important

This Vagrant create a `Host-only` network adapter, therefore, the web application can't be accessed by the local network, only by your host.

### Warning!

Read this [warning](https://github.com/digininja/DVWA#warning) for important care.

When not using the application, turn it off:

```bash
$ vagrant halt
```

To remove the VM completely:

```bash
$ vagrant destroy
```

## Help

- [DVWA Page](https://dvwa.co.uk/)
- [Github project](https://github.com/digininja/DVWA#warning)
- [Vagrant Documentation](https://www.vagrantup.com/docs/index)
