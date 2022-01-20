# aries-docker

Criação de infraestrutura do Hyperledger Aries para o desenvolvimento

# Pré-requisito : 
Ter o docker e o docker composer instalados e em execução.

### 1)Criar a rede Von-network
$ git clone https://github.com/bcgov/von-network
$ cd von-network
$ ./manage start --logs

### 2)Criação do servidor de tail-server para revogações
$ git clone https://github.com/bcgov/indy-tails-server
$ cd indy-tails-server
$ ./docker/manage start

### 3)Ajustar o arquivo .env com as portas e credenciais utilizadas
$ cat .env
<pre>
AGENT_WALLET_SEED=seed com 32 caracteres Ex.: 000000000000000000000000000teste
LABEL=nome da aplica
ACAPY_ENDPOINT_PORT=8000
ACAPY_ENDPOINT_URL=http://localhost:8000/
ACAPY_ADMIN_PORT=11000
LEDGER_URL=http://172.17.0.1:9000
TAILS_SERVER_URL=http://tails-server:6543
CONTROLLER_PORT=8080
WALLET_NAME=nome da wallet
WALLET_KEY=senha
</pre>

### 4)Clonar o diretório com os arquivos
$git clone https://github.com/guilherme-funchal/aries-docker.git

### 5)Criar um banco de dados para as wallets no Postgres ou incluir no docker compose as entradas : 
<pre>
services:
  #
  # un-managed trustee agent
  #
  db:
    image: postgres:latest
    hostname: db
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
    volumes:
      - ./postgres:/docker-entrypoint-initdb.d/
      - ./.postgres:/var/lib/postgresql
    ports:
      - "5432:5432"
</pre>
### 6)Ajustar o docker-compose com as credenciais de banco e endereços dos demais serviços.
  
###### 7)Iniciar os conteiners
  $cd aries-docker
  $docker-compose up
  
  
### 8) A interface da von-network poderá ser acessa com o endereço http://127.0.0.1:9000
  
### 9) A interface do Aries poderá ser acessada com o endereço http://127.0.0.1:8021
  
