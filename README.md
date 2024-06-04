# curso_docker_kubernetes


# flags docker
-p = definir portas
-d = liberar o cmd para outros comandos
-n = definir nome imagem
-i = executa o container no iterativo
-f = força o comando

# Baixando imagens 
docker pull python 
docker pull node

# Tipos de docker help
docker run --help
docker start --help
docker stop --help

# Nomeando uma imagem criada
docker tag  87bf5a144a72 minhaimagem -> versão latest
docker tag  87bf5a144a72 minhaimagem:minhatag -> versão com tag 


# Criando uma imagem com nome
docker build -t meunode_diferente . -> imagem com nome
docker build . -> imagem sem nome
docker build -t meunode_diferente:minhatagdiferente . -> imagem com nome e tag

# Deletando imagems
docker rmi meunode_diferente:minhatagdiferente -> teletando imagem e tag
docker rmi meunode_diferente -> teletando imagem
docker rmi -f meunode_diferente -> forçando deleção imagem




# OBS: acesso ao projeto pelo cmder
```
cd /d R:\documentos\github\curso_docker_kubernetes
```
