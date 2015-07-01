# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 expandtab:

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "boxcutter/centos66"

  # Desabilita a atualização automática do VirtualBox Guest Additions
  # (feita pelo plugin vbguest - https://github.com/dotless-de/vagrant-vbguest)
  #config.vbguest.auto_update = false

  # Exporta as portas utilizadas pelo WildFly
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.network :forwarded_port, guest: 9990, host: 9990

  # Exporta portas utilizadas pelo PostgreSQL
  config.vm.network :forwarded_port, guest: 5432, host: 5432

  config.vm.provider "virtualbox" do |v|
    # Apresenta a console da VM dentro do VirtualBox:
    #v.gui = true

    # Ajusta a quantidade de memória utilizada pela VM:
    v.memory = 2048
  end

  # Local comum para os diretórios compartilhados entre os ambientes
  config.vm.synced_folder "../sislegis-ambiente-comum", 
    "/sislegis-ambiente-comum", create: true
end
