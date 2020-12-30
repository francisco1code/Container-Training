# Chroot

## Motivação para usar o Chroot
 
É um comando do Linux que permite definir o diretório raiz de um novo processo. Nesse caso de uso em contêiner, apenas configuramos o diretório raiz para estar onde o novo diretório raiz do novo contêiner deve estar. E agora o novo grupo de processos de contêiner não consegue ver nada fora dele, eliminando nosso problema de segurança porque o novo processo não tem visibilidade fora de sua nova raiz.

## Como usar Chroot

**Primeiro etapa :** 
Primeiramente temos que está dentro de um container então iremos rodar o comandos para construir um container

`docker run -it --name docker-host --rm --privileged ubuntu:bionic`

**Segunda etapa :**
1-Crie uma nova pasta em seu diretório inicial 

 `mkdir /my-new-root`

 `mkdir /my-new-root/bin`

 `cp /bin/bash /bin/ls /my-new-root/bin/`

  `chroot /my-new-root bash`

2-O problema é que esses comandos dependem de bibliotecas para ativá-los e não os trouxemos conosco. Então, vamos fazer isso também. rode o comando  `ldd /bin/bash` Esta impressão é mais ou menos assim:

``
$ldd /bin/bash
  linux-vdso.so.1 (0x00007fffa89d8000)
  libtinfo.so.5 => /lib/x86_64-linux-gnu/libtinfo.so.5 (0x00007f6fb8a07000)
  libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007f6fb8803000)
  libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f6fb8412000)
  /lib64/ld-linux-x86-64.so.2 (0x00007f6fb8f4b000)
``

Estas são as bibliotecas de que precisamos para o bash. Vamos copiá-los em nosso novo ambiente.

`mkdir /my-new-root/lib /my-new-root/lib64`

`cp /lib/x86_64-linux-gnu/libtinfo.so.5 /lib/x86_64-linux-gnu/libdl.so.2 /lib/x86_64-linux-gnu/libc.so.6 /my-new-root/lib`

`cp /lib64/ld-linux-x86-64.so.2 /my-new-root/lib64`

Faça de novo para ls. use o commando `ldd /bin/ls`

`cp /lib/x86_64-linux-gnu/libselinux.so.1 /lib/x86_64-linux-gnu/libpcre.so.3 /lib/x86_64-linux-gnu/libpthread.so.0 /my-new-root/lib`

Agora, finalmente, use o commando `chroot /my-new-root bashe` agora use o ls. Você vai ver tudo no diretório. Agora tente pwd e veja seu diretório de trabalho. Você deveria ver ` /.` Você não pode sair daqui!, antes de ser chamado de contêiner, era chamado de jaula por esse motivo. A qualquer momento, pressione CTRL + D ou execute exit para sair de seu ambiente chroot.
  