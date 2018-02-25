# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "centos/7"

    config.vm.define 'tower-node1' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.201'
        vmconfig.vm.hostname = 'tower-node1'
    end

    config.vm.define 'tower-node2' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.202'
        vmconfig.vm.hostname = 'tower-node2'
    end

    config.vm.define 'tower-node3' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.203'
        vmconfig.vm.hostname = 'tower-node3'
    end

    config.vm.define 'tower-isolated-node1' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.204'
        vmconfig.vm.hostname = 'tower-isolated-node1'
    end

    config.vm.define 'tower-db-pri' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.210'
        vmconfig.vm.hostname = 'tower-db-pri'
    end

    config.vm.define 'tower-db-sec' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.211'
        vmconfig.vm.hostname = 'tower-db-sec'
    end

    config.vm.define 'tower-haproxy-pri' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.221'
        vmconfig.vm.hostname = 'tower-haproxy-pri'
    end

    config.vm.define 'tower-haproxy-sec' do |vmconfig|
        vmconfig.vm.network :private_network, ip: '192.168.122.222'
        vmconfig.vm.hostname = 'tower-haproxy-pri'
    end

   config.vm.provider "libvirt" do |kvm|
     kvm.memory = "4096"
     kvm.cpus = "2"
   end

   config.vm.provision "shell", inline: <<-SHELL
     cp -p /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
     sed 's/PasswordAuthentication no/PasswordAuthentication yes/g;s/#PermitRootLogin yes/PermitRootLogin without-password/g' /etc/ssh/sshd_config > /etc/ssh/sshd_config.new
     mv /etc/ssh/sshd_config.new /etc/ssh/sshd_config
     ssh-keygen -f id_rsa -t rsa -N ''
     mkdir /root/.ssh
     service sshd restart
     echo 192.168.122.201 tower-node1 >> /etc/hosts
     echo 192.168.122.202 tower-node2 >> /etc/hosts
     echo 192.168.122.203 tower-node3 >> /etc/hosts
<<<<<<< HEAD
     echo 192.168.122.210 tower-db-pri >> /etc/hosts
     echo 192.168.122.211 tower-db-sec >> /etc/hosts
     echo 192.168.122.221 tower-haproxy-pri >> /etc/hosts
     echo 192.168.122.222 tower-haproxy-sec >> /etc/hosts
     echo 192.168.122.204 tower-isolated-node1
=======
     echo 192.168.122.210 tower-db >> /etc/hosts
     echo 192.168.122.220 tower-haproxy >> /etc/hosts
     echo 192.168.122.204 tower-isolated-node1 >> /etc/hosts
>>>>>>> 7d82566790d7d8c87fea462d7b42f5db95f026ba
   SHELL
end
