Xfce buildbot for [buildbot.xfce.org](http://buildbot.xfce.org)

This project uses Vagrant, VirtualBox, and Ansible to provision a [Jenkins](https://jenkins.io/doc/) automation server and multiple builders running [Ubuntu](https://www.ubuntu.com/), [FreeBSD](https://www.freebsd.org/), [OpenBSD](https://www.openbsd.org/), and [Debian](https://www.debian.org/). Once the cluster is provisioned, Jenkins will then build the entire Xfce project to ensure the code compiles without errors on those platforms. By following the instructions below you can run that same cluster, test changes, and submit pull requests to contribute back.

## Requirements

- [Vagrant](https://www.vagrantup.com/intro/index.html)
- [VirtualBox](https://www.virtualbox.org/manual/ch01.html)
- [Ansible](https://www.ansible.com/how-ansible-works)

## Setup

### Install external roles to ansible/roles
```
    ansible-galaxy install -r requirements.yml
```
### Deploy
```
    vagrant up
```
### Post deployment

Connect to the default page of http://10.10.10.10:8080

The default jenkins username/password: admin/admin

The list of default values are in [ansible/vars/common_vars.yml](./ansible/vars/common_vars.yml)

You can also remote into the VMs by running:
```
    cagrant ssh Debian
    vagrant ssh FreeBSD
    vagrant ssh Jenkins
    vagrant ssh OpenBSD
    vagrant ssh Ubuntu
```
