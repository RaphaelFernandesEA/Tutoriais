# Criando uma conexão no MongoDB usando Mongoose

Assim como qualquer outro pacote do Node.js, o Mongoose precisa ser instalado. Para instalá-lo, podemos acessar a [documentação](https://mongoosejs.com/docs/guide.html) e já teremos uma breve explicação de como podemos instalar e usar esse pacote. 

    npm install mongoose@6.1.8

Pensando no código da aplicação, criar um arquivo chamado connection.ts

    import { connect } from 'mongoose'

      const options = {
      user: 'user', // Usuário do banco de dados.
      pass: 'password', // senha do usuário do banco de dados.
      dbName: 'trixDB', // Define qual banco de dados você irá utilizar.
    };

    connect('mongodb://localhost:27017/', options);

    
O método connect() não é a única forma para trabalhar com conexões usando o Mongoose. Para conhecer mais detalhes sobre esse e outros métodos de conexão, seção de [Conexões na documentação do Mongoose](https://mongoosejs.com/docs/connections.html).

# Schemas & Model

## Schema:

Um schema pode ser visto como um molde de uma coleção, e será responsável por descrever toda a estrutura dos dados. Portanto, precisamos de um molde para cada tipo de coleção que teremos em nossa base de dados.

    import { Schema } from 'mongoose';

    const petSchema = new Schema({
      name: { type: String, required: true },
      species: { type: String, required: true },
      age: { type: Number, required: false },
      weight: { type: Number, required: true },
      dailyMealsNumber: { type: Number, required: true, min: 2, max: 5 },
    });

## Model

Definido o Schema, precisa-se pensar na Model para a Collection. A Model irá prover todas as funções necessárias para acessar e manipular os dados (Documents) da Collection. 

    import { Schema, model } from 'mongoose';

     const petSchema = new Schema({
       name: { type: String, required: true },
       species: { type: String, required: true },
       age: { type: Number, required: false },
       weight: { type: Number, required: true },
       dailyMealsNumber: { type: Number, required: true, min: 2, max: 5 },
     });


    const Pet = model('Pet', petSchema);

Afunção model(), usada no trecho de código anterior, cria uma Model para uma Collection. Essa função recebe como parâmetros, e nessa ordem, uma String contendo o nome da Collection e o Schema com o “molde” definido anteriormente.

Na primeira vez que essa Model for utilizada, o Mongoose se encarregará de criar toda a estrutura no MongoDB, ou seja, se a Collection ainda não existir, o Mongoose irá criá-la no banco de dados. Posteriormente, essa mesma model será utilizada para acessar os recursos fornecidos pelo MongoDB através do Mongoose. 😃

Vale lembrar que, quando você definir a String com o nome da Collection, esse nome sofrerá pequenas alterações no MongoDB, realizadas pelo Mongoose. Por exemplo, o nome <strong>Pet </strong>será modificado para <strong>pets </strong>(em caixa baixa e no plural).