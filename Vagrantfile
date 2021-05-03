# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
   config.vm.network :public_network, bridge: ''

   config.vm.provider:virtualbox do |vb|
    vb.memory = 2048
    vb.cpus = 1
    vb.linked_clone = false
   end

  config.vm.define "jenkins-ci-cd-enviroment" do |subconfig|
    subconfig.vm.box = "ubuntu/bionic64"
    subconfig.vm.hostname = "jenkins-ci-cd-enviroment"
    subconfig.vm.synced_folder "./", "/home/vagrant/shared"

    subconfig.vm.provider :virtualbox do |vb|
     vb.name = "jenkins-ci-cd-enviroment"
     end

    subconfig.vm.network "forwarded_port", guest: 3000, host: 3000
    subconfig.vm.network "forwarded_port", guest: 80, host: 8080
    subconfig.vm.network "forwarded_port", guest: 27017, host: 27017

#  config.vm.provision "shell", inline: <<-SHELL
#    sudo curl -fsSL https://deb.nodesource.com/setup_15.x | sudo -E bash -
#    sudo apt-get install -y nodejs
#    wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
#    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
#    sudo apt-get update
#    sudo apt-get install -y mongodb-org
#    sudo systemctl start mongod.service
#    sudo apt install software-properties-common
#    sudo apt-add-repository --yes --update ppa:ansible/ansible
#    sudo apt install ansible -y
#    SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.config_file = "ansible/ansible.cfg"
    ansible.playbook = "ansible/play.build-ventum-ci.yml"
   end
  end
end
