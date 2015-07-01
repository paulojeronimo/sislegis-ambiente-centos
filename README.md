# Ambiente CentOS para execução do SISLEGIS

## Resumo

Este projeto prepara uma máquina CentOS para executar o SISLEGIS num ambiente de desenvolvimento ou de homologação.

## Requisitos

* Se o nome configurado para APP_HOST não estiver no DNS, ele deverá ser configurado localmente no arquivo /etc/hosts.
    * Deverá haver uma linha no arquivo /etc/hosts com os seguintes valores: "$APP_IP $APP_HOST"

## Instalação através do Vagrant

* Procedimentos para o provisionamento:
```bash
git clone http://github.com/pensandoodireito/sislegis-ambiente-centos
cd sislegis-ambiente-centos
cp config.exemplo config
vim config
vagrant up
vagrant ssh -c /vagrant/restaurar
vagrant ssh -c /vagrant/instalar-git
vagrant ssh -c /vagrant/instalar
``` 
* URLS de acesso:
    * As mesmas informadas em https://github.com/pensandoodireito/sislegis-ambiente-fedora/blob/master/README.md
    
* Procedimentos para o salvamento:
```bash
vagrant ssh -c /vagrant/salvar
```

## Instalação sem o uso do Vagrant

* Configure o IP da VM com o valor que será configurado no arquivo config.
    * Alguns procedimentos, caso esteja sendo utilizada uma VM rodando no VirtualBox:
        * Habilite a interface de rede para "Attached to: Host-only Adapter";
        * Configure a rede;
        * Inicie a VM;
        * Instale o VirtualBox Guest Additions;
        * Configure o diretório ``sislegis-ambiente-comum`` para que ele seja compartilhado com o Host;
        * Monte o diretório ``sislegis-ambiente-comum`` no mesmo diretório pai do diretório ``sislegis-ambiente-centos``;
* Procedimentos para o provisionamento:
```bash
sudo yum -y install curl
bash <(curl https://raw.githubusercontent.com/pensandoodireito/sislegis-ambiente-centos/master/instalar-git)
source /etc/profile.d/git.sh
git clone http://github.com/pensandoodireito/sislegis-ambiente-centos
cd sislegis-ambiente-centos
cp config.exemplo config
vim config
./instalar
```
