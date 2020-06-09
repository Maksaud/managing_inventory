# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.define "controlnode" do |controlnode|
    controlnode.vm.hostname = "controlnode"
    controlnode.vm.network "private_network", ip: "192.168.10.100"
  end

  config.vm.define "webserver" do |webserver|
    webserver.vm.hostname = "webserver"
    webserver.vm.network "private_network", ip: "192.168.10.110"
  end
  
  config.vm.define "server" do |server|
    server.vm.hostname = "server"
    server.vm.network "private_network", ip: "192.168.10.120"
  end
end
