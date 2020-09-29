# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "8192"
    vb.cpus = '2'
  end

  config.vm.provision "shell", inline: <<-'SCRIPT'
    apt-get -y update
    apt-get -y dist-upgrade
  SCRIPT

  config.vm.provision "shell", inline: <<-'SCRIPT'
    apt-get -y install build-essential tar curl zip unzip
    apt-get -y install clang
    apt-get -y install cmake
    apt-get -y install python3 python3-pip
    apt-get -y install openssl libssl-dev
  SCRIPT

  config.vm.provision "shell", privileged: false, inline: <<-'SCRIPT'
    git clone https://github.com/microsoft/vcpkg
    ./vcpkg/bootstrap-vcpkg.sh
  SCRIPT

  config.vm.provision "shell", inline: <<-'SCRIPT'
    apt-get -y clean
  SCRIPT

end

