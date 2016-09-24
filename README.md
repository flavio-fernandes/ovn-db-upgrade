ovn-db-upgrade
==============

This repo provides an automated way of ensuring that the ovs databases
get properly updated across any 2 ovs builds. It does so by using
Ansible.

Steps you should follow in order to exercise the ovn db update:

- tweak file vagrant.conf.yml

- tweak ansible/group_vars/local

- tweak file ansible/run.yml

- vagrant up



If you chose 'auto_start_upgrade_check: true' in vagrant.conf.yml,
it will do these steps:

- vagrant ssh

- cd ansible

- ansible-playbook -i hosts run.yml


