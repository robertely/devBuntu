# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.hostname = "devBuntu"
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "public_network"
  config.vm.synced_folder "Projects", "/home/vagrant/Projects",
    create: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = "2"
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Setup
    export DEBIAN_FRONTEND="noninteractive"
    export TERM="xterm"
    # Start up
    apt-get update
    # Essential tools
    apt-get install -y curl vim-nox git make build-essential
    # Python tools
    apt-get install -y python-dev python-pip
    pip install --upgrade pip
    pip install pep8
    # Go tools
    apt-get install -y golang
    # Terminal helpers
    apt-get install -y byobu tree htop atop jq cabal
    byobu-enable
    # Zed FS - perhaps i'll setup this up at some point...
    # apt-get install -y zfsutils-linux
    # Install docker
    apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
    apt-get update
    apt-get install -y docker-engine bridge-utils
    sudo usermod -aG docker vagrant
    # Seed docker
    docker pull ubuntu & docker pull ubuntu:14.04 & docker pull centos:centos7 & docker pull centos:centos6
    wait
    sudo apt-get clean
    echo "--------------------------"
    echo "- Setup complete.        -"
    echo "--------------------------"
  SHELL
end
