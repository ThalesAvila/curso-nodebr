## ----Mostra os processos rodando na máquina
sudo docker ps

## ----Executa a imagem, se ela não existir efetua o download
sudo docker run --name postgres -e POSTGRES_USER=thalesavila -e POSTGRES_PASSWORD=minhasenhasecreta -e POSTGRES_DB=heroes -p 5432:5432 -d postgres

## ----Acessar container
sudo docker exec -it postgres /bin/bash

## ----Executar painel administrativo em paralelo
sudo docker run --name adminer -p 8080:8080 --link postgres:postgres -d adminer

## ----MONGODB
sudo docker run --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=senhaadmin -d mongo:4

## ----Paneil administrativo p/ o MongoDB
sudo docker run --name mongoclient -p 3000:3000 --link mongodb:mongodb -d mongoclient/mongoclient

## ----Acessando o container mongodb
sudo docker exec -it mongodb mongo --host localhost -u admin -p senhaadmin --authenticationDatabase admin --eval "db.getSiblingDB('herois').createUser({user: 'thalesavila', pwd: 'minhasenhasecreta', roles: [{role: 'readWrite', db:'herois'}]})"