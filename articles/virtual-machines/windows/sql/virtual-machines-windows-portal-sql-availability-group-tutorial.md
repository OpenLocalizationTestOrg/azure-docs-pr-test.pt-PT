---
title: aaaSQL grupos de disponibilidade de servidor - Virtual Machines do Azure - Tutorial | Microsoft Docs
description: Este tutorial mostra como toocreate um servidor sempre no grupo de disponibilidade SQL em Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Configurar sempre no grupo de disponibilidade na VM do Azure manualmente

Este tutorial mostra como toocreate um servidor sempre no grupo de disponibilidade SQL em Azure Virtual Machines. tutorial de conclusão de Olá cria um grupo de disponibilidade com uma réplica de base de dados em dois servidores do SQL Server.

**Estimativa de tempo**: demora cerca de 30 minutos toocomplete depois Olá pré-requisitos são cumpridos.

Diagrama de Olá ilustra a compilação no tutorial Olá.

![Grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Pré-requisitos

Olá tutorial parte do princípio de que tem uma compreensão básica do SQL Server em grupos de disponibilidade Always. Se precisar de mais informações, consulte o artigo [descrição geral de grupos de disponibilidade Always (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Olá tabela seguinte lista os pré-requisitos de Olá terá toocomplete antes de iniciar este tutorial:

|  |Requisito |Descrição |
|----- |----- |----- |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Dois servidores do SQL Server | -Num conjunto de disponibilidade do Azure <br/> -Num único domínio <br/> -Com a funcionalidade de Clustering de ativação pós-falha instalada |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Partilha de ficheiros para o testemunho de cluster |  
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Conta de serviço do SQL Server | Conta de domínio |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Conta de serviço do SQL Server Agent | Conta de domínio |  
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Abrir portas de firewall | -SQL Server: **1433** para a instância predefinida <br/> -Ponto final de espelhamento: **5022** ou qualquer porta disponível <br/> -Sonda do Balanceador de carga as do azure: **59999** ou qualquer porta disponível |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Adicionar a funcionalidade de Clustering de ativação pós-falha | Esta funcionalidade necessitam de ambos os servidores do SQL Server |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Conta de domínio de instalação | -Administrador local em cada servidor de SQL <br/> -O membro da função de servidor fixa sysadmin do SQL Server para cada instância do SQL Server  |


Antes de começar Olá tutorial, terá de demasiado[concluir os pré-requisitos para a criação de grupos de disponibilidade Always em Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md). Se os pré-requisitos são já foi concluídos, pode saltar demasiado[criar Cluster](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Criar cluster Olá

Depois de Olá pré-requisitos estão concluídos, Step-by-Olá primeiro passo é toocreate num Cluster de ativação pós-falha do Windows Server que inclua dois SQL Servers e um servidor de testemunho.  

1. RDP toohello primeiro servidor de SQL Server utilizando uma conta de domínio que seja de administrador nos servidores do SQL Server e servidor de testemunho Olá.

   >[!TIP]
   >Se seguiu Olá [documento de pré-requisitos](virtual-machines-windows-portal-sql-availability-group-prereq.md), criou uma conta chamada **CORP\Install**. Utilize esta conta.

2. No Olá **Gestor de servidor** dashboard, selecione **ferramentas**e, em seguida, clique em **Gestor de clusters de ativação pós-falha**.
3. No painel esquerdo Olá, faça duplo clique **Gestor de clusters de ativação pós-falha**e, em seguida, clique em **criar um Cluster**.
   ![Criar Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. No Assistente para criar clusters de Olá, criar um cluster de um nó, avance nas páginas de Olá com definições de Olá no Olá a tabela seguinte:

   | Página | Definições |
   | --- | --- |
   | Antes de começar |Utilize as predefinições |
   | Selecionar servidores |Olá tipo nome do primeiro servidor de SQL no **introduza o nome de servidor** e clique em **adicionar**. |
   | Aviso de validação |Selecione **um número não precisar do suporte da Microsoft para este cluster e, por conseguinte, não pretender que a validação de Olá toorun os testes. Quando posso clicar em seguinte, continuar a criar o cluster de Olá**. |
   | Ponto de acesso para administrar Olá Cluster |Escreva um nome de cluster, por exemplo **SQLAGCluster1** no **nome do Cluster**.|
   | Confirmação |Utilize as predefinições, exceto se estiver a utilizar os espaços de armazenamento. Consulte a nota Olá após esta tabela. |

### <a name="set-hello-cluster-ip-address"></a>Definir o endereço IP de cluster Olá

1. No **Gestor de clusters de ativação pós-falha**, desloque para baixo demasiado**recursos principais do Cluster** e expanda os detalhes do cluster Olá. Deverá ver dois Olá **nome** e Olá **endereço IP** recursos Olá **falha** estado. Olá recurso de endereço IP não pode ser colocado online porque o cluster de Olá é atribuído Olá mesmo endereço IP como Olá computador, pelo que é um endereço duplicado.

2. Olá de contexto não conseguiu **endereço IP** recursos e, em seguida, clique em **propriedades**.

   ![Propriedades do cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Selecione **endereço IP estático** e especifique um endereço de sub-rede onde Olá do SQL Server está na caixa de texto endereço Olá disponível. Em seguida, clique em **OK**.
4. No Olá **recursos principais do Cluster** secção, clique no nome do cluster e clique em **colocar Online**. Em seguida, aguarde até que ambos os recursos estão online. Quando o recurso de nome de cluster Olá fica online, atualiza o servidor de DC Olá com uma nova conta de computador do AD. Utilize este Olá de toorun do AD conta serviço de grupo de disponibilidade em cluster mais tarde.

### <a name="addNode"></a>Adicionar Olá outro toocluster do SQL Server

Adicionar Olá outro cluster de toohello do SQL Server.

1. Na árvore de browser de Olá, faça duplo clique cluster Olá e clique em **adicionar nó**.

    ![Adicionar nó toohello Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. No Olá **Assistente de adicionar nó**, clique em **seguinte**. No Olá **selecionar servidores** página, adicione Olá segundo servidor de SQL. Nome do servidor do tipo Olá na **introduza o nome de servidor** e, em seguida, clique em **adicionar**. Quando tiver terminado, clique em **seguinte**.

1. No Olá **aviso de validação** página, clique em **não** (num cenário de produção, deve executar testes de validação de Olá). Clique depois em **Seguinte**.

8. No Olá **confirmação** página se estiver a utilizar espaços de armazenamento, desmarque Olá caixa de verificação com etiqueta **adicionar todos os clusters de toohello o armazenamento elegível.**

   ![Adicionar a confirmação do nó](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Se estiver a utilizar os espaços de armazenamento e não desmarque **adicionar todos os clusters de toohello o armazenamento elegível**, Windows Desanexa discos virtuais Olá durante Olá clustering processo. Como resultado, não aparecerem no Gestor de discos ou Explorer até que os espaços de armazenamento Olá são removidos do cluster de Olá e novamente ligado com o PowerShell. Vários discos no toostorage conjuntos de grupos de espaços de armazenamento. Para obter mais informações, consulte [espaços de armazenamento](https://technet.microsoft.com/library/hh831739).

1. Clique em **Seguinte**.

1. Clique em **Concluir**.

   Gestor de clusters de ativação pós-falha mostra que o cluster tem um novo nó e listas-lo no Olá **nós** contentor.

10. Terminar sessão de ambiente de trabalho remoto Olá.

### <a name="add-a-cluster-quorum-file-share"></a>Adicionar uma partilha de ficheiros de quórum do cluster

Neste exemplo o cluster do Windows hello utiliza um toocreate de partilha de ficheiros um quórum de cluster. Este tutorial utiliza um quórum maioria de partilha de ficheiros e de nó. Para obter mais informações, consulte [Noções sobre configurações de quórum num Cluster de ativação pós-falha](http://technet.microsoft.com/library/cc731739.aspx).

1. Ligar o servidor de membro de testemunho de partilha de ficheiros de toohello com uma sessão de ambiente de trabalho remoto.

1. No **Gestor de servidor**, clique em **ferramentas**. Abra **gestão de computadores**.

1. Clique em **pastas partilhadas**.

1. Clique com botão direito **partilhas**e clique em **nova partilha...** .

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Utilize **partilhado pasta Assistente para criar um** toocreate uma partilha.

1. No **caminho da pasta**, clique em **procurar** e localizem ou criar um caminho de pasta partilhada Olá. Clique em **Seguinte**.

1. No **nome, descrição e as definições** verificar Olá partilha nome e caminho. Clique em **Seguinte**.

1. No **as permissões da pasta partilhada** definir **personalizar permissões**. Clique em **personalizados...** .

1. No **personalizar permissões**, clique em **adicionar...** .

1. Certifique-se de que Olá conta utilizada toocreate Olá cluster tem controlo total.

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Clique em **OK**.

1. No **as permissões da pasta partilhada**, clique em **concluir**. Clique em **concluir** novamente.  

1. Termine sessão no servidor de Olá

### <a name="configure-cluster-quorum"></a>Configurar o quórum do cluster

Em seguida, configure o quórum do cluster Olá.

1. Ligar toohello primeiro nó de cluster com o ambiente de trabalho remoto.

1. No **Gestor de clusters de ativação pós-falha**, clique no cluster de Olá, aponte demasiado**mais ações**e clique em **configurar definições de quórum do Cluster...** .

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. No **Cluster Assistente para configurar quórum**, clique em **seguinte**.

1. No **selecionar opção de configuração de quórum**, escolha **selecionar testemunho de quórum Olá**e clique em **seguinte**.

1. No **selecionar testemunho de quórum**, clique em **configurar um testemunho de partilha de ficheiros**.

   >[!TIP]
   >Windows Server 2016 suporta um testemunho de nuvem. Se escolher este tipo de testemunho, não precisa de um ficheiro de testemunho de partilha. Para obter mais informações, consulte [implementar um testemunho de nuvem para um Cluster de ativação pós-falha](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Este tutorial utiliza um testemunho de partilha de ficheiros, que é suportado pelos sistemas operativos anteriores.

1. No **configurar testemunho de partilha de ficheiros**, o caminho para partilha de Olá criou Olá do tipo. Clique em **Seguinte**.

1. Verifique as definições de Olá no **confirmação**. Clique em **Seguinte**.

1. Clique em **Concluir**.

recursos de principais do cluster Olá estão configurados com um testemunho de partilha de ficheiros.

## <a name="enable-availability-groups"></a>Ativar grupos de disponibilidade

Em seguida, ative Olá **grupos de Disponibilidade AlwaysOn** funcionalidade. Execute estes passos em ambos os servidores SQL.

1. De Olá **iniciar** ecrã, iniciar **Gestor de configuração do SQL Server**.
2. Na árvore de browser de Olá, clique em **do SQL Server Services**, em seguida, clique com botão direito Olá **SQL Server (MSSQLSERVER)** de serviço e clique em **propriedades**.
3. Clique em Olá **elevada disponibilidade do AlwaysOn** separador, em seguida, selecione **ative os grupos de Disponibilidade AlwaysOn**, da seguinte forma:

    ![Ativar grupos de Disponibilidade AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Clique em **Aplicar**. Clique em **OK** na caixa de diálogo de pop-up Olá.

5. Reinicie o serviço do SQL Server Olá.

Repita estes passos em Olá outro servidor do SQL Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Criar uma base de dados Olá primeiro o SQL Server

1. Iniciar Olá RDP ficheiro toohello primeiro o SQL Server com um domínio de conta que seja um membro do administrador do sistema a função de servidor fixo.
1. Abra o SQL Server Management Studio e ligue toohello primeiro o SQL Server.
7. No **Object Explorer**, faça duplo clique **bases de dados** e clique em **nova base de dados**.
8. No **nome de base de dados**, tipo **MyDB1**, em seguida, clique em **OK**.

### <a name="backupshare"></a>Criar uma partilha de cópia de segurança

1. No Olá primeiro o SQL Server no **Gestor de servidor**, clique em **ferramentas**. Abra **gestão de computadores**.

1. Clique em **pastas partilhadas**.

1. Clique com botão direito **partilhas**e clique em **nova partilha...** .

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Utilize **partilhado pasta Assistente para criar um** toocreate uma partilha.

1. No **caminho da pasta**, clique em **procurar** e localizem ou criar um caminho de pasta partilhada do Olá da base de dados cópia de segurança. Clique em **Seguinte**.

1. No **nome, descrição e as definições** verificar Olá partilha nome e caminho. Clique em **Seguinte**.

1. No **as permissões da pasta partilhada** definir **personalizar permissões**. Clique em **personalizados...** .

1. No **personalizar permissões**, clique em **adicionar...** .

1. Certifique-se de que as contas de serviço de SQL Server e SQL Server Agent Olá para ambos os servidores têm controlo total.

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Clique em **OK**.

1. No **as permissões da pasta partilhada**, clique em **concluir**. Clique em **concluir** novamente.  

### <a name="take-a-full-backup-of-hello-database"></a>Criar um completo cópia de segurança da base de dados de Olá

É necessário tooback segurança Olá nova base de dados tooinitialize Olá da cadeia de registos. Se não efetuar uma cópia de segurança da base de dados nova Olá, não pode ser incluído num grupo de disponibilidade.

1. No **Object Explorer**, faça duplo clique de base de dados de Olá, aponte demasiado**tarefas...** , clique em **cópia de segurança**.

1. Clique em **OK** tootake uma localização de cópia de segurança predefinida toohello cópia de segurança completa.

## <a name="create-hello-availability-group"></a>Criar grupo de disponibilidade de Olá
Agora, está pronto tooconfigure um grupo de disponibilidade com Olá os seguintes passos:

* Criar uma base de dados Olá primeiro o SQL Server.
* Coloque uma cópia de segurança completa e uma cópia de segurança do registo de transações da base de dados de Olá
* Olá de restauro completa e toohello de cópias de segurança de registo segundo do SQL Server com Olá **NORECOVERY** opção
* Criar grupo de disponibilidade de Olá (**AG1**) com consolidação síncrona, ativação pós-falha automática e as réplicas secundárias legíveis

### <a name="create-hello-availability-group"></a>Crie grupo de disponibilidade de Olá:

1. Na sessão de ambiente de trabalho remoto toohello primeiro o SQL Server. No **Object Explorer** no SSMS, faça duplo clique **elevada disponibilidade do AlwaysOn** e clique em **Assistente de novo grupo de disponibilidade**.

    ![Iniciar o Assistente de novo grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. No Olá **introdução** página, clique em **seguinte**. No Olá **Especificar nome do grupo de disponibilidade** , escreva um nome para Olá grupo de disponibilidade, por exemplo **AG1**, na **nome do grupo de disponibilidade**. Clique em **Seguinte**.

    ![Assistente de nova AG, especifique o nome de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. No Olá **selecionar bases de dados** página, selecione a base de dados e clique em **seguinte**.

   >[!NOTE]
   >base de dados de Olá cumpre Olá pré-requisitos para um grupo de disponibilidade como efetuou, pelo menos, uma cópia de segurança completa em Olá pretendido, réplica primária.

   ![Assistente de nova AG, selecione as bases de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. No Olá **especificar réplicas** página, clique em **Adicionar réplica**.

   ![Assistente de nova AG, especifique as réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Olá **ligar tooServer** aparece a caixa de diálogo. Nome do tipo Olá de Olá segundo servidor **nome do servidor**. Clique em **Ligar**.

   Novamente no Olá **especificar réplicas** página, deverá ver segundo servidor de Olá listado no **réplicas de disponibilidade**. Configure réplicas de Olá da seguinte forma.

   ![Assistente de nova AG, especifique as réplicas (completa)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Clique em **pontos finais** toosee Olá ponto final de espelhamento para este grupo de disponibilidade. Olá utilize mesma porta que utilizou quando definiu Olá [regra de firewall para pontos finais de espelhamento da base de dados](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Assistente de nova AG, selecione a sincronização inicial de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. No Olá **selecionar sincronização de dados inicial** página, selecione **completa** e especifique uma localização de rede partilhada. Para a localização de Olá, utilize Olá [partilha de cópia de segurança que criou](#backupshare). Exemplo de Olá estava, **\\\\\<primeiro o SQL Server\>\Backup\**. Clique em **Seguinte**.

   >[!NOTE]
   >Sincronização completa demora uma cópia de segurança completa da base de dados de Olá na primeira instância de Olá do SQL Server e restaura-toohello segunda instância. Sincronização completa não é recomendada para bases de dados grandes, porque poderá demorar muito tempo. Pode reduzir este tempo manualmente fazer uma cópia de segurança da base de dados de Olá e restaurado com `NO RECOVERY`. Se a base de dados de Olá já for restaurada com `NO RECOVERY` no Olá segundo do SQL Server antes de configurar Olá grupo de disponibilidade, escolha **apenas junção**. Se pretender que a cópia de segurança do tootake Olá depois de configurar Olá grupo de disponibilidade, escolha **ignorar sincronização de dados inicial**.

    ![Assistente de nova AG, selecione a sincronização inicial de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. No Olá **validação** página, clique em **seguinte**. Esta página deve ter um aspeto semelhante toohello seguinte imagem:

    ![Assistente de nova AG, validação](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Não há um aviso para a configuração do serviço de escuta de Olá porque não tiver configurado um serviço de escuta do grupo de disponibilidade. Pode ignorar este aviso porque em máquinas virtuais do Azure cria serviço de escuta de Olá depois de criar Balanceador de carga do Azure de Olá.

10. No Olá **resumo** página, clique em **concluir**, em seguida, aguarde enquanto o Assistente de Olá configura Olá novo grupo de disponibilidade. No Olá **progresso** página, pode clicar **mais detalhes** tooview Olá detalhadas progresso. Assim que o Assistente de Olá estiver concluído, Inspecione Olá **resultados** tooverify de página que Olá o grupo de disponibilidade é criado com êxito.

     ![Assistente de novo AG resulta](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Clique em **fechar** Assistente de Olá tooexit.

### <a name="check-hello-availability-group"></a>Olá de verificação de grupo de disponibilidade

1. No **Object Explorer**, expanda **elevada disponibilidade do AlwaysOn**, em seguida, expanda **grupos de disponibilidade**. Deverá ver Olá novo grupo de disponibilidade neste contentor. Faça duplo clique Olá grupo de disponibilidade e clique em **Mostrar Dashboard**.

   ![Mostrar AG Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   O **AlwaysOn Dashboard** deverá ter um aspeto semelhante toothis.

   ![Dashboard de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Pode ver réplicas Olá, modo de ativação pós-falha de Olá cada réplica e Olá do Estado de sincronização.

2. No **Gestor de clusters de ativação pós-falha**, clique em cluster. Selecione **funções**. o nome do grupo de disponibilidade Olá utilizou é uma função em cluster Olá. Se o grupo de disponibilidade não tem um endereço IP para ligações de cliente, porque não foi possível configurar um serviço de escuta. Irá configurar o serviço de escuta de Olá depois de criar um balanceador de carga do Azure.

   ![AG no Gestor de clusters de ativação pós-falha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Não tente toofail através de Olá grupo de disponibilidade de Olá Gestor de clusters de ativação pós-falha. Todas as operações de ativação pós-falha devem ser efetuadas a partir do **AlwaysOn Dashboard** no SSMS. Para obter mais informações, consulte [restrições Using Olá Gestor de clusters de ativação pós-falha com grupos de disponibilidade](https://msdn.microsoft.com/library/ff929171.aspx).
    >

Neste momento, tem um grupo de disponibilidade com réplicas em duas instâncias do SQL Server. Pode mover o grupo de disponibilidade de Olá entre instâncias. Não é possível ligar toohello grupo de disponibilidade ainda porque não dispõe de um serviço de escuta. Nas máquinas virtuais do Azure, o serviço de escuta de Olá requer um balanceador de carga. Olá passo seguinte consiste em Balanceador de carga Olá toocreate no Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Criar um balanceador de carga do Azure

Máquinas virtuais do Azure, um grupo de disponibilidade do SQL Server necessita de um balanceador de carga. Balanceador de carga Olá contém o endereço IP Olá para o serviço de escuta do grupo de disponibilidade Olá. Esta secção resume como toocreate Olá carregar balanceador no Olá portal do Azure.

1. Olá portal do Azure, aceda toohello grupo de recursos em que os servidores do SQL Server estão e clique em **+ adicionar**.
2. Procurar **Balanceador de carga**. Escolha o Balanceador de carga Olá publicado pela Microsoft.

   ![AG no Gestor de clusters de ativação pós-falha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Clique em **Criar**.
3. Configure Olá seguir os parâmetros Olá Balanceador de carga.

   | Definição | Campo |
   | --- | --- |
   | **Nome** |Utilizar um nome de texto para o Balanceador de carga Olá, por exemplo **sqlLB**. |
   | **Tipo** |Interno |
   | **Rede virtual** |Utilize o nome de Olá de Olá rede virtual do Azure. |
   | **Sub-rede** |Utilize o nome de Olá da sub-rede Olá que Olá máquina virtual está a ser.  |
   | **Atribuição de endereços IP** |Estático |
   | **Endereço IP** |Utilize um endereço disponível da sub-rede. |
   | **Subscrição** |Utilize Olá mesmo subscrição como máquina virtual de Olá. |
   | **Localização** |Utilize Olá mesma localização da máquina virtual de Olá. |

   Olá painel do portal do Azure deve ter o seguinte aspeto:

   ![Criar Balanceador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Clique em **criar**, Balanceador de carga de Olá toocreate.

Balanceador de carga do tooconfigure Olá, terá de toocreate um conjunto de back-end, uma pesquisa e regras de balanceamento de carga de Olá de conjunto. Efetue estes no Olá portal do Azure.

### <a name="add-backend-pool"></a>Adicionar o conjunto de back-end

1. No portal do Azure Olá, visite tooyour grupo de disponibilidade. Poderá ter de Balanceador de carga do toorefresh Olá vista toosee Olá recentemente criado.

   ![Localizar o Balanceador de carga no grupo de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Clique em Balanceador de carga Olá, clique em **conjuntos back-end**e clique em **+ adicionar**. Defina o conjunto de back-end Olá da seguinte forma:

   | Definição | Descrição | Exemplo
   | --- | --- |---
   | **Nome** | Escreva um nome de texto | SQLLBBE
   | **Associado a** | Escolha a partir da lista | Conjunto de disponibilidade
   | **Conjunto de disponibilidade** | Utilize um nome de conjunto de disponibilidade de Olá que as suas VMs do SQL Server estão em | sqlAvailabilitySet |
   | **Máquinas virtuais** |Olá, dois nomes de VM do Azure SQL Server | SQLServer-0, sqlserver 1

1. Nome do conjunto de back-end Olá Olá.

1. Clique em **+ adicionar uma máquina virtual**.

1. Olá para conjunto de disponibilidade, escolha o conjunto de disponibilidade de Olá esse Olá servidores SQL Server estão em.

1. Para máquinas virtuais, incluem ambos Olá SQL Servers. Não inclua o servidor de testemunho de partilha de ficheiros de Olá.

1. Clique em **OK** pool de back-end de Olá toocreate.

### <a name="set-hello-probe"></a>Conjunto Olá sonda

1. Clique em Balanceador de carga Olá, clique em **sondas de estado de funcionamento**e clique em **+ adicionar**.

1. Defina a sonda de estado de funcionamento de Olá da seguinte forma:

   | Definição | Descrição | Exemplo
   | --- | --- |---
   | **Nome** | Texto | SQLAlwaysOnEndPointProbe |
   | **Protocolo** | Escolha TCP | TCP |
   | **Porta** | Qualquer porta não utilizada | 59999 |
   | **Intervalo**  | Olá período de tempo entre sonda tenta em segundos |5 |
   | **Limiar de mau estado de funcionamento** | Olá, número de falhas de sonda consecutivas que deve ocorrer para toobe uma máquina virtual considerado em mau estado de funcionamento  | 2 |

1. Clique em **OK** sonda de estado de funcionamento de Olá tooset.

### <a name="set-hello-load-balancing-rules"></a>Definir regras de balanceamento de carga Olá

1. Clique em Balanceador de carga Olá, clique em **as regras de balanceamento de carga**e clique em **+ adicionar**.

1. Definir a forma de regras de balanceamento de carga de Olá.
   | Definição | Descrição | Exemplo
   | --- | --- |---
   | **Nome** | Texto | SQLAlwaysOnEndPointListener |
   | **Endereço IP de front-end** | Escolha um endereço |Utilize o endereço de Olá que criou quando criou o Balanceador de carga Olá. |
   | **Protocolo** | Escolha TCP |TCP |
   | **Porta** | Utilizar a porta de Olá para a instância do SQL Server Olá | 1433 |
   | **Porta de back-end** | Este campo não é utilizado quando o IP flutuante está definido para direta do servidor retorno | 1433 |
   | **Sonda** |nome de Olá especificado para a sonda de Olá | SQLAlwaysOnEndPointProbe |
   | **Persistência da sessão** | Na lista pendente | **Nenhum** |
   | **Tempo limite de inatividade** | Tookeep minutos abrir uma ligação de TCP | 4 |
   | **Vírgula flutuante (devolução direta do servidor) de IP** | |Ativado |

   > [!WARNING]
   > Devolução direta do servidor é definida durante a criação. Não pode ser alterada.

1. Clique em **OK** regras de balanceamento de carga na Olá tooset.

## <a name="configure-listener"></a>Configurar o serviço de escuta de Olá

Olá seguinte coisa toodo é tooconfigure um serviço de escuta do grupo de disponibilidade no cluster de ativação pós-falha de Olá.

> [!NOTE]
> Este tutorial mostra como endereço toocreate um único serviço de escuta - um IP do ILB. toocreate um ou mais serviços de escuta com um ou mais endereços IP, consulte [Balanceador de carga e do serviço de escuta do grupo de disponibilidade criar | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Porta do serviço de escuta de conjunto

No SQL Server Management Studio, defina a porta de serviço de escuta de Olá.

1. Inicie o SQL Server Management Studio e ligue a réplica primária toohello.

1. Navegue demasiado**elevada disponibilidade do AlwaysOn** | **grupos de disponibilidade** | **escuta do grupo de disponibilidade**.

1. Deverá ver agora o nome do serviço de escuta de Olá que criou no Gestor de clusters de ativação pós-falha. Clique no nome do serviço de escuta de Olá e clique em **propriedades**.

1. No Olá **porta** caixa, especifique o número da porta de escuta do grupo de disponibilidade de Olá Olá utilizando Olá $EndpointPort que utilizou anteriormente (1433 foi predefinido Olá), em seguida, clique em **OK**.

Tem agora um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure em execução no modo Resource Manager.

## <a name="test-connection-toolistener"></a>Toolistener de ligação de teste

ligação de Olá tootest:

1. RDP tooa SQL Server que está a ser Olá mesmo virtual de rede, mas não réplica Olá próprio. Pode utilizar Olá outro servidor de SQL no cluster de Olá.

1. Utilize **sqlcmd** ligação do utilitário tootest Olá. Por exemplo, o seguinte script de Olá estabelece uma **sqlcmd** réplica primária de toohello ligação através do serviço de escuta de Olá com autenticação do Windows:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Se o serviço de escuta de Olá é utilizar uma porta diferente de Olá predefinido (1433) de porta, especifique a porta de Olá na cadeia de ligação de Olá. Por exemplo, hello seguinte comando sqlcmd liga tooa escuta na porta 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Olá ligação SQLCMD liga automaticamente toowhichever instância da réplica primária do SQL Server anfitriões Olá.

> [!TIP]
> Certifique-se de que a porta de Olá que especificar está aberta na firewall de Olá de ambos os servidores SQL. Ambos os servidores necessitam de uma regra de entrada para Olá a porta TCP que utiliza. Para obter mais informações, consulte [adicionar ou Editar regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Passos seguintes

- [Adicionar um balanceador de carga do tooa de endereço IP para um segundo grupo de disponibilidade](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
