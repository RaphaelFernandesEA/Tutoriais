# Configurando o MySQL no Express

Para criar a aplicação do zero, criei o diretório que armazenará a aplicação com a pasta src

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

Crie o arquivo src/db/connection.js:


      //connection.js
      const mysql = require('mysql2/promise');

      const connection = mysql.createPool({
        host: 'localhost',
        port: 33060,
        user: 'root',
        password: 'root',
        database: 'trybecashdb',
        waitForConnections: true,
        connectionLimit: 10,
        queueLimit: 0,
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

## Cirando o servidor

No diretório src e criar dois arquivos:

    touch app.js server.js
---
    // src/app.js
    const express = require('express');

    const app = express();

    app.use(express.json());

    module.exports = app;
---
    // src/server.js
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
