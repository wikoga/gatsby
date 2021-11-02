---
title: HestiaCP no ARM
date: "2021-11-02T22:12:03.284Z"
description: "A Oracle oferece gratuitamente um servidor com 4 núcleos e 24 gb de ram, o único problema é que a arquitetura arm não tem muitas opções de LEMP/LAMP stack. A solução? HestiaCP um painel de controle seguro, grátis e bem eficiente, basta seguir as instruções pra instalar na sua Oracle Cloud"
---
Como a Oracle oferece no nível "always free" 4 núcleos do processador arm e 24gb de ram para o mesmo, as instâncias ampere são bbem úteis pra quem quer ter uma hospedagem parruda sem custos extras.

O intuito desse post não é ensinar a setar a máquina virtual, vou escrever esse outro dia. Porém, uma vez a instância preparada, basta seguir a receita pra instalar o HestiaCP

    sudo -i

outro

    sudo apt-get update
    sudo apt-get upgrade -y

clonar

    git clone https://github.com/hestiacp/hestiacp.git

então 

    cd hestiacp/src/
    ./hst_autocompile.sh --all --noinstall --keepbuild release

E

    cd ../install/
    groupdel admin
    bash hst-install-ubuntu.sh --with-debs /tmp/hestiacp-src/deb/
