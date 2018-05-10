Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "master" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "master"
    node.vm.network :private_network, ip: "192.168.33.200"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2210
    node.vm.provision "shell", inline: $script1
  end
  config.vm.define "slave" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "slave"
    node.vm.network :private_network, ip: "192.168.33.201"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2220
    node.vm.provision "shell", inline: $script2
  end
  config.vm.define "web" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "web"
    node.vm.network :private_network, ip: "192.168.33.210"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2230
    node.vm.provision "shell", inline: $script3
  end
  config.vm.define "db" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "db"
    node.vm.network :private_network, ip: "192.168.33.211"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2240
    node.vm.provision "shell", inline: $script3
  end
end

$script1 = <<END
sudo localectl set-locale LANG=en_US.utf8
export LANG=en_US.utf8
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
END

$script2 = <<END
sudo localectl set-locale LANG=en_US.utf8
export LANG=en_US.utf8
sudo timedatectl set-timezone Asia/Tokyo
sudo sed -i '2a nameserver 8.8.8.8' /etc/resolv.conf
sudo yum install -y java-1.8.0-openjdk  java-1.8.0-openjdk-devel
sudo yum install -y git
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
systemctl restart sshd

END

$script3 = <<END
sudo localectl set-locale LANG=en_US.utf8
export LANG=en_US.utf8
sudo timedatectl set-timezone Asia/Tokyo
sudo sed -i '2a nameserver 8.8.8.8' /etc/resolv.conf
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
systemctl restart sshd
END