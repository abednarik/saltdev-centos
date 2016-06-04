# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.define :salt do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "salt"

    node.vm.synced_folder "saltstack/srv", "/srv"
    node.vm.synced_folder "saltstack/etc", "/etc/salt"
    node.vm.synced_folder "~/work/code/salt/", "/root/salt"

    node.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "2048"
      vb.name = "saltdev-centos"
    end

    node.vm.provision "shell", inline: <<-SHELL
      sudo yum -y update
      yum install -y epel-release
      sudo yum install -y vim tmux git python-devel python-pip git-core virt-what gcc-c++ m2crypto
      sudo yum clean all
      sudo pip install --upgrade pip
      sudo pip install pyzmq PyYAML pycrypto msgpack-python jinja2 psutil futures
    SHELL

    # Setup Docker to run salt tests inside a container
    node.vm.provision "shell", inline: <<-SHELL
      sudo docker 2> /dev/null
      if [ $? -eq 0 ]
        then
          echo "Docker exists, skipping..."
        else
          sudo curl -sSL https://get.docker.com/ | sh
      fi
      sudo usermod -aG docker vagrant
    SHELL
  end
end
