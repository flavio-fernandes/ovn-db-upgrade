# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

vagrant_config = YAML.load_file("vagrant.conf.yml")

Vagrant.configure(2) do |config|
  config.vm.box = vagrant_config['box']
  config.vm.box_check_update = false

  # install ansible (http://docs.ansible.com/ansible/intro_installation.html#getting-ansible)
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" # avoids 'stdin: is not a tty' error.
  config.vm.provision "shell", inline: <<-SCRIPT
    if [ -d /home/vagrant ]; then ln -s /vagrant/ansible /home/vagrant/ansible ; fi
    apt-get update && \
    apt-get install -y software-properties-common && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible && \
    echo "installed ansible via apt"
  SCRIPT

  config.vm.define "box1", primary: true, autostart: vagrant_config['box1']['autostart'] do |box1|
    box1.vm.hostname = vagrant_config['box1']['host_name']

    box1.vm.provider :virtualbox do |vb|
      # vb.gui = true
      vb.memory = vagrant_config['box1']['memory']
      vb.cpus = vagrant_config['box1']['cpus']
      vb.customize [
        "guestproperty", "set", :id,
        "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000
      ]
    end
  end
end
