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


# Deletando imagens e containers não utilizandos
docker system prune


# Copiando arquivos no docker
docker cp ID_OU_NOME_IMAGEM:/app/app.js ./NOME_PASTA_DESTINO/

# verificando processamento do container
docker top ID_DO_CONTAINER

# Inspecionar um container
docker inspect ID_DO_CONTAINER -> retorna todas informações em um container

# Verificando processamento do docker
docker stats 

# comando para subir e baixar imagem no docker hub
docker push NOMEREPO/NOMEIMAGEM  -> obs, criar a imagem no hub antes
docker pull NOMEREPO/NOMEIMAGEM 

# executando imagem baixada do repositorio
docker run --name testando_imagem -p 3001:3001 -d gabrielao/nodeteste:novaversao


# Criando uma pasta para salvar arquivos fora do docker
 docker run -d -p 80:80 --name phpmessages_container -v R:\documentos\github\curso_docker_kubernetes\repo_curso\curso_docker\2_volumes\messages:/var/www/html/messages --rm phpmessages


# OBS: acesso ao projeto pelo cmder
```
cd /d R:\documentos\github\curso_docker_kubernetes
```
