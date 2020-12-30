 # Chroot

 ## Motivação para usar o Chroot
 
É um comando do Linux que permite definir o diretório raiz de um novo processo. Nesse caso de uso em contêiner, apenas configuramos o diretório raiz para estar onde o novo diretório raiz do novo contêiner deve estar. E agora o novo grupo de processos de contêiner não consegue ver nada fora dele, eliminando nosso problema de segurança porque o novo processo não tem visibilidade fora de sua nova raiz.

