# Curso GRATUITO de Laravel 10.x

- :movie_camera: [Acesse o Curso](https://academy.especializati.com.br/curso/laravel-10-gratuito).


Links Úteis:

- :tada: [Saiba Mais](https://linktr.ee/especializati)

## Passo a passo para rodar o projeto
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
