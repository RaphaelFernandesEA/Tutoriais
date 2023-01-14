# Instalação do Node - Linux e MacOS

Para conseguir rodar projetos no computador, é necessário instalar o Node, que possibilita utilizar pacotes externos nas aplicações por meio do NPM (Node Package Manager).

Para instalar o Node no computador, podemos realizar a instalação do nvm (Node Version Manager), que permite alternações entre versões do Node. Alternar entre versões do Node é interessante porque muitas vezes, ao baixar códigos da internet, pode-se deparar com programas que só são executadas com uma versão específica do Node.

## Primeiro passo - Configurando a instalação

Linux 🐧: Atualizar o sistema

Para isso, abrir o terminal e executar o comando:

    sudo apt update && sudo apt upgrade

MacOS 🍎: Instalar o brew

Para poder instalar o curl é necessário utilizar o brew. Se ainda não tiver o brew instalado, executar o comando:

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null

## Segundo passo 💻: Instalando o curl

Linux 🐧: 

    sudo apt install curl

MacOS 🍎: 

    brew install curl

## Terceiro passo 💻: Verificando a versão do curl

    curl --version

## Quarto passo: Instalando o nvm

Linux 🐧:

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

MacOS 🍎:

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

- Após tudo ser concluído, vá para o diretório home. Caso não saiba como fazer isso, execute o seguinte comando:

      cd ~

- Será necessário editar o arquivo bash_profile, que executa cada vez que você abre o terminal. Para isso, executar o comando:

      nano .bash_profile

Esse comando abrirá o arquivo dentro do terminal.

Dentro do arquivo bash_profile, cole o seguinte código abaixo:

    export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

Pronto! O nvm está instalado no MacOS 🍎!

## Quinto passo: Verificando a versão do nvm

    nvm -v

## Sexto passo 💻: Escolha a versão do nvm a ser instalada

O comando abaixo instala a versão mais recente do nvm.

    nvm install --lts

👀 Obs: Para instalar outra versão, basta digitar o comando anterior e alterar o campo --lts para o número da versão desejada.

## Sétimo passo 💻: Verificar a versão do npm instalada

Ao instalar o nvm, também é instalado o npm (Node Package Manager), que é um gerenciador de pacotes que ajuda a instalar diversos pacotes de código para auxiliar no desenvolvimento.

    npm -v

## Alternando entre versões do Node

Caso queira transitar entre as versões instaladas, basta digitar em seu terminal nvm use <versão desejada>, por exemplo:

    nvm use 16

    OU

    nvm use --lts

Para configurar a versão LTS do Node como padrão, executar o seguinte comando:

    nvm alias default node

Após a execução do comando, fechar e abrir o terminal novamente.