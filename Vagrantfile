# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

vagrant_config = YAML.load_file("vagrant.conf.yml")

$apt_install_ansible = <<SCRIPT
  # install ansible (http://docs.ansible.com/ansible/intro_installation.html#getting-ansible)
  apt-get update && \
  apt-get install -y software-properties-common && \
  apt-add-repository ppa:ansible/ansible && \
  apt-get update && \
  apt-get install -y ansible && \
  echo "installed ansible via apt"
SCRIPT

$create_ansible_slink = <<SCRIPT
  if [ -d /home/vagrant ]; then ln -s /vagrant/ansible /home/vagrant/ansible ; fi
SCRIPT

$auto_start_upgrade_check = <<SCRIPT
  cd /vagrant/ansible && ansible-playbook -i hosts run.yml && echo 'Happy happy, joy joy!!'
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box_check_update = false

  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" # avoids 'stdin: is not a tty' error.
  config.vm.provision "create_ansible_slink", type: "shell", inline: $create_ansible_slink

  config.vm.define "ubuntu", primary: true, autostart: vagrant_config['ubuntu']['autostart'] do |ubuntu|
    ubuntu.vm.box = vagrant_config['ubuntu']['box']
    ubuntu.vm.hostname = vagrant_config['ubuntu']['host_name']

    ubuntu.vm.provider :virtualbox do |vb|
      vb.memory = vagrant_config['ubuntu']['memory']
      vb.cpus = vagrant_config['ubuntu']['cpus']
    end

    ubuntu.vm.provision "apt_install_ansible", type: "shell", inline: $apt_install_ansible
    if vagrant_config['auto_start_upgrade_check']
      ubuntu.vm.provision "auto_start_upgrade_check", type: "shell", inline: $auto_start_upgrade_check
    end
  end
end
