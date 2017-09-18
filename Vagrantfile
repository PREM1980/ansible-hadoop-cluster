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
# Vagrant.configure(2) do |config|
#   # The most common configuration options are documented and commented below.
#   # For a complete reference, please see the online documentation at
#   # https://docs.vagrantup.com.

#   # Every Vagrant development environment requires a box. You can search for
#   # boxes at https://atlas.hashicorp.com/search.
#   config.vm.box = "ubuntu/trusty64"
#   TCP_PORTS_LIST.each do |guest, host|
#     config.vm.network "forwarded_port", guest: "#{guest}", host: "#{host}", protocol: "tcp"
#   end

#   # Disable automatic box update checking. If you disable this, then
#   # boxes will only be checked for updates when the user runs
#   # `vagrant box outdated`. This is not recommended.
#   # config.vm.box_check_update = false

#   # Create a forwarded port mapping which allows access to a specific port
#   # within the machine from a port on the host machine. In the example below,
#   # accessing "localhost:8080" will access port 80 on the guest machine.
#   # config.vm.network "forwarded_port", guest: 80, host: 8080
  
#   # Create a private network, which allows host-only access to the machine
#   # using a specific IP.
#   # config.vm.network "private_network", ip: "192.168.33.10"

#   # Create a public network, which generally matched to bridged network.
#   # Bridged networks make the machine appear as another physical device on
#   # your network.
#   # config.vm.network "public_network"

#   # Share an additional folder to the guest VM. The first argument is
#   # the path on the host to the actual folder. The second argument is
#   # the path on the guest to mount the folder. And the optional third
#   # argument is a set of non-required options.
#   # config.vm.synced_folder "../data", "/vagrant_data"

#   # Provider-specific configuration so you can fine-tune various
#   # backing providers for Vagrant. These expose provider-specific options.
#   # Example for VirtualBox:
#   #
#   config.vm.provider "virtualbox" do |vb|
#     # Display the VirtualBox GUI when booting the machine
#     # vb.gui = true
  
#     # Customize the amount of memory on the VM:
#     vb.memory = "2048"
#   end
  
#   # View the documentation for the provider you are using for more
#   # information on available options.

#   # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
#   # such as FTP and Heroku are also available. See the documentation at
#   # https://docs.vagrantup.com/v2/push/atlas.html for more information.
#   # config.push.define "atlas" do |push|
#   #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
#   # end

#   # Enable provisioning with a shell script. Additional provisioners such as
#   # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
#   # documentation for more information about their specific syntax and use.
#   # config.vm.provision "shell", inline: <<-SHELL
#   #   sudo apt-get update
#   #   sudo apt-get install -y apache2
#   # SHELL
#   config.vm.provision :ansible do |ansible|
#     ansible.playbook = "playbook.yml"
#   end
#   config.vm.provider :virtualbox do |vb|
#         vb.name = "foohost"
#     end
  
# end


Vagrant.require_version ">= 1.4.3"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  numNodes = 1
  r = numNodes..1
  (r.first).downto(r.last).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "ubuntu/Xenial64"
      node.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.1/centos65-x86_64-20131205.box"
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
      end
      # node.vm.provision "shell", path: "scripts/setup-centos.sh"
      # node.vm.provision "shell" do |s|
      #   s.path = "scripts/setup-centos-hosts.sh"
      #   s.args = "-t #{numNodes}"
      # end
      # if i == 2
      #   node.vm.provision "shell" do |s|
      #     s.path = "scripts/setup-centos-ssh.sh"
      #     s.args = "-s 3 -t #{numNodes}"
      #   end
      # end
      # if i == 1
      #   node.vm.provision "shell" do |s|
      #     s.path = "scripts/setup-centos-ssh.sh"
      #     s.args = "-s 2 -t #{numNodes}"
      #   end
      # end
      # node.vm.provision "shell", path: "scripts/setup-java.sh"
      # node.vm.provision "shell", path: "scripts/setup-hadoop.sh"
      # node.vm.provision "shell" do |s|
      #   s.path = "scripts/setup-hadoop-slaves.sh"
      #   s.args = "-s 3 -t #{numNodes}"
      # end
      # node.vm.provision "shell", path: "scripts/setup-spark.sh"
      # node.vm.provision "shell" do |s|
      #   s.path = "scripts/setup-spark-slaves.sh"
      #   s.args = "-s 3 -t #{numNodes}"
      # end
    end
  end
end
