# Criando servidor Node.js

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

## Instale o Express na aplicação:

    npm i express@4.17

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

👀 Obs: Mais sobre estas configurações do ESLint -->>   [documentação ESLint.](https://eslint.org/docs/latest/user-guide/configuring/)


## Por fim iniciar o repositório git

    git init && touch .gitignore
----
    // .gitignore

    node_modules

## Cirando o servidor

No diretório src e criar dois arquivos:

    touch app.js server.js
---
    // src/app.js
    const express = require('express');

    const app = express();

    module.exports = app;
---
    // src/server.js
    const app = require('./app');

    app.listen(3001, () => console.log('server running on port 3001'));

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
