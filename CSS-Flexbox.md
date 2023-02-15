# CSS FLEXBOX

Para começar a usar Flexbox, é necessário criar um Flex container. Elementos filhos de um Flex container são chamados Flex items e são dispostos dentro dele usando as propriedades Flexbox. Algumas das propriedades Flexbox são aplicadas ao container, e outras aos seus itens.

Um Flex container é criado ao usar a propriedade display de um elemento com o valor flex:

    .flex-container {
      display: flex;
    }

Antes da apresentação das propriedades Flexbox, dois conceitos devem ser explicados:

## Flex Axis

O layout do Flexbox é baseado em flex-directions (direções flex). Essas direções são determinadas por eixos (axis). A imagem abaixo mostra os eixos definidos em um Flex container:

![Flexbox Axis](CSS-Flexbox-Axis.png)

Os flex items são dispostos dentro de um Flex container seguindo o Main Axis. O Main Axis tem a direção definida pela propriedade flex-direction, que pode ser horizontal, quando flex-direction é **row** ou **row-reverse**, e vertical, quando é **column** ou **column-reverse.**

## Flex Lines

Flex Lines são linhas imaginárias usadas para agrupamento e alinhamento de flex items dentro de seus respectivos containers. Um Flex container pode ser single-line ou multi-line, dependendo da propriedade flex-wrap:

- Um Flex container single-line dispõe todos os seus filhos (flex items) em uma única linha;

- Um Flex container multi-line quebra seus flex items em múltiplas linhas. Isso é similar ao que acontece quando um texto é quebrado em uma nova linha quando está muito grande (overflow).

### Propriedades do ***container:***

- **flex-direction:** Define a direção dos flex items e modifica quem é o Main Axis. ***Por padrão essa propriedade é*** **row** ***(linha)*** e com isso os elementos ficam um ao lado do outro. Os outros valores que essa propriedade possui são o **row-reverse**, em que os itens ficam em linha reversa, o **column**, onde os itens ficam em uma única coluna, um embaixo do outro, e o **column-reverse**, em que os itens também ficam um embaixo do outro, porém em ordem reversa.

- **flex-wrap:** Define se os itens devem quebrar ou não a linha, sendo que ***por padrão essa propriedade é*** **nowrap**, ou seja, os itens não quebram a linha. Os valores que fazem com que a linha quebre são o **wrap**, que quebra a linha, e o **wrap-reverse**, que quebra a linha na direção contrária.

- **flex-flow:** É um atalho para as propriedades **flex-direction e flex-wrap.** O primeiro valor que recebe é o do flex-direction, e o segundo, o do flex-wrap.

- **justify-content:** Alinha os flex items no container de acordo com a direção. Essa propriedade possui os seguintes valores:
  - **flex-start:** Alinha os itens ao início do container;
  - **flex-end:** Alinha os itens ao final do container;
  - **Center:** Alinha os itens ao centro do container;
  - **space-between:** Cria um espaçamento igual entre os elementos, mantendo o primeiro grudado no início e o último no final;
  - **space-around:** Também cria um espaçamento entre os elementos, mas os espaçamentos do meio são duas vezes maiores que o inicial e final.

- **align-items:**  Alinha os flex items de acordo com o eixo transversal (cross-axis). Os valores que essa propriedade aceita são:
  - **stretch:** Valor padrão e faz com que os flex items cresçam igualmente;
  - **flex-start:** Alinha os itens ao início;
  - **flex-end:** Alinha os itens ao final;
  - **center:** Alinha os itens ao centro e;
  - **baseline:** Alinha os itens de acordo com a linha base da tipografia.

- **align-content:** Alinha as linhas do container em relação ao eixo transversal (cross-axis), sendo que essa propriedade só funciona caso haja mais de uma linha de flex items. As opções de alinhamento que o align-content apresenta são:
  - **stretch:** Valor padrão que faz com que os flex items cresçam igualmente na vertical;
  - **flex-start:** Alinha todas as linhas de itens ao início;
  - **flex-end:** Alinha todas as linhas de itens ao final;
  - **center:** Alinha todas as linhas ao centro;
  - **space-between:** Cria um espaçamento igual entre as linhas, mantendo a primeira grudada no topo e a última no bottom e;
  - **space-around:** Também cria um espaçamento entre as linhas, mas os espaçamentos do meio são duas vezes maiores que o top e o bottom.

### Propriedades dos ***Flex items:***

Os elementos presentes em um **Flex container** são chamados de **Flex items**. O **Flexbox** possui propriedades que impactam diretamente esses elementos, fazendo com que a pessoa desenvolvedora tenha um controle melhor em relação à estrutura da página.

- **align-self:** A propriedade **align-self** nos permite utilizar os valores de alinhamento **flex-start, flex-end, stretch, baseline** e **center** somente para um item. Assim, podemos criar uma nova classe, pseudoclasse ou id para um item e editar sua posição individualmente, fazendo com que ele, diferente dos demais, fique no início ou ao final do container, centralizado, como preferir.

- **order:** A propriedade **order** nos permite ordenar itens de um determinado container. Essa propriedade é particular de cada item e, quando utilizada, fará com que o flexbox os exiba em ordem crescente. Por padrão, a propriedade order, implicitamente, possui o valor 0, isso significa que, se apenas um item dentre 5 em um container recebe a propriedade order: 1, todos os outros ficarão ordenados da forma que foram construídos no HTML, enquanto este será posicionado após os demais.
É interessante chamar a atenção para o fato de que a propriedade aceita valores negativos. Assim, caso o item diferentão receba **order: -1**, ele será exibido antes dos demais (porque order sempre tratará os itens em ordem crescente).

#### Relação de tamanhos no container:

- **flex-grow:** A propriedade **flex-grow** define o quanto de espaço vago será ocupado por um item - **valor padrão 0**.

- **flex-shrink:** Surge para garantir o quanto um item será comprimido em comparação aos demais - **valor padrão 1**.

- **flex-basis:** A propriedade **flex-basis** tem a função de definir o tamanho base de um item no container. **O valor padrão dessa propriedade é auto** - mantendo a flexibilidade do item de acordo com o tamanho do container.

- **FLEX**: Pela propriedade **flex**, é possível fazer a atribuição das 3 propriedade acima de uma só vez pelo ordem apresentada 

      Exemplo:

      div {
        felx: 1 1 auto
      }
      flex-grow - flex-shrink - flex-basis

      👀 Observação: Na utilização de apenas 2 parametros o CSS entende que estão sendo passados apenas o flex-grow e o flex-basis.
