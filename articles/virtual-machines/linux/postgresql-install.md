---
title: "aaaSet segurança PostgreSQL numa VM com Linux | Microsoft Docs"
description: "Saiba como tooinstall e configurar PostgreSQL numa máquina virtual com Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Instalar e configurar o PostgreSQL no Azure
PostgreSQL é uma base de dados de open source avançadas de tooOracle semelhante e DB2. Inclui funcionalidades de preparada para empresa, tais como a conformidade completa ACID, processamento transacional fiável e o controlo de simultaneidade de versão multi. Também suporta as normas, como ANSI SQL e SQL/MED (incluindo wrappers de dados externa para Oracle, MySQL, MongoDB e muitas outras). É altamente extensível com suporte para 12 mais idiomas procedimental, índices GIN e GiST, suporte de dados geográficos e várias funcionalidades como o NoSQL para JSON ou chave-valor baseados em aplicações.

Neste artigo, ficará a saber como tooinstall e configurar PostgreSQL numa máquina virtual do Azure com o Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Instalar PostgreSQL
> [!NOTE]
> Já tem de ter uma máquina virtual do Azure com o Linux na ordem toocomplete neste tutorial. toocreate e configurar uma VM com Linux antes de continuar, consulte o [tutorial da VM do Linux do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

Neste caso, utilize a porta 1999 como Olá PostgreSQL porta.  

Ligar toohello VM com Linux criados através do PuTTY. Se este for Olá pela primeira vez que está a utilizar uma VM com Linux do Azure, consulte [como tooUse SSH com o Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn como toouse PuTTY tooconnect tooa VM com Linux.

1. Execute Olá os seguintes comandos tooswitch toohello de raiz (administrador):
   
        # sudo su -
2. Algumas distribuições têm dependências que tem de instalar antes de instalar PostgreSQL. Verifique o distro nesta lista e executar comandos adequadas Olá:
   
   * Red Hat base com Linux:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian base Linux:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Transfira PostgreSQL no diretório de raiz de Olá e, em seguida, deszipe o pacote de Olá:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Olá acima é um exemplo. Pode encontrar Olá mais detalhadas Transferir endereço Olá [índice da/pub/origem/](https://ftp.postgresql.org/pub/source/).
4. compilação de Olá do toostart, execute estes comandos:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Se quiser toobuild tudo o que pode ser incorporado, incluindo documentação Olá (páginas HTML e man) e módulos adicionais (contrib), execute Olá em vez disso, os seguintes comandos:
   
        # gmake install-world
   
    Deverá receber Olá seguir a mensagem de confirmação:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Configurar PostgreSQL
1. (Opcional) Criar um Olá tooshorten de ligação simbólica PostgreSQL referência toonot incluem o número de versão Olá:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Crie um diretório para a base de dados de Olá:
   
        # mkdir -p /opt/pgsql_data
3. Criar um utilizador não raiz e modificar o perfil do utilizador. Em seguida, mude toothis novo utilizador (chamado *postgres* no nosso exemplo):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Por motivos de segurança, PostgreSQL utiliza um tooinitialize de utilizador não raiz, em seguida, iniciar ou encerrar a base de dados de Olá.
   > 
   > 
4. Editar Olá *bash_profile* ficheiro introduzindo comandos Olá abaixo. Estas linhas serão adicionadas final toohello Olá *bash_profile* ficheiro:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Executar Olá *bash_profile* ficheiro:
   
        $ source .bash_profile
6. Valide a instalação utilizando Olá os seguintes comandos:
   
        $ which psql
   
    Se a instalação for bem sucedida, verá Olá seguinte resposta:
   
        /opt/pgsql/bin/psql
7. Também pode verificar a versão de PostgreSQL de Olá:
   
        $ psql -V
8. Inicializar a base de dados de Olá:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Deverá receber Olá seguinte saída:

![Imagem](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Configurar PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Execute Olá os seguintes comandos:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Modifique as duas variáveis no ficheiro de /etc/init.d/postgresql Olá. prefixo de Olá está definido toohello o caminho de instalação do PostgreSQL: **optar ativamente por participar/pgsql**. PGDATA é definir o caminho de armazenamento de dados de toohello de PostgreSQL: **optar ativamente por participar/pgsql_data**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Imagem](./media/postgresql-install/no2.png)

Alterar Olá ficheiro toomake-executável:

    # chmod +x /etc/init.d/postgresql

Inicie PostgreSQL:

    # /etc/init.d/postgresql start

Verifique se o ponto final de Olá de PostgreSQL no:

    # netstat -tunlp|grep 1999

Deverá ver Olá seguinte saída:

![Imagem](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Ligar a base de dados do toohello Postgres
Comutador toohello postgres utilizador novamente:

    # su - postgres

Crie uma base de dados Postgres:

    $ createdb events

Ligar a base de dados do eventos toohello que acabou de criar:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Criar e eliminar uma tabela de Postgres
Agora que o se ligou toohello base de dados, pode criar tabelas no mesmo.

Por exemplo, crie uma nova tabela de Postgres de exemplo utilizando Olá os seguintes comandos:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Agora definiu uma tabela de quatro colunas com Olá os seguintes nomes de colunas e as restrições:

1. Olá "name" coluna foi limitou por Olá VARCHAR comando toobe em 20 carateres de comprimento.
2. coluna de "prato" Olá indica o item de prato Olá que cada pessoa será apresentada. VARCHAR limita toobe este texto em 30 carateres.
3. Olá "confirmada" registos de coluna se a pessoa Olá tem RSVP'd toohello potluck. os valores aceitáveis Olá são "Y" e "N".
4. Data"Olá" coluna será apresentado quando se inscreveu no evento Olá. Postgres requer que as datas ser escritas como aaaa-mm-dd.

Deverá ver o seguinte Olá se a tabela foi criada com êxito:

![Imagem](./media/postgresql-install/no4.png)

Também pode verificar a estrutura da tabela Olá utilizando Olá os seguintes comandos:

![Imagem](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Adicionar dados tooa tabela
Em primeiro lugar, inserir informações de uma linha:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Deverá ver este resultado:

![Imagem](./media/postgresql-install/no6.png)

Pode adicionar alguns mais pessoas toohello tabela bem. Seguem-se algumas opções, ou pode criar os seus próprios:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Mostrar tabelas
Utilize Olá comando tooshow uma tabela a seguir:

    select * from potluck;

o resultado da Olá é:

![Imagem](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Eliminar dados numa tabela
Utilize Olá dados toodelete de comando de uma tabela a seguir:

    delete from potluck where name=’John’;

Isto elimina todas as informações de Olá Olá linha "João". o resultado da Olá é:

![Imagem](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Atualize dados em tabela
Utilize Olá dados tooupdate de comando de uma tabela a seguir. Para este Sandy tiver confirmado que ela é attending, pelo que iremos irá alterar utras RSVP de "N" "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Obter mais informações sobre PostgreSQL
Agora que concluiu a instalação de Olá do PostgreSQL no VM Linux do Azure, possam desfrutar de utilizá-la no Azure. toolearn mais informações sobre PostgreSQL, visite Olá [PostgreSQL site](http://www.postgresql.org/).

