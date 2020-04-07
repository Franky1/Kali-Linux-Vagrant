# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "kalilinux/rolling"
    config.vm.box_check_update = true

    # check if guest addition needs update
    if Vagrant.has_plugin?("vagrant-vbguest") then
        config.vbguest.auto_update = false
    end

    # Create a forwarded port
    # config.vm.network "forwarded_port", guest: 80, host: 8080

    # Create a private network. In VirtualBox, this is a Host-Only network
    # config.vm.network "private_network", ip: "192.168.33.10"

    # VirtualBox specific settings
    config.vm.provider "virtualbox" do |vb|
        # friendly name of the virtual machine
        vb.name = "Kali Linux"

        # Hide/show the VirtualBox GUI when booting the machine
        vb.gui = true

        # Customize the amount of memory 4GB on the VM:
        vb.memory = "4096"

        # use max of 80% cpu
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
        # enable USB
        vb.customize ["modifyvm", :id, "--usb", "on"]
    end

    # Provision the machine with a shell script
    # config.vm.provision "shell", inline: <<-SHELL
    #     apt-get update
    #     apt-get install -y ansible
    # SHELL

    config.vm.provision "ansible_local" do |ansible|
        # set compatibility mode to 2.0 to disable warnings:
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "playbook.yml"
        # ansible.verbose = true
        ansible.verbose = false
        ansible.install = true
        ansible.limit = "all"
        ansible.become = true
        ansible.raw_arguments = [ '-e', 'ansible_python_interpreter=/usr/bin/python' ]
        # ansible.become_user = "kali"
        # ansible.config_file = "ansible.cfg"
        # ansible.galaxy_role_file = "requirements.yml"
        # ansible.galaxy_roles_path = "roles"
        # ansible.extra_vars = { }
        # ansible.inventory_path = "inventory"
    end
vagrant_synced_folder_default_type = ""
end
