ovn-db-upgrade
==============

This repo provides an automated way of ensuring that the [OVS][ovs] databases
remain properly updated across any 2 [OVS][ovs] builds. Mostly accomplished
by using [Ansible][ansible].

Howto
-----

* tweak file [vagrant.conf.yml][1]
* tweak file [ansible/group_vars/local][2]
* tweak file [ansible/run.yml][3]
* vagrant up


If you use '[auto_start_upgrade_check: true][1]' in vagrant.conf.yml,
vagrant will also do these steps as part of provisioning:

* vagrant ssh
* cd ansible
* ansible-playbook -i hosts run.yml

References
----------

[Ansible][ansible]


The OVN configuration is accomplished by using one of the scripts created by [Guru Shetty][4],
located in [https://github.com/shettyg/ovn-namespace.git][5].

[ovs]: http://openvswitch.org
[ansible]: http://docs.ansible.com/ansible/list_of_all_modules.html
[1]: https://github.com/flavio-fernandes/ovn-db-upgrade/blob/master/vagrant.conf.yml
[2]: https://github.com/flavio-fernandes/ovn-db-upgrade/blob/master/ansible/group_vars/local
[3]: https://github.com/flavio-fernandes/ovn-db-upgrade/blob/master/ansible/run.yml
[4]: https://github.com/shettyg
[5]: https://github.com/shettyg/ovn-namespace.git
