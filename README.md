# BaseParaProjetosVueLaravel
Uma base para iniciar projetos com Laravel e Vue com docker configurado.

Precisa ter Git, e o Docker instaldo e rodando.

Clone o arquivo

navegue para a pasta criada

digite bash e dê um enter

execute docker compose build

execute docker compose up -d# BaseParaProjetosVueLaravel
Uma base para iniciar projetos com Laravel e Vue com Docker configurado.

## Pré-requisitos
- Git instalado
- Docker instalado e rodando

## Instruções

1. Clone o repositório:
   ```sh
   git clone https://github.com/MarcusAbagnale/BaseParaProjetosVueLaravel```
Navegue para a pasta criada:

```
cd BaseParaProjetosVueLaravel```
Inicie o terminal bash:

```
bash```

Construa os containers Docker:

```
docker compose build```
Inicie os containers Docker:

```
docker compose up -d```
Execute as migrações e os seeders:

```
docker exec -it web php artisan migrate && php artisan db:seed```
Acesse o frontend em: http://localhost:8080/

Acesse o backend em: http://localhost:80/

execute  docker exec -it web php artisan migrate && php artisan db:seed

O frontend vai estar disponível em http://localhost:8080/

O backend tem a sua raiz em http://localhost:80/
