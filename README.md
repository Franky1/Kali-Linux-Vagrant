# Kali Linux Vagrant

Vagrantfile and Ansible Playbook for Kali Linux

https://www.kali.org/news/announcing-kali-for-vagrant/

## First run

```shell
$ vagrant init kalilinux/rolling
```

A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

```shell
$ vagrant up
```

```shell
$ vagrant ssh
```

## ToDo

- Name vergeben
- CPUs vergeben
- RAM vergeben
- Playbook erstellen
  - apt update, upgrade, dist-upgrade
  - Treiber installieren
  - zusätzliche Pakete?
    - crowbar
