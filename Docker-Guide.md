# Passo a passo para utilização do Docker

👀 Curiosidade: o Docker é feito de três grandes programas: Docker Daemon, a API e o CLI. Está sendo instalados os três de uma vez só, entretanto vamos interagir com o Docker apenas por meio da sua interface de linha de comando.

No Linux, o Docker não possui uma interface gráfica de utilização (GUI) oficial, mas existem várias opções não-oficiais disponíveis, bem como uma extensão oficial da Microsoft para a plataforma no VSCode. [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

## Desinstale versões anteriores

    sudo apt-get remove docker* containerd runc

⚠️  Caso nenhum dos pacotes esteja instalado, esse comando retornará o erro E: Impossível encontrar o <nóme-do-pacote>. Nesse caso, é só prosseguir com a instalação.

👀 Observação: o Docker preserva informações sobre imagens, containers, volumes e redes na pasta /var/lib/docker/. Nesse processo, esses arquivos não são apagados. Para remoção completa do Docker no seu sistema, consulte a seção <i><b>Desinstalando o Docker</i></b> no final desse tópico.

## Instalando as dependências iniciais

Para habilitar a obtenção dos repositórios via HTTPS pelo apt-get, instale os pacotes listados abaixo. Nós precisamos disso para prosseguir a instalação:

    sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

## Adicione a chave pública do repositório Docker em nossa máquina

Para adicionar a chave GPG* oficial do repositório do Docker, execute o comando a seguir:

⚠️ Este passo é necessário para obter uma chave pública dos servidores da empresa Docker Inc para garantir que qualquer pacote obtido através da Internet esteja assinado por esta chave, evitando assim possíveis ataques de segurança.

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

Se tudo der certo, não haverá nenhum retorno visual.

## Adicionar o repositório remoto na lista do apt 

Para finalmente adicionar o repositório oficial do Docker no apt, execute o seguinte comando:

    echo \
    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

⚠️ Perceba que adicionado o repositório stable (em $(lsb_release -cs) stable), isso significa que teremos somente o repositório com as versões estáveis do Docker.

Em distribuições baseadas no Ubuntu (como o Linux Mint), talvez você precise alterar o comando $(lsb_release -cs) para uma versão do Ubuntu que seja compatível com aquele sistema. Por exemplo: caso utilize o Linux Mint Tessa, você deve alterar o valor para bionic.

## Instalando o Docker no Linux

Primeiro, garantir que os índices dos pacotes do apt estão atualizados, já que foi adicionado um novo repositório:

    sudo apt-get update

Instalar a última versão estável do Docker Engine - Community, que é uma versão mantida pela própria comunidade, já que o Docker é open source.

    sudo apt-get install docker-ce docker-ce-cli containerd.io

## Instalando o Docker no MacOs

Para instalação do Docker em um Mac basta seguir os passos de [Instalação do Docker no Mac Desktop da documentação do Docker](https://docs.docker.com/desktop/install/mac-install/).

## Adicionando seu usuário ao grupo de usuários Docker

Para evitar o uso de sudo em todos os comandos Docker que for executado, dar as devidas permissões ao nosso usuário.

- Primeiro criar um grupo chamado docker:

    sudo groupadd docker

- Então, usar o comando abaixo para adicionar seu usuário a este novo grupo:

      sudo usermod -aG docker $USER

⚠️ Executar o comando exatamente como ele está acima, considerando as letras maiúsculas e minúsculas.

- Para ativar as alterações realizadas nos grupos, pode-se realizar logout e login de sua sessão ou executar o seguinte comando no terminal:

      newgrp docker

⚠️ Se após esse comando você ocorrer algum problema, reiniciar a máquina. Depois de reiniciar seguir para os próximos passos.

## Iniciando o Daemon do Docker

O Daemon é um serviço que fica no background, ou seja, é um serviço que sempre está em execução e aguarda por comandos feitos por meio do CLI. Entretanto, para que este serviço fique sempre disponível, precisamos ativá-lo, até mesmo após reiniciarmos nosso computador.

Para consultar o status atual do daemon do Docker, executar o comando:

    sudo systemctl status docker

⚠️ O comando anterior deve retornar algo como um pequeno relatório sobre o serviço, onde consta seu status de funcionamento: 

      ● docker.service - Docker Application Container Engine
      Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
      Active: inactive (dead) since Thu 2021-09-23 11:55:11 -03; 2s ago
    TriggeredBy: ● docker.socket
          Docs: https://docs.docker.com
        Process: 2034 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=0>
      Main PID: 2034 (code=exited, status=0/SUCCESS

👀  Caso o parâmetro Active esteja como stop/waiting ou no nosso caso, como inactive, rode o comando start para iniciá-lo:

    sudo systemctl start docker

✅ Ao consultar o status novamente, o processo deverá estar como start/running/active.

- Habilite o daemon do Docker para iniciar durante o boot:

      sudo systemctl enable docker

## Validando a instalação

Para validar se tudo ocorreu como deveria na instalação, vamos executar o tão esperado hello world do Docker:

    docker run hello-world

✅ O terminal deve retornar uma mensagem com um <i><b>"Hello from Docker!" </i> </b> e algumas dicas. 🙌🏼

## Comandos básicos do Docker

Formato padrão para comandos não-abreviados no CLI:

         docker </comando/> </subcomando/>  <parâmetros>

- Utilize o parâmetro --help no </comando/> ou </subcomando/> para ter a relação completa do que pode ser executado a partir deles;

    - Exemplo: 
    
            docker container --help 
                OU 
            docker container run --help.
- Os <parâmetros> são opcionais na execução dos comandos;

 ⚠️ O conteúdo faz referência à [ 📘documentação oficial](https://docs.docker.com/engine/reference/commandline/docker/) do Docker.

- <u><b><i>Listando imagens :</i></b></u>

        docker images

- <u><b><i>Listando containers :</i></b></u>

        docker ps
    OU

        docker container ps

    ⚠️ Por padrão, o comando docker ps <b>não exibe containers que foram parados ou que terminaram sua execução.</b> Para visualizar todos os containers atuais, incluindo os que estão em execução e também parados, é necessário utilizar a flag -a.

        docker ps -a
            OU        
        docker container ls -a

- <u><b><i>Executando um novo container :</i></b></u>

        docker container run <flags>? <imagem>:<tag> <argumentos>?

    👀 Executa um container utilizando a imagem identificada pelo </imagem/>:</tag/>.

    ⚠️ Os parâmetros </flags/>? e </argumentos/>? são opcionais (o que é sinalizado pelo uso de ?).

- <u><b><i>Parar a de execução do container :</i></b></u>

        docker stop <nome-do-container>

- <u><b><i>Remover um container :</i></b></u>

        docker rm <nome-do-container>

- <u><b><i>Remover uma imagem :</i></b></u>

        docker rmi

- ⚠️ <u><b><i> Remover todos os containers e imagens Docker :</i></b></u>

        docker system prune -af

# Criando uma imagem Docker

O arquivo <i><b>Dockerfile</b></i> é um arquivo de configuração com uma linguagem própria, que é usado pelo Docker como um passo a passo do que você deseja que aconteça.

⚠️  Atenção: O arquivo Dockerfile deve ser criado na raiz do seu projeto e não tem nenhuma extensão.

<u><b>Comando de exemplo :</u></b>

        FROM alpine:3.14
        CMD ["echo", "Eu sou uma pessoa estudante da Trybe!"]

- <i><b>FROM alpine:3.14</b></i>

    - A palavra reservada <b>FROM</b> significa que o início da construção desta imagem será partir da imagem Docker <i>"alpine:3.14</i>"  já existente!

    - <b>Construção em múltiplos estágios :</b>

        - Cada FROM dentro do Dockerfile significa o início de um novo estágio;
        - Processo de criação de uma imagem Docker super otimizada, com o uso de imagens intermediárias.
        - Exemplo:

                Primeiro Estágio

                FROM alpine:3.14 AS primeiro-estagio
                WORKDIR /site

                COPY config.toml config.toml
                COPY index.html /site/layouts/index.html
                COPY _index.md /site/content/_index.md

                RUN apk add hugo
                RUN hugo --minify --gc

                Segundo Estágio

                FROM nginx:1.21-alpine AS segundo-estagio
                COPY --from=primeiro-estagio /site/public/ /usr/share/nginx/html
                ENTRYPOINT ["nginx", "-g", "daemon off;"]

    ⚠️ No segundo estágio, a linha <b>COPY</b> possui uma flag extra <b>--from=primeiro-estagio:</b>

    - Esse é o segredo principal de construção de múltiplos estágios;
    - O COPY possui a capacidade de copiar arquivos entre os estágios;
    - A flag <b>--from</b> indica que devemos copiar o seguinte arquivo ou pasta de um estágio para o estágio atual;
    - Neste caso acima, estamos copiando as páginas HTML resultantes do Hugo diretamente para uma imagem Docker limpa de nginx!

- <b>CMD ["echo", "Eu sou uma pessoa estudante da Trybe!"]</b>

    - A palavra reservada CMD mostra qual comando deve ser utilizado ao iniciar a imagem como um container;
Neste caso, o CMD aceita uma lista de parâmetros (como o exemplo acima) ou apenas os comandos, sem declarar como lista, por exemplo:


            CMD echo "olá mundo"
    - Conside o CMD como sugestão de comando a ser executado;
    - Ele pode ser substituído ao executar o comando docker <b>run imagem </comando/> </argumento1/>.</b>

## Palavras reservadas do arquivo Dockerfile


<b> Cógido de exemplo para os comandos: </b>
        
        FROM nginx:1.21-alpine AS primeiro-estagio
        WORKDIR /site

        COPY config.toml config.toml
        COPY index.html /site/layouts/index.html
        COPY _index.md /site/content/_index.md

        RUN apk add hugo
        RUN hugo --minify --gc
        RUN mv /site/public/* /usr/share/nginx/html

        ENTRYPOINT ["nginx", "-g", "daemon off;"]

- <b> EXPOSE :</b>

        Exemplo: 
        EXPOSE 80

    - Esta linha indica que a imagem poderá receber conexões pelo número da porta que for informado;
    - Neste caso, indica que a imagem poderá receber conexões na porta 80, que é a porta padrão utilizada pelo httpd.
    
- <b> COPY :</b> 

        Exemplo:
        COPY index.html /site/layouts/index.html

    - Esta linha vai copiar um arquivo no computador local e colocá-lo dentro da imagem, no caminho especificado à frente. Ou seja, a linha vai copiar o arquivo index.html, que está na pasta atual da execução do comando docker build, e vai copiá-lo para o caminho /site/layouts/index.html, dentro da imagem!

    - Este caminho específico é onde o httpd vai procurar por arquivos HTML a serem servidos.
     - Alternativamente pode-se utilizar o comando <b>ADD index.html //site/layouts/index.html </b>. Nesse caso, não mudaria nada, mas o comando ADD tem duas funcionalidades interessantes, tais como:
        - Fazer o download do conteúdo de uma URL </src/> na pasta de destino </dest/>
        - Descompactar automaticamente arquivos compactados de formatos reconhecidos (.tar, .gzip, .bzip2, etc).

- <b> WORKDIR :</b>

        Exemplo: 
        WORKDIR /site

    - A palavra reservada WORKDIR indica para o Docker qual é a pasta atual de trabalho dentro da imagem;
    - Ou seja, nas próximas ações deste build e também quando essa imagem for executada como um container, estaremos no caminho especificado pelo WORKDIR.

- <b> RUN </comando/> </argumento1/> </argumento2/> </argumentoN/> : </b>
        Exemplo: 

        RUN apk add hugo
        RUN hugo --minify --gc
        RUN mv /site/public/* /usr/share/nginx/html

    - A palavra reservada <b>RUN</b> indica que o comando à frente deve ser executado imediatamente, durante o processo de build. Logo:

        - Indica que o comando dado deve ser executado durante a construção da imagem Docker!
        - Ou seja, é muito comum utilizar o RUN para fazer instalações de dependências.
        - A primeira linha com RUN instala o ferramenta Hugo na nossa imagem Docker;
        - A segunda linha executa o comando hugo –minify –gc para gerar as páginas finais em HTML, baseados nos arquivos de templates (index.html) e conteúdos (_index.md);
        - A terceira linha executa o comando mv para mover as páginas resultantes do Hugo para o caminho onde o nginx espera que tenha páginas HTML para serem servidas.
        
- <b>ENTRYPOINT [] - ENTRYPOINT </comando/> </argumento1/> </argumento2/> </argumentoN/></b>

        Exemplo: 
        ENTRYPOINT ["nginx", "-g", "daemon off;"]

    - A palavra reservada ENTRYPOINT indica para o Docker qual comando e seus argumentos deve ser executado ao iniciar a imagem  como um container.
    - Considere o ENTRYPOINT como obrigação de comando a ser executado;
    - Ele sempre será utilizado como ponto de entrada da imagem.

### <b> Diferença entre RUN, ENTRYPOINT e CMD </b>

- <b>RUN </b> é a execução imediata durante o build;
- <b>ENTRYPOINT </b> é a execução obrigatória ao iniciar o container;
- <b>CMD</b> é uma sugestão de parâmetros ao iniciar o container.

## Contruindo a imagem Docker

Para criar a imagem Docker utilize o comando: 
        
        docker build <flags> -t <nome-da-imagem> <contexto>

Este comando espera:

- A flag -t, que indicará qual será o nome da imagem, e também a tag, se utilizar o formato </nome/>:</tag/>;

- Um contexto, ou seja, em qual caminho de pasta o Docker deve se basear para processar o arquivo Dockerfile.

    - Normalmente utiliza-se apenas . (ponto final), que indica a pasta atual.

Baseando-se então no Dockerfile de exemplo, executar o comando: 

    docker build -t primeira-imagem .

- Flag <b> -d :</b>
    - Roda o container em background.

- Flag <b>-p :</b>

        Exeplo: 
        docker run --rm -d -p 1234:80 --name meu-container meu-servidor-web

    - Com o uso dessa flag, durante o <b>docker run</b> estamos solicitando ao Docker que abra uma exceção neste isolamento, fazendo um mapeamento da porta 1234 do nosso computador para a porta 80, dentro da rede do container.

- Flag <b>-P :</b>

    - Mapeia uma porta aleatória da minha máquina à porta do contanier





    


