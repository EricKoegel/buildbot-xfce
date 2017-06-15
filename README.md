# Xfce buildbot for buildbot.xfce.org

## Requirements

- Vagrant
- VirtualBox
- Ansible

## Setup

### Install external roles to ansible/roles

    ansible-galaxy install -r requirements.yml

### Deploy

    vagrant up

### Post deployment

Connect to the default page of http://10.10.10.10:8080
The default jenkins username/password: admin/admin
The list of default values are in ansible/vars/common_vars.yml
