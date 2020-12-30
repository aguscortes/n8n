# -*- mode: ruby -*-
# vi: set ft=ruby :

hosts = {"n8nserver" => "192.168.1.200"}
$msg = <<MSG
------------------------------------------------------
Welcome to the n8n test environment"

URL:
 - n8n  - http://192.168.1.200:5678

------------------------------------------------------
MSG

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  hosts.each do |name, ip|
    config.vm.define name do |machine|  
      machine.vm.box = "centos/7"
      machine.vm.hostname = "prod"
      machine.vm.box_url = "centos/7"
      machine.vm.synced_folder "prod/n8n", "/home/vagrant/n8n", type: "virtualbox", owner: "vagrant", group: "vagrant"
      machine.vm.synced_folder "prod/db_data", "/home/vagrant/db_data", type: "virtualbox", owner: "vagrant", group: "vagrant"
      machine.vm.network :public_network, ip: ip
      machine.vm.post_up_message = $msg    
      machine.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 512]
        v.customize ["modifyvm", :id, "--name", name]
      end
    config.vm.provision "shell", path: 'docker.sh'   
    end
  end
end
