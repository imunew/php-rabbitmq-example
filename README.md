# RabbitMQ PHP example

## Setup
### Install VirtualBox
https://www.virtualbox.org/wiki/Downloads

### Install Vagrant
https://www.vagrantup.com/downloads.html

```bash
$ vagrant -v
Vagrant 1.5.4
```

### Install Ansible
http://docs.ansible.com/ansible/intro_installation.html

```bash
$ ansible --version
ansible 2.0.0.2
```

### Download example

```bash
$ mkdir /path/to/example
$ cd /path/to/example
$ git clone git@github.com:imunew/php-rabbitmq-example.git .
```

### Provisioning (Automatically）

```bash
$ cd /path/to/example
$ vagrant up
```

## Run example

### Receiving

1. Start console (for receiving)

1. SSH login to virtual machine

    ```bash
    $ vagrant ssh
    ```

1. Run receiver script

    ```bash
    [vagrant@vagrant-centos65 ~]$ cd /apps
    [vagrant@vagrant-centos65 apps]$ php bin/receiver.php
     [*] Waiting for messages. To exit press CTRL+C
    
    ```

### Sending

1. Start console (for Sending)

1. SSH login to virtual machine

    ```bash
    $ vagrant ssh
    ```

1. Run sender script

    ```bash
    [vagrant@vagrant-centos65 ~]$ cd /apps
    [vagrant@vagrant-centos65 apps]$ php bin/sender.php
     [x] Sent 'Hello World!'
    ```

1. Confirm console for receiving

    ```bash
    [vagrant@vagrant-centos65 ~]$ cd /apps
    [vagrant@vagrant-centos65 apps]$ php bin/receiver.php
     [*] Waiting for messages. To exit press CTRL+C
     [x] Received Hello World!
    
    ```
