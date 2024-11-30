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

docker build -t gabrielao/flask-kub-projeto . 

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

# Listando volumes
docker volume ls

# Listando networks
docker network ls

# Criando um volume
network create <NOMEDONETWORK>

# Executando um prune no network - redes não utilizadas em massa
docker network prune

# Escutando containers com network

docker build -t mysqlnetworkapi .
docker network create flasknetwork
docker run -d -p 3307:3306 --name mysql_api_container --network flasknetwork -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysqlnetworkapi

docker build -t flaskapinetwork .
docker run -d -p 5001:5000 --name flask_api_container --network flasknetwork flaskapinetwork


# Connect container ao network
docker network connect NOME_NETWORK NOME_CONTAINER

# Disconnect container ao network
docker network disconnect NOME_NETWORK NOME_CONTAINER

# Docker compose
docker-compose up -d = cria/executa container
docker-compose down  = deleta o container
docker-compose stop  = pausa o container




# docker swarm
 
docker swarm init --advertise-addr NUMERO_IP_MAQUINA   
docker swarm init      = criar um swarm
docker swarm leave -f  = deletar o swarm


# dado dockerlabs
docker labs: https://labs.play-with-docker.com/p/cr575siim2rg00e3jh5g#cr575sii_cr5761qim2rg00e3jh6g
dia 01/09/24

conectar ao nó dockerlabs -> 
docker swarm join --token SWMTKN-1-0jkjaee2e232bdv927dzlbotwfgxzz72y5vlakv49gq9rqpivz-f4fh1nu7zu2wxov8nfb77k2ck 192.168.0.28:2377

# abrir porta
OBS: clicar em "OPEN PORT" e escolher o numero(ex: 80) e partir para um link como exemplo:  http://ip172-18-0-7-cr9tjjaim2rg00fl4tp0-80.direct.labs.play-with-docker.com/

docker node ls -> listar nós conectados ao swarm

docker service ls -> serviços que estão executando no swarm                                                                                                                                                                                                                                                                                                                                                                                               
criando service           
docker service create --name nginxswarm -p 80:80 nginx -> OBS executar no node1

# deletar service
docker service rm nginxswarm

# replicar serviços
docker service create --name nginxreplicas --replicas 4 -p 80:80 nginx 
    OBS: o numero 4 depois de replicar informa a quantidade de nós que vc tem e que seram utilizados

# recuperar token - conectar mais uma instancia ao nó principal
docker swarm join-token manager

# diminuir instancia para evitar gastos
docker swarm leave 
    OBS: usar comando no worker removido

# removendo node do swarm 
docker node rm <ID>

# inpescionar serviços
docker service inspect <ID>

# docker swarm list
docker node ls

# verificando quais containers estão rodando
docker service ps <nomeContainer>

# Compose 


# Escalando aplicação

docker service scale nginx_swarm_web=3




# INICIANDO KUBERNETES
minikube start --driver=docker
minikube status
minikube stop


minikube dashboard


# criando projeto 
    docker build -t gabrielao/flask-kub-projeto .

# executando projeto
    docker run -d -p 5000:5000 --name flask-kub --rm gabrielao/flask-kub-projeto

# verificar o dashboard do minikube
    minikube dashboard

# subindo imagem no dockerhub
    docker push gabrielao/flask-kub-projeto

# criando deployment
    kubectl create deployment flask-deployment --image=gabrielao/flask-kub-projeto

# descrição do deploy
    kubectl describe deployments

# checando um pod
    kubectl get pods

# configurando kubernets
    kubectl config view


# expondo porta
    kubectl expose deployment <NOME> --type=<TIPO> --port=<PORT>

    kubectl expose deployment flask-deployment --type=LoadBalancer --port=5000

# gerando IP service

    minikube service flask-deployment

# saber mais sobre o service
    kubectl describe services/flask-deployment

# replicar aplicação

    kubectl scale deployment/<NOME> --replicas=<QUANTIDADE_REPLICAS>

    kubectl scale deployment/flask-deployment --replicas=5

# verificar o número de replicas

    kubectl get rs -> saber varios projetos executando

# diminuir Escalando

    scale down


# atualizar imagem do projeto
    kubectl set image deployment/<NOME>

    # atualizando arquivo
    docker build -t gabrielao/flask-kub-projeto:2 .     
    docker push gabrielao/flask-kub-projeto:2

    realizando update do container
    kubectl set image deployment/flask-deployment flask-kub-projeto=gabrielao/flask-kub-projeto:2

# rollback
    kubectl rollout status deployment/<NOME>
    
    kubectl rollout status deployment/flask-deployment

    kubectl rollout undo deployment/flask-deployment

# deletando serviço
    kubectl delete service <NOME>
    kubectl delete service flask-deployment
    

# deletando deployment
    kubectl delete deployment <NOME>
    kubectl delete deployment flask-deployment




# executar o deployment:
    kubectl apply -f <ARQUIVO>
    kubectl apply -f flask.yaml

# parando o deployment:
    kubectl delete -f <ARQUIVO>
    kubectl delete -f flask.yaml


# executando o service
    kubectl apply -f <ARQUIVO>
    kubectl apply -f flask-service.yaml

# gerar o ip
    minikube service flask-servide

# parando o deployment:
    kubectl delete -f <ARQUIVO>
    kubectl delete -f flask-service.yaml


3_uniao_arquivos



# OBS: acesso ao projeto pelo cmder
```
cd /d D:\documentos\github\curso_docker_kubernetes
```



