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
