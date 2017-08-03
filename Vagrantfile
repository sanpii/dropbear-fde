# -*- mode: ruby -*-
# vi: set ft=ruby :

$pre_provision = <<SCRIPT
export DEBIAN_FRONTEND=noninteractive
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install python
SCRIPT

Vagrant.configure("2") do |config|
    config.vm.box = "debian/stretch64"

    config.vm.provision "shell", inline: $pre_provision
end
