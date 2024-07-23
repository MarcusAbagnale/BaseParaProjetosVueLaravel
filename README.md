# BaseParaProjetosVueLaravel
Este repositório fornece uma estrutura inicial para projetos utilizando Laravel e Vue.js com Docker configurado. A configuração requer que o Git e o Docker estejam instalados e funcionando corretamente no sistema.

## Pré-requisitos
- Git instalado
- Docker instalado e rodando

## Instruções

1. Clone o repositório:
   ```git clone https://github.com/MarcusAbagnale/BaseParaProjetosVueLaravel
   
Navegue para a pasta criada:

```cd BaseParaProjetosVueLaravel

Inicie o terminal bash:

```bash

Construa os containers Docker:

```docker compose build

Inicie os containers Docker:

```docker compose up -d

Execute as migrações e os seeders:

```docker exec -it web php artisan migrate && php artisan db:seed

Acesse o frontend em: http://localhost:8080/

Acesse o backend em: http://localhost:80/

execute  docker exec -it web php artisan migrate && php artisan db:seed

O frontend vai estar disponível em http://localhost:8080/

O backend tem a sua raiz em http://localhost:80/
