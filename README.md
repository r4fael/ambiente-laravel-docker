<h1>Ambiente Dev PHP Laravel</h1>

<p>O ambiente foi pensado para agilisar a criação de um abiente de desenvolvimento para aplicações laravel.<p>
 

- PHP 8.1-fpm

- Composer (latest)

- GIT (latest)

- NGINX Alpine (latest)

- NodeJs (latest)

- NPM (latest)

- Extras: curl | libpng-dev | libonig-dev | libxml2-dev | libpq-dev | zip | unzip | rsync | pdo | pdo_pgsql | pdo_mysql | mbstring | exif | pcntl | bcmath | gd | mysqli 

- Banco de Dados Postgres e Mysql (desativados por padrão)

- Servidor Web NGINX (desativado por padrão)


<h2>Instalação do Docker (pré-requisito) </h2>

<h3>Via  Windows WSL2</h3>

- https://github.com/codeedu/wsl2-docker-quickstart#docker-engine-docker-nativo-diretamente-instalado-no-wsl2

<h3>Via Linux</h3>

- https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt

<hr/>

<h2>USO</h2>

<h3>Configuração do Ambiente</h3>

- Clone do Repositório: ```git clone https://github.com/r4fael/ambiente-laravel-docker.git```

- Caso necessário renomeia a pasta para o nome do projeto: ```mv ambiente-laravel-docker/ <nome-do-projeto>```.

- Caso precise dos containers de banco de dados e servidor web, descomente eles no arquivo docker-compose.yaml. Antes de modificar este arquivo é recomendado que os containers que ele gerencia estejam desligados. 

- Acesse a pasta do projeto ```cd <nome-do-projeto>``` e faça o build do ambiente: ```docker-compose up -d --build```. 

Vai demorar um pouco baixando e instalando todas as dependências para criar os containers se for a primeira vez.

Caso precise rodar mais de um ambiente, renomeie o containers e redes dentro do arquivo docker-compose.yaml para não conflitar com containers já instanciados.

Altere a estrutura dos arquivos para a sua realidade,se precisar de mais dependências pesquise como adicioná-las.

- Depois de finalizar, veja se os container estão ativos: ```docker ps```. 

Se precisar parar algum ambinete, entre no diretório que está o docker-compose.yaml e use o comando ```docker-compose down``` ou ```docker stop (nome do container. Veja eles com o docker ps, esse comando pode ser feito de qualquer diretório)```.

- Se for adiciona posteriormente novos containers, como o de banco de dados, não esqueça de fazer o build novamente. 


É possível ainda criar um docker-compose.yml em outra pasta para separar o banco de dados para utilizar em outros projetos. Lembre de mapear a pasta de dados (volumes) e expor a porta para acesso externo (ports)


<h3>Acessando o Ambiente</h3>

- Para acessar o terminal do ambiente, acesse o diretório do projeto e execute o comando: ```docker-compose exec -it app bash``` . Será através deles que você rodará os comandos do artisan e composer. Ou use o comando: ```docker exec -it app bash```. Nesses comandos o "app" é o nome do container definido para ser o ambiente de desenvolvimento laravel, você pode alterar se necessário.

- Para voltar ao terminal da sua máquina use o comando ``` exit ```.

<h3>Novo Projeto ou Clonando um Existente</h3>

- Depois de acessar o ambiente via terminal é possivel criar um novo projeto: ```composer create-project laravel/laravel example-app``` ou fazer o clone do seu repositório.

- Mova os arquivos e diretórios (inclusive ocultos) gerados ou clonados para a pasta que contem o Dockerfile e o docker-compose-yaml: ```rsync -rtv <nome-da-pasta-do-projeto>/ .``` . Após isso pode excluir a pasta original: ``` rm -r <nome-da-pasta-do-projeto> ``` .

- Inicie o Servidor de desenvolvimento ``` php artisan serve ``` .

- Acesse o ambiente no endereço que o artisan expor: http://localhost:8000/ .

Boa sorte!