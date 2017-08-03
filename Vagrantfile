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

    config.vm.network "forwarded_port", guest: 4748, host: 4748

    config.vm.provider "virtualbox" do |v|
        second_disk = '.vagrant/machines/default/virtualbox/disk2.vdi'

        # Create and attach disk
        unless File.exist?(second_disk)
            v.customize ['createhd', '--filename', second_disk, '--format', 'VDI', '--size', 1 * 1024]
        end
        v.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', second_disk]
    end

    config.vm.provision "shell", inline: $pre_provision

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/playbook.yml"
    end
end
