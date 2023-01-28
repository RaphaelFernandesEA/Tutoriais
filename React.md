# React

O [React](https://pt-br.reactjs.org/) é, atualmente, uma das principais bibliotecas Javascript para construção de interfaces de usuário. Esta poderosa ferramenta foi criada pelos times de desenvolvimento do Facebook com objetivo de organizar, componentizar e, consequentemente, tornar muito mais eficiente cada parte das aplicações que a utilizam.

A ideia principal é tornar possível dividir a aplicação em pequenos blocos, reutilizáveis ou não, que podem fazer a gestão das suas próprias informações através do seu estado, ou seja, reagir a eventos, interações, dados, etc. Toda vez que houver uma mudança em um componente, o React atua especificamente na renderização dele, sem que seja necessário atualizar os outros blocos.

## Criando aplicações em React

Para criar aplicações React , utilizamos o pacote create-react-app. Como ele é um pacote que tem como função a criação de todos os arquivos necessários para termos uma aplicação React, não precisamos instalá-lo. Desta forma, criaremos ela executando o seguinte comando:

    npx create-react-app nome-da-aplicacao

Após o NPX terminar de executar, perceba que um novo diretório foi criado com o nome da aplicação que você utilizou ao executar o comando acima, contendo todos os arquivos necessários de uma aplicação React.

    npm start 
    
    // O comando npm start é um script predefinido pelo React que inicia o servidor da sua aplicação. Utilizando esse comando, uma nova página deverá abrir no seu navegador, contendo a sua aplicação.

## Extensão JSX

Por ser um código Javascript, o JSX permite injeções de algoritmos dentro da estrutura HTML. Portanto, é possível que se aplique diretamente na estrutura da aplicação códigos que renderizarão outras diversas expressões, por exemplo:

    const nome = 'Jorge Maravilha';
    const element = <h1>Hello, {nome}</h1>;

    function nomeCompleto (nome, sobrenome) {
    return `${nome} ${sobrenome}`;
    }

    const element = <h1>Hello, {nomeCompleto('Jorge', 'Maravilha')}</h1>;

    function helloWorld (nome, sobrenome) {
      return <h1>Hello, {`${nome} ${sobrenome}`}</h1>;
    }

    const element = helloWorld('Jorge', 'Maravilha');
    const container = <div>{element}</div>;

⚠️  Atenção: No JSX é necessário substituir **class** por **className**, para evitar conflitos entre o Javascript e o HTML, mas também podemos utilizar expressões Javascript para atribuir valor à este atributo.

    const nome = 'Jorge Maravilha';
    const classe = 'hello-class';
    const element = <h1 className={classe}>Hello, {nome}</h1>;

## CSS e import

Para importar um arquivo que está dentro do próprio projeto ou que esteja em uma biblioteca externa, você pode utilizar o import, com a seguinte sintaxe:

    import React from 'react' 
    // importando de uma biblioteca
    import Header from './components/Header.js' 
    // importando de um caminho relativo

Caso você queira importar algo que não seja a exportação default, será necessário colocar o nome do que está sendo importado entre chaves:
    
    import { myImport } from 'file';

### Para o Arquivo CSS:
    import './App.css';

### Estrutra básica de um componente de classe no React:
  #### 👀 Atentar que o que ficar dentro do return que será renderizado
    import React from 'react';

    class ReactClass extends React.Component {
      render() {
        return (
          <h1>My first React Class Component!</h1>
        )
      }
    }

    export default ReactClass;

### Estrutra básica de um componente funcional no React

    import React from 'react';
    import ReactClass from './ReactClass'

    function App() {
      return (
        <span className="HelloWorld> Hello, world! </span>
        <ReactClass />
        )
    }

    export default App;

⚠️ O nome do componente começa com letra maiúscula, pois é uma convenção importante do React, para diferenciar os componentes dos elementos HTML.

⚠️ Atenção: Para renderização de listas, o React alerta de que uma key deve ser definida para cada item renderizado. Essas keys são importantes para o React identificar, com precisão, quais itens foram adicionados, removidos ou alterados. Vale ressaltar que não é recomendado o uso de índices como keys em listas que possibilitam a alteração na ordem dos itens, pois podem impactar negativamente o desempenho da aplicação ou gerar problemas relacionados ao estado do componente.

## Props

Pelas props é que são passados os valores para o componente, e é como o torna reutilizável em diferentes contextos.

 Um componente Greeting ficaria assim:
    import React from 'react';

    class Greeting extends React.Component {
      render() {
        const { name, lastName } = this.props;
        return <h1>Hello, {name} {lastName}</h1>;
      }
    }

    export default Greeting;

Sua chamada seria:

    import React from 'react';
    import Greeting from './Greeting';

    class App extends React.Component {
      render() {
        return (
          <main>
            <Greeting name="Samuel" lastName="Silva" />
          </main>
        );
      }
    }

    export default App;

## Checagem de tipos - PropTypes

A checagem de tipos ajuda a previnir cenários como esse, pois verifica os tipos das props passadas para um componente durante o desenvolvimento e levanta um warning se algo não estiver como planejado. 

👀 Obs: Caso não tenha utilizado o create-react-app para preparar o aplicativo React, será necessário o download da depedência externa do PropTypes através do seguinte comando:

    npm install --save-dev prop-types

- O primeiro passo para utilizar o prop-types é importá-lo no componente:

- Em seguida, para executarmos a checagem de tipos no componente Greeting, adicionamos a seguinte estrutura **ANTES** do export default:

---
Exemplo prático: 

    import React from 'react';
    import PropTypes from 'prop-types';

    class Greeting extends React.Component {
      render() {
        const { name, lastName } = this.props;
        return (<h1>Hello, {name} {lastName}</h1>);
      }
    }

    Greeting.propTypes = {
      name: PropTypes.string,
      lastName: PropTypes.string,
    };

    export default Greeting;