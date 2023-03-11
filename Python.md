# Preparando o ambiente Python
Versões mais atuais do ubuntu (ou similares) e Mac já vem com o python 3 instalado, e inclusive, a partir da versão 17.10, essa passa a ser a versão padrão do sistema.

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

Depois de criado, tem-se que ativar este ambiente para usá-lo. Isto é importante pois sempre que decidirmos trabalhar neste projeto devemos repetir este passo.

***
    source .venv/bin/activate
***
Para conferir se o comando de ativação do ambiente virtual deu certo:

***
    which python3
***
O resultado será o caminho para a pasta onde você criou seu ambiente virtual (pwd), acrescido de ***".venv/bin/python3"*** e o ambiente estará preparado para a instalação das bibliotecas que precisaremos nos projetos.

Quando precisar desativar o ambiente virtual, execute o comando:
***
    deactivate
***
**⚠️ Atenção:** Lembrar de ativar novamente quando voltar a trabalhar no projeto.

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

A função **print** é a principal função para se imprimir um valores em “tela”. Normalmente esta função escreve na saída padrão do sistema operacional, mas é possível modificar este e outros comportamentos.

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

### **Desempacotamento de valores**

O desempacotamento de valores é um recurso muito útil de Python quando queremos separar os valores recebidos em variáveis diferentes. Quando há uma atribuição múltipla e o valor da direita pode ser percorrido, o Python entende que deve atribuir cada um dos valores a uma variável da esquerda, seguindo a ordem.

***
    a, b = "cd"
    print(a)  # saída: c
    print(b)  # saída: d

    head, *tail = (1, 2, 3) # Quando um * está presente no desempacotamento, os valores são desempacotados em formato de lista.
    print(head)  # saída: 1
    print(tail)  # saída: [2, 3]
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

**str** representa uma cadeia de caracteres ou, como popularmente conhecida, uma string. As strings são definidas envolvendo um valor com aspas simples ou duplas. Sabemos que por vezes valores numéricos podem ser passados como strings e para contornar tal situação, o método **isdigit**, embutido no tipo **str**, pode ser utilizado para verificar se a string corresponde a um número natural.

***
    string.isdigit()    # O método isdigit() retorna True se todos os caracteres forem dígitos, caso contrário, False.
***

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

⚠️ **Acesso e operações:**
***
    permissions = {"member", "group"}  # elementos separados por vírgula, envolvidos por chaves

    permissions.add("root")  # adiciona um novo elemento ao conjunto

    permissions.add("member")  # como o elemento já existe, nenhum novo item é adicionado ao conjunto

    permissions.union({"user"})  # retorna um conjunto resultado da união

    permissions.intersection({"user", "member"})  # retorna um conjunto resultante da intersecção dos conjuntos

    permissions.difference({"user"})  # retorna a diferença entre os dois conjuntos
***

### **Conjuntos imutáveis (frozenset)**

É uma variação do set, porém imutável, ou seja, seus elementos não podem ser modificados durante a execução do programa.


⚠️ **Acesso e operações:**
***
    permissions = frozenset(["member", "group"])  # assim como o set, qualquer estrutura iterável pode ser utilizada para criar um frozenset
    
    permissions.union({"user"})  # novos conjuntos imutáveis podem ser criados à partir do original, mas o mesmo não pode ser modificado

    permissions.intersection({"user", "member"})  # retorna um conjunto resultante da intersecção dos conjuntos

    permissions.difference({"user"})  # retorna a diferença entre os dois conjuntos
***
### **Dicionários (dict)**

Estrutura que associa uma chave a um determinado valor. É a representação do tão famoso objeto que utilizamos em JavaScript.

O modo mais simples de criar um dicionário:
***
    people_by_id = {1: "Maria", 2: "Fernanda", 3: "Felipe"}  # elementos no formato "chave: valor" separados por vírgula, envolvidos por chaves.
***

Também podemos utilizar a função dict do próprio Python (built-in function), passando as chaves e valores como parâmetros:

***
    dicio = dict(primeiro=1, segundo=2, terceiro=3)
***

Utilizando a função zip para concatenar a chave:valor em um elemento do objeto dict:

***
    dicio_3 = dict(zip(['primeiro', 'segundo', 'terceiro'], [1, 2, 3]))
***

Utilizando uma lista de tuplas com itens simbolizando chave e valor em um objeto dict:

***
    dicio_4 = dict([('primeiro', 1), ('segundo', 2), ('terceiro', 3)])
***

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

## **Manipulação de arquivos**

Para manipulação de arquivos em Python, deve-se fazer uso da função **open()**. Por padrão, arquivos são abertos somente para leitura, mas podemos modificar isto passando o modo com que vamos abrir o arquivo para leitura **mode="r"** ou escrita **mode="w"**
- A leitura do conteúdo de um arquivo pode ser feita utilizando a função **read()**:
***
    file = open("arquivo.txt", mode="r")
    content = file.read()

    print(content)

    file.close()  # não podemos esquecer de fechar o arquivo
***

- Para escrever um conteúdo em um arquivo utilizamos a função **write():**
***
    file = open("arquivo.txt", mode="w")    # ao abrir um arquivo para escrita, um novo arquivo é criado mesmo que ele já exista, sobrescrevendo o antigo.

    file.write("nome idade\n")
    file.write("Maria 45\n")    # o \n indica uma quebra de linha no arquivo em questão.
***

- Outra forma de se escrever em arquvos é através do redirecionamento do conteúdo digitado dentro do print para o arquivo destino:
***
    print("Túlio 22", file=file)
***

- Para escrever múltiplas linhas podemos utilizar a função writelines:

***
    LINES = ["Alberto 35\n", "Betina 22\n", "João 42\n", "Victor 19\n"]
    
    file.writelines(LINES)

⚠️ ⚠️ ⚠️ **ATENÇÂO :** Pelo fato de termos uma quantidade limite de arquivos que podemos abrir de uma só vez e um erro é retornado quando atingimos esse limite, devemos ***SEMPRE*** fechar os arquivos abertos.

Outro motivo importante para se fechar os arquivos é que normalmente a manipulação de arquivos é feita através de buffers. Ou seja, a escrita em disco pode não ser imediata. Quando fechamos o arquivo, garantimos que tudo aquilo que ainda não está escrito seja persistido.

***
    file.close()
***

### **with 👾**
- Com o uso da palavra-chave **with** junto com a função **open()**, o arquivo será aberto e; enquanto dentro do contexto do bloco da função with, é possível fazer a manipulação do arquivo; no fim do bloco da função, o arquivo é automaticamente fechado.

***
    with open("pokemons.json") as file:
        content = file.read()  # leitura do arquivo

            # não necessita de fechar o arquivo, evitando erros no código
***
### **Manipulação de arquivos JSON**

JSON é um formato textual muito utilizado para integração de sistemas. Ele é baseado em um subconjunto de regras JavaScript, embora seja independente de linguagem.

Por sua legibilidade e tamanho (é bem leve), além da facilidade de leitura e escrita por seres humanos e máquinas, vem sendo bastante utilizado na web e para troca de informações entre sistemas.

A linguagem Python já inclui um módulo para manipulação desse tipo de arquivo e seu nome é json.

- Seus principais métodos para manipulação são: **load, loads, dump, dumps.**

***
    import json  # json é um modulo que vem embutido, porém precisamos importá-lo

    with open("pokemons.json") as file:
        content = file.read()  # leitura do arquivo
        pokemons = json.loads(content)["results"]  # o conteúdo é transformado em estrutura python equivalente, dicionário neste caso.
        # acessamos a chave results que é onde contém nossa lista de pokemons

    print(pokemons[0])  # imprime o primeiro pokemon da lista
***

- 👀 **OBS:** A leitura pode ser feita diretamente do arquivo, utilizando o método **load** ao invés de **loads**. 

    - ⚠️ **Atenção :** *O **loads** carrega o JSON a partir de um texto e o **load** carrega o JSON a partir de um arquivo.*
***
    import json


    with open("pokemons.json") as file:
        pokemons = json.load(file)["results"]

    print(pokemons[0])  # imprime o primeiro pokemon da lista
***

- A escrita de arquivos no formato JSON é similar à escrita de arquivos comuns, porém temos que transformar os dados primeiro.

***
    import json

    # Leitura de todos os pokemons
    with open("pokemons.json") as file:
        pokemons = json.load(file)["results"]

    # Separamos somente os do tipo grama
    grass_type_pokemons = [
        pokemon for pokemon in pokemons if "Grass" in pokemon["type"]
    ]

    # Abre o arquivo para escrevermos apenas o pokemons do tipo grama
    with open("grass_pokemons.json", "w") as file:
        json_to_write = json.dumps(
            grass_type_pokemons
        )  # conversão de Python para o formato json (str)
        file.write(json_to_write)
***

- **👀 OBS:** Assim como a desserialização, que faz a **transformação de texto em formato JSON para Python**, a serialização (caminho inverso) possui um método equivalente para **escrever em arquivos JSON de forma direta.**

***
    import json

    # leitura de todos os pokemons
    with open("pokemons.json") as file:
        pokemons = json.load(file)["results"]

    # separamos somente os do tipo grama
    grass_type_pokemons = [
        pokemon for pokemon in pokemons if "Grass" in pokemon["type"]
    ]

    # abre o arquivo para escrita
    with open("grass_pokemons.json", "w") as file:
        # escreve no arquivo já transformando em formato json a estrutura
        json.dump(grass_type_pokemons, file)

### **Manipulação de arquivos CSV**

O formato CSV (Comma Separated Values) é muito comum em exportações de planilhas de dados e base de dados. Foi utilizado por muito tempo antes de sua definição formal, o que gerou uma despadronização deste formato e o surgimento de vários dialetos.

Cada dialeto tem seus próprios delimitadores e caracteres de citação, porém o formato geral é semelhante o suficiente para utilizarmos o mesmo módulo para este processamento.

Ainda que seu nome indique que o delimitador seja a “,“ (vírgula), existem variações que utilizam “;“ (ponto e vírgula) ou até mesmo tabulações (“\t“).
O módulo csv, contém duas principais funções:

- Um leitor (reader) que nos ajuda a ler o conteúdo, já fazendo as transformações dos valores para Python;

- E um escritor (writer) para facilitar a escrita nesse formato.

***
    import csv

    with open("graduacao_unb.csv", encoding = "utf-8") as file:
        graduacao_reader = csv.reader(file, delimiter=",", quotechar='"')
        # Usando o conceito de desempacotamento
        header, *data = graduacao_reader

    print(data)
    group_by_department = {}
    for row in data:
        department = row[15]
        if department not in group_by_department:
            group_by_department[department] = 0
        group_by_department[department] += 1

    # Escreve o relatório em .csv
    # Abre um arquivo para escrita
    with open("department_report.csv", "w", encoding = "utf-8") as file:
        writer = csv.writer(file)

        # Escreve o cabeçalho
        headers = [
            "Departamento",
            "Total de Cursos",
        ]
        writer.writerow(headers)

        # Escreve as linhas de dados
        # Desempacotamento de valores
        for department, grades in group_by_department.items():
            # Agrupa o dado com o turno
            row = [
                department,
                grades,
            ]
            writer.writerow(row)
***

O leitor define como dialeto padrão excel, o que significa dizer que o delimitador de campos será “,“ e o caractere de citação será aspas duplas ("). Uma forma de modificar estes padrões é definindo-os de forma diferente na criação do leitor. Além disso, o leitor irá usar o decodificador padrão do sistema para decodificar em unicode o arquivo .csv. Para utilizar um decodificador diferente, deve ser passado o argumento encoding com o valor do decodificador esperado. Um leitor de .csv pode ser percorrido utilizando o laço de repetição for e, a cada iteração, retorna uma nova linha já transformada em uma lista Python com seus respectivos valores.
***
#### **DictReader()**

Existem ainda o leitor e o escritor baseados em dicionários. A principal vantagem é que não precisamos manipular os índices para acessar os dados das colunas. A desvantagem é o espaço ocupado em memória (que é maior que o comum), devido à estrutura de dados utilizada.

    import csv

    # lê os dados
    with open("graduacao_unb.csv", encoding = "utf-8") as file:
        graduacao_reader = csv.DictReader(file, delimiter=",", quotechar='"')

        # a linha de cabeçalhos é utilizada como chave do dicionário
        # agrupa cursos por departamento
        group_by_department = {}
        for row in graduacao_reader:
            department = row["unidade_responsavel"]
            if department not in group_by_department:
                group_by_department[department] = 0
            group_by_department[department] += 1

    # abre um arquivo para escrita
    with open("new_department_report.csv", "w", encoding = "utf-8") as file:
        # os valores a serem escritos devem ser dicionários
        headers = [
            "Departamento",
            "Total de Cursos",
        ]
        # É necessário passar o arquivo e o cabeçalho
        writer = csv.DictWriter(file, fieldnames=headers)
        writer.writeheader()
        # escreve as linhas de dados
        for department, grades in group_by_department.items():
            # Agrupa o dado com o turno
            row = {"Departamento": department, "Total de Cursos": grades}
            writer.writerow(row)

## **Lidando com exceções**

Erros podem acontecer: um arquivo pode não existir, permissões podem faltar e codificações podem falhar. Por isso temoos que garantir que, ainda que um erro ocorra, faremos o fechamento do nosso arquivo.

Há pelo menos dois tipos de erros que podem ser destacados: **erros de sintaxe e exceções.**

### **Erros de Sintaxe**

Erros de sintaxe ocorrem quando o código utiliza recursos inexistentes da linguagem que não consegue interpretá-los. É como executar print{"Olá, mundo!"} em vez de print("Olá, mundo!").

### **Exceções**

Já as exceções ocorrem durante a execução e resultam em mensagem de erro. Veja exemplos de exceções:

    print(10 * (1 / 0))
    # Traceback (most recent call last):
    #   File "<stdin>", line 1, in <module>
    # ZeroDivisionError: division by zero
    print(4 + spam * 3)
    # Traceback (most recent call last):
    #   File "<stdin>", line 1, in <module>
    # NameError: name 'spam' is not defined
    print('2' + 2)
    # Traceback (most recent call last):
    #   File "<stdin>", line 1, in <module>
    # TypeError: can only concatenate str (not "int") to str

Lista completa de **[exceções já embutidas na linguagem.](https://docs.python.org/pt-br/3/library/exceptions.html#bltin-exceptions)**

### **Tratamento de exceções**

Para tratar exceções utilizamos o conjunto de instruções try, com as palavras reservadas **try** e **except**. O funcionamento dessa cláusula ocorre da seguinte forma:

- Se nenhuma exceção ocorrer, a cláusula except é ignorada e a execução da instrução try é finalizada.

- Se ocorrer uma exceção durante a execução da cláusula try, as instruções remanescentes na cláusula são ignoradas. Se o tipo da exceção ocorrida tiver sido previsto em algum except, então essa cláusula será executada.

- Se não existir nenhum tratador previsto para tal exceção, trata-se de uma exceção não tratada e a execução do programa termina com uma mensagem de erro.

***
    while True:
        try:
            x = int(input("Please enter a number: "))
            break
        except ValueError:
            print("Oops!  That was no valid number.  Try again...")
***

⚠️ **FINALLY** 

Sempre devemos fechar um arquivo e podemos, em um bloco **try**, fazer isso utilizando a instrução **finally** ou **else**. O **finally** é uma outra cláusula do conjunto **try**, cuja finalidade é permitir a implementação de ações de limpeza, que sempre devem ser executadas independentemente da ocorrência de ações. Já o **else** ocorre sempre que todo o **try** for bem sucedido.

***
    try:
        arquivo = open("arquivo.txt", "r")
    except OSError:
        # será executado caso haja uma exceção
        print("arquivo inexistente")
    else:
        # será executado se tudo ocorrer bem no try
        print("arquivo manipulado e fechado com sucesso")
        arquivo.close()
    finally:
        # será sempre executado, independentemente de erro
        print("Tentativa de abrir arquivo")


- **⚠️ Atenção:** Como estamos abrindo o arquivo em modo de leitura, uma exceção será levantada caso ele não exista, executando as cláusulas except e finally. Entretanto, se alterarmos o modo para escrita, o arquivo será criado mesmo se inexistente, executando as cláusulas **else** e **finally.**
***

## **Testes em Python - Pytest**

A biblioteca **pytest,** é um framework que facilita a escrita de testes simples, mas capazes de testar funcionalidades complexas em aplicações e bibliotecas.

A instalação é feita através do pip utilizando o comando:

***
    python3 -m pip install pytest

⚠️ **Atenção:** Lembrar de instalar a biblioteca somente no ambiente virtual do projeto.
***

Verificar  a instalação utilizando o comando:

***
    python3 -m pytest --version
    # A saída esperada é similar à:

    This is pytest version 5.3.0, imported from /home/cassiobotaro/projects/gerenciador-tarefas/.venv/lib/python3.8/site-packages/pytest.py
***
- Para que seus testes sejam descobertos pela ferramenta, o nome do arquivo de testes deve possuir o prefixo ***test_***, assim como a definição das funções de teste.

- Uma função de teste é similar a qualquer outra, porém tem o propósito de verificar se o resultado obtido foi o mesmo do esperado. No código, isto é feito através da utilização da palavra reservada **assert.**

- O comando **assert** funciona da seguinte maneira: caso a expressão recebida seja verdadeira (avaliada como True), nada acontece. Porém, caso seja falsa (avaliada como False), uma exceção do tipo *AssertionError* é lançada. A pytest captura este erro e tenta apresentar uma comparação entre o esperado e o recebido da melhor maneira possível.

- O **pytest** por defalut, não permite colocar parâmetros nas funções de teste, apenas os decorators para criação de contextos.

***
    codigo.py

    def is_odd(number):
        'Retorna True se um número é ímpar, senão False.'
        return number % 2 != 0

    def divide(a_number, other_number):
        "Retorna a divisão de a_number por other_number"
        return a_number / other_number
***
    test_codigo.py

    from codigo import is_odd, divide

    def test_is_odd_when_number_is_odd_returns_true():
        'Para um número ímpar a função deve retornar o valor True'
        assert is_odd(3) is True

    def test_is_odd_when_number_is_even_returns_false():
        'Para um número par a função deve retornar o valor False'
        assert is_odd(2) is False

    def test_divide_when_other_number_is_zero_raises_an_exception():
        with pytest.raises(ZeroDivisionError, match="division by zero"):
            divide(2, 0)

**⚠️ Atenção:** Utilizamos a função raises da pytest para verificar se a exceção ocorreu. Caso contrário, ela lança um AssertionError, indicando que o teste não passou. Podemos verificar também se o texto retornado na exceção é o esperado através do parâmetro match, que pode receber uma expressão regular. No exemplo, temos uma divisão por zero, que lança a exceção esperada e o teste passa com sucesso.
***

- Para rodar os testes e ver o resultado:

***
    python3 -m pytest

**⚠️ Atenção:** Para receber uma resposta mais verbosa, basta adicionar a tag -v ao comando:

    python3 -m pytest -v 
***

### **Contexto de testes**

Para utilização deste e outros recursos, se faz necessária a importação do pytest no arquivo de testes da seguinte forma:
***
    import pytest
***

 Ao escrever testes e pensar em cenários distintos que podem ocorrer no sistema: “dado um arquivo com as seguintes linhas”, “visto que temos um banco de dados com um dado registro” ou “a partir de um cliente web”. Damos o nome de *test fixture* (ou apenas fixture) às precondições ou estados necessários para a execução de um teste.

Cada teste pode ter seu próprio cenário (contexto) ou compartilhá-lo com outros testes.

***

    # get_most_ordered_dish_per_costumer é uma função que retorna o prato mais pedido por uma
    # determinada pessoa cliente, considerando que os pedidos estão em uma lista.

    # get_order_frequency_per_costumer é uma função que retorna a frequência que uma determinada
    # pessoa cliente pede um determinado prato, considerando que os pedidos estão em uma lista.


    # uma fixture utilizando a biblioteca pytest
    # é definida utilizando a sintaxe abaixo
    @pytest.fixture
    def orders():
        """Nosso cenário (contexto) temos os seguintes pedidos"""
        return [
            {"customer": "maria", "order": "pizza", "day": "terça-feira"},
            {"customer": "joao", "order": "hamburger", "day": "terça-feira"},
            {"customer": "maria", "order": "pizza", "day": "quarta-feira"},
            {"customer": "maria", "order": "hamburger", "day": "quinta-feira"},
        ]

    # estamos adicionando a fixture "orders" ao teste
    # ou seja, temos um contexto onde os pedidos são os definidos anteriormente
    def test_get_most_ordered_dish_per_costumer_when_customer_is_maria(orders):
        assert get_most_ordered_dish_per_costumer(orders, "maria") == "pizza"

    # novamente adicionamos um cenário (contexto) ao teste onde os pedidos realizados são os
    # definidos na fixture
    def test_get_order_frequency_per_costumer_when_customer_is_joao_and_order_is_pizza(orders):
        assert get_order_frequency_per_costumer(orders, "joao", "pizza") == 0

    def test_get_order_frequency_per_costumer_when_customer_is_maria_and_order_is_hamburger(orders):
        assert get_order_frequency_per_costumer(orders, "maria", "hamburger") == 1
**⚠️ Atenção:** É importante ressaltar que este contexto poderia ser a abertura de uma conexão com o banco de dados, uma referência à conexão a um cliente web, um arquivo temporário ou qualquer outro contexto. Também vale lembrar que é possível usar mais de um contexto por teste caso seja necessário, bem como um contexto dentro de outro.
***

### **Dublês de teste**

Em testes automatizados (de unidade) é desejado que cada teste não interfira no estado manipulado por outro teste, e também que recursos externos (arquivos, internet, banco de dados) não atrapalhem a sua execução. Por isso, é muito comum a utilização de dublês de testes para simular estes recursos externos.

Podemos substituir componentes para que retornem um determinado valor simulado ou podemos substituir os componentes por objetos falsos que registram as informações sobre sua invocação, como o número de vezes em que foram chamados ou os parâmetros com o qual foram chamados.

Na literatura encontramos as técnicas de dublê com os nomes fakes, mocks, stubs e spies. De uma forma bem resumida, podemos defini-las da seguinte maneira:

- **Fakes:** Objetos que possuem implementações funcionais, porém normalmente simplificadas;

- **Mocks:** São pré programados para verificar as chamadas das funções que receberem;

- **Stubs:** Fornecem respostas predefinidas;

- **Spies:** São como stubs, mas também armazenam informações de como foram chamados.

Vamos analisar dois cenários e escrever seus respectivos testes utilizando dublês, evitando assim a dependência externa a um arquivo real.

No primeiro cenário nós temos nossa dependência externa (o arquivo) sendo recebido como parâmetro.
***
    pokemon.py


    import json


    def retrieve_pokemons_by_type(type, reader):
        # lê o conteudo de reader e o transforma de json
        # para dicionário
        pokemons = json.load(reader)["results"]
        # filtra somente os pokemons do tipo escolhido
        pokemons_by_type = [
            pokemon for pokemon in pokemons if type in pokemon["type"]
        ]
        return pokemons_by_type
***

Vamos utilizar uma técnica onde substituiremos a abertura do nosso arquivo real por um objeto que possui as implementações funcionais de um arquivo (método read, necessário na operação de leitura). Este objeto será alocado na memória, “simulando” nosso arquivo real.

***
    test_pokemon.py


    import json
    import pytest
    from pokemon import retrieve_pokemons_by_type
    from io import StringIO
    # Criamos o contexto de um pokemon do tipo grama
    @pytest.fixture
    def grass_type_pokemon():
        return {
            "national_number": "001",
            "evolution": None,
            "name": "Bulbasaur",
            "type": ["Grass", "Poison"],
            "total": 318,
            "hp": 45,
            "attack": 49,
            "defense": 49,
            "sp_atk": 65,
            "sp_def": 65,
            "speed": 45,
        }
    # Criamos o contexto de um pokemon do tipo água
    @pytest.fixture
    def water_type_pokemon():
        return {
            "national_number": "007",
            "evolution": None,
            "name": "Squirtle",
            "type": ["Water"],
            "total": 314,
            "hp": 44,
            "attack": 48,
            "defense": 65,
            "sp_atk": 50,
            "sp_def": 64,
            "speed": 43,
        }


    def test_retrieve_pokemons_by_type(grass_type_pokemon, water_type_pokemon):
        # criamos um arquivo em memória que o seu conteúdo são os dois pokemons
        fake_file = StringIO(
            json.dumps({"results": [grass_type_pokemon, water_type_pokemon]})
        )
        # quando pesquisamos por pokemons do tipo grama,
        # o pokemon do tipo água não deve ser retornado
        assert grass_type_pokemon in retrieve_pokemons_by_type("Grass", fake_file)
***
Um segundo cenário é onde a função espera o nome de um arquivo e a abertura do mesmo acontece dentro da função.

***
    pokemon.py


    import json


    def retrieve_pokemons_by_type(type, filepath):
        with open(filepath) as file:
            pokemons = json.load(file)["results"]
            pokemons_by_type = [
                pokemon for pokemon in pokemons if type in pokemon["type"]
            ]
            return pokemons_by_type
***

Para escrever este teste, vamos aproveitar da natureza dinâmica da linguagem e substituir o método open em tempo de execução por um objeto mock_open, que já vem embutido na linguagem e se comporta como o open, retornando o que foi definido em read_data como seu conteúdo. Um detalhe interessante é que esse objeto obtido através da função mock_open também possui a capacidade de armazenar informações sobre como foram as chamadas de seus métodos e os parâmetros recebidos.

    test_pokemon.py


    import json
    from unittest.mock import mock_open, patch
    from pokemon import retrieve_pokemons_by_type

    def test_retrieve_pokemons_by_type():
        # definimos um pokemon do tipo grama
        grass_type_pokemon = {
            "national_number": "001",
            "evolution": None,
            "name": "Bulbasaur",
            "type": ["Grass", "Poison"],
            "total": 318,
            "hp": 45,
            "attack": 49,
            "defense": 49,
            "sp_atk": 65,
            "sp_def": 65,
            "speed": 45,
        }
        # definimos também um pokemon do tipo água
        water_type_pokemon = {
            "national_number": "007",
            "evolution": None,
            "name": "Squirtle",
            "type": ["Water"],
            "total": 314,
            "hp": 44,
            "attack": 48,
            "defense": 65,
            "sp_atk": 50,
            "sp_def": 64,
            "speed": 43,
        }
        pokemon_json_content = json.dumps({"results": [grass_type_pokemon, water_type_pokemon]})
        # substituímos a função padrão do python open por mock_open
        # uma versão que se comporta de forma parecida, porém simulada
        with patch("builtins.open", mock_open(read_data=pokemon_json_content)):
            # repare que o nome do arquivo não é importante aqui
            # a esses parâmetros não utilizados damos o nome de dummies
            # como neste contexto alteramos o open pelo mock_open,
            # o argumento "dummy" poderia ser substituído por qualquer coisa, já que não será utilizado pela função
            assert retrieve_pokemons_by_type("Grass", "dummy") == [
                grass_type_pokemon
            ]
A primeira abordagem torna o código menos acoplado a um arquivo e nos permite utilizar qualquer objeto (que tenha o método reader) em seu lugar. Assim, essa função pode ser reutilizada, por exemplo, para ler pokemons a partir de uma requisição web ou outra fonte.






