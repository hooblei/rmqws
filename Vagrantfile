# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/debian-8.6"
  config.vm.box_check_update = false
  config.vm.network "public_network"
  config.vm.synced_folder ".", "/home/vagrant/rmqws"

  config.vm.define "rmqws" do |rmqs|
  end

  config.vm.provider "virtualbox" do |vb|
    vb.name = "rmqws"
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y curl
    apt-get install -y php5-common php5-cli php5-dev php5-json php-pear php5-readline php-pear
    apt-get install -y librabbitmq1 librabbitmq-dev
    apt-get install -y tmux
    apt-get install -y vim vim-common
    #pecl install --force amqp-1.7.1
    #echo "extension=amqp.so" > /etc/php5/cli/conf.d/30-amqp.ini
  SHELL
end
