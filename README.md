# IMAGEM PARA RODAR O REDIS 6 EM AMBIENTE DE DESENVOLVIMENTO:

Este repositório contem os arquivos para montar uma imagem do banco NOSQL chave-valor Redis 6.0 e um passo a passo de como rodar containers a partir da imagem criada.

## PASSO A PASSO PARA CRIAR A IMAGEM REDIS 6.0

1) Criar um volume para armazenar os dados do Redis.

```docker 
docker create volume redis-volume
```
2) Devemos expor a porta 6379 para conectar ao nosso banco. Entretanto, a documentação oficial da imagem nós mostra que uma vez que fornecemos uma porta para acesso ao nosso banco, ele fica acessível para todos os usuários. Para que o banco tenha uma senha é necessário ter um arquivo redis.conf com uma senha de acesso a ser informada.

3) Para criar a nossa imagem usaremos o seguinte comando:

```docker
docker image build -t <nome_repositorio>/redis6:v1 .
```
4) Criada a nossa imagem, vamos fazer o push para o Docker Hub(Docker Registry)

```docker
docker login
docker push <nome_repositorio>/redis6:v1 
```
Como boa prática, devemos sempre criar uma versão latest a partir da versão vigente da nossa imagem:

```docker
docker tag <nome_repositorio>/redis6:v1 <nome_repositorio>/redis6:latest
docker push <nome_repositorio>/redis6:latest
```
5) Vamos criar um container a partir da nossa imagem criada:

```docker
docker container run -d -p 6379:6379 --name redis-container <nome-repositorio>/redis6:v1
```
Para verificar se o nosso redis está em execução podemos executar:
```
docker exec -it redis-container /bin/bash
```
Para maiores informações de como criar imagens e containers Redis. Acesse:

[Documentação da imagem oficial](https://hub.docker.com/_/redis)

