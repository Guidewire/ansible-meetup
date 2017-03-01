# -*- mode: ruby -*-
# vi: set ft=ruby :

defaultbox = "ubuntu/xenial64"
box = ENV['BOX'] || defaultbox

ENV['ANSIBLE_ROLES_PATH'] = "roles/"

Vagrant.configure(2) do |config|

  config.vm.box = box

  config.vm.define "ubuntu16" do |ubuntu16_cfg|
    ubuntu16_cfg.vm.hostname = "ubuntu16.vagrant"
    ubuntu16_cfg.vm.network "private_network", type: "dhcp"
    ubuntu16_cfg.vm.provider :virtualbox do |v|
      v.memory = 768
      v.name = "ubuntu16"
    end
  end

  config.vm.define "centos7" do |centos7_cfg|
    centos7_cfg.vm.box = 'centos/7'
    centos7_cfg.vm.network "private_network", type: "dhcp"
    centos7_cfg.vm.provider :virtualbox do |v|
      v.memory = 512
      v.name = "centos7"
      # v.gui = true
    end
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.groups = {
      "vagrant" => ["ubuntu16", "centos7"]
    }

  end

end
