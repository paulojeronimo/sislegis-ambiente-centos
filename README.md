# Ambiente CentOS para execução do SISLEGIS

## Resumo

Este projeto prepara uma máquina CentOS para execução do SISLEGIS em ambiente de homologação (default) ou de desenvolvimento.

## Requisitos

Verifique o conteúdo do arquivo ``config`` (tua cópia de ``config.exemplo``). Se o nome configurado para APP_HOST não estiver no DNS de tua rede, ele deverá ser configurado localmente no arquivo ``/etc/hosts`` de tua máquina. Ou seja, deverá haver uma linha no arquivo ``/etc/hosts`` com os valores informados para ``$APP_IP`` e ``$APP_HOST``.

## Instalação através do Vagrant

### Procedimentos para o provisionamento

```bash
git clone http://github.com/pensandoodireito/sislegis-ambiente-centos
cd sislegis-ambiente-centos
cp config.exemplo config
vi config
vagrant up
vagrant ssh -c /vagrant/instalar
``` 

### Procedimentos para o salvamento

```bash
vagrant ssh -c /vagrant/salvar
```

## Instalação sem o uso do Vagrant

### Criação do usuário sislegis-admin

```
sudo useradd sislegis-admin
echo '%sislegis-admin ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/sislegis-admin
```

### Procedimentos para o provisionamento

```bash
sudo su - sislegis-admin
sudo yum -y install curl
bash <(curl https://raw.githubusercontent.com/pensandoodireito/sislegis-ambiente-centos/master/instalar-git)
source /etc/profile.d/git.sh
git clone http://github.com/pensandoodireito/sislegis-ambiente-centos
cd sislegis-ambiente-centos
cp config.exemplo config
vi config
./instalar
```

## IMPORTANTE!!!

Após a instalação do JBoss (WildFly), editar o arquivo ``$JBOSS_HOME/bin/standalone.conf`` e ajustar os parâmetros de memória!

Recomenda-se para o ambiente de homologação do SISLEGIS, numa com 8GB de memória, os seguintes parâmetros de memória: ``-Xms4096m -Xmx4096m``.

## Instalação em ambiente de desenvolvimento

Os passos a serem seguidos são idênticos aos apresentados acima. A única diferença é que, antes da execução do script ``instalar``, as três linhas a seguir devem ser removidas do arquivo ``config``:
```
APP_AMBIENTE=homologacao
APP_HOST=homologacao-sislegis.pensandoodireito.mj.gov.br
APP_IP=172.17.6.80
```
