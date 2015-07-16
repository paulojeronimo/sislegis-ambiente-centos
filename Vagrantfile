# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 expandtab:

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "boxcutter/centos66"

  # Desabilita a atualização automática do VirtualBox Guest Additions
  # (feita pelo plugin vbguest - https://github.com/dotless-de/vagrant-vbguest)
  #config.vbguest.auto_update = false

  # Configura o hostname
  config.vm.hostname = "sislegis0"

  # Configura o ip
  config.vm.network "private_network", ip: "172.17.6.80"

  # Exporta as portas 8080 e 8443 (para testes em desenvolvimento)
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.network :forwarded_port, guest: 8443, host: 8443

  # Exporta a porta de administração do WildFly
  config.vm.network :forwarded_port, guest: 9990, host: 9990

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
