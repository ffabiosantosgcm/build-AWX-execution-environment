<img src="https://github.com/ffabiosantosgcm/build-AWX-execution-environment/blob/main/build-icon.jpg" style="width:150px;height:150px;">

## Build-AWX-execution-environment

## Arquivos descrição

* execution-environment.1.0.yml - Arquivo de instalação 1.0.
* execution-environment.2.0.yml - Arquivo de instalação 2.0.

## Primeira etapa

* mkdir /tmp/awx/
* copias os arquivos:

1 - sudo apt update && sudo apt upgrade -y
2 - sudo apt install podman -y
3 - sudo apt update -y
4 - sudo apt install curl -y
5 - echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
6 - curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key" | sudo apt-key add -
7 - mkdir -p  ~/venv/ansible-builder
8 - sudo apt install python3.10-venv -y
9 - python3 -m venv ~/venv/ansible-builder
10 - source ~/venv/ansible-builder/bin/activate
11 - pip3 install ansible-builder
12 - cd /tmp/awx/
13 - ansible-builder build --tag ghcr.io/ffabiosantosgcm/awx-vmware-ee:1.0 -f execution-environment.1.0.yml
14 - ansible-builder build --tag ghcr.io/ffabiosantosgcm/awx-vmware-ee:2.0 -f execution-environment.2.0.yml


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
