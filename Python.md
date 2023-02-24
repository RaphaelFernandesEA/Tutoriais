# Preparando o ambiente Python
Versões mais atuais do ubuntu (ou similares) já vem com o python 3 instalado, e inclusive, a partir da versão 17.10, essa passa a ser a versão padrão do sistema.

Caso python 3 não esteja instalado, utilize:
***
    sudo apt install python3.
***
Para verificar se deu certo, no terminal digitar o comando abaixo para verificação de versão:
***
    python3 --version.
***

## **Pyenv**

É comum em Python precisar trabalhar com versões diferentes da linguagem, seja na atuação em múltiplos projetos, seja para estudar novas funcionalidades da linguagem que ainda estão em fase de desenvolvimento ou testes. O pyenv ajuda a lidar com isso!

Em outras palavras, pode-se ter quantas versões da linguagem quisermos ou forem necessárias, instaladas no sistema. É um papel análogo ao node_modules, do JavaScript!

### **Instalação em Linux e MacOS**

- Certificar de que a lib curl está instalada no sistema.

- Baixar e instalar o pyenv:

***
    curl https://pyenv.run | bash
***
- Reiniciar shell para que as mudanças tenham efeito:

***
    exec $SHELL
***

- Será necessário acessar o arquivo .bashrc (ou .zshrc, se você usa zsh/ohmyzsh) para adicionar algumas linhas.

👀 **Obs:** Para abrir o arquivo no local ~/.bashrc use o nano ou algum outro editor de arquivos:

***
    nano ~/.bashrc
***
- Certificar que as seguintes linhas estão no arquivo de configuração .bashrc e, caso não estejam, incluir no final do arquivo:

***
    export PYENV_ROOT="$HOME/.pyenv"
    export PATH="$PYENV_ROOT/bin:$PATH"
    if command -v pyenv 1>/dev/null 2>&1; then
      eval "$(pyenv init --path)"
    fi
***

- Abrir um novo terminal e executar o comando para verificar a instalação:

***
    pyenv
    >
***
### **Como usar**

- Para listar tudo que se pode instalar com o pyenv:

***
    pyenv install -l
***
- Exemplo de instalação de uma versão do Python 3.9.1

***
    pyenv install 3.9.1:
***

- Tornar a versão instalada a versão global de seu sistema:

***
    pyenv global 3.9.1

***
- Verificar se a versão foi setada:

***
    pyenv global
***

- Listar todas as versões que já foram baixadas:
***
    pyenv versions
***

## **Pip**

**Pip** é o gerenciador de pacotes do python. É um cliente de linha de comandos utilizado para controle das dependências do projeto. O *pip* serve para controlar a versão das bibliotecas utilizadas para desenvolvimento do sistema. O pip permite baixar uma versão específica de uma biblioteca como por exemplo ***python3 -m pip install fastapi==0.43.0***

Esta ferramenta não vem por padrão no sistema operacional Ubuntu e pode ser instalada utilizando o comando: 

***
    sudo apt install python3-pip
***

- Para verificar se a instalação deu certo digitar no terrminal: 
***
    python3 -m pip --version
***
- A saída deverá ser similar a apresentada abaixo:

***
    pip 19.2.3 from /usr/lib/python3.8/site-packages (python 3.8)
***

## **Venv**

Responsável por criar ambientes virtuais Python e provê um isolamento dos pacotes instalados e suas respectivas versões.

É um cliente de linha de comando que auxilia na separação de ambientes para diferentes projetos.

Ao iniciamos um projeto que tem uma biblioteca na versão 1.4, e de repente, um novo projeto é iniciado na versão 2.0. O que fazer? Será que são compatíveis? E se eu atualizo o sistema e a versão antiga para de funcionar?

É onde o venv entra, ele serve para isolar ambientes entre projetos, ou seja, eu consigo ter dois projetos rodando, em dois ambientes diferentes, com versões diferentes da mesma biblioteca.

**Versões atuais do Ubuntu já vem com python 3 instalado**. 
- Para as mais antigas utilize o comando:

***
    sudo apt install python3-venv.
***

- Para verificar se deu tudo certo em um terminal digite:

***
    python3 -m venv -h.
***

- A saída deverá ser similar a apresentada abaixo:

***
    usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear]
                [--upgrade] [--without-pip] [--prompt PROMPT]
                ENV_DIR [ENV_DIR ...]

    Creates virtual Python environments in one or more target directories.

    positional arguments:
      ENV_DIR               A directory to create the environment in.

    optional arguments:
    ...
***

## **Flake8**

O **Flake8** é um programa de linha de comando que verifica o código e busca por erros ou formatações que não seguem o guia de estilo padrão do python, conhecido como PEP-8. Além disso também verifica a complexidade ciclamática do seu código.

É muito comum cometermos alguns erros de sintaxe, principalmente quando ainda estamos nos familiarizando com uma linguagem nova. Assim como durante o nosso dia a dia podemos esquecer algum código não utilizado. Esta ferramenta vai analisar o seu código e procurar possíveis erros, evitando assim que só ocorram no momento em que o código for executado.

Esta ferramenta também aponta possíveis linhas que não estão seguindo o estilo de código definido para a linguagem python.

Outra coisa bem comum ao se escrever um código é que uma parte dele começa a se tornar tão complexa que há n caminhos por onde seu algoritmo pode seguir. Normalmente isto indica que deve-se modificar o código para torná-lo mais simples e legível. O Flake8 irá apontar qual parte do seu código está complexa e que deve ser modificada.

Esta ferramenta será integrada ao editor, dessa maneira, ao salvar o arquivo, teremos os erros encontrados apontados diretamente no mesmo.

O pacote flake8 pode ser instalado utilizando a ferramenta pip vista anteriormente. Será utilizado o sudo neste caso para garantir que ela esteja disponível para todos os usuários do sistema operacional. Para Linux e MacOS digitar o comando:

***
    sudo python3 -m pip install flake8
***
👀 **Obs:** No MacOS temos a opção de instalar o flake8 usando o Homebrew:

  - Caso não possua o Homebrew instalado em seu Mac, você pode instalá-lo com o comando abaixo:

        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  - Depois é só instalar o flake8:

***
    brew install flake8
***

  - Para verificar se deu tudo certo digitar o comando:

***
    python3 -m flake8 --version.
***
  - A saída deverá ser similar a apresentada abaixo:

***
    3.8.4 (mccabe: 0.6.1, pycodestyle: 2.6.0, pyflakes: 2.2.0)
***

## **Black**

O **black** é um formatador automático de código, ele irá modificar o seu código seguindo o guia de estilo do Python. Iremos configurá-lo junto ao nosso editor para que a formatação seja feita através de um atalho do teclado como shift + ctrl + i no Linux, ou Shift + Option + F no MacOS.

O pacote black pode ser instalado utilizando a ferramenta pip vista anteriormente. Vamos utilizar sudo neste caso para garantir que ela esteja disponível para todos os usuários do sistema operacional. Digite o comando:

***
    sudo python3 -m pip install black
***

👀 **Obs:** No MacOS também pode-se instalar o black usando o Homebrew:

***
    brew install black
***

- Para verificar se deu tudo certo digitar o comando:

***
    python3 -m black --version.
***

- A saída deverá ser similar a apresentada abaixo:

***
    __main__.py, version 20.8b1
***

## **VSCode(Python)**

O VSCode é um editor de texto e possui uma excelente extensão para Python que pode ser instalada através da marketplace.

O **plugin de Python para VSCode** fornece auto-complete, integração com os linters vistos anteriormente, também é uma ferramenta para depuração de código.

- Para instalar, abra o VS Code Quick Open (Ctrl+P), cole o comando a seguir e pressione enter.

***
    ext install ms-python.python
***

- Após instalar a extensão, digite ctrl + shift + p, vá em Preferences: Open Settings (JSON) e acrescente as seguintes configurações.

***
    // ...
        "python.linting.enabled": true,
        "python.linting.flake8Enabled": true,
        "python.formatting.blackArgs": [
            "-l 79"
        ],
        "python.formatting.provider": "black",
    // ...
***
- Para verificar se deu tudo certo, abra um arquivo com extensão .py no VSCode e digite o código lista = [1,2,3]. Salve o arquivo e um aviso de erro deve acontecer.

Passando o mouse sobre a linha veremos que o erro é: missing whitespace after ','flake8(E231).

⚠️ **Para corrigir e testar se o nosso formatador está funcionando corretamente, digite ctrl + shift + i. Após salvar novamente o erro deve ter desaparecido. Caso isto não aconteça certifique que tenha feitos os passos anteriormente para instalação do flake8 e black.**

## **CodeRunner**

O **CodeRunner** é uma extensão do VSCode que permite rodar códigos ou trechos de códigos em mais de 30 linguagens de programação e adicionar também comandos customizados sem sair do VSCode.
- Como instalar?

Abra o VS Code Quick Open (Ctrl+P), cole o comando a seguir e pressione enter.

***
    ext install formulahendry.code-runner
***

Após instalar a extensão, digite ctrl + shift + p, ou cmd + shift + p no MacOS, vá em Preferences: Open Settings (JSON) e acrescente as seguintes configurações.

***
    // ...

        "code-runner.executorMap": {
            "python": "python3 -u"
        },
        "code-runner.runInTerminal": true,

    // ...
***
Esta configuração garante que nosso script será executado utilizando a versão 3 do Python.

**⚠️ Para verificar se deu tudo certo, escreva um pequeno código como print("Olá Mundo") e apertando ctrl + alt + N, ou ctrl+ opt +N no MacOS, o código será executado.**

# **[Python](https://docs.python.org/pt-br/3/library/index.html)**

Um primeiro grande detalhe da linguagem **Python** é a sua simplicidade e legibilidade. Dessa forma, cabe traçar algumas especificidades da linguagem:

- Todo arquivo com extensão .py é considerado um módulo. Módulos são declarados utilizando snake case, ou seja, com nomes minúsculos e quando possuírem mais de uma palavra, devem ser separadas por **underscore (_)**.

- O **import** é utilizado para termos todas as funções do módulo disponíveis em outro arquivo. Uma outra maneira de utilizarmos é escrevendo ***from area import rectangle***, por exemplo, se quisermos importar apenas rectangle a partir de area.

**⚠️ Atenção: Tomar cuidado com conflitos de nomes caso use essa segunda maneira.**

***
**Exemplos:**

    #importa o módulo area criado com todas as suas funções
    import area 

    #importa apenas a função rectangle do modulo area
    from area import rectangle
***

- Não se faz necessário o uso do **" ; "** no final de cada linha de fim de código.

- A linguagem se baseia na identação e utiliza como padrão 4 espaços;

- Há ausência de chaves para definir blocos de funções. Para isso utiliza-se o caractere **" : "** um bloco que iniciará na pŕoxima linha.

- Entre cada função usa-se um espaço de 2 linhas;

- As funções são declaradas com nomes em letras minúsculas;

- Não é necessário a utilização de **let, var** ou **const** nas atribuições;

- Uma constante é definida em letras maiúsculas.
    - **⚠️ Aviso:** Existe uma convenção de declarar valores considerados constantes com letras maiúsculas, e o respeito por outros programadores de não alterarem aquele valor.

- O operador **" // "** realiza a divisão e arredonda o resultado para baixo. Ou seja, realiza o quociente.

- No caso de código de testes presentes nos módulos, a variável __ name__ é utilizada pelo interpretador Python para identificar o arquivo que esta sendo executado e seu valor será "__ main__" quando invocamos um módulo como script:

*** 
**Exemplo:**

    if __name__ == "__main__":
        print("Área do quadrado:", square(10))
        print("Área do retângulo:", rectangle(2, 2))
        print("Área do círculo:", circle(3))
***

## **Módulos**

Um módulo é um arquivo que contém definições e instruções em Python. O nome do arquivo é um nome acrescido de .py. Pode-se importar um módulo dentro de um outro arquivo Python e ter acesso às suas funções, classes, etc.

Em linhas gerais, todo arquivo que é escrito com a linguagem Python e com a extensão .py é considerado um módulo.

## **Pacotes**

Pacotes são módulos Python que contêm outros módulos e/ou pacotes, comumente separados por responsabilidades similares. Na prática, um pacote é um diretório que pode conter vários módulos (arquivos de extensão .py) e/ou outros pacotes.

***
Exemplo de tipos diferentes de imports de pacotes:

    import http  # importa o pacote http como um módulo

    from http import client  # importa o módulo client do pacote http

    from http.client import HTTP_PORT  # importa a constante HTTP_POST do módulo client do pacote http
***     

## **Ambiente Virtual**

Em **Python** é possível ter ter dois projetos rodando em dois ambientes diferentes, que podem ter versões diferentes de uma mesma biblioteca.

Na prática, são instaladas as bibliotecas em um diretório que está relacionado ao projeto. Assim, cada projeto pode ter suas próprias bibliotecas na versão que quiser. A ideia é a mesma do npm.

Para crição de um ambiente virtual usa-se o comando **na raiz do projeto:**

***
    python3 -m venv .venv
    # .venv é o nome do ambiente isolado
***

⚠️ *Caso o venv não esteja instalado, utilize o comando **sudo apt install python3-venv**.*

Este ambiente isolado será visto como um diretório criado na raiz do projeto. O ponto na frente do nome faz com que o diretório fique oculto.

Depois de criado, temos que ativar este ambiente para usá-lo. Isto é importante pois sempre que decidirmos trabalhar neste projeto devemos repetir este passo.

***
    source .venv/bin/activate
***
Para conferir se o comando de ativação do ambiente virtual deu certo:

***
    which python3
***
O resultado será o caminho para a pasta onde você criou seu ambiente virtual (pwd), acrescido de ***".venv/bin/python3"*** e o ambiente estará preparado para a instalação das bibliotecas que precisaremos nos projetos.

## **Entrada e saída de dados**

### **Entrada**

Uma das maneiras que existem de receber valores em nossos programas é através da função input, que vem embutida na própria linguagem. Esta função está vinculada à entrada padrão do sistema operacional e tem como parâmetro opcional o prompt que, caso seja fornecido, exibirá a mensagem passada para ele em tela. **O valor recebido através da função será do tipo texto (str):**

***
    input("Digite uma mensagem:")
***

Outra maneira de recebermos valores externos na execução de nossos programas é utilizando o módulo sys. Quando executamos um script e adicionamos parâmetros, os mesmos estarão disponíveis através de uma variável chamada sys.argv, que é preenchida sem que precisemos fazer nada. Na prática, podemos escrever o conteúdo abaixo em um arquivo e passar alguns parâmetros ao executá-lo.

***
    import sys


    if __name__ == "__main__":
        for argument in sys.argv:
            print("Received -> ", argument)
***
Executa-se o código usando os parâmetros através do comando abaixo por exemplo:
***
    python3 arquivo.py 2 4 "teste"
***
A saída será:
***
    Received ->  arquivo.py
    Received ->  2
    Received ->  4
    Received ->  teste
***

### **Saída**

A função ***print** é a principal função para se imprimir um valores em “tela”. Normalmente esta função escreve na saída padrão do sistema operacional, mas é possível modificar este e outros comportamentos.

A função recebe parâmetros de forma variável, ou seja, pode receber nenhum, um, dois ou n parâmetros durante sua invocação. 
- Seu separador padrão dos argumentos é um espaço em branco, que pode ser alterado:

***
    print("Os resultados são", 6, 23, 42)  # saída: Os resultados são 6 23 42
    print("Maria", "João", "Miguel", "Ana")  # saída: Maria João Miguel Ana
    print("Maria", "João", "Miguel", "Ana", sep=", ")  # saída: Maria, João, Miguel, Ana
***
- Além do separador, pode-se também alterar o caractere de fim de linha que, por regra, é uma quebra de linha:

***
    print("Em duas ")
    print("linhas.")

    #saída: 
    Em duas
    linhas.
***
  - Alterando o padrão:
***
    print("Na mesma", end=" ")
    print("linha.")

    #saída:
    Na mesma linha.
*** 

## **Tipos de dados embutidos**

#### **[Outros tipos de dados - aprofundamento](https://docs.python.org/3/library/datatypes.html)**

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

⚠️ **Acesso e operações:**

    fruits = ["laranja", "maçã", "uva", "abacaxi"] # elementos são definidos separados por vírgula, envolvidos por colchetes

    fruits[0]  # o acesso é feito por índices iniciados em 0

    fruits[-1]  # o acesso também pode ser negativo

    fruits.append("banana")  # adicionando uma nova fruta

    fruits.remove("abacaxi")  # removendo uma fruta baseado no critério do seu valor e não na sua posição

    del fruits[0] # remove um item da lista baseado na posição indicada 

    fruits.extend(["pera", "melão", "kiwi"])  # acrescenta uma lista de frutas a lista original

    fruits.index("maçã")  # retorna o índice onde a fruta está localizada, neste caso, 1

    item = fruits.pop(-2) #remove da lista de frutas o penúltimo item, mas não o exclui (serve para atribuir o elemento a uma varíavel).

***
⚠️ **Atenção:** O método sort(), altera a lista original ordenando-a e não serve para reatribuição em outra variável, pois não possui nada como retorno. Para isso, deve-se usar o método ***sorted()***.

***
    fruits = ["laranja", "maçã", "uva", "abacaxi"]

    fruits.sort() #ordena a lista de frutas (modificando-a) - ['abacaxi', 'laranja', 'maçã', 'uva']

    order_fruits = fruits.sort() #retorna none

    order_fruits = sorted(fruits) #retorna as frutas ordenadas na nova variável sem alterar a lista original - ['abacaxi', 'laranja', 'maçã', 'uva']

    order_fruits = sorted(fruits, reverse=True) #retorna as frutas ordenadas em ordem decrescente na nova variável sem alterar a lista original - ['uva', 'maçã', 'laranja', 'abacaxi']
***

#### **Fatiamento de listas**

Da mesma forma que no método ***range***, é possível "acessar de forma editada" os valores desejados de uma lista, serve também para strings:

***
    fruits = ["laranja", "maçã", "uva", "abacaxi"]

    fruits[0:2] # retorna ["laranja", "maçã"] - iniciando de zero té o indice 2, exclusive

    fruits[0:3:2] # retorna ["laranja", "uva"] - iniciando do indice zero, até o indice 3(exclusive), pulando de dois em dois

    fruits[::-1] # retorna os itens na ordem contrária ["abacaxi", "uva", "maçã", "laranja"]
***

### **Tuplas (tuple)**

São similares a listas, porém não podem ser modificados durante a execução do programa.

***
    **user = ("Will", "Marcondes", 42)**  # elementos são definidos separados por vírgula, envolvidos por parênteses

    user[0]  # acesso também por índices
***

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

**people_by_id = {1: "Maria", 2: "Fernanda", 3: "Felipe"}**  # elementos no formato "chave: valor" separados por vírgula, envolvidos por chaves.

Podemos percorrer os elementos de um Dicionário a partir de suas chaves **dict.keys()** ou a partir de seus valores **dict.values().**

***
⚠️ **Acesso e operações:**

    people_by_id = {1: "Maria", 2: "Fernanda", 3: "Felipe"}

    people_by_id.keys() # saída: [1, 2, 3]

    people_by_id.values() # saída: ['Maria', 'Fernanda', 'Felipe']

    # outro exemplo, dessa vez usando strings como chaves. As aspas são necessárias para que o Python não ache que `Maria`, `Fernanda` e `Felipe` sejam variáveis.
    people_by_name = {"Maria": 1, "Fernanda": 2, "Felipe": 3}

    people_by_name["Rodrigo"] = 4 # saída: {"Maria": 1, "Fernanda": 2, "Felipe": 3, "Rodrigo": 4} - adiciona uma chave e um valor ao dicionário

    # elementos são acessados por suas chaves
    people_by_id[1]  # saída: Maria

    # elementos podem ser removidos com a palavra chave del
    del people_by_id[1]

**👀 Obs:** No caso de se tentar acessar um elemento do dicionario com uma chave ***inexistente***, ocasionará um erro na aplicação. Para se evitar isso e fazer com que o programa continue rodando, deve se utilizar o método **dict.get():**

    people_by_name.get("Fábio") # saída: None - sem ocasionar erro

    # A função ainda aceita um segundo parâmetro que pode ser uma string explicando o erro

    people_by_name.get("Fábio", "Key not found") # saída: Key not found

***

  **⚠️ Atenção:** Outra forma para acessar e trabalhar as chaves e valores de um dicionário de forma individualizadas é atribui-los como tuplas através do método **dict.items().**
    
    people_by_id.items()  
    # dict_items([(1, "Maria"), (2, "Fernanda"), (3, "Felipe")])
    # um conjunto é retornado com tuplas contendo chaves e valores

---

### **Range (range)**

Estrutura capaz de gerar uma sequência numérica de um valor inicial até um valor final, modificando seu valor de acordo com o passo (step) definido. Pode ser declarado como **range( [start], stop[, step] )**, em que ***start e step*** podem ser omitidos, possuindo valores iniciais iguais a 0 e 1 respectivamente.

**👀 Obs:** O stop não é incluído na sequência, portanto, caso queira uma sequência de 1 até 10 a chamada deverá ser range(1, 11). Seus valores são criados à medida que esta sequência é percorrida.

#### **Demonstrações:**
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

**👀 Obs:** Além de listas, várias outras estruturas são iteráveis, como strings (str), tuplas (tuple), conjuntos (set), dicionários (dict) e até mesmo arquivos.

## **Compreensão de lista (list comprehension)**

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

## **Compreensão de dicionários (dict comprehension)**

Da mesma forma que na compreensão de listas, é possível fazer com dicionários. Para isso deve-se fazer a atribuição da chave e valor simultaneamente na criação do dicionário e utilizar os **":"** no lugar do **"="** para a atribuição.
***
    pessoas = [("Raphael", 1.71), ("Diogenes", 1.63), ("Bruno", 1.80)]
    dicio = {nome:altura for nome, altura in pessoas} # saída: {"Raphael": 1.71, "Diogenes": 1.63, "Bruno": 1.80}
***
👀 **Observação:** De forma similar e mais rápida, pode-se usar a função **dict()**, podendo ser usada para listas de tuplas ou listas de listas:
***
    dicio = dict(pessoas) #saída: {"Raphael": 1.71, "Diogenes": 1.63, "Bruno": 1.80}
⚠️  **Atenção:** O método só funciona com pares de valores. Sendo assim, ocasionará erro se tiver alguma estrutura com mais de dois elementos.
***
### **while**

Com o while pode-se executar um conjunto de declarações enquanto a condição for verdadeira. No código abaixo é implementada uma Sequência de Fibonacci, presente em diversas formas na natureza. É uma sequência numérica começando por 0 e 1, e cada termo subsequente corresponde à soma dos dois anteriores:

---

    n = 10
    last, next = 0, 1
    while last < n:
        print(last)
        last, next = next, last + next

---

👀 Neste caso, foi utilizado um truque chamado ***atribuição múltipla***. Isto é, atribuição de vários valores a múltiplas variáveis ao mesmo tempo. Pode ser utilizado também para fazer a troca de valores entre variáveis: 
      
---
    a, b = b, a

---

### **all**
Retorna True se todos metodos booleanos forem True.

**👀 Obs:** Em valores numéricos retorna false para o número 0.
***
    languages = ['Python', 'Java', 'JavaScript']
    languages2 = ['Python', 'Java', 'JavaScript', '']

    test = all(languages)  # retorna true

    tes2 = all(languages2)  # retorna false
***

### **any**
Retorna True se algum dos metodos booleanos for True.

***
    languages = ['Python', 'Java', 'JavaScript']
    languages2 = ['Python', 'Java', 'JavaScript', '']

    test = all(languages)  # retorna true

    tes2 = all(languages2)  # também retorna true
***

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

### **Counter**
O método counter é uma classe que cria, a partir de um objeto iterável (lista), um dicionário com o número de repetições de cada elemento presente na lista.

***
**Exemplo:**

    from collections import Counter

    numbers = [1, 1, 1, 2, 3, 4, 5, 5, 6, 6, 6, 6, 7, 8, 8, 9, 9, 9, 9]

    conter = Counter(numbers)
    print(counter)

    #saída Counter({6: 4, 9: 4, 1: 3, 5: 2, 8: 2, 2: 1, 3: 1, 4: 1, 7: 1})

**👀 Obs:** Por ser um dicionário, ele não apresenta os números no resultado ordenados pela ordem em que aparecem e sim pela quantidade de ocorrências. 

    print(counter[1]) #saída 3 => por que o número 1 aparece 3 vezes, não fazendo referência ao segundo elemento da lista de fato. 
#### **.most_common()**

O método .most_common() retorna uma lista de duplas com a ordem dos elementos mais comuns da lista pela ordem de ocorrências apresentando o elemento e seu número de ocorrências.

    mais_comum = counter.most_common()

    #saída [(6, 4), (9, 4), (1, 3), (5, 2), (8, 2), (2, 1), (3, 1), (4, 1), (7, 1)]


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

## **PEP 257 - Convenções Docstring**

As **docstrings do Python** são os literais de string que aparecem logo após a definição de uma função, método, classe ou módulo. O objetivo deste PEP é padronizar a estrutura de alto nível das docstrings: o que elas devem conter e como dizê-lo (sem tocar em nenhuma sintaxe de marcação dentro das docstrings). O PEP contém convenções, não leis ou sintaxe.

***
Exemplo:

    def quadrado(n):
        '''Recebe um número n, retorna o quadrado de n''' # Literal de string
        return n**2

Dentro das aspas triplas está a docstring da função quadrado() como aparece logo após sua definição.

**👀 Obs:** Pode-se também usar aspas """ triplas para criar docstrings.
***

### **Atributo __ doc__ do Python**
Como mencionado anteriormente, as docstrings do Python são strings usadas logo após a definição de uma função, método, classe ou módulo (como no exemplo anterior). Eles são usados para documentar nosso código.

[Documentação Python Docstrings](https://peps.python.org/pep-0257/)

Podemos acessar essas docstrings usando o atributo __ doc__.

***
    def quadrado(n):
        '''Recebe um número n, retorna o quadrado de n''' # Literal de string
        return n**2

    print(quadrado.__doc__)

    # Saída
    Recebe um número n, retorna o quadrado de n
