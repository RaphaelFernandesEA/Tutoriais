# **POO em Python**

## **Classes**
Classe é o primeiro dos conceitos. Ele é utilizado para determinar algo genérico. Na programação orientada a objetos, toda classe tem como finalidade modelar com precisão a representação de uma entidade do mundo real. Um exemplo de uma classe é o conceito Liquidificador. Existem vários liquidificadores no mundo, de várias marcas e modelos, com várias funcionalidades diferentes, mas todos possuem algumas coisas em comum.

## **Objetos**

Objetos são elementos diferentes de uma mesma classe. Seguindo a linha de raciocínio do liquidificador:

- Supondo que eu tenho um liquidificador em casa. E provavelmente você tem um também, mas mesmo que não. Ambos são liquidificadores, mas o meu é diferente do seu. Na verdade, mesmo que seja igual (mesma marca, mesmo modelo, mesma cor, etc), não são o mesmo liquidificador. Inclusive podemos colocar um do lado do outro e ver que são dois liquidificadores distintos. Isto quer dizer que são objetos diferentes de uma mesma classe. Objeto (ou instância da classe) é algo específico.

## **Atributos / Propriedades**

Atributos são propriedades das coisas. No contexto de uma classe ou objeto, atributos são variáveis. Uma classe define atributos, e um objeto os valora:
- Um liquidificador possui uma cor e uma potência. A classe Liquidificador vai declarar esses atributos, mas não irá definir valores para eles. Isso quer dizer que todo liquidificador vai ter essas duas propriedades: cor e potência;
   - O meu liquidificador é preto, e ele tem 1200W (Watts) de potência. 
   - O seu, vamos supor, é vermelho e tem 1500W de potência.
   - É perceptível que todo liquidificador possui valores diferentes (ou que podem ser diferentes), logo, a valoração dos atributos é feita no objeto criado a partir da classe e não na classe.

## **Métodos / Comportamentos**
A classe, além de definir os atributos do objeto, também define seus métodos (ou comportamentos). Métodos são ações que um objeto ou classe podem realizar. No contexto de uma classe ou objeto, métodos são funções. Uma classe costuma definir os métodos e os objetos os chamam (mas em alguns casos os métodos podem ser chamados a partir da classe):
- Classe Liquidificador
  - ligar
  - desligar
  
  **👀 Obs:** Os métodos podem manipular os atributos.

## **Método Construtor/Inicializador**

O construtor é um método especial que roda automaticamente quando se é criado (instanciado) o objeto. Na maioria das linguagens, o construtor cria e devolve a instância do objeto e já inicializa os seus atributos.

Em python, esta operação é dividida em dois métodos:

__ new__ (Construtor)

__ init__ (Inicializador)

**👀 Obs:** O Python já implementa estes métodos por padrão para cada nova classe criada, mas podemos implementá-los novamente, ou seja, sobrescrevê-los. É desse modo que customizamos nosso construtor/inicializador.

⚠️ **Importante:** Apesar do método __ init__ ser “apenas” o inicializador, é comum ver referências a ele como o construtor. Isso acontece pois são raras as vezes que precisamos alterar o __ new__ para customizar nossas classes. Como a comunidade já adotou que “o __ init__ é o construtor de objetos no Python“, melhor
manter assim. 😉

Com isso, basta recriar o método __ init__ dentro da classe, conforme exemplo:

***
    class Liquidificador:
        def __init__(self, cor, potencia, tensao, preco):
            self.preco = preco
            self.cor = cor
            self._potencia = potencia
            self._tensao = tensao
            self.__ligado = False
            self.__velocidade = 0
            self.__velocidade_maxima = 3
            self.__corrente_atual_no_motor = 0
***

O primeiro parâmetro, o self, representa a instância do objeto, ou seja, tem acesso ao objeto na memória.

⚠️ **Atenção:** Em muitas linguagens também é chamado de this, e como em Python é um parâmetro explícito, você pode chamá-lo como quiser, mas self é uma convenção adotada pela comunidade.

## **Encapsulamento e Abstração**

Após a criação de objetos, o próximo passo é saber como simplificar seu uso e esconder os detalhes de implementação.

### **Encapsulamento**

O encapsulamento é um dos pilares da orientação a objetos. Por meio dele, é possível simplificar bastante a implementação da abstração. 

Apesar de em **Python** não termos palavras reservadas como **public, private e protected** para declarar um atributo ou método como público, privado ou protegido, respectivamente.Ainda assim, segmentamos nossos atributos e métodos em 3 categorias. E para isso, existe uma convenção de nomenclatura para definir a acessibilidade de cada recurso::

- **Protegidos:** Nomes iniciados com **_ (underline)**: são considerados “protegidos“, como os atributos _potencia e _tensao. 

  Podem ser acessados apenas pela classe que os definem e, quando há herança envolvida, também pelas classes “abaixo” na hierarquia (veremos o tópico herança a seguir)
  
  ⚠️ Isso é apenas uma convenção entre pessoas desenvolvedoras Python, pois ainda será possível fazer um acesso direto por fora da classe;

- **Privados:** Nomes iniciados com **__ (dunder/duplo underline)**: são considerados “privados“, como os atributos __ligado e __velocidade.

  Podem ser acessados apenas pela classe que os definem.
  
  ⚠️ Não será possível fazer o acesso diretamente por fora da classe, mas existem formas de burlar isso (caso queira saber mais pesquise name mangling);

- **Públicos:** Quaisquer outros nomes válidos: são público. 

  Podem ser acessados livremente por qualquer parte da aplicação;


