# project-laravel-docker
**Projeto base Laravel com ambiente Docker**
Webserver: Nginx
PHP 7.2
SGBD: MySQL 5.7

**Premissas:** Ter o Git, Docker e Docker-composer instalados

Clonar o repositório

`git clone https://github.com/rmsaitam/project-laravel-docker.git`

Acessar o diretório do repositório clonado

`cd project-laravel-docker`

PS: Por padrão nesse ambiente foi definido as credencias default que pode conferir no arquivo docker-compose.yml em environment do serviço db.

Caso desejar alterar, é recomendo fazer antes do build as alteraçes de credencias default referente ao banco de dados, conforme comentado anteriormente.

Build do ambiente

`docker-compose build; docker-compose up -d`

Instalar o framework Laravel no container PHP

`docker exec -it php_laravel composer create-project --prefer-dist laravel/laravel .
 `

Setar permissão no diretório storage

`docker exec -it php_laravel chown -R www-data:www-data storage/`

Gerar Key do projeto

`docker exec -it php_laravel php artisan key:generate`

Com isso, a princípio ao acessar no browser http://localhost:8080 deve acessar a página default do Laravel

**Execução de Migrations && Seeds**

**Credencias do banco de dados**

Primeiro deve adicionar as credencias do banco de dados no arquivo .env

Nesse ambiente o diretório *src* é o volume mapeado com o diretório */var/www/html* do container PHP

Então, o que for adicionado no diretório src do Host, será adicionado simultaneamente no diretório */var/www/html*

Renomar o .env.example para .env e adicionar as credencias do banco de dados.

Por padrão nesse ambiente foi definido as credencias default que pode conferir no arquivo docker-compose.yml em environment do serviço db

**Criação da Migrations**

`docker exec -it php_laravel php artisan make:migration create_tabela_table`

Irá criar no diretório *src/database/migrations* do Host e simultaneamente no diretório */var/www/html/database/migrations* do container

**Criação do Seed**

`docker exec -it php_laravel php artisan make:seeder TabelaTableSeeder`

**Execução do migrations e seeds criados**

```
docker exec -it php_laravel php artisan migrate
docker exec -it php_laravel php artisan db:seeds
```

Feito!
