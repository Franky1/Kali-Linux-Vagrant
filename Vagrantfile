# -*- mode: ruby -*-
# vi: set ft=ruby :

# this is maybe an improvement to avoid
# duplicate USB filters on every vagrant up/reload
# but not tested yet:
# require_relative 'betterusbfilter'

Vagrant.configure("2") do |config|
    config.vm.box = "kalilinux/rolling"
    config.vm.box_check_update = true
    config.vm.synced_folder ".", "/vagrant"

    # disable guest addition plugin update
    if Vagrant.has_plugin?("vagrant-vbguest") then
        config.vbguest.auto_update = false
    end

    # Create a forwarded port
    # config.vm.network "forwarded_port", guest: 80, host: 8080

    # Create a private network. In VirtualBox, this is a Host-Only network
    # config.vm.network "private_network", ip: "192.168.33.10"

    # VirtualBox specific settings
    config.vm.provider "virtualbox" do |vb|
        # user friendly name of the VM in VirtualBox
        vb.name = "Kali Linux"

        # Hide/show the VirtualBox GUI when booting the machine
        vb.gui = true

        # Customize the amount of memory to 4GB or 8GB on the VM:
        # vb.memory = 4096
        vb.memory = 8192
        # Customize the number of cpus to 2 on the VM:
        vb.cpus = 2

        # use max 80% of the cpu
        # removed the cpuexecutioncap, because VirtualBox complains about iz
        # vb.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
        # enable USB
        # my Wifi Adapter uses USB 3.0 therefore enable USB 3.0 here:
        # vb.customize ["modifyvm", :id, "--usb", "on"]       # enable USB 1.x
        # vb.customize ["modifyvm", :id, "--usbehci", "on"]   # enable USB 2.x
        vb.customize ["modifyvm", :id, "--usbxhci", "on"]   # enable USB 3.x
        # enable usbfilter
        # did not use usbfilter here due to problem with duplicated usb devices:
        # vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', '802.11n NIC', '--vendorid', '0x0bda', '--productid', '0x8812']
    end

    # Provision the machine with a shell script
    # config.vm.provision "shell", inline: <<-SHELL
    #     apt-get update
    #     apt-get install -y something
    # SHELL

    # Provision the machine with Ansible
    config.vm.provision "ansible_local" do |ansible|
        ansible.install = true
        # set compatibility mode to ansible 2.0 to mute warnings:
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "playbook.yml"
        # ansible.verbose = true
        ansible.verbose = false
        ansible.limit = "all"
        ansible.become = true
        ansible.raw_arguments = [ '-e', 'ansible_python_interpreter=/usr/bin/python' ]
        ansible.config_file = "ansible.cfg"
        # ansible.become_user = "kali"
        # ansible.galaxy_role_file = "requirements.yml"
        # ansible.galaxy_roles_path = "roles"
        # ansible.extra_vars = { }
        # ansible.inventory_path = "inventory"
    end
vagrant_synced_folder_default_type = ""
end
