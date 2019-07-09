# -*- mode: ruby -*-
# vi: set ft=ruby :
BOX = "bento/ubuntu-16.04"
MASTERS = 2
WORKERS = 4

Vagrant.configure("2") do |c|
  c.ssh.insert_key = false

  (1..MASTERS).each do |m|
    c.vm.define "swarm-master-#{m}" do |node|
      node.vm.provider "virtualbox" do |v|
        v.name = "swarm-master-#{m}"
        v.memory = 1024
        v.cpus = 2
      end 

      node.vm.box = BOX
      node.vm.network "private_network", ip: "192.168.50.#{m +10}"
      node.vm.hostname = "swarm-master-#{m}"
      node.vm.provision "ansible" do |a|
        a.playbook = "ansible/playbook.yml"
        a.extra_vars = {
            node_ip: "192.168.50.#{m + 10}",
        }
      end      
    end  
  end

  (1..WORKERS).each do |w|
    c.vm.define "swarm-worker-#{w}" do |node|
      node.vm.provider "virtualbox" do |v|
        v.name = "swarm-worker-#{w}"
        v.memory = 2048
        v.cpus = 4
      end  

      node.vm.box = BOX
      node.vm.network "private_network", ip: "192.168.50.#{w + MASTERS + 10}"
      node.vm.hostname = "swarm-worker-#{w}"
      node.vm.provision "ansible" do |a|
        a.playbook = "ansible/playbook.yml"
        a.extra_vars = {
            node_ip: "192.168.50.#{w + MASTERS + 10}",
        }
      end     
    end  
  end
end

