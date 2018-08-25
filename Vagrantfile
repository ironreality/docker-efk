# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')

Vagrant.configure("2") do |config|
 config.vm.box = "ubuntu/xenial64"

 # icrease the VM's RAM
 config.vm.provider "virtualbox" do |v|
   v.memory = 2048
 end

 # test host preparation: Docker, Ansible, docker-compose etc.
 config.vm.provision "shell", inline: <<-SHELL
   # change default mirrors to Mirohost's ones to speed up provisioning
   sed -i 's/archive\.ubuntu\.com/mirror.mirohost.net/g' /etc/apt/sources.list
   sudo apt-get update

   sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   sudo apt-get update
   sudo apt-get install -y docker-ce
   sudo cp -v /lib/systemd/system/docker.service /etc/systemd/system/
   sudo sed -i 's@fd://@tcp://0.0.0.0:2375@g' /etc/systemd/system/docker.service
   sudo systemctl enable docker
   sudo systemctl restart docker
   sudo usermod -aG docker vagrant
   echo 'export DOCKER_HOST=tcp://localhost:2375' >> /home/vagrant/.bashrc

   sudo apt-get install -y python-pip
   sudo pip install docker-compose==1.9.0
   pip install ansible
   sudo sysctl -w vm.max_map_count=262144
  SHELL

 # copy the Ansible role
 config.vm.synced_folder "./", "/home/vagrant/docker-efk", type: 'rsync'
 # run Ansible
 config.vm.provision "shell", inline: "ansible-playbook docker-efk/tests/test_vagrant.yml"
end
