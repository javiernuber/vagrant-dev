# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# Use config.yml for basic VM configuration.
require 'yaml'
if !File.exist?('./config.yml')
  raise 'Configuration file not found! Please copy example.config.yml to config.yml and try again.'
end
vconfig = YAML::load_file("./config.yml")

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = "ubuntu/trusty64"
	config.vm.network "forwarded_port", guest: 80, host: 8880
	config.vm.network "private_network", ip: "192.168.33.10"
	config.vm.synced_folder ".", "/vagrant", type: "nfs"
	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "ansible/provision.yml"
		ansible.extra_vars = { 
			#symfony2_project_root: '/vagrant',
    		apache_user: 'vagrant',
    		apache_group: 'vagrant'
		}
	end
	config.vm.provider "virtualbox" do |v|
		v.memory = 2048
  		v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
	end
end