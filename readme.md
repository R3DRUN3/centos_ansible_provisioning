# CentOS Ansible provisioning

<p align="center"><img width="180" height="180" src="https://github.com/yurijserrano/Github-Profile-Readme-Logos/blob/master/cloud/ansible.svg"></p>

## Abstract
This repo contains IaaC scripts to aumtomate the followings:
1. Provisioning of 3 CentOS virtual machines
2. Creation of a 50 GB ext4 partition for Docker
3. Installation of Docker
4. Installation of Docker Swarm 
5. Securing of Docker Rest Api via TLS certificate generation
6. Configure Docker auto-start at boot
7. Interact and deploy services on the Swarm from the third machine.

## Prerequisites
This code has been tested on a `windows 11` host with `vagrant` version `2.2.19`.

By making use of the `Ansible Local` Vagrant Provider we are able to provision the guest using Ansible playbooks by executing ansible-playbook directly on the guest machine.

Followings are the required Vagrant Plugins:

1. `vagrant-disksize (0.1.3, global)`
2. `vagrant-vbguest (0.21.0, global)`

## Instructions
Clone this repo and start the provisioning:

```console
git clone https://github.com/R3DRUN3/DevOps.git \
&& cd DevOps && Vagrant up
``` 
## Github Action
An [ansible linting](https://ansible-lint.readthedocs.io/en/latest/) GitHub action is associated with this repo:

[![Ansible Lint](https://github.com/R3DRUN3/centos_ansible_provisioning/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/R3DRUN3/centos_ansible_provisioning/actions/workflows/ansible-lint.yml)

Note that it fails because it cannot find some of the roles referenced in the playbook provisioning.yml:
