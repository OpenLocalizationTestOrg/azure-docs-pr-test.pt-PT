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
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="46abb-103">Instalar e configurar o PostgreSQL no Azure</span><span class="sxs-lookup"><span data-stu-id="46abb-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="46abb-104">PostgreSQL é uma base de dados de open source avançadas de tooOracle semelhante e DB2.</span><span class="sxs-lookup"><span data-stu-id="46abb-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="46abb-105">Inclui funcionalidades de preparada para empresa, tais como a conformidade completa ACID, processamento transacional fiável e o controlo de simultaneidade de versão multi.</span><span class="sxs-lookup"><span data-stu-id="46abb-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="46abb-106">Também suporta as normas, como ANSI SQL e SQL/MED (incluindo wrappers de dados externa para Oracle, MySQL, MongoDB e muitas outras).</span><span class="sxs-lookup"><span data-stu-id="46abb-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="46abb-107">É altamente extensível com suporte para 12 mais idiomas procedimental, índices GIN e GiST, suporte de dados geográficos e várias funcionalidades como o NoSQL para JSON ou chave-valor baseados em aplicações.</span><span class="sxs-lookup"><span data-stu-id="46abb-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="46abb-108">Neste artigo, ficará a saber como tooinstall e configurar PostgreSQL numa máquina virtual do Azure com o Linux.</span><span class="sxs-lookup"><span data-stu-id="46abb-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="46abb-109">Instalar PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="46abb-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="46abb-110">Já tem de ter uma máquina virtual do Azure com o Linux na ordem toocomplete neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="46abb-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="46abb-111">toocreate e configurar uma VM com Linux antes de continuar, consulte o [tutorial da VM do Linux do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="46abb-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="46abb-112">Neste caso, utilize a porta 1999 como Olá PostgreSQL porta.</span><span class="sxs-lookup"><span data-stu-id="46abb-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="46abb-113">Ligar toohello VM com Linux criados através do PuTTY.</span><span class="sxs-lookup"><span data-stu-id="46abb-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="46abb-114">Se este for Olá pela primeira vez que está a utilizar uma VM com Linux do Azure, consulte [como tooUse SSH com o Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn como toouse PuTTY tooconnect tooa VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="46abb-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="46abb-115">Execute Olá os seguintes comandos tooswitch toohello de raiz (administrador):</span><span class="sxs-lookup"><span data-stu-id="46abb-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="46abb-116">Algumas distribuições têm dependências que tem de instalar antes de instalar PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="46abb-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="46abb-117">Verifique o distro nesta lista e executar comandos adequadas Olá:</span><span class="sxs-lookup"><span data-stu-id="46abb-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="46abb-118">Red Hat base com Linux:</span><span class="sxs-lookup"><span data-stu-id="46abb-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="46abb-119">Debian base Linux:</span><span class="sxs-lookup"><span data-stu-id="46abb-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="46abb-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="46abb-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="46abb-121">Transfira PostgreSQL no diretório de raiz de Olá e, em seguida, deszipe o pacote de Olá:</span><span class="sxs-lookup"><span data-stu-id="46abb-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="46abb-122">Olá acima é um exemplo.</span><span class="sxs-lookup"><span data-stu-id="46abb-122">hello above is an example.</span></span> <span data-ttu-id="46abb-123">Pode encontrar Olá mais detalhadas Transferir endereço Olá [índice da/pub/origem/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="46abb-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="46abb-124">compilação de Olá do toostart, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="46abb-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="46abb-125">Se quiser toobuild tudo o que pode ser incorporado, incluindo documentação Olá (páginas HTML e man) e módulos adicionais (contrib), execute Olá em vez disso, os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46abb-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="46abb-126">Deverá receber Olá seguir a mensagem de confirmação:</span><span class="sxs-lookup"><span data-stu-id="46abb-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="46abb-127">Configurar PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="46abb-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="46abb-128">(Opcional) Criar um Olá tooshorten de ligação simbólica PostgreSQL referência toonot incluem o número de versão Olá:</span><span class="sxs-lookup"><span data-stu-id="46abb-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="46abb-129">Crie um diretório para a base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="46abb-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="46abb-130">Criar um utilizador não raiz e modificar o perfil do utilizador.</span><span class="sxs-lookup"><span data-stu-id="46abb-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="46abb-131">Em seguida, mude toothis novo utilizador (chamado *postgres* no nosso exemplo):</span><span class="sxs-lookup"><span data-stu-id="46abb-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="46abb-132">Por motivos de segurança, PostgreSQL utiliza um tooinitialize de utilizador não raiz, em seguida, iniciar ou encerrar a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="46abb-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="46abb-133">Editar Olá *bash_profile* ficheiro introduzindo comandos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="46abb-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="46abb-134">Estas linhas serão adicionadas final toohello Olá *bash_profile* ficheiro:</span><span class="sxs-lookup"><span data-stu-id="46abb-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="46abb-135">Executar Olá *bash_profile* ficheiro:</span><span class="sxs-lookup"><span data-stu-id="46abb-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="46abb-136">Valide a instalação utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46abb-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="46abb-137">Se a instalação for bem sucedida, verá Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="46abb-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="46abb-138">Também pode verificar a versão de PostgreSQL de Olá:</span><span class="sxs-lookup"><span data-stu-id="46abb-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="46abb-139">Inicializar a base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="46abb-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="46abb-140">Deverá receber Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="46abb-140">You should receive hello following output:</span></span>

![Imagem](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="46abb-142">Configurar PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="46abb-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="46abb-143">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46abb-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="46abb-144">Modifique as duas variáveis no ficheiro de /etc/init.d/postgresql Olá.</span><span class="sxs-lookup"><span data-stu-id="46abb-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="46abb-145">prefixo de Olá está definido toohello o caminho de instalação do PostgreSQL: **optar ativamente por participar/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="46abb-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="46abb-146">PGDATA é definir o caminho de armazenamento de dados de toohello de PostgreSQL: **optar ativamente por participar/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="46abb-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Imagem](./media/postgresql-install/no2.png)

<span data-ttu-id="46abb-148">Alterar Olá ficheiro toomake-executável:</span><span class="sxs-lookup"><span data-stu-id="46abb-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="46abb-149">Inicie PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="46abb-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="46abb-150">Verifique se o ponto final de Olá de PostgreSQL no:</span><span class="sxs-lookup"><span data-stu-id="46abb-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="46abb-151">Deverá ver Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="46abb-151">You should see hello following output:</span></span>

![Imagem](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="46abb-153">Ligar a base de dados do toohello Postgres</span><span class="sxs-lookup"><span data-stu-id="46abb-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="46abb-154">Comutador toohello postgres utilizador novamente:</span><span class="sxs-lookup"><span data-stu-id="46abb-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="46abb-155">Crie uma base de dados Postgres:</span><span class="sxs-lookup"><span data-stu-id="46abb-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="46abb-156">Ligar a base de dados do eventos toohello que acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="46abb-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="46abb-157">Criar e eliminar uma tabela de Postgres</span><span class="sxs-lookup"><span data-stu-id="46abb-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="46abb-158">Agora que o se ligou toohello base de dados, pode criar tabelas no mesmo.</span><span class="sxs-lookup"><span data-stu-id="46abb-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="46abb-159">Por exemplo, crie uma nova tabela de Postgres de exemplo utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46abb-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="46abb-160">Agora definiu uma tabela de quatro colunas com Olá os seguintes nomes de colunas e as restrições:</span><span class="sxs-lookup"><span data-stu-id="46abb-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="46abb-161">Olá "name" coluna foi limitou por Olá VARCHAR comando toobe em 20 carateres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="46abb-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="46abb-162">coluna de "prato" Olá indica o item de prato Olá que cada pessoa será apresentada.</span><span class="sxs-lookup"><span data-stu-id="46abb-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="46abb-163">VARCHAR limita toobe este texto em 30 carateres.</span><span class="sxs-lookup"><span data-stu-id="46abb-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="46abb-164">Olá "confirmada" registos de coluna se a pessoa Olá tem RSVP'd toohello potluck.</span><span class="sxs-lookup"><span data-stu-id="46abb-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="46abb-165">os valores aceitáveis Olá são "Y" e "N".</span><span class="sxs-lookup"><span data-stu-id="46abb-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="46abb-166">Data"Olá" coluna será apresentado quando se inscreveu no evento Olá.</span><span class="sxs-lookup"><span data-stu-id="46abb-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="46abb-167">Postgres requer que as datas ser escritas como aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="46abb-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="46abb-168">Deverá ver o seguinte Olá se a tabela foi criada com êxito:</span><span class="sxs-lookup"><span data-stu-id="46abb-168">You should see hello following if your table has been successfully created:</span></span>

![Imagem](./media/postgresql-install/no4.png)

<span data-ttu-id="46abb-170">Também pode verificar a estrutura da tabela Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46abb-170">You can also check hello table structure by using hello following command:</span></span>

![Imagem](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="46abb-172">Adicionar dados tooa tabela</span><span class="sxs-lookup"><span data-stu-id="46abb-172">Add data tooa table</span></span>
<span data-ttu-id="46abb-173">Em primeiro lugar, inserir informações de uma linha:</span><span class="sxs-lookup"><span data-stu-id="46abb-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="46abb-174">Deverá ver este resultado:</span><span class="sxs-lookup"><span data-stu-id="46abb-174">You should see this output:</span></span>

![Imagem](./media/postgresql-install/no6.png)

<span data-ttu-id="46abb-176">Pode adicionar alguns mais pessoas toohello tabela bem.</span><span class="sxs-lookup"><span data-stu-id="46abb-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="46abb-177">Seguem-se algumas opções, ou pode criar os seus próprios:</span><span class="sxs-lookup"><span data-stu-id="46abb-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="46abb-178">Mostrar tabelas</span><span class="sxs-lookup"><span data-stu-id="46abb-178">Show tables</span></span>
<span data-ttu-id="46abb-179">Utilize Olá comando tooshow uma tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="46abb-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="46abb-180">o resultado da Olá é:</span><span class="sxs-lookup"><span data-stu-id="46abb-180">hello output is:</span></span>

![Imagem](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="46abb-182">Eliminar dados numa tabela</span><span class="sxs-lookup"><span data-stu-id="46abb-182">Delete data in a table</span></span>
<span data-ttu-id="46abb-183">Utilize Olá dados toodelete de comando de uma tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="46abb-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="46abb-184">Isto elimina todas as informações de Olá Olá linha "João".</span><span class="sxs-lookup"><span data-stu-id="46abb-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="46abb-185">o resultado da Olá é:</span><span class="sxs-lookup"><span data-stu-id="46abb-185">hello output is:</span></span>

![Imagem](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="46abb-187">Atualize dados em tabela</span><span class="sxs-lookup"><span data-stu-id="46abb-187">Update data in a table</span></span>
<span data-ttu-id="46abb-188">Utilize Olá dados tooupdate de comando de uma tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="46abb-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="46abb-189">Para este Sandy tiver confirmado que ela é attending, pelo que iremos irá alterar utras RSVP de "N" "Y":</span><span class="sxs-lookup"><span data-stu-id="46abb-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="46abb-190">Obter mais informações sobre PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="46abb-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="46abb-191">Agora que concluiu a instalação de Olá do PostgreSQL no VM Linux do Azure, possam desfrutar de utilizá-la no Azure.</span><span class="sxs-lookup"><span data-stu-id="46abb-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="46abb-192">toolearn mais informações sobre PostgreSQL, visite Olá [PostgreSQL site](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="46abb-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

