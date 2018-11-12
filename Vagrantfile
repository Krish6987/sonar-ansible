# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.5.0"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.synced_folder ".", "/vagrant", type: 'nfs'

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize [
      "modifyvm", :id,
      "--memory", "4096",
      # set available CPU's count
      "--cpus", 2
    ]
  end

  config.vm.network :forwarded_port, guest: 9000, host: 9000

  config.vm.define :dev, primary: true do |config|
    config.vm.network :private_network, ip: "192.168.3.5"
    config.vm.provision :ansible_local, playbook: "playbook.yml", galaxy_role_file: "requirements.yml"
  end
end