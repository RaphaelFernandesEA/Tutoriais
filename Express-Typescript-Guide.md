# Configurando aplicação Express com Typescript

## **Configurando o ambiente de desenvolvimento**
---

Para criar a aplicação do zero, crie o diretório que armazenará a aplicação com a pasta src e inicie a aplicação node:

    mkdir nome-do-projeto
    cd nome-do-projeto

    npm init -y

Adicionar o suporte ao TypeScript ao projeto, para isso instalar o pacote npm do TypeScript como dependência de desenvolvimento do projeto. Lembrando que em produção sempre iremos usar o código compilado de TypeScript para JavaScript, por isso utilizamos como dependência de desenvolvimento.
Com isso conseguimos garantir que todas as pessoas que vão trabalhar nesse projeto estejam sempre executando uma mesma versão, evitando possíveis incompatibilidades, caso uma tenha uma versão diferente da outra.

    npm install -D typescript

Gere o arquivo tsconfig.json:

    tsc --init

    OU caso queira utilizar o tsc como um executável npx:
    
    npx tsc --init

Configure o arquivo tsconfig.json:

    {
      "compilerOptions": {
        "module": "commonjs",
        "target": "es6",
        "rootDir": "./",
        "outDir": "./dist",
        "esModuleInterop": true,
        "strict": true
      }
    }


Instalar como dependência de desenvolvimento o pacote npm de declarações de tipos para os módulos padrões do Node.

    npm install -D @types/node

### **Ganhando produtividade com ts-node-dev**
---

Instale o ts-node-dev, que é um pacote de utilitários ajuda a executar o servidor de desenvolvimento, escrito em TypeScript, diretamente no terminal, sem necessidade de se compilar o código em JavaScript, além de reiniciar o servidor a cada alteração feita, sem a necessidade de encerramento do processo e o inicio novamente.

    npm install -D ts-node-dev

## **Instalando o Express e inicializando a aplicação**
---

Instale o pacote Express:

    npm install express

E posteriormente instale o pacote npm de declarações de tipos do Express:

    npm install -D @types/express

### **Criando a aplicação Express**
---
Para criar a aplicação Express, crie um arquivo chamado index.ts na raiz do diretório do projeto, com o seguinte conteúdo:

    touch index.ts
---

    // ./index.ts

    import express from 'express';
    import statusCodes from './statusCodes';

    const app = express();

    app.use(express.json());

    const PORT = 8000;

    app.get('/', (req, res) => {
      res.status(statusCodes.OK).send('Express + TypeScript')
    });

    app.listen(PORT, () => {
      console.log(`Server is running at http://localhost:${PORT}`);
    });