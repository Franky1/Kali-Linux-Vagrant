# Kali Linux Vagrant

Vagrantfile and Ansible Playbook for Kali Linux

## Links

- <https://www.kali.org/news/announcing-kali-for-vagrant/>
- <https://pablo.tools/posts/computers/custom-kali-box/>
- <https://github.com/pinpox/kali-i3>
- <https://computingforgeeks.com/how-to-run-kali-linux-rolling-release-with-vagrant-on-virtualbox/>
- <https://www.terasq.com/2019/03/building-kali-with-vagrant-ansible-p1/>
- <https://github.com/M507/Kali-TX>
- <http://mohad.red/Kali-Linux-is-Missing-Many-tools/>

## First run

Please read the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

```shell
$ vagrant up
```

```shell
$ vagrant ssh
```

```shell
$ vagrant provision
```

## ToDo

- Playbook erstellen
  - apt update, upgrade, dist-upgrade, remove
  - Treiber installieren
  - zusätzliche Pakete?
