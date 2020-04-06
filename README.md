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
```

### Guest Additions

```shell
vagrant plugin install vagrant-vbguest
```

- <https://www.serverlab.ca/tutorials/virtualization/how-to-auto-upgrade-virtualbox-guest-additions-with-vagrant/>
- <https://shanemcd.org/2018/12/15/installing-virtualbox-guest-additions-in-a-debian-vagrant-box-on-windows-10/>
- <https://subscription.packtpub.com/book/virtualization_and_cloud/9781786464910/1/ch01lvl1sec12/enabling-virtualbox-guest-additions-in-vagrant>

## ToDo

- Playbook erstellen
  - apt update, upgrade, dist-upgrade, remove
  - Treiber installieren
  - zusätzliche Pakete?

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
