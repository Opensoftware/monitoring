# -*- mode: ruby -*-
# vi: set ft=ruby :

domain = 'example.com'

nodes = [
  {:hostname => 'monit',  :ip => '172.16.36.10'}
]

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"
#  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
#  config.vm.provision "shell", inline: "cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/site.yml"
  end

  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.provider "virtualbox" do |v|
        v.memory = 1512
      end
      node_config.vm.box = 'ubuntu/trusty64'
      node_config.vm.hostname = node[:hostname] + '.' + domain
      node_config.vm.network :private_network, ip: node[:ip]
    end
  end

end


