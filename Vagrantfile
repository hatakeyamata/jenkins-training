# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "master" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "master"
    node.vm.network :private_network, ip: "192.168.33.11"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2210
  config.vm.provision "shell", inline: <<-SHELL
    sudo timedatectl set-timezone Asia/Tokyo
    sudo sed -i '2a nameserver 8.8.8.8' /etc/resolv.conf
    sudo yum install -y java-1.8.0-openjdk  java-1.8.0-openjdk-devel
    sudo yum install -y git initscripts wget
    sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
    sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
    sudo yum install -y jenkins
    sudo sed -i 's/gpgcheck=0/gpgcheck=1/' /etc/yum.repos.d/jenkins.repo
    sudo sed -i 's%jenkins:/bin/false%jenkins:/bin/bash%' /etc/passwd
    sudo chkconfig jenkins on
    sudo systemctl start jenkins
  SHELL
  end
  config.vm.define "slave" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "slave"
    node.vm.network :private_network, ip: "192.168.33.21"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2220
  config.vm.provision "shell", inline: <<-SHELL
    sudo timedatectl set-timezone Asia/Tokyo
    sudo sed -i '2a nameserver 8.8.8.8' /etc/resolv.conf
    sudo yum install -y java-1.8.0-openjdk  java-1.8.0-openjdk-devel
    sudo yum install -y git
  SHELL
    
    
  end
  config.vm.define "web" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "web"
    node.vm.network :private_network, ip: "192.168.33.31"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2230
  config.vm.provision "shell", inline: <<-SHELL
    sudo timedatectl set-timezone Asia/Tokyo
    sudo sed -i '2a nameserver 8.8.8.8' /etc/resolv.conf
  SHELL
  end
  config.vm.define "db" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "db"
    node.vm.network :private_network, ip: "192.168.33.32"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2240
  end
end