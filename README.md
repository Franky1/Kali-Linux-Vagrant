# Kali Linux Vagrant

Vagrantfile and Ansible Playbook for a fresh and up-to-date Kali Linux VM running in VirtualBox.

## Prerequisites

- VirtualBox installed
- VirtualBox Extensionpack installed
- Vagrant installed

## Usage

Run `vagrant up` for the initial build of the VM. Download of image and update of all packages can take quite a bit of time.

After initial build of the VM, shutdown the VM with `vagrant halt` and restart it again to make sure, every setting is in place.

## Hints

- If you need more packages that are not part of the default kali image, add them in the Ansible playbook.
- I set language and keyboard setting of the VM to `de_DE`. Change this in the playbook if needed.
- Default user of the `kalilinux/rolling` image is `vagrant/vagrant` and not `kali/kali`.
- My host system was a Windows 10 x64

## Issues

- Package update takes a lot of time on first run of playbook.
- I commented out the `cpuexecutioncap` setting in the Vagrantfile, because VirtualBox complains about it.
- I commented out the `usbfilter` setting in the Vagrantfile, because it results in duplicated USB devices, whenever the VM is started with Vagrant.

## Changes

Last changes on 11.04.2020

## Appendix

Just a collection of links, snippest and hints.

### Links

Here some links where  i got ideas and hints from:

- <https://www.kali.org/news/announcing-kali-for-vagrant/>
- <https://pablo.tools/posts/computers/custom-kali-box/>
- <https://github.com/pinpox/kali-i3>
- <https://computingforgeeks.com/how-to-run-kali-linux-rolling-release-with-vagrant-on-virtualbox/>
- <https://www.terasq.com/2019/03/building-kali-with-vagrant-ansible-p1/>
- <https://github.com/M507/Kali-TX>
- <http://mohad.red/Kali-Linux-is-Missing-Many-tools/>

### Vagrant

Please read the comments in the Vagrantfile as well as documentation on `vagrantup.com` for more information on using Vagrant.

To check a `Vagrantfile` before using it:

```shell
vagrant validate
```

First time run:

```shell
vagrant up
```

To ssh into the running VM:

```shell
vagrant ssh
```

To stop and to destroy the running VM:

```shell
vagrant halt
vagrant destroy
```

To reload the Vagrantfile and to re-run the provisioner:

```shell
vagrant reload
vagrant provision
vagrant up --provision
```

### VirtualBox Guest Additions

```shell
vagrant plugin install vagrant-vbguest
```

- <https://www.serverlab.ca/tutorials/virtualization/how-to-auto-upgrade-virtualbox-guest-additions-with-vagrant/>
- <https://shanemcd.org/2018/12/15/installing-virtualbox-guest-additions-in-a-debian-vagrant-box-on-windows-10/>
- <https://subscription.packtpub.com/book/virtualization_and_cloud/9781786464910/1/ch01lvl1sec12/enabling-virtualbox-guest-additions-in-vagrant>

### USB Devices in VirtualBox

- <https://sonnguyen.ws/connect-usb-from-virtual-machine-using-vagrant-and-virtualbox/>
- <https://stackoverflow.com/questions/38956127/usb-device-is-not-visible-inside-vagrant>
- <https://stackoverflow.com/questions/22503168/vagrant-usbfilter-make-the-guest-machine-entered-an-invalid-state>

List all USB devices.

```shell
cd C:\Program Files\Oracle\VirtualBox
VBoxManage.exe list usbhost
Host USB Devices:

UUID:               dab09972-6ca3-43f3-ac28-6242a070d7cb
VendorId:           0x0bda (0BDA)
ProductId:          0x8812 (8812)
Revision:           0.0 (0000)
Port:               1
USB version/speed:  2/High
Manufacturer:       Realtek
Product:            802.11n NIC
SerialNumber:       123456
Address:            {4d36e972-e325-11ce-bfc1-08002be10318}\0015
Current State:      Busy
```

### USB Filters in Vagrant/VirtualBox

```ruby
vb.customize ["modifyvm", :id, "--usb", "on"]
vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'ESP', '--vendorid', '0x1a86', '--productid', '0x7523']
```

```ruby
# Enable USB Controller on VirtualBox
config.vm.provider "virtualbox" do |vb|
  vb.customize ["modifyvm", :id, "--usb", "on"]
  vb.customize ["modifyvm", :id, "--usbehci", "on"]
end

# Implement determined configuration attributes
config.vm.provider "virtualbox" do |vb|
  vb.customize ["usbfilter", "add", "0",
      "--target", :id,
      "--name", "Any Cruzer Glide",
      "--product", "Cruzer Glide"]
end
```

### Issue: Duplicate USB Devices with Vagrant

- <https://github.com/hashicorp/vagrant/issues/5774>
- <https://github.com/hypriot/flash/blob/master/Vagrantfile>

### Users in Ansible

List all users in running VM:

```shell
cat /etc/passwd
```

- <https://www.kali.org/docs/introduction/default-credentials/>
- <https://stackoverflow.com/questions/47873671/becoming-non-root-user-in-ansible-fails>
- <https://stackoverflow.com/questions/19292899/creating-a-new-user-and-password-with-ansible>

### Locale setting with Ansible

```shell
cat /etc/default/keyboard
localectl status
```

- <https://serverfault.com/questions/959026/how-do-i-generate-and-set-the-locale-using-ansible>
