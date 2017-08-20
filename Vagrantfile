# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_IMAGE = "centos/7"
NODE_COUNT = 2
MACHINES = ['master','node1', 'node2']
IP_ADDRESS_START = "192.168.56.120"

Vagrant.configure("2") do |config|
	#-------------------------------------
	# MASTER
  config.vm.define "#{MACHINES[0]}" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "#{MACHINES[0]}.local"

    subconfig.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end

    subconfig.vm.network :private_network, ip: "#{IP_ADDRESS_START}"
    subconfig.vm.network "forwarded_port", guest: 80, host: 8080
    subconfig.vm.network "forwarded_port", guest: 443, host: 8443
    subconfig.vm.network "forwarded_port", guest: 3000, host: 8300
    subconfig.vm.synced_folder "./files", "/root", type: "nfs"
    subconfig.vm.synced_folder "./ansible", "/etc/ansible", type: "nfs"

    subconfig.vm.provision "shell" do |s|
      s.inline = <<-SHELL
        yum update -y
	      yum install -y epel-release ansible git
      SHELL
    end
  end
  	# -----------------------------------------
	# NODES
  (1..NODE_COUNT).each do |i|
    config.vm.define "#{MACHINES[i]}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "#{MACHINES[i]}"
      subconfig.vm.network :private_network, ip: "192.168.56.#{i + 120}"
    end

  end

  # Install avahi on all machines & copy ssh key for quick logins
  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      yum update -y
      yum install -y epel-release
      yum install -y avahi nss-mdns
      echo "<==== Copying KEYS ====>"
      mkdir -p /root/.ssh
      touch /root/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
  end
end
