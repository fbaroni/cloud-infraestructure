# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.box = "bento/ubuntu-16.04"

    config.vm.define :db do |db_config|
        db_config.vm.hostname = "db"
        db_config.vm.network :private_network, :ip => "192.168.33.10"

        db_config.vm.provision "ansible" do |ansible|
          ansible.playbook = "provision/db/playbook.yml"
        end

        db_config.vm.provider "virtualbox" do |vb|
            vb.memory = "768"
        end
    end

    config.vm.define :web do |web_config|

        web_config.vm.hostname = "web1"
        web_config.vm.network :private_network, :ip => "192.168.33.11"

        web_config.vm.provision "ansible" do |ansible|
          ansible.playbook = "provision/web/playbook.yml"
        end

        web_config.vm.provider "virtualbox" do |vb|
            vb.memory = "512"
        end
    end

    config.vm.define :web2 do |web_config|

        web_config.vm.hostname = "web2"
        web_config.vm.network :private_network, :ip => "192.168.33.12"

        web_config.vm.provision "ansible" do |ansible|
          ansible.playbook = "provision/web/playbook.yml"
        end

        web_config.vm.provider "virtualbox" do |vb|
            vb.memory = "512"
        end
    end

    config.vm.define :web3 do |web_config|

        web_config.vm.hostname = "web3"
        web_config.vm.network :private_network, :ip => "192.168.33.13"

        web_config.vm.provision "ansible" do |ansible|
          ansible.playbook = "provision/web/playbook.yml"
        end

        web_config.vm.provider "virtualbox" do |vb|
            vb.memory = "512"
        end
    end
end
