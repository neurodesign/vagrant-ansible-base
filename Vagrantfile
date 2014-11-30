# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

unless Vagrant.has_plugin?("vagrant-hostmanager")
  raise "vagrant-hostmanager plugin is missing. Install with 'vagrant plugin install vagrant-hostmanager'"
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.10"
  
  config.vm.hostname = "myproject"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.aliases = %w(myproject)

  config.vm.synced_folder ".", "/var/www/myproject"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/playbook.yml"
    ansible.sudo = true
  end

  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 1
  end
end
