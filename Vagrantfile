# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "bento/ubuntu-16.04"

    config.vm.define :db do |db_config|
        db_config.vm.hostname = "db"
        db_config.vm.network :private_network, :ip => "192.168.33.18"
        db_config.vm.synced_folder "www/", "/var/www/html"

        db_config.vm.provision "ansible" do |ansible|
          ansible.playbook = "provision/db/playbook.yml"
        end

        db_config.vm.provider "virtualbox" do |vb|
            vb.memory = "384"
        end
    end

    config.vm.define :loadbalancer do |loadbalancer|
           loadbalancer.vm.provider :virtualbox do |v|
               v.name = "loadbalancer"
               v.customize [
                   "modifyvm", :id,
                   "--name", "loadbalancer",
                   "--memory", 384,
                   "--natdnshostresolver1", "on",
                   "--cpus", 1,
               ]
           end

           loadbalancer.vm.box = "bento/ubuntu-16.04"
           loadbalancer.vm.network :private_network, ip: "192.168.33.19"
           loadbalancer.ssh.forward_agent = true
           loadbalancer.vm.synced_folder "./", "/vagrant"

           loadbalancer.vm.provision "ansible" do |ansible|
                ansible.playbook = "provision/loadbalancer/playbook.yml"
           end
    end

    (1..2).each do |i|
      config.vm.define "web#{i}" do |web_config|

          web_config.vm.hostname = "web#{i}"
          web_config.vm.network :private_network, :ip => "192.168.33.1#{i}"

          #web_config.vm.provision "docker",
         #  images: ["alexcheng/magento"]
         web_config.vm.provision "ansible" do |ansible|
           ansible.playbook = "provision/web/playbook.yml"
           ansible.extra_vars = {
               vagrant_db_ip: "192.168.33.18",
               vagrant_host: "192.168.33.1#{i}",
           }
         end

          web_config.vm.provider "virtualbox" do |vb|
              vb.memory = "1024"
          end
      end
    end
end
