# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "master" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "master"
    node.vm.network :private_network, ip: "192.168.33.11"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2210
  end
  config.vm.define "slave" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "slave"
    node.vm.network :private_network, ip: "192.168.33.21"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2220
  end
  config.vm.define "web" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "web"
    node.vm.network :private_network, ip: "192.168.33.31"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2230
  end
  config.vm.define "db" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "db"
    node.vm.network :private_network, ip: "192.168.33.32"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2240
  end
end
