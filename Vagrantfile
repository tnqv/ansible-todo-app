# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "geerlingguy/centos7"
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true

  # General VirtualBox VM configuration.
  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
    v.linked_clone = true
    # Make VM can connect to Internet
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Service running GO app.
  config.vm.define "service" do |www1|
    www1.vm.hostname = "service.test"
    www1.vm.network :private_network, ip: "192.168.2.2"

    www1.vm.provision "shell",
      inline: "sudo yum update -y"

    www1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 256]
    end
  end

  # MySQL db.
  config.vm.define "db" do |db1|
    db1.vm.hostname = "db.test"
    db1.vm.network :private_network, ip: "192.168.2.5"
  end
end