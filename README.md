
# RMQWS

A RabbitMQ workshop and playground.

## Setup

If not already installed - install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
and [Varagnt](https://www.vagrantup.com/docs/installation/).

With VirtualBox and Varagnt installed, run `vagrant up` within the current
directory, to fetch and initialize the virtual mashine.

Note: The VM will use a bridged network interface in order to communicate with
the remote RabbitMQ server so vagrant may ask you for a network interface to
use.

Now you should be able to access your VM via `vagrant ssh`, run commands etc.

### Manual Steps

I was not able to install the PHP `amqp` extension within the VM provision - so
you have to manually execute the following steps.

Login into the rmqws VM via `vagrant ssh`

    vagrant@debian-8:~$ sudo pecl install --force amqp-1.7.1
    downloading amqp-1.7.1.tgz ...
    Starting to download amqp-1.7.1.tgz (79,905 bytes)
    ..................done: 79,905 bytes
    18 source files, building
    running: phpize
    Configuring for:
    PHP Api Version:         20131106
    Zend Module Api No:      20131226
    Zend Extension Api No:   220131226
    Set the path to librabbitmq install prefix [autodetect] : # OMGWTF! just press enter
    ...

After installing the pecl extension, you have to enable it manually. Sadly a
`sudo echo "extension=amqp.so" >> /etc/php5/cli/conf.d/30-amqp.ini` doesn't
work and you have to create and edit the file by your self ...

    vagrant@debian-8:~$ sudo vim/nano/whatever /etc/php/cli/conf.d/99-amqp.ini

After that, a check for the `amqp` extension should succeed

    vagrant@debian-8:~$ php -m | grep amqp
    amqp

The current directory is shared in your VM home directory as `rmqws`.
Everything you add/change/remove within the current directory is automatically
synced with `/home/vagrant/rmqws` and vice versa.


## Links

* [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html)
* [php-amqp Repository Docs and Examples](https://github.com/pdezwart/php-amqp)

