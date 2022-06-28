<h1>Versão Atual</h1>
- Ambiente PHP 8.1-fpm
- Composer (lateste)
- GIT (lateste)
- NGINX Alpine (lateste)
- NodeJs (lateste)
- NPM (lateste)

- Extras: 
-- curl
-- libpng-dev
-- libonig-dev
-- libxml2-dev
-- libpq-dev
-- zip
-- unzip
-- pdo
-- pdo_pgsql
-- pdo_mysql
-- mbstring
-- exif 
-- pcntl 
-- bcmath
-- gd
-- mysqli 


 - <strong>Não Contem Banco de Dados</strong>


<h1>Instalação do Docker (pré requisitos) </h1>
<h2> Windows WSL2</h2>

### https://github.com/codeedu/wsl2-docker-quickstart#docker-engine-docker-nativo-diretamente-instalado-no-wsl2

<h2>Linux</h2>

### https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt


<hr/>

<h1> Comandos </h1>

- Clone do Repositório: https://github.com/r4fael/ambiente-laravel-docker.git

- Acesse a pasta do projeto e faça o build do ambiente: ``` docker-compose up -d --build ```. 
Vai demorar um pouco baixando e instalando todas as dependências para criar os containers.
Caso precise rodar mais de um ambiente, renomeie o containers e redes dentro do arquivo docker-compose.yml para não conflitar com containers já instanciados.

- Depois de finalizar, veja se os container estão ativos: ``` docker ps ```.
Se precisar parar algum ambinete, entre na pasta que está o docker-compose.yml e use o comando ``` docker-compose down ``` ou ``` docker stop (nome do container que pode saber pelo docker ps) ```.

- Se quiser, adicione as instruções para carregar a imagem do banco de dados da sua preferência no arquivo docker-compose-yml. Exemplo (
não esquecer e fazer o build novamente): 

````
mysql:
    image: mysql
    command: --default-authentication-plugin=mysql_native_password
    container_name: mysql
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: **colocar-a-senha-do-root-aqui**
    ports:
      - "3306:3306"
    networks:
      - app-network
    volumes:
      - ./dados:/var/lib/mysql
````

````

postgres:
  container_name: postgres
  image: postgres:9.5-alpine
  restart: always
  environment:
    POSTGRES_DB: **nome-base-de-dados**
    POSTGRES_USER: **nome-user**
    POSTGRES_PASSWORD: **senha**
  ports:
    - 5432:5432
  networks:
    - app-network
  volumes:
    - ./database/data:/var/lib/postgresql/data

````


É possível ainda criar um docker-compose.yml em outra pasta para separar o banco de dados para utilizar em outros projetos. Lembre de mapear a pasta de dados (volumes) e expor a porta para acesso externo (ports)


- Acesse o ambiente pelo terminal pelos comando: ``` docker-compose exec -it app bash ``` . O terminal deve estar na mesma pasta que o docker-compose-yml

- Rode os comandos laravel neste terminal. Para sair: ``` exit ```.

- Criando um novo projeto: ``` composer create-project laravel/laravel example-app ```

- Acesse o ambiente na porta configurada: http://localhost:8000/