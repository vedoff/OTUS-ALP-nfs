# -*- mode: ruby -*-
# vim: set ft=ruby :
home = ENV['HOME']
ENV["LC_ALL"] = "en_US.UTF-8"


Vagrant.configure(2) do |config|
  # образ системы Ubuntu 18/04 LTS (Bionic Beaver)
#  server.vm.box = "vedoff/centos-7-5"
  # не проверять репозиторий на наличие обновлений
#  config.vm.box_check_update = false
  # отменить создание ssh-ключа
#  config.ssh.insert_key = false

  # ПЕРВАЯ ВИРТУАЛЬНАЯ МАШИНА
    config.vm.define "nfs-server" do |server|
    # имя виртуальной машины
    server.vm.box = 'vedoff/centos-7-5' 
    server.vm.provider "virtualbox" do |vb|
      vb.name = "nfs-server"
    end
    # hostname виртуальной машины
    server.vm.hostname = "nfs-server"
    # настройки сети
    server.vm.network "private_network", ip: "192.168.56.100"
    server.vm.synced_folder ".", "/vagrant",  
          type: "rsync",
          rsync_auto: "true",
          rsync_exclude: [".git/",".vagrant/",".gitignore","Vagrantfile"]
          server.vm.provision "shell", path: "provision-server/nfs-server.sh"
    # установка пакетов
#    subconfig.vm.provision "apache", type: "shell", inline: "apt-get install -y apache2"
#
#    subconfig.vm.provision "shell", inline: <<-SHELL
#          sh /provision-client/nfs-client.sh
#      SHELL
   end
end



Vagrant.configure(2) do |client|
  # образ системы Ubuntu 18/04 LTS (Bionic Beaver)
  client.vm.box = "vedoff/centos-7-5"
  # не проверять репозиторий на наличие обновлений
#  config.vm.box_check_update = false
  # отменить создание ssh-ключа
#  config.ssh.insert_key = false

  # ПЕРВАЯ ВИРТУАЛЬНАЯ МАШИНА
    client.vm.define "nfs-client" do |client|
    # имя виртуальной машины
    client.vm.box = 'vedoff/centos-7-5'
    client.vm.provider "virtualbox" do |vb|
      vb.name = "nfs-client"
    end
    # hostname виртуальной машины
    client.vm.hostname = "nfs-client"
    # настройки сети
    client.vm.network "private_network", ip: "192.168.56.101"
    client.vm.synced_folder ".", "/vagrant",  
          type: "rsync",
          rsync_auto: "true",
          rsync_exclude: [".git/",".vagrant/",".gitignore","Vagrantfile"]
          client.vm.provision "shell", path: "provision-client/nfs-client.sh"
    # установка пакетов
#    subconfig.vm.provision "apache", type: "shell", inline: "apt-get install -y apache2"
#
#    subconfig.vm.provision "shell", inline: <<-SHELL
#          sh /provision-client/nfs-client.sh
#      SHELL
end
end
#end
