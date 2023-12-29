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



---

# Mãos a Obra

## Passo a passo para usar o ambiente dev

Clone o projeto
```sh
git clone git@github.com:r4fael/ambiente-laravel-docker.git <<nome-do-projeto>>
```
```sh
cd <<nome-do-projeto>>
```


Utilizar o .env e alterer as variáveis para o projeto
```sh
cp .env.example.docker .env
```

Suba os containers do projeto
```sh
docker compose up -d
#se estiver rodando a versão mais antiga do composer utilise 'docker-compose up -d'
```

Caso altere dados sensíveis do Dockerfile ou docker-compose.yml, faça o build ```docker compose up -d --build```.

Verifique se os container estão ativos: ```docker ps```.  Use  ```docker-compose down``` para pará-los se necessário.

Acesse o container da aplicação (Por padrão é que começa com "app-")
```sh
docker exec -it <<nome-do-container>> bash
```

Instale o Laravel em uma pasta chamada "temp". 
Depois iremos mover o conteúdo para a raiz do projeto, pois o Laravel não consegue criar um novo projeto em uma pasta que já contenha arquivos
```sh
composer create-project laravel/laravel temp 
```

Mova os arquivos para a raiz do projeto e apague a pasta "temp".
**importante ignorar o .env da nova instalação**. Depois no .env.example você poderá verificar se exister alguma variável que precisa ser adicionada.
```sh
rsync -r --exclude=.env /var/www/temp/ . && rm -Rf /var/www/temp
```


Gere a key do projeto Laravel
```sh
php artisan key:generate && php artisan migrate && php artisan db:seed
```



Acesse o projeto
http://localhost:<<APP_PORT>> 
