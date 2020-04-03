# -*- mode: ruby -*-
# vi: set ft=ruby :

# Set host locale which is propagated to guest
ENV["LC_ALL"] = "en_US.UTF-8"

# Load local developer settings
require 'yaml'
devconfig = YAML.load_file('developer.yml')

Vagrant.configure("2") do |config|

    # Base box definition, currently using
    #  Official Ubuntu 18.04 LTS (Bionic Beaver) Daily Build
    config.vm.box = "ubuntu/bionic64"

    # Disable automatic box update checking
    config.vm.box_check_update = false

    # Make sure required plugins are installed
    required_plugins = %w( vagrant-vbguest vagrant-disksize)
    _retry = false
    required_plugins.each do |plugin|
        unless Vagrant.has_plugin? plugin
            system "vagrant plugin install #{plugin}"
            _retry=true
        end
    end

    if (_retry)
        exec "vagrant " + ARGV.join(' ')
    end


    # configure virtual machine for running eternaltwin
    config.vm.define "eternaltwin", primary: true do |eternaltwin|

	eternaltwin.vm.hostname = "eternaltwin"

	# Configure private network with static IP address
        eternaltwin.vm.network "private_network", ip: devconfig['portal']['ip']
        #eternaltwin.vm.network "forwarded_port", guest: 80, host: 8080

        # Set higher virtual drive size to make room for whole eternaltwin stack
	eternaltwin.disksize.size = "30GB"

        # Virtualbox machine configuration
        eternaltwin.vm.provider "virtualbox" do |vb|
            vb.name = "eternaltwin"
            # Run in headless mode
            vb.gui = false

            # Customize the amount of memory and CPUs assigned:
            vb.memory = devconfig['system']['memory']
            vb.cpus = devconfig['system']['cpus']

	    # Set chipset to ich9
            vb.customize ["modifyvm", :id, "--chipset", "ich9"]

        end

	# Provision the box using ansible local (no Ansible installation needed on host)
	eternaltwin.vm.provision "ansible_local" do |ansible|
            ansible.version = "latest"
            ansible.compatibility_mode = "2.0"
            ansible.become = true
            ansible.verbose = false
            ansible.limit = "all"
	    ansible.inventory_path = "ansible/inventory/hosts"
            ansible.playbook = "ansible/main.yml"
            ansible.extra_vars = "developer.yml"
        end

    end

    config.vm.post_up_message = <<-MESSAGE

    Your eternal-twin development environment is configured!

    Login to the eternal-twin VM using command: 
         vagrant ssh

    MESSAGE

end
