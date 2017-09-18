# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
# TCP_PORTS_LIST={
#   "50070" => 50070, 
#   "50030" => 50030, 
#   "50060" => 50060, 
# }

Vagrant.require_version ">= 1.4.3"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  numNodes = 1
  r = numNodes..1
  (r.first).downto(r.last).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "ubuntu/Xenial64"
      # node.vm.box = "debian/stretch64"
      # node.vm.box = "geerlingguy/ubuntu1604"
      # node.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.1/centos65-x86_64-20131205.box"
      node.vm.provider "virtualbox" do |v|
        v.name = "node#{i}"
        v.customize ["modifyvm", :id, "--memory", "1024"]
      end
      if i < 10
        node.vm.network :private_network, ip: "10.211.55.10#{i}"
      else
        node.vm.network :private_network, ip: "10.211.55.1#{i}"
      end
      node.vm.hostname = "node#{i}"
      node.vm.provision :ansible do |ansible|
        # ansible.verbose = 'vvvv'
        ansible.playbook = "playbook.yml"
        # ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
      end      
      
    end
  end
end
