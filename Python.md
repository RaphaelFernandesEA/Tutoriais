# Python

Um primeiro grande detalçhe da linguagem **Python** é a sua simplicidade e legibilidade. Dessa forma, cabe traçar algumas especificidades da linguagem:

-  Não é necessário a utilização de **let, var** ou **const** nas atribuições;
- Não se faz necessário o uso do **" ; "** no final de cada linha de fim de código.
- A linguagem se baseia na identação e utiliza como padrão 4 espaços;
- Há ausência de chaves para definir blocos de funções. Para isso utiliza-se o caractere **" : "** um bloco que iniciará na pŕoxima linha.
- O operador **" // "** realiza a divisão e arredonda o resultado para baixo. Ou seja, realiza o quociente.

## **Tipos de dados embutidos**

### **Booleanos (bool)**

Os valores booleanos **True** e **False** pertencem ao tipo embutido bool e deve-se ter atenção ao início maiúsculo dessas palavras reservadas.

### **Números inteiros (int)**

O tipo numérico **int** representa um número inteiro, ou seja, é escrito sem parte fracionária.

### **Números fracionários (float)**

O tipo numérico **float**, também conhecido por ponto flutuante, representa um número decimal ou fracionário.

### **Strings (str)**

**str** representa uma cadeia de caracteres ou, como popularmente conhecida, uma string. As strings são definidas envolvendo um valor com aspas simples ou duplas.

### **Listas (list)**

Uma lista é uma sequência mutável e ordenada de elementos. Ela pode armazenar elementos heterogêneos, ter seu tamanho variável e crescer à medida que itens são adicionados.


**fruits = ["laranja", "maçã", "uva", "abacaxi"]** # elementos são definidos separados por vírgula, envolvidos por colchetes

⚠️ **Acesso e operações:**

    fruits[0]  # o acesso é feito por índices iniciados em 0

    fruits[-1]  # o acesso também pode ser negativo

    fruits.append("banana")  # adicionando uma nova fruta

    fruits.remove("abacaxi")  # removendo uma fruta

    fruits.extend(["pera", "melão", "kiwi"])  # acrescenta uma lista de frutas a lista original

    fruits.index("maçã")  # retorna o índice onde a fruta está localizada, neste caso, 1

    fruits.sort()  # ordena a lista de frutas

### **Tuplas (tuple)**

São similares a listas, porém não podem ser modificados durante a execução do programa.

**user = ("Will", "Marcondes", 42)**  # elementos são definidos separados por vírgula, envolvidos por parênteses

    user[0]  # acesso também por índices

### **Conjuntos (set)**

Um conjunto é uma coleção de elementos únicos e não ordenados. Conjuntos implementam operações de união, intersecção e outras.

**permissions = {"member", "group"}**  # elementos separados por vírgula, envolvidos por chaves

⚠️ **Acesso e operações:**
***
    permissions.add("root")  # adiciona um novo elemento ao conjunto

    permissions.add("member")  # como o elemento já existe, nenhum novo item é adicionado ao conjunto

    permissions.union({"user"})  # retorna um conjunto resultado da união

    permissions.intersection({"user", "member"})  # retorna um conjunto resultante da intersecção dos conjuntos

    permissions.difference({"user"})  # retorna a diferença entre os dois conjuntos
***

### **Conjuntos imutáveis (frozenset)**

É uma variação do set, porém imutável, ou seja, seus elementos não podem ser modificados durante a execução do programa.

**permissions = frozenset(["member", "group"])**  # assim como o set, qualquer estrutura iterável pode ser utilizada para criar um frozenset

⚠️ **Acesso e operações:**
***
    permissions.union({"user"})  # novos conjuntos imutáveis podem ser criados à partir do original, mas o mesmo não pode ser modificado

    permissions.intersection({"user", "member"})  # retorna um conjunto resultante da intersecção dos conjuntos

    permissions.difference({"user"})  # retorna a diferença entre os dois conjuntos
***
### **Dicionários (dict)**

Estrutura que associa uma chave a um determinado valor. É a representação do tão famoso objeto que utilizamos em JavaScript.

**people_by_id = {1: "Maria", 2: "Fernanda", 3: "Felipe"}**  # elementos no formato "chave: valor" separados por vírgula, envolvidos por chaves

⚠️ **Acesso e operações:**
***

    # outro exemplo, dessa vez usando strings como chaves. As aspas são necessárias para que o Python não ache que `Maria`, `Fernanda` e `Felipe` sejam variáveis.
    people_by_name = {"Maria": 1, "Fernanda": 2, "Felipe": 3}

    # elementos são acessados por suas chaves
    people_by_id[1]  # saída: Maria

    # elementos podem ser removidos com a palavra chave del
    del people_by_id[1]
---

  **⚠️ Atenção:**

  ---
    
    people_by_id.items()  
    # dict_items([(1, "Maria"), (2, "Fernanda"), (3, "Felipe")])
    # um conjunto é retornado com tuplas contendo chaves e valores

---

### **Range (range)**

Estrutura capaz de gerar uma sequência numérica de um valor inicial até um valor final, modificando seu valor de acordo com o passo (step) definido. Pode ser declarado como **range( [start], stop[, step] )**, em que ***start e step*** podem ser omitidos, possuindo valores iniciais iguais a 0 e 1 respectivamente.

**👀 Observação:** O stop não é incluído na sequência, portanto, caso queira uma sequência de 1 até 10 a chamada deverá ser range(1, 11). Seus valores são criados à medida que esta sequência é percorrida.

**Demonstrações:**

---

    # vamos converter o range em uma lista para ajudar na visualização

    # definimos somente o valor de parada
    list(range(5))  # saída: [0, 1, 2, 3, 4]

    # definimos o valor inicial e o de parada
    list(range(1, 6))  # saída: [1, 2, 3, 4, 5]

    # definimos valor inicial, de parada e modificamos o passo para 2
    list(range(1, 11, 2))  # saída: [1, 3, 5, 7, 9]

    # podemos utilizar valores negativos para as entradas também
    list(range(10, 0, -1))  # saída: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
---
**⚠️ Atenção:**  Além dos tipos básicos, temos outros como datas, tuplas nomeadas, arrays, enumerações e outros, mas estes têm de ser importados de seus respectivos módulos.

### **Método type()**

O método type(operando) corresponde ao operador typeof operando no JavaScript.

### **Método help()**

- Assim como qualquer linguagem de programação, Python também possui uma grande quantidade de comandos. Para ajudar a saber o que cada comnado faz, podemos digitar **help()** dentro da linha de comandos do Python que ele nos dará detalhes do comando passado por parâmetro.

---

      Exemplo:
        help(list)

---
## **Estrutura condicional -  if / elif / else**

- Diferentemente do **Javascriptt**, no **Python** no encadeamento de condicionais, usamos o **elif** no ludar do ***else if***.
- Outro detalhe é a ausência de chaves para definir o bloco. Utiliza-se o caractere **:** para indicar abertura de um bloco e somente indentação para indicar o término.
- Em **Python** não existe a estrutura do ***switch***.

⚠️ Aviso: O bloco **else** será executado se nenhuma das condições anteriores for satisfeita.

## **Estruturas de repetição**

### **for**

Dado que a maior parte do tempo estamos percorrendo estruturas, os criadores do Python decidiram que o ***for each*** seria o laço de repetição principal na linguagem.

- Usa-se a palavra reservada **for**, atribui-se um nome para representar o elemento da iteração do conjunto e define o que se fazer em cada lastro de repetição.

**Exemplo:**

---
    restaurants = [
    {"name": "Restaurante A", "nota": 4.5},
    {"name": "Restaurante B", "nota": 3.0},
    {"name": "Restaurante C", "nota": 4.2},
    {"name": "Restaurante D", "nota": 2.3},
    ]

    filtered_restaurants = []
    min_rating = 3.0

    for restaurant in restaurants:
        if restaurant["nota"] > min_rating:
            filtered_restaurants.append(restaurant)

    print(filtered_restaurants)  # imprime a lista de restaurantes, sem o B e D
---

**👀 Observação:** Além de listas, várias outras estruturas são iteráveis, como strings (str), tuplas (tuple), conjuntos (set), dicionários (dict) e até mesmo arquivos.

### **Compreensão de lista (list comprehension)**

A compreensão de listas em Python possui uma sintaxe fácil e compacta para criação de listas, seja a partir de uma string ou de outra lista. É uma maneira concisa de criação que executa uma operação em cada item da lista já existente. A compreensão de lista é equivalente às operações de **map** e **filter** em JavaScript.

- A compreensão de listas é declarada da mesma maneira que uma lista comum, porém no lugar dos elementos nós colocamos a iteração que vai gerar os elementos da nova lista.

    - Define o elemento e depois se faz a validação/atribuição do que será aquele elemento dentro da lista prévia.
---
**Exemplos:**

      min_rating = 3.0
      
      filtered_restaurants = [restaurant
                              for restaurant in restaurants
                              if restaurant["nota"] > min_rating]

      print(filtered_restaurants)  # imprime a lista de restaurantes, sem o B e D

Listando somente o nome dos restaurantes:

---

    # min_rating = 3.0

    # aqui pedimos somente o nome do restaurante
    filtered_restaurants = [restaurant["name"]
                            for restaurant in restaurants
                            if restaurant["nota"] > min_rating]

    print(filtered_restaurants)  # imprime a lista de nomes dos restaurantes, sem o B e D

---
A compreensão de listas também funciona com listas de strings. A seguinte cria uma nova lista de strings com os nomes que contém a letra ‘a’:

---

    names_list = ['Duda', 'Rafa', 'Cris', 'Yuri']
    new_names_list = [name for name in names_list if 'a' in name]

    # Aqui o for percorre cada nome em "names_list", verifica se existe a letra "a" nele, o adiciona à variável "name", e então gera nossa nova lista "new_names_list"
    
    print(new_names_list)    # Saída ['Duda', 'Rafa']

---

Uma compreensão de listas pode também para criar uma lista com o quadrado dos números entre 1 e 10.

---

    quadrados = [x*x for x in range(11)]
    print(quadrados)

    # Saída
    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
---

### **while**

Com o while pode-se executar um conjunto de declarações enquanto a condição for verdadeira. No código abaixo é implementada uma Sequência de Fibonacci, presente em diversas formas na natureza. É uma sequência numérica começando por 0 e 1, e cada termo subsequente corresponde à soma dos dois anteriores:

---

    n = 10
    last, next = 0, 1
    while last < n:
        print(last)
        last, next = next, last + next

---

👀 Neste caso, foi utilizado um truque chamado atribuição múltipla. Isto é, atribuição de vários valores a múltiplas variáveis ao mesmo tempo. Pode ser utilizado também para fazer a troca de valores entre variáveis: 
      
---
    a, b = b, a

---    
### **enumerate**

Em Python, um loop for geralmente é escrito como um loop sobre um objeto iterável. Isso significa que não precisa de uma variável de contagem para acessar itens no iterável.

No caso de se querer uma variável que muda em cada iteração do loop. Em vez de se criar e incrementar uma variável, pode-se usar enumerate() do Python para obter um contador e o valor do iterável ao mesmo tempo!

---

    languages = ['Python', 'Java', 'JavaScript']

    enumerate_prime = enumerate(languages)

    # converte um objeto enumerate em uma lista
    print(list(enumerate_prime))

    # Saída: [(0, 'Python'), (1, 'Java'), (2, 'JavaScript')]
---
pode-se também desestruturar (unpack) os itens da lista ou tupla:

---

    languages = ['Python', 'Java', 'JavaScript']

    for index, language in enumerate(['Python', 'Java']):
        print(f'{index} - {language}')

    # Saída:
    0 - Python
    1 - Java

---
👀 **Obs:** A letra ***f*** usada dentro do print é chamada de **f-string.** Ela fornece uma maneira de incorporar expressões dentro de strings literais, usando uma sintaxe mínima.

## **Funções**

As **funções** são definidas através da palavra reservada ***def***, seguida por um nome e os parâmetros entre parênteses. Como todo bloco de código em Python, o caractere : define o início do bloco, e a indentação define seu fim.

- Seus parâmetros podem ser passados de forma:

  - **posicional:** são aqueles definidos por meio da posição em que cada um é passado;
  - **nomeada:** são definidos por meio de seus nomes.

---
    def soma(x, y):
        return x + y

    soma(2, 2)  # os parâmetros aqui são posicionais

    soma(x=2, y=2)  # aqui estamos nomeando os parâmetros

- Os parâmetros também podem ser variádicos, ou seja, variam em sua quantidade.
Parâmetros posicionais variádicos são acessados como uma tupla no interior de uma função, e parâmetros nomeados variádicos como um dicionário.

***
    # Equivalente a um ", ".join(strings), que concatena os elementos de um iterável em uma string utilizando um separador
    # Nesse caso a string resultante estaria separada por vírgula

      def concat(*strings):
          final_string = ""
          for string in strings:
              final_string += string
              if not string == strings[-1]:
                  final_string += ', '
          return final_string


    # pode ser chamado com 2 parâmetros

      concat("Carlos", "Cristina")  # saída: "Carlos, Cristina"

    # pode ser chamado com um número n de parâmetros

      concat("Carlos", "Cristina", "Maria")  # saída: "Carlos, Cristina, Maria"

    # dict é uma função que já vem embutida no python

      dict(nome="Felipe", sobrenome="Silva", idade=25)

    # cria um dicionário utilizando as chaves passadas

      dict(nome="Ana", sobrenome="Souza", idade=21, turma=1) 
      # o número de parâmetros passados para a função pode variar
***
As variáveis definidas dentro das funções tem escopo local. Porém, quando uma função não encontra um nome no escopo local, ela irá procurar no espaço de nomes global.

Em alguns casos, podemos querer limitar um parâmetro em nomeado ou posicional para evitar ambiguidades e/ou aumentar legibilidade.

***
    len([1, 2, 3, 4])  # função len não aceita argumentos nomeados

    len(obj=[1, 2, 3, 4])  # este código irá falhar

    print("Coin", "Rodrigo", ", ")  # imprime Coin Rodrigo ,

    print("Coin", "Rodrigo", sep=", ")  # nomeando o terceiro parâmetro, agora temos a saída: Coin, Rodrigo
    
    print("Jorge", "Rodrigo", "Bruno", sep=", ") # imprime: Jorge, Rodrigo, Bruno
    ***
