# Ambiente Dev com Docker para desenvolvimento de aplicações Laravel 10.x

O objetivo é agilisar a criação de um ambiente de desenvolvimento Laravel sem precisar instalar o php, composer e outras dependências necessárias para utilizar o framework. Tudo isso dentro de containers garantindo que a aplicação seja replicada sem quebras em outros ambientes.

**Essa versão não é recomendada para o uso em produção antes de uma revisão.**

## Pacotes Inclusos:

- PHP 8.1-fpm

- Composer (latest)

- GIT (latest)

- NGINX Alpine (latest)

- Extras: git | curl | libpng-dev | libonig-dev | libxml2-dev | zip | rsync | unzip | npm | nodejs 

- Banco de Dados MySQL 8.2

- Cache com Redis


### Repositório de Referência
- https://github.com/especializati/curso-de-laravel-10.git

### Curso do Autor:
- https://academy.especializati.com.br/curso/laravel-10-gratuito



## Instalação do Docker (pré-requisito)

### Via  Windows WSL2

- https://github.com/codeedu/wsl2-docker-quickstart#docker-engine-docker-nativo-diretamente-instalado-no-wsl2

### Via Linux

- https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt

## Instação do Docker Compose

- https://docs.docker.com/compose/install/compose-plugin/#installing-compose-on-linux-systems  


------------------------------------------------------------


## Passo a passo para usar o ambiente dev
Clone o projeto
```sh
git clone <<endereço-do-repositorio-git>> <<nome-do-projeto>>
```
```sh
cd <<nome-do-projeto>>
```


Crie o Arquivo .env 
```sh
cp .env.example.docker .env
```


Atualize essas variáveis no arquivo .env com as informações do projeto
```dosini
APP_NAME="Especializa Ti"
APP_URL=http://localhost:8989
.
.
.
```


Suba os containers do projeto ()
```sh
docker-compose up -d
#se estiver rodando a versão mais nova do composer utilise 'docker compose up -d'
```

Alterando dados sensíveis do Dockerfile faça o build ```docker compose up -d --build```.

Verifique se os container estão ativos: ```docker ps```.  Use  ```docker-compose down``` para pará-los se necessário.

Acesse o container
```sh
docker-compose exec app-<<APP_SLUG>> bash 
# ou 'docker exec -it <nome-do-container> bash'
```


Instale o Laravel na raiz da pasta atual
```sh
composer create-project laravel/laravel .
```


Gere a key do projeto Laravel
```sh
php artisan key:generate
```


Acesse o projeto
http://localhost:<<APP_PORT>> 
