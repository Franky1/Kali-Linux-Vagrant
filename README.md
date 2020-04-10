# Kali Linux Vagrant

Vagrantfile and Ansible Playbook for Kali Linux

## Tipps

Default user is `vagrant` and password is `vagrant`.

## Links

- <https://www.kali.org/news/announcing-kali-for-vagrant/>
- <https://pablo.tools/posts/computers/custom-kali-box/>
- <https://github.com/pinpox/kali-i3>
- <https://computingforgeeks.com/how-to-run-kali-linux-rolling-release-with-vagrant-on-virtualbox/>
- <https://www.terasq.com/2019/03/building-kali-with-vagrant-ansible-p1/>
- <https://github.com/M507/Kali-TX>
- <http://mohad.red/Kali-Linux-is-Missing-Many-tools/>

## Vagrant

Please read the comments in the Vagrantfile as well as documentation on `vagrantup.com` for more information on using Vagrant.

```shell
vagrant validate
```

```shell
vagrant up
```

```shell
vagrant ssh
```

```shell
vagrant halt
vagrant destroy
```

```shell
vagrant reload
vagrant provision
vagrant up --provision
```

### Guest Additions

```shell
vagrant plugin install vagrant-vbguest
```

- <https://www.serverlab.ca/tutorials/virtualization/how-to-auto-upgrade-virtualbox-guest-additions-with-vagrant/>
- <https://shanemcd.org/2018/12/15/installing-virtualbox-guest-additions-in-a-debian-vagrant-box-on-windows-10/>
- <https://subscription.packtpub.com/book/virtualization_and_cloud/9781786464910/1/ch01lvl1sec12/enabling-virtualbox-guest-additions-in-vagrant>

### USB Devices

- <https://sonnguyen.ws/connect-usb-from-virtual-machine-using-vagrant-and-virtualbox/>
- <https://stackoverflow.com/questions/38956127/usb-device-is-not-visible-inside-vagrant>
- <https://stackoverflow.com/questions/22503168/vagrant-usbfilter-make-the-guest-machine-entered-an-invalid-state>

```shell
VBoxManage.exe list usbhost
Host USB Devices:

UUID: 7c078866-a1ef-43fc-a67c-df06ae84e4ac
VendorId: 0x04f2 (04F2)
ProductId: 0xb40a (B40A)
Revision: 105.100 (105100)
Port: 0
USB version/speed: 2/High
Manufacturer: Chicony Electronics Co., Ltd
Address: {36fc9e60-c465-11cf-8056-444553540000}\0008
Current State: Busy
```

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

## ToDo

- Playbook erstellen
  - apt update, upgrade, dist-upgrade, remove
  - Treiber installieren
  - zusätzliche Pakete?
  - USB aktivieren
  - USB Filter aktivieren

## Probleme

### Kali User

Playbook funktioniert so nicht wegen fehlendem `kali` root user!?

```shell
cat /etc/passwd | grep kali
```

- <https://www.kali.org/docs/introduction/default-credentials/>
- <https://stackoverflow.com/questions/47873671/becoming-non-root-user-in-ansible-fails>
- <https://stackoverflow.com/questions/19292899/creating-a-new-user-and-password-with-ansible>

### Locale

```shell
cat /etc/default/keyboard
localectl status
```

- <https://serverfault.com/questions/959026/how-do-i-generate-and-set-the-locale-using-ansible>

## Ansible

Tipps and Tricks for Ansible.
