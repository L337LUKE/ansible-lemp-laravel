# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # The box we want to pull in, in this case ubuntu 14.04
  config.vm.box = "ubuntu/trusty64"

  # Forward ports so we can test nginx and that frontends load
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  # Assign a private ip address for us to connect to
  config.vm.network "private_network", ip: "192.168.50.5"
  
  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'dependencies.yml'
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'provision.yml'
  end
end
