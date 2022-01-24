# aries-docker

Building Hyperledger Aries infrastructure for development

# Requirements : 
Have docker and docker composer installed and running.

### 1)Create the network Von-network
<pre>
$ git clone https://github.com/bcgov/von-network
$ cd von-network
$ ./manage start --logs
</pre>

### 2)Tail-server creation for revocations
<pre>
$ git clone https://github.com/bcgov/indy-tails-server
$ cd indy-tails-server
$ ./docker/manage start
</pre>

### 3)Adjust the .env file with the ports and credentials used
<pre>
$ cat .env
</pre><pre>
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

### 4)Clone the directory with the files
<pre>$git clone https://github.com/guilherme-funchal/aries-docker.git</pre>

### 5)If you don't have a running Postgres database, add the entry to docker-compose.yml file:
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
### 6)Adjust docker-compose with the bank credentials and addresses of the other services.
  
###### 7)Start the containers
  <pre>
  $cd aries-docker
  $docker-compose up
  </pre>
  
### 8)The von-network interface can be accessed at the address
<pre>http://127.0.0.1:9000</pre>
  
### 9)The Aries interface can be accessed at:
<pre>http://127.0.0.1:8021</pre>

## 10)In the docker-compose.yml file you can change the features that are available in Aries.


  
