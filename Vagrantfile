# -*- mode: ruby -*-
# vi: set ft=ruby :

USER_CONFIG = File.join(File.dirname(__FILE__), "config.user.rb")
HAS_USER_CONFIG = File.exist?(USER_CONFIG)
if HAS_USER_CONFIG
    require USER_CONFIG
end


Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "8192"
    vb.cpus = '2'
  end

  config.vm.network "private_network", type: "dhcp"
  config.vm.synced_folder "~/src", "/vagrant", type: "nfs", nfs_udp: false

  config.vm.provision "shell", inline: <<-'SCRIPT'
    apt-get -y update
    apt-get -y dist-upgrade
    apt-get -y install nfs-common
  SCRIPT

  config.vm.provision "shell", inline: <<-'SCRIPT'
    apt-get -y install build-essential tar curl zip unzip
    apt-get -y install clang-10 llvm-10-dev libclang-10-dev
    apt-get -y install cmake
    apt-get -y install python3 python3-pip
    apt-get -y install openssl libssl-dev
    apt-get -y install doxygen graphviz
    apt-get -y install cppcheck
  SCRIPT

  config.vm.provision "shell", privileged: false, inline: <<-'SCRIPT'
    git clone https://github.com/microsoft/vcpkg
    ./vcpkg/bootstrap-vcpkg.sh
  SCRIPT

  if HAS_USER_CONFIG
    userConfig(config)
  end

  config.vm.provision "shell", inline: <<-'SCRIPT'
    apt-get -y clean
  SCRIPT

end

