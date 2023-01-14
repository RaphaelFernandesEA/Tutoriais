# Configurando o MySQL no Express

Para criar a aplicação do zero, crie o diretório que armazenará a aplicação com a pasta src

    mkdir nome-do-projeto
    cd nome-do-projeto
    mkdir src

👀 Obs: O diretório src só irá conter arquivos e diretórios referentes ao código fonte da aplicação (código escrito por você)!
Mantendo um comportamento comum:

- na raiz do projeto ficam arquivos de configuração como: .gitignore, .eslintrc.json, package.json, docker-compose.yml e outros;
- o código da aplicação fica em diretórios como: src, app, ou similar.

Após isso inicie um pacote Node.js:

    npm init 

      ou 

    npm init -y

👀 Obs: o comando acima vai criar o arquivo package.json para você. Com este arquivo criado e configurado, você pode instalar as dependências que usará ao longo da construção da sua API.

## Instale as dependências necessárias para configurarmos um projeto Express capaz de conectar ao MySQL:

    npm i express@4.17 mysql2@2.3
⚠️ Aviso: Aqui, usei versão 4.17, pois é a mesma versão que irei usar no projeto deste bloco! Iremos determinar uma versão para todas as nossas dependências para evitarmos comportamentos inesperados.

Após executar o comando acima, um arquivo e um diretório serão criados automaticamente - o package-lock.json e o node_modules!

O arquivo package-lock.json serve para gerenciar as dependências de nossas dependências;
O diretório (node_modules) é onde todas as nossas dependências, e dependências de nossas dependências, serão instaladas. 

## Garantindo a qualidade do código

Para garantir a qualidade de escrita do código! Instalar e configurar o ESLint. 

👀 Regras que usamos na Trybe na nossa aplicação.

    npm i eslint@6.8 eslint-config-trybe-backend@1.0 -D

Criar os arquivos referentes a configuração do ESLint na raiz: 

    touch .eslintignore .eslintrc.json

- .eslintignore: Usado para você dizer ao ESLint que ignore arquivos e diretórios específicos;
- .eslintrc.json: Usado para você sobrescrever regras do ESLint;
---

    // .eslintignore

    node_modules

---
    // .eslintrc.json
    {
      "env": {
        "es2020": true
      },
      "extends": "trybe-backend",
      "rules": {
        "sonarjs/no-duplicate-string": ["error", 5]
      }
    }
 
Aqui, foi especificado o padrão de qualidade a ser usado - as regras de estilo de 2020, estendendo as regras da Trybe para Back-end e acrescentando uma regra em particular que usamos no projeto.

👀 Obs: Se quiser saber mais sobre estas configurações do ESLint, acesse a [documentação](https://eslint.org/docs/latest/user-guide/configuring/)


## Por fim iniciar o repositório git

    git init && touch .gitignore
----
    // .gitignore

    node_modules

## Crie o arquivo connection.js, que será responsável por realizar a conexão com o servidor MySQL utilizando a biblioteca mysql2:

No trecho de código abaixo estamos importamos a biblioteca mysql2 com o recurso de promises. Isso permitirá utilizar o MySQL de forma assíncrona com async/await. Em seguida, criamos uma constante connection que recebe um pool de conexões criado com a função createPool.

- Uma pool de conexões é um repositório que contêm um conjunto de conexões estabelecidas previamente com o banco de dados. Essas conexões serão reutilizadas durante a execução da aplicação conforme a necessidade. Em outras palavras, quando uma operação no banco de dados for necessária nossa aplicação irá:

  - Requisitar uma conexão no pool de conexões;
  - Utilizar essa conexão para enviar uma operação SQL ao servidor MySQL;
  - Devolver a conexão para o pool de conexões ao final da operação com o MySQL;
  - Tornar a conexão disponível para ser utilizada em requisições futuras.

- O uso do pool de conexões é encorajado, pois sem ele, para cada operação com o MySQL uma conexão seria aberta e, após seu uso, seria fechada. Assim, seria necessário abrir novamente uma nova conexão com o MySQL para executar uma nova operação. E abrir uma nova conexão com o MySQL demanda tempo, adicionando um atraso para cada requisição da API como consequência. Logo, o uso de um pool de conexões acelera o processo de execução de consultas no MySQL, pois reutiliza as conexões em operações futuras, não precisando criar uma nova conexão a cada operação.

Crie o arquivo src/db/connection.js já com as variáveis de ambiente a serem criadas na seção seguinte:

    //connection.js

    const mysql = require('mysql2/promise');

    const connection = mysql.createPool({
      host: process.env.MYSQL_HOST,
      port: process.env.MYSQL_PORT,
      user: process.env.MYSQL_USER,
      password: process.env.MYSQL_PASSWORD,
      database: process.env.MYSQL_DATABASE_NAME,
      waitForConnections: process.env.MYSQL_WAIT_FOR_CONNECTIONS,
      connectionLimit: process.env.MYSQL_CONNECTION_LIMIT,
      queueLimit: process.env.MYSQL_QUEUE_LIMIT,
    });

    module.exports = connection;

A função createPool recebe um objeto com os seguintes parâmetros:

 - host: O endereço IP do MySQL:

    Como temos um container docker sendo executado em nossa máquina local, o valor será localhost ou 127.0.0.1 (ambos são equivalentes).

- user: O nome de usuário que nossa aplicação utilizará para acessar o MySQL.

  Estamos utilizando o usuário root do MySQL.

- port: O número da porta que nossa aplicação utilizará para acessar o MySQL.

  Estamos utilizando a porta 33060 (a porta do computador local que vinculamos com o container no docker compose).

- password: 	A senha do usuário que nossa aplicação utilizará para acessar o MySQL.

	Estamos utilizando a senha root que foi definida na variável de ambiente MYSQL_ROOT_PASSWORD no docker compose criado anteriormente.
- database: O nome do banco de dados MySQL, o qual queremos que nossa aplicação realize uma conexão.
	
  Estamos utilizando o nome do banco que foi definido na variável de ambiente MYSQL_DATABASE no docker compose
- waitForConnections: Determina qual será a ação da pool de conexões quando nenhuma conexão estiver disponível na pool e quando o limite de criação de novas conexões tiver sido alcançado.

  Se o valor for true, será criada uma fila de espera por conexões, caso contrário a pool retornará uma callback com um erro. Caso este parâmetro for omitido, o valor padrão será true
- connectionLimit: O número máximo de requisições de conexão que a pool criará de uma vez.

  Caso este parâmetro for omitido, o valor padrão será 10
- queueLimit: O número máximo de requisições de conexão que a pool irá enfileirar antes de retornar um erro.
  
  Se o valor deste parâmetro for igual a 0 significa que não existe limite. Caso este parâmetro seja omitido, o valor padrão será 0.

## Variáveis de ambiente

Quando o código for versionado em um repositório GitHub por exemplo, esses dados estarão lá e se o repositório for PÚBLICO todas as pessoas que olharem o arquivo src/repository/connection.js verão os dados utilizados para conectar ao servidor MySQL.

Portanto devemos separar os dados de configuração (no nosso caso do servidor MySQL) da nossa aplicação Node.js e express. Para alcançar esse objetivo vamos utilizar um recurso chamado variável de ambiente. 

  - Uma variável de ambiente é um recurso disponível nos sistemas operacionais que permite criar uma variável no formato NOME_DA_VARIÁVEL=VALOR, onde NOME_DA_VARIÁVEL é o nome da variável de ambiente, e VALOR se refere a um valor que será vinculado à variável. Toda vez que solicitarmos ao sistema operacional o valor de uma variável de ambiente, fornecemos a ele uma NOME_DA_VARIÁVEL e ele retorna o VALOR associado a esta chave, se ela estiver definida.

  A biblioteca dotenv é um módulo Javascript que carrega variáveis de ambientes armazenadas em um arquivo .env para o process.env.

  Para refatorar a aplicação, primeiramente instale o módulo dotenv como dependência do projeto:

    npm i dotenv@16.0.1

Em seguida, crie o arquivo .env na raiz do projeto com o seguinte conteúdo:

    //.env

    MYSQL_HOST=localhost
    MYSQL_PORT=33060
    MYSQL_USER=root
    MYSQL_PASSWORD=root
    MYSQL_DATABASE_NAME=trybecashdb
    MYSQL_WAIT_FOR_CONNECTIONS=true
    MYSQL_CONNECTION_LIMIT=10
    MYSQL_QUEUE_LIMIT=0

⚠️ **Atenção**: NUNCA se esqueça de adicionar o arquivo .env no arquivo .gitignore

    //.gitignore

    node_modules
    .env

👀 Obs: Uma boa prática é criar um arquivo .env de exemplo. Assim, quando outras pessoas realizarem um clone do seu repositório, elas terão um exemplo das variáveis de ambientes que devem estar no arquivo .env e podem preencher com os valores pertinentes ao seu ambiente de desenvolvimento.

    //.env-example

    MYSQL_HOST=<ENDEREÇO DO BANCO>
    MYSQL_USER=<NOME DE USUÁRIO DO BANCO>
    MYSQL_USER=<PORTA DE CONEXÃO DO BANCO>
    MYSQL_PASSWORD=<SENHA DE ACESSO DO BANCO>
    MYSQL_DATABASE_NAME=<NOME DO BANCO DE DADOS>
    MYSQL_WAIT_FOR_CONNECTIONS=true
    MYSQL_CONNECTION_LIMIT=10
    MYSQL_QUEUE_LIMIT=0

- Os dados sensíveis foram substituídos por valores informativos e este arquivo pode ser versionado normalmente no GitHub sem prejuízo de vazamento de dados de acesso ao banco de dados.
  - 👀 Obs: No arquivo README.md do seu repositório crie uma seção explicando a necessidade de renomear o arquivo .env-example para .env e alterar o arquivo com os dados necessários para acessar o banco de dados.

## Criando o servidor

No diretório src e criar os arquivos com os seguintes conteúdos:

    touch app.js server.js
---
    // src/app.js
    const express = require('express');

    const app = express();

    app.use(express.json());

    module.exports = app;
---
    // src/server.js

    // a linha abaixo carrega as variáveis de ambiente definidas no arquivo .env inicializando o dotenv:

    require('dotenv').config();
    const app = require('./app');
    const connection = require('./db/connection');

    app.listen(3001, () => {
      console.log('server running on port 3001');

    // O código abaixo é só para testar a comunicação com o MySQL

      const [ result ] = await connection.execute('SELECT 1');
      if (result) {
        console.log('MySQL connection OK');
      }
    });

## Configurando os scripts

Configurar os scripts feitos até aqui no arquivo package.json:

    // package.json

    "start": "node src/server.js",
    "lint": "eslint --no-inline-config --no-error-on-unmatched-pattern -c .eslintrc.json ."

## Ganhando produtividade com Nodemon

Para não precisar ficar reiniciando o servidor a cada mudança no código, basta instalar o pacote Nodemon como dependência de desenvolvimento:

    npm i nodemon -D

- Não esquecer de configurar o script no arquivo package.json:
---
    // package.json
    "dev": "nodemon src/server.js",
