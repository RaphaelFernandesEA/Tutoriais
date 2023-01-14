# Projetos em Typescript

👀 Obs: Interessante já ter iniciado um pacote Node.js  do projeto anteriormente.

O que define que um projeto é TypeScript é a presença de um arquivo de configuração TSConfig. O arquivo tsconfig.json possui as variáveis de configuração que definirão como o nosso código será compilado.

👀 Obs: A melhor prática para a utilização do Typescript em um projeto é instalá-lo como uma devDependency por meio do comando: 

    npm i -D typescript 

E utilizá-lo por meio do npx. Isso garante que todas as pessoas que forem compilar o projeto o façam utilizando a mesma versão do TypeScript, e não a versão instalada em suas respectivas máquinas.

Para gerar o tsconfig.json vamos utilizar o tsc. Caso tenha instalado o compilador globalmente em sua máquina:

    tsc --init

OU caso queira utilizar o tsc como um executável npx:

    npx tsc --init

O arquivo gerado traz as principais configurações e um comentário à frente de cada linha dizendo o que aquela configuração em específico faz e quais são os valores aceitos. A seguir as principais configurações: 

- module: especifica o sistema de módulo a ser utilizado no código JavaScript que será gerado pelo compilador como sendo o CommonJS;
- target: define a versão do JavaScript do código compilado como ES6;
- rootDir: define a localização raiz dos arquivos do projeto;
- outDir: define a pasta onde ficará nosso código compilado;
- esModuleInterop: habilitamos essa opção para ser possível compilar módulos ES6 para módulos CommonJS;
- strict: habilitamos essa opção para ativar a verificação estrita de tipo;
- include: essa chave vai depois do objeto CompilerOptions e com ela conseguimos incluir na compilação os arquivos ou diretórios mencionados; e
- exclude: essa chave também vai depois do objeto CompilerOptions e com ela conseguimos excluir da compilação os arquivos mencionados.

Também podemos utilizar uma configuração base para o ambiente JavaScript (versão do Node) que estamos utilizando provida pela própria equipe de desenvolvimento do TypeScript por meio de um repositório no GitHub. Não existe uma versão base para todos os ambientes JavaScript, apenas para os mais recentes. Com node, é possível utilizar a partir da versão 12.

Por exemplo, se estivermos desenvolvendo um projeto que usará a versão 16 do Node, podemos utilizar o módulo base @typescript/node16.

    npm i -D @tsconfig/node16

Complementando as configurações iniciais, o arquivo tsconfig.json dev fiar parecido com:

    {
    "extends": "@tsconfig/node16/tsconfig.json",
    "compilerOptions": {
        "target": "es2016",                                 
        "module": "commonjs",
        "rootDir": "./",
        "outDir": "./dist",
        "preserveConstEnums": true,
        "esModuleInterop": true,
        "forceConsistentCasingInFileNames": true,
        "strict": true,
        "skipLibCheck": true
    },
    "include":["src/**/*"], /* aqui estamos incluindo todos os arquivos dentro da pasta src */
    "exclude": ["node_modules", "**/*.spec.ts"] /* aqui estamos excluindo a pasta node_modules e os arquivos de teste */
    }

Por fim, instalar o pacote npm com as definições de tipos para o Node.js.

    npm install -D @types/node

Após a edição dos arquivos e comando a sequir irá compilar o programa:

    npx tsc

Os arquivos JavaScript foram gerados dentro do diretório dist. Agora, basta rodar o programa compilado utilizando o Node.

    node ./dist/index.js
