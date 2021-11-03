---
title: HestiaCP no ARM
date: "2021-11-03T01:20:25.284Z"
description: "A Oracle oferece gratuitamente um servidor com 4 núcleos e 24 gb de ram, o único problema é que a arquitetura arm não tem muitas opções de LEMP/LAMP stack. A solução? HestiaCP um painel de controle seguro, grátis e bem eficiente, basta seguir as instruções pra instalar na sua Oracle Cloud"
---
Como a Oracle oferece no nível "always free" 4 núcleos do processador arm e 24gb de ram para o mesmo, as instâncias ampere são bbem úteis pra quem quer ter uma hospedagem parruda sem custos extras.

O intuito desse post não é ensinar a setar a máquina virtual, vou escrever esse outro dia. Porém, uma vez a instância preparada, basta seguir a receita pra instalar o HestiaCP

A primeira parte é ser root. Para isso usamos o comando sudo para elevar o usuário padrão pro usuário raiz, capaz de alterar tudo na máquina

    sudo -i

Então usamos o comando apt update e apt upgrade para garantir que nosso sistema esteja atualizado

    sudo apt update && sudo apt upgrade -y

Clonamos o repositório do HestiaCP no github

    git clone https://github.com/hestiacp/hestiacp.git

Em seguida mudamos para a pasta src (source) e usamos o script para auto compilar todos os pacotes necessários sem instalar nada por enquanto.

    cd hestiacp/src/
    ./hst_autocompile.sh --all --noinstall --keepbuild release

Após a compilação, temos na pasta install o script para instalar o HestiaCP. Antes disso lembre-se de deletar o grupo admin (groupdel admin) para evitar incompatibilidades.

    cd ../install/
    groupdel admin
    bash hst-install-ubuntu.sh --with-debs /tmp/hestiacp-src/deb/

E voilá, após a instalação o script deve exibir o caminho para acessar o painel, geralmente em https://ip-do-seu-servidor:8083 ou algo do gênero