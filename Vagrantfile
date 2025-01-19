# -*- mode: ruby -*-
# vi: set ft=ruby :
# Before executing this Vagrant File, type the command below in your Linux Terminal
# export VAGRANT_EXPERIMENTAL="disks"

Vagrant.configure("2") do |config|
    config.vm.box = "generic/debian12"
    config.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "1024"
    end

    config.vm.define "p01_Avelange" do |vm|
        vm.vm.hostname = "p01-Avelange"
        vm.vm.network "private_network", ip: "192.168.57.10"

        vm.vm.provider "virtualbox" do |vb|
          vb.name = "p01_Avelange"
        end

        (1..3).each do |i|
          vm.vm.disk :disk, size: "10GB", name: "disk-#{i}"
        end

        vm.vm.provision "ansible" do |ansible|
          ansible.playbook = "playbook.yml"
        end
    end
end
