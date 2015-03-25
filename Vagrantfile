# -*- mode: ruby -*-
# vi: set ft=ruby :
##################################################
# By javiernuber
##################################################

VAGRANTFILE_API_VERSION = "2"

# Use config.yml for basic VM configuration.
require 'yaml'
if !File.exist?('./config.yml')
  raise 'Configuration file not found! Please copy example.config.yml to config.yml and try again.'
end
vconfig = YAML::load_file("./config.yml")

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.hostname = vconfig['vagrant_hostname']

	config.vm.box = "ubuntu/trusty64"
	config.vm.network "forwarded_port", guest: 80, host: 8880
	config.vm.network :private_network, ip: vconfig['vagrant_ip']
	config.vm.synced_folder ".", "/vagrant", type: "nfs"
	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "ansible/provision.yml"
	end
	config.vm.provider "virtualbox" do |v|
		v.memory = 2048
		v.cpus = 2
  		v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
	end
end