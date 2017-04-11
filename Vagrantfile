# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.define "ubuntu-php7" do |srv|

    srv.vm.box = "bento/ubuntu-16.04"

    srv.vm.hostname = "desarrollo"
    srv.vm.network "forwarded_port", guest: 80, host: 8098
    srv.vm.network "private_network", ip: "192.168.33.18"

    srv.vm.synced_folder "www/", "/var/www/html"

    srv.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end

    srv.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision/playbook.yml"
    end
  end
end
