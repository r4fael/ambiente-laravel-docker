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
<h2> Windowns WSL2</h2>

### Tutorial oficial: 
https://docs.microsoft.com/en-us/windows/wsl/install-win10

### Passo 1 (PowerShell Admin): 
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

### Passo 2 (PowerShell Admin):
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

### Passo 3
REINICIE O COMPUTADOR

### Passo 4 (Download the Linux kernel update package):
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

### Passo 5 (PowerShell Admin):
wsl --set-default-version 2

### Passo 7 (Instale o docker):
Tutorial: https://docs.docker.com/docker-for-windows/install/

<h2>Linux</h2>

### https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt


<hr/>

<h1> Comandos </h1>

- Clone do Repositório: https://github.com/r4fael/ambiente-laravel-docker.git

- Faça o build do ambiente: ``` docker-compose up -d --build ```. 
Vai demorar um pouco baixando e instalando todas as dependências para criar os containers).
Caso precise rodar mais de um ambiente, renomeie o containers e redes dentro do arquivo docker-compose.yml para não conflitar com containers já instanciados.

- Veja se os container estão ativos: ``` docker ps ```. 
Se precisar parar algum ambinete, entre na pasta que está o docker-compose docker-compose.yml e use o comando ``` docker-compose down ``` ou ``` docker stop (nome do container que pode saber pelo docker ps) ```.

- Adicione a imagem do banco de dados de preferência no arquivos docker-compose-yml exemplo (
Não esquecer e fazer o build novamente): 

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

- Acesse o ambiente pelo terminal pelos comando: ``` docker-compose exec -it app bash ``` . O terminal deve estar na mesma pasta que o docker-compose-yml

- Rode os comandos laravel neste terminal. Para sair: ``` exit ```.

- Criando um novo projeto: ``` composer create-project laravel/laravel example-app ```

- Acesse o ambiente na porta configurada: http://localhost:8000/