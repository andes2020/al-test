# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/bionic64"
    config.ssh.insert_key = false
    config.vm.provider "virtualbox"
    config.vm.synced_folder '.', '/vagrant', disabled: true

    config.vm.provider :virtualbox do |v|
        v.memory = 2048
        v.cpus = 2
        v.linked_clone = true
        v.customize ['modifyvm', :id, '--audio', 'none']
    end

    # Define three Vms with static private ip
    boxes = [
        { :name => "loadbalancer", :ip => "12.168.7.2" },
        { :name => "web1", :ip => "12.168.7.3" },
        { :name => "web2", :ip => "12.168.7.4" }
    ]

    # Configure each of the Vms hostnames
    boxes.each_with_index do |opts, index|
        config.vm.define opts[:name] do |config|
            config.vm.hostname = opts[:name] + ".cluster.test"
            config.vm.network "private_network", ip: opts[:ip]
        end
    end

end

