# Web Storage
O HTML Web Storage provê dois objetos para armazenamento de dados no cliente (browser da pessoa), no formato de chave-valor:

⚠️ **Atenção :** Tanto o localStorage quanto o sessionStorage armazenam dados no formato chave e valor e os valores salvos serão sempre no formato string. Para isso se faz necessário o uso de duas funções ***JSON*** :
  - **JSON.stringify()**, que transforma um dado em uma string JSON.
  - **JSON.parse()**, que converte essa string de volta para o formato original. 


## Local Storage & Session Storage

- localStorage - salva os dados sem data de expiração. Os dados não serão removidos quando o browser for fechado, ou seja, eles ficarão disponíveis enquanto não forem explicitamente removidos.

- sessionStorage - salva os dados apenas para a sessão atual. Os dados são removidos assim que a pessoa fecha a aba (tab) ou o navegador (browser).

      console.log(localStorage.length); // não possui nada salvo, então o retorno é o valor: 0
      localStorage.setItem('firstname', 'Adam'); // salva uma entrada com a key = 'firstname' e value = 'Adam'
      localStorage.setItem('lastname', 'Smith'); // salva uma entrada com a key = 'lastname' e value = 'Smith'
      console.log(localStorage.getItem('lastname')); // retorna o valor 'Smith'
      console.log(localStorage.length); // possui duas entradas, então o retorno é o valor: 2
      localStorage.removeItem('lastname'); // remove a entrada referente a key = 'lastname'
      console.log(localStorage.length); // possui uma entrada, então o retorno é o valor: 1
      localStorage.clear(); // limpa todas as entradas salvas em localStorage
      console.log(localStorage.length); // não possui nada salvo, então o retorno é o valor: 0


## Cookies

Quando o servidor envia a página Web para o browser, a conexão é desligada e o servidor não tem mais acesso às informações da requisição - como os itens que a pessoa usuária adicionou a um carrinho de compras ou o e-mail que lhe dará acesso a sua conta. Cookies foram inventados para salvar dados das pessoas usuárias no próprio browser, pois, dessa forma, uma página conseguirá acessá-los para executar uma lógica com os parâmetros personalizados por pessoa.

Cookies são salvos no formato chave-valor. Quando o navegador faz a requisição ao servidor para acessar uma página Web, os cookies dessa página são adicionados à requisição. Dessa forma, o servidor tem acesso aos dados da pessoa usuária. 

### Criar cookie

- Para criar ou alterar o valor de um cookie basta atribuir à propriedade document.cookie uma string contendo o nome e o valor do que se pretende armazenar:

      document.cookie = 'email=isabella@email.com';
  - Por definição, o cookie é deletado quando fechamos o navegador. Para que isso não aconteça, você pode adicionar uma data para expiração:

        document.cookie = 'email=isabella@email.com; expires=Thu, 17 Dec 2020 12:00:00 UTC';

- Pode-se adicionar também o parâmetro path, que dirá ao navegador a qual caminho o cookie que você criou pertence. 

      document.cookie = 'email=isabella@email.com; expires=Thu, 17 Dec 2020 12:00:00 UTC; path=/';

  👀  Por padrão, o cookie pertence à página atual.
- Para deletar o cookie, não precisa especificar o valor que pretende deletar. Basta deletá-lo passando uma data que já expirou:

      document.cookie = 'email=; expires=Tue, 01 Dec 2020 12:00:00 UTC;'