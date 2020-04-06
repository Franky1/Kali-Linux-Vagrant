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

## First run

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

## ToDo

- Playbook erstellen
  - apt update, upgrade, dist-upgrade, remove
  - Treiber installieren
  - zusätzliche Pakete?

## Probleme

Playbook funktioniert so nicht wegen fehlendem `kali` root user!?

```shell
cat /etc/passwd | grep kali
```

- <https://www.kali.org/docs/introduction/default-credentials/>
- <https://stackoverflow.com/questions/47873671/becoming-non-root-user-in-ansible-fails>

## Ansible

Tipps and Tricks for Ansible.

### User

- <https://stackoverflow.com/questions/19292899/creating-a-new-user-and-password-with-ansible>

