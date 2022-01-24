# aries-docker

为开发构建 Hyperledger Aries 基础设施

# Requirements : 
安装并运行 docker 和 docker composer。

### 1)创建网络 Von-network
<pre>
$ git clone https://github.com/bcgov/von-network
$ cd von-network
$ ./manage start --logs
</pre>

### 2)Tail-server 撤销创建
<pre>
$ git clone https://github.com/bcgov/indy-tails-server
$ cd indy-tails-server
$ ./docker/manage start
</pre>

### 3)调整 .env 包含使用的端口和凭据的文件
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

### 4)克隆包含文件的目录
<pre>$git clone https://github.com/guilherme-funchal/aries-docker.git</pre>

### 5)如果您没有正在运行的 Postgres 数据库，请将条目添加到 docker-compose.yml 文件：:
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
### 6)使用银行凭证和其他服务的地址调整 docker-compose.yml。
  
###### 7)启动容器
  <pre>
  $cd aries-docker
  $docker-compose up
  </pre>
  
### 8)von-network接口可以在地址访问
<pre>http://127.0.0.1:9000</pre>
  
### 9)Aries 界面可在以下位置访问：:
<pre>http://127.0.0.1:8021</pre>

## 10在 docker-compose.yml 文件中，您可以更改 Aries 中可用的功能。


## 重要的 : 我的第一语言是葡萄牙语和英语，如果翻译不好，您可以将我承诺更正的文本发给我。
