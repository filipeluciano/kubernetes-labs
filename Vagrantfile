VAGRANT_BOX_IMAGE = "ubuntu/bionic64"
NODE_COUNT = 1

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |virtualbox|
    virtualbox.cpus = 2
    virtualbox.memory = 2048
  end

  config.vm.define "master", primary: true do |master|
    master.vm.box = VAGRANT_BOX_IMAGE
    master.vm.hostname = "master.local"
    master.vm.network :private_network, ip: "192.168.0.100"

  end

  (1..NODE_COUNT).each do |id|
    config.vm.define "node#{id}" do |node|
      node.vm.box = VAGRANT_BOX_IMAGE
      node.vm.hostname = "node#{id}.local"
      node.vm.network :private_network, ip: "192.168.0.#{100+id}"

      # Only execute once the Ansible provisioner,
      # when all the machines are up and ready.
      if id == NODE_COUNT
        node.vm.provision "ansible" do |ansible|
          # Disable default limit to connect to all the machines
          ansible.limit = "all"
          ansible.playbook = "playbook.yaml"
        end
      end
    end
  end

end

