# Informações para uso da aplicação
[]: # Title: Informações para uso da aplicação

### Url da aplicação
`http://localhost:8080/api-docs/`


### Parâmetros de configuração
| Parâmetro | Descrição | Valor padrão |
| --- | --- | --- |
| MONGODB_URI | URI de conexão com o MongoDB | mongodb://$USER:$PASS@$NAME_CONTAINER:27017/$Database |


### Etapas:
1. Criar o container volume para persistir os dados do MongoDB
`docker volume create mongo_vol`
1. Criar a network para comunicação entre os containers
`docker network create produto_net`
1. Iniciar o container do MongoDB
`docker container run -d --network produto_net -e MONGO_INITDB_ROOT_USERNAME=mongouser -e MONGO_INITDB_ROOT_PASSWORD=mongopwd --name mongodb -p 27017:27017 -v mongo_vol:/data/db mongo:4.4.3`
1. Iniciar o container da aplicação
`docker container run -d --network produto_net -e MONGODB_URI=mongodb://mongouser:mongopwd@mongodb:27017/admin -p 3000:3000 --name api-produto rodrigoturatti/api-produto:latest`