<img src="https://github.com/ffabiosantosgcm/build-AWX-execution-environment/blob/main/build-icon.jpg" style="width:150px;height:150px;">

## Build-AWX-execution-environment

## Arquivos descrição

* execution-environment.1.0.yml - Arquivo de instalação 1.0.
* execution-environment.2.0.yml - Arquivo de instalação 2.0.

## Primeira etapa

* mkdir /tmp/awx/
* copias os arquivos:

* sudo apt update && sudo apt upgrade -y
* sudo apt install podman -y
* sudo apt update -y
* sudo apt install curl -y
* echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list curl -L 

* "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key" | sudo apt-key add -

* mkdir -p  ~/venv/ansible-builder
* sudo apt install python3.10-venv -y
* python3 -m venv ~/venv/ansible-builder
* source ~/venv/ansible-builder/bin/activate
* pip3 install ansible-builder
* cd /tmp/awx/
* ansible-builder build --tag ghcr.io/ffabiosantosgcm/awx-vmware-ee:1.0 -f execution-environment.1.0.yml
* ansible-builder build --tag ghcr.io/ffabiosantosgcm/awx-vmware-ee:2.0 -f execution-environment.2.0.yml


## Segunda etapa - Teste local

* podman run -it --rm ghcr.io/ffabiosantosgcm/awx-vmware-ee:2.0 /bin/bash
* ansible-galaxy collection list
* cd /usr/share/ansible/collections/ansible_collections

## Terceira etapa - Enviando para o git hub

* Gere um token no git hub.

* export CR_PAT=(TOKEN AQUI!)
* echo $CR_PAT | podman login ghcr.io -u USERNAME --password-stdin

* Exemplo de criação de pacote.

* podman tag cc74f1f0650f ghcr.io/ffabiosantosgcm/awx-vmware-ee:tag

* Exemplo de updates.

* podman push ghcr.io/ffabiosantosgcm/awx-vmware-ee:1.0
* podman push ghcr.io/ffabiosantosgcm/awx-vmware-ee:2.0

## Change log

## 24/06/2023

* Criação dos arquivos.
