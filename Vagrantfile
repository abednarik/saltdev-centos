# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "salt"

  config.vm.box_check_update = false
  config.vm.synced_folder "saltstack/srv", "/srv"
  config.vm.synced_folder "saltstack/etc", "/etc/salt"
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.name = "salt"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo rpm -iUvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
    sudo yum -y update
    sudo yum -y upgrade
    sudo yum install -y vim tmux git python-devel python-pip git-core virt-what gcc-c++ m2crypto 
    sudo yum clean all
    sudo pip install --upgrade pip
    sudo pip install pyzmq PyYAML pycrypto msgpack-python jinja2 psutil futures
  SHELL
end
