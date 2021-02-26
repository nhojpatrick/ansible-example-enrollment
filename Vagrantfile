# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.boot_timeout = 1200

  # do not auto upgrade on boot
  config.vm.box_check_update = false
  config.vbguest.auto_update = false
  config.vbguest.no_remote = true

  # setup custom ssh keys
  config.ssh.insert_key = false
  config.ssh.private_key_path = [
    'provisioning/.ssh/id_ed25519',
    '~/.vagrant.d/insecure_private_key'
  ]
  config.vm.provision 'file', 
    source: 'provisioning/.ssh/id_ed25519.pub', 
    destination: '~/.ssh/authorized_keys'
  config.vm.provision 'file',
    source: 'provisioning/.ssh/id_ed25519',
    destination: '~/.ssh/id_rsa'

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.cpus = "1"
    vb.memory = "256"
    vb.customize ["modifyvm", :id, "--audio", "none"]
  end

  config.vm.define "touchdown", autostart: true do |inst|
    inst.vm.hostname = "touchdown"
    inst.vm.network "private_network", ip: "192.168.123.100"
    inst.vm.network :forwarded_port, guest: 22, host: 2100

    inst.vm.provider "virtualbox" do |vb|
      vb.memory = "384"
    end

    inst.vm.synced_folder ".", "/vagrant"

    # automated ansible install fails so manual install
    inst.vm.provision "shell", inline: "sudo apt update"
    inst.vm.provision "shell", inline: "sudo apt install -y ansible"

    # ansible setup of touchdown
    inst.vm.provision "ansible_local" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "provisioning/touchdown_setup.yaml"
    end
  end

  config.vm.define "p0web0", autostart: true do |inst|
    inst.vm.hostname = "p0web0"
    inst.vm.network "private_network", ip: "192.168.123.110"
    inst.vm.network :forwarded_port, guest: 22, host: 2110
  end

  config.vm.define "p0web1", autostart: true do |inst|
    inst.vm.hostname = "p0web1"
    inst.vm.network "private_network", ip: "192.168.123.111"
    inst.vm.network :forwarded_port, guest: 22, host: 2111
  end

end
