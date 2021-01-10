# Imagens

## O que é imagem?
Images Docker são compostas por sistemas de arquivos de camadas que ficam uma sobre as outras. Ela é a nossa base para construção de uma aplicação, uma imagem é um arquivo inerte, como uma imagem ISO de um sisema operacional. Ela geralmente contém o núcleo de um sistema operacional, o núcleo de um sistema com um ou mais serviços. Como por exemplo a imagem oficial "ubuntu", que contém somente o núcleo do Ubuntu na última versão em 72,9MB.

## Como Executar uma imagem docker

`docker run -it nome_da_imagem:tipo`

**Exemplos de comandos**

**Comando em segundo plano**

`docker run --detach -it ubuntu:bionic`

**Rodar ua imagem em primeiro plano**

`docker run -it ubuntu:bionic`


