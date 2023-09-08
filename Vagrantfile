# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  { :hostname => "md-5", :mac => "525400737f44", :ram => 4096 },
  { :hostname => "ps5-1", :mac => "525400f8453e", :ram => 2048 },
  { :hostname => "ps5-2", :mac => "52540043c86b", :ram => 2048 },
  { :hostname => "ps5-3", :mac => "525400cb704d", :ram => 2048 }

]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.box = "ubuntu/focal64"
      node_config.vm.network :public_network, :mac => node[:mac], bridge: "enp0s20f0u2"
      node_config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"

      node_config.vm.hostname = node[:hostname]
      config.vm.boot_timeout = 600
      node_config.vm.provider :virtualbox do |domain|
        domain.memory = node[:ram]
        domain.cpus = 1
      end
    end
  end

#  config.vm.provision "ansible" do |ansible|
#    ansible.compatibility_mode = "2.0"
#    ansible.playbook = "Testpoint-MD-build-U20.yml"
#    ansible.groups = {
#      "testpoint" => ["ps5-1", "ps5-2", "ps5-3"],
#      "md-arch"   => ["md-5"]
#    }
#  end
end
