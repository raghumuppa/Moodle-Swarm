# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

 NodeCount = 4

 (1..NodeCount).each do |i|
    config.vm.define "test#{i}" do |demo|
      demo.vm.box = "centos/7"
      demo.vm.hostname = "temp#{i}"
      demo.vm.network "private_network", ip: "10.10.10.1#{i}"
      demo.vm.network "forwarded_port", guest: "80", host: "8#{i}",
      	auto_correct: true
      demo.vm.network "forwarded_port", guest: "8080", host: "808#{i}",
      	auto_correct: true
      demo.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 1024
      end
      demo.vm.provision "shell", inline: <<-SHELL
        yum update
	yum install wget vim
	yum install centos-release-gluster -y
	yum install epel-release -y
	yum install glusterfs-server -y
	systemctl enable glusterd
	systemctl start glusterd
        echo "[TASK 11] Enable ssh password authentication"
        sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
        systemctl reload sshd
        echo "[TASK 12] Set root password"
        echo "test" | passwd --stdin root >/dev/null 2>&1
      SHELL
     end
   end
end
