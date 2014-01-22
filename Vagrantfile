# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :node do |node_config|
    node_config.vm.box = "precise32"
    node_config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    node_config.ssh.forward_agent = true

    node_config.vm.network :forwarded_port, guest: 80, host: 1080
    node_config.vm.network :forwarded_port, guest: 443, host: 1443

    node_config.vm.hostname = "g2k-node"

    node_config.vm.synced_folder "C:\\WebsitesNode", "/home/vagrant/projects", {:mount_options => ['dmode=777', 'fmode=777']}
    node_config.vm.provision :shell, :inline => "echo \"Europe/Rome\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

    node_config.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", "512"]
    end

    node_config.vm.provision :shell, :inline => "sudo apt-get update"
    node_config.vm.provision :shell, :inline => "sudo apt-get install -y python-software-properties python g++ make"
    node_config.vm.provision :shell, :inline => "sudo add-apt-repository -y ppa:chris-lea/node.js"
    node_config.vm.provision :shell, :inline => "sudo apt-get update"
    node_config.vm.provision :shell, :inline => "sudo apt-get install -y nodejs"
    node_config.vm.provision :shell, :inline => "sudo apt-get install -y git-core"
  end
end
