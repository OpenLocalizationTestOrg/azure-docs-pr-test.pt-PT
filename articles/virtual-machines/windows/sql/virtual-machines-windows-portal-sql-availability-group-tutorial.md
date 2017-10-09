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
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="5752d-103">Configurar sempre no grupo de disponibilidade na VM do Azure manualmente</span><span class="sxs-lookup"><span data-stu-id="5752d-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="5752d-104">Este tutorial mostra como toocreate um servidor sempre no grupo de disponibilidade SQL em Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="5752d-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="5752d-105">tutorial de conclusão de Olá cria um grupo de disponibilidade com uma réplica de base de dados em dois servidores do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="5752d-106">**Estimativa de tempo**: demora cerca de 30 minutos toocomplete depois Olá pré-requisitos são cumpridos.</span><span class="sxs-lookup"><span data-stu-id="5752d-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="5752d-107">Diagrama de Olá ilustra a compilação no tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="5752d-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5752d-109">Prerequisites</span></span>

<span data-ttu-id="5752d-110">Olá tutorial parte do princípio de que tem uma compreensão básica do SQL Server em grupos de disponibilidade Always.</span><span class="sxs-lookup"><span data-stu-id="5752d-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="5752d-111">Se precisar de mais informações, consulte o artigo [descrição geral de grupos de disponibilidade Always (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="5752d-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="5752d-112">Olá tabela seguinte lista os pré-requisitos de Olá terá toocomplete antes de iniciar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="5752d-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="5752d-113">Requisito</span><span class="sxs-lookup"><span data-stu-id="5752d-113">Requirement</span></span> |<span data-ttu-id="5752d-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="5752d-114">Description</span></span> |
|----- |----- |----- |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="5752d-116">Dois servidores do SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-116">Two SQL Servers</span></span> | <span data-ttu-id="5752d-117">-Num conjunto de disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="5752d-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="5752d-118">-Num único domínio</span><span class="sxs-lookup"><span data-stu-id="5752d-118">- In a single domain</span></span> <br/> <span data-ttu-id="5752d-119">-Com a funcionalidade de Clustering de ativação pós-falha instalada</span><span class="sxs-lookup"><span data-stu-id="5752d-119">- With Failover Clustering feature installed</span></span> |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="5752d-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="5752d-121">Windows Server</span></span> | <span data-ttu-id="5752d-122">Partilha de ficheiros para o testemunho de cluster</span><span class="sxs-lookup"><span data-stu-id="5752d-122">File share for cluster witness</span></span> |  
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5752d-124">Conta de serviço do SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-124">SQL Server service account</span></span> | <span data-ttu-id="5752d-125">Conta de domínio</span><span class="sxs-lookup"><span data-stu-id="5752d-125">Domain account</span></span> |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5752d-127">Conta de serviço do SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="5752d-127">SQL Server Agent service account</span></span> | <span data-ttu-id="5752d-128">Conta de domínio</span><span class="sxs-lookup"><span data-stu-id="5752d-128">Domain account</span></span> |  
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5752d-130">Abrir portas de firewall</span><span class="sxs-lookup"><span data-stu-id="5752d-130">Firewall ports open</span></span> | <span data-ttu-id="5752d-131">-SQL Server: **1433** para a instância predefinida</span><span class="sxs-lookup"><span data-stu-id="5752d-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="5752d-132">-Ponto final de espelhamento: **5022** ou qualquer porta disponível</span><span class="sxs-lookup"><span data-stu-id="5752d-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="5752d-133">-Sonda do Balanceador de carga as do azure: **59999** ou qualquer porta disponível</span><span class="sxs-lookup"><span data-stu-id="5752d-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5752d-135">Adicionar a funcionalidade de Clustering de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="5752d-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="5752d-136">Esta funcionalidade necessitam de ambos os servidores do SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-136">Both SQL Servers require this feature</span></span> |
|![parênteses](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5752d-138">Conta de domínio de instalação</span><span class="sxs-lookup"><span data-stu-id="5752d-138">Installation domain account</span></span> | <span data-ttu-id="5752d-139">-Administrador local em cada servidor de SQL</span><span class="sxs-lookup"><span data-stu-id="5752d-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="5752d-140">-O membro da função de servidor fixa sysadmin do SQL Server para cada instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="5752d-141">Antes de começar Olá tutorial, terá de demasiado[concluir os pré-requisitos para a criação de grupos de disponibilidade Always em Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="5752d-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="5752d-142">Se os pré-requisitos são já foi concluídos, pode saltar demasiado[criar Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="5752d-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="5752d-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="5752d-144">Depois de Olá pré-requisitos estão concluídos, Step-by-Olá primeiro passo é toocreate num Cluster de ativação pós-falha do Windows Server que inclua dois SQL Servers e um servidor de testemunho.</span><span class="sxs-lookup"><span data-stu-id="5752d-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="5752d-145">RDP toohello primeiro servidor de SQL Server utilizando uma conta de domínio que seja de administrador nos servidores do SQL Server e servidor de testemunho Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="5752d-146">Se seguiu Olá [documento de pré-requisitos](virtual-machines-windows-portal-sql-availability-group-prereq.md), criou uma conta chamada **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="5752d-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="5752d-147">Utilize esta conta.</span><span class="sxs-lookup"><span data-stu-id="5752d-147">Use this account.</span></span>

2. <span data-ttu-id="5752d-148">No Olá **Gestor de servidor** dashboard, selecione **ferramentas**e, em seguida, clique em **Gestor de clusters de ativação pós-falha**.</span><span class="sxs-lookup"><span data-stu-id="5752d-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="5752d-149">No painel esquerdo Olá, faça duplo clique **Gestor de clusters de ativação pós-falha**e, em seguida, clique em **criar um Cluster**.</span><span class="sxs-lookup"><span data-stu-id="5752d-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="5752d-150">![Criar Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="5752d-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="5752d-151">No Assistente para criar clusters de Olá, criar um cluster de um nó, avance nas páginas de Olá com definições de Olá no Olá a tabela seguinte:</span><span class="sxs-lookup"><span data-stu-id="5752d-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="5752d-152">Página</span><span class="sxs-lookup"><span data-stu-id="5752d-152">Page</span></span> | <span data-ttu-id="5752d-153">Definições</span><span class="sxs-lookup"><span data-stu-id="5752d-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="5752d-154">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5752d-154">Before You Begin</span></span> |<span data-ttu-id="5752d-155">Utilize as predefinições</span><span class="sxs-lookup"><span data-stu-id="5752d-155">Use defaults</span></span> |
   | <span data-ttu-id="5752d-156">Selecionar servidores</span><span class="sxs-lookup"><span data-stu-id="5752d-156">Select Servers</span></span> |<span data-ttu-id="5752d-157">Olá tipo nome do primeiro servidor de SQL no **introduza o nome de servidor** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="5752d-158">Aviso de validação</span><span class="sxs-lookup"><span data-stu-id="5752d-158">Validation Warning</span></span> |<span data-ttu-id="5752d-159">Selecione **um número não precisar do suporte da Microsoft para este cluster e, por conseguinte, não pretender que a validação de Olá toorun os testes. Quando posso clicar em seguinte, continuar a criar o cluster de Olá**.</span><span class="sxs-lookup"><span data-stu-id="5752d-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="5752d-160">Ponto de acesso para administrar Olá Cluster</span><span class="sxs-lookup"><span data-stu-id="5752d-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="5752d-161">Escreva um nome de cluster, por exemplo **SQLAGCluster1** no **nome do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="5752d-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="5752d-162">Confirmação</span><span class="sxs-lookup"><span data-stu-id="5752d-162">Confirmation</span></span> |<span data-ttu-id="5752d-163">Utilize as predefinições, exceto se estiver a utilizar os espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5752d-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="5752d-164">Consulte a nota Olá após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="5752d-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="5752d-165">Definir o endereço IP de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="5752d-166">No **Gestor de clusters de ativação pós-falha**, desloque para baixo demasiado**recursos principais do Cluster** e expanda os detalhes do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="5752d-167">Deverá ver dois Olá **nome** e Olá **endereço IP** recursos Olá **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="5752d-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="5752d-168">Olá recurso de endereço IP não pode ser colocado online porque o cluster de Olá é atribuído Olá mesmo endereço IP como Olá computador, pelo que é um endereço duplicado.</span><span class="sxs-lookup"><span data-stu-id="5752d-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="5752d-169">Olá de contexto não conseguiu **endereço IP** recursos e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5752d-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Propriedades do cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="5752d-171">Selecione **endereço IP estático** e especifique um endereço de sub-rede onde Olá do SQL Server está na caixa de texto endereço Olá disponível.</span><span class="sxs-lookup"><span data-stu-id="5752d-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="5752d-172">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5752d-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="5752d-173">No Olá **recursos principais do Cluster** secção, clique no nome do cluster e clique em **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="5752d-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="5752d-174">Em seguida, aguarde até que ambos os recursos estão online.</span><span class="sxs-lookup"><span data-stu-id="5752d-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="5752d-175">Quando o recurso de nome de cluster Olá fica online, atualiza o servidor de DC Olá com uma nova conta de computador do AD.</span><span class="sxs-lookup"><span data-stu-id="5752d-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="5752d-176">Utilize este Olá de toorun do AD conta serviço de grupo de disponibilidade em cluster mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5752d-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="5752d-177"><a name="addNode"></a>Adicionar Olá outro toocluster do SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="5752d-178">Adicionar Olá outro cluster de toohello do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="5752d-179">Na árvore de browser de Olá, faça duplo clique cluster Olá e clique em **adicionar nó**.</span><span class="sxs-lookup"><span data-stu-id="5752d-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Adicionar nó toohello Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="5752d-181">No Olá **Assistente de adicionar nó**, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="5752d-182">No Olá **selecionar servidores** página, adicione Olá segundo servidor de SQL.</span><span class="sxs-lookup"><span data-stu-id="5752d-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="5752d-183">Nome do servidor do tipo Olá na **introduza o nome de servidor** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="5752d-184">Quando tiver terminado, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="5752d-185">No Olá **aviso de validação** página, clique em **não** (num cenário de produção, deve executar testes de validação de Olá).</span><span class="sxs-lookup"><span data-stu-id="5752d-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="5752d-186">Clique depois em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="5752d-187">No Olá **confirmação** página se estiver a utilizar espaços de armazenamento, desmarque Olá caixa de verificação com etiqueta **adicionar todos os clusters de toohello o armazenamento elegível.**</span><span class="sxs-lookup"><span data-stu-id="5752d-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Adicionar a confirmação do nó](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="5752d-189">Se estiver a utilizar os espaços de armazenamento e não desmarque **adicionar todos os clusters de toohello o armazenamento elegível**, Windows Desanexa discos virtuais Olá durante Olá clustering processo.</span><span class="sxs-lookup"><span data-stu-id="5752d-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="5752d-190">Como resultado, não aparecerem no Gestor de discos ou Explorer até que os espaços de armazenamento Olá são removidos do cluster de Olá e novamente ligado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5752d-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="5752d-191">Vários discos no toostorage conjuntos de grupos de espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5752d-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="5752d-192">Para obter mais informações, consulte [espaços de armazenamento](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="5752d-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="5752d-193">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-193">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-194">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="5752d-194">Click **Finish**.</span></span>

   <span data-ttu-id="5752d-195">Gestor de clusters de ativação pós-falha mostra que o cluster tem um novo nó e listas-lo no Olá **nós** contentor.</span><span class="sxs-lookup"><span data-stu-id="5752d-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="5752d-196">Terminar sessão de ambiente de trabalho remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="5752d-197">Adicionar uma partilha de ficheiros de quórum do cluster</span><span class="sxs-lookup"><span data-stu-id="5752d-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="5752d-198">Neste exemplo o cluster do Windows hello utiliza um toocreate de partilha de ficheiros um quórum de cluster.</span><span class="sxs-lookup"><span data-stu-id="5752d-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="5752d-199">Este tutorial utiliza um quórum maioria de partilha de ficheiros e de nó.</span><span class="sxs-lookup"><span data-stu-id="5752d-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="5752d-200">Para obter mais informações, consulte [Noções sobre configurações de quórum num Cluster de ativação pós-falha](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="5752d-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="5752d-201">Ligar o servidor de membro de testemunho de partilha de ficheiros de toohello com uma sessão de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="5752d-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="5752d-202">No **Gestor de servidor**, clique em **ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="5752d-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="5752d-203">Abra **gestão de computadores**.</span><span class="sxs-lookup"><span data-stu-id="5752d-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="5752d-204">Clique em **pastas partilhadas**.</span><span class="sxs-lookup"><span data-stu-id="5752d-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="5752d-205">Clique com botão direito **partilhas**e clique em **nova partilha...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="5752d-207">Utilize **partilhado pasta Assistente para criar um** toocreate uma partilha.</span><span class="sxs-lookup"><span data-stu-id="5752d-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="5752d-208">No **caminho da pasta**, clique em **procurar** e localizem ou criar um caminho de pasta partilhada Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="5752d-209">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-209">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-210">No **nome, descrição e as definições** verificar Olá partilha nome e caminho.</span><span class="sxs-lookup"><span data-stu-id="5752d-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="5752d-211">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-211">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-212">No **as permissões da pasta partilhada** definir **personalizar permissões**.</span><span class="sxs-lookup"><span data-stu-id="5752d-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="5752d-213">Clique em **personalizados...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="5752d-214">No **personalizar permissões**, clique em **adicionar...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="5752d-215">Certifique-se de que Olá conta utilizada toocreate Olá cluster tem controlo total.</span><span class="sxs-lookup"><span data-stu-id="5752d-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="5752d-217">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5752d-217">Click **OK**.</span></span>

1. <span data-ttu-id="5752d-218">No **as permissões da pasta partilhada**, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="5752d-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="5752d-219">Clique em **concluir** novamente.</span><span class="sxs-lookup"><span data-stu-id="5752d-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="5752d-220">Termine sessão no servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="5752d-221">Configurar o quórum do cluster</span><span class="sxs-lookup"><span data-stu-id="5752d-221">Configure cluster quorum</span></span>

<span data-ttu-id="5752d-222">Em seguida, configure o quórum do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="5752d-223">Ligar toohello primeiro nó de cluster com o ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="5752d-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="5752d-224">No **Gestor de clusters de ativação pós-falha**, clique no cluster de Olá, aponte demasiado**mais ações**e clique em **configurar definições de quórum do Cluster...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="5752d-226">No **Cluster Assistente para configurar quórum**, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="5752d-227">No **selecionar opção de configuração de quórum**, escolha **selecionar testemunho de quórum Olá**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="5752d-228">No **selecionar testemunho de quórum**, clique em **configurar um testemunho de partilha de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="5752d-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="5752d-229">Windows Server 2016 suporta um testemunho de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5752d-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="5752d-230">Se escolher este tipo de testemunho, não precisa de um ficheiro de testemunho de partilha.</span><span class="sxs-lookup"><span data-stu-id="5752d-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="5752d-231">Para obter mais informações, consulte [implementar um testemunho de nuvem para um Cluster de ativação pós-falha](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="5752d-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="5752d-232">Este tutorial utiliza um testemunho de partilha de ficheiros, que é suportado pelos sistemas operativos anteriores.</span><span class="sxs-lookup"><span data-stu-id="5752d-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="5752d-233">No **configurar testemunho de partilha de ficheiros**, o caminho para partilha de Olá criou Olá do tipo.</span><span class="sxs-lookup"><span data-stu-id="5752d-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="5752d-234">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-234">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-235">Verifique as definições de Olá no **confirmação**.</span><span class="sxs-lookup"><span data-stu-id="5752d-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="5752d-236">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-236">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-237">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="5752d-237">Click **Finish**.</span></span>

<span data-ttu-id="5752d-238">recursos de principais do cluster Olá estão configurados com um testemunho de partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="5752d-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="5752d-239">Ativar grupos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5752d-239">Enable Availability Groups</span></span>

<span data-ttu-id="5752d-240">Em seguida, ative Olá **grupos de Disponibilidade AlwaysOn** funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="5752d-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="5752d-241">Execute estes passos em ambos os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="5752d-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="5752d-242">De Olá **iniciar** ecrã, iniciar **Gestor de configuração do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="5752d-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="5752d-243">Na árvore de browser de Olá, clique em **do SQL Server Services**, em seguida, clique com botão direito Olá **SQL Server (MSSQLSERVER)** de serviço e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5752d-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="5752d-244">Clique em Olá **elevada disponibilidade do AlwaysOn** separador, em seguida, selecione **ative os grupos de Disponibilidade AlwaysOn**, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5752d-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Ativar grupos de Disponibilidade AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="5752d-246">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-246">Click **Apply**.</span></span> <span data-ttu-id="5752d-247">Clique em **OK** na caixa de diálogo de pop-up Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="5752d-248">Reinicie o serviço do SQL Server Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="5752d-249">Repita estes passos em Olá outro servidor do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-249">Repeat these steps on hello other SQL Server.</span></span>

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

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="5752d-250">Criar uma base de dados Olá primeiro o SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="5752d-251">Iniciar Olá RDP ficheiro toohello primeiro o SQL Server com um domínio de conta que seja um membro do administrador do sistema a função de servidor fixo.</span><span class="sxs-lookup"><span data-stu-id="5752d-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="5752d-252">Abra o SQL Server Management Studio e ligue toohello primeiro o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="5752d-253">No **Object Explorer**, faça duplo clique **bases de dados** e clique em **nova base de dados**.</span><span class="sxs-lookup"><span data-stu-id="5752d-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="5752d-254">No **nome de base de dados**, tipo **MyDB1**, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5752d-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="5752d-255"><a name="backupshare"></a>Criar uma partilha de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="5752d-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="5752d-256">No Olá primeiro o SQL Server no **Gestor de servidor**, clique em **ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="5752d-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="5752d-257">Abra **gestão de computadores**.</span><span class="sxs-lookup"><span data-stu-id="5752d-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="5752d-258">Clique em **pastas partilhadas**.</span><span class="sxs-lookup"><span data-stu-id="5752d-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="5752d-259">Clique com botão direito **partilhas**e clique em **nova partilha...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="5752d-261">Utilize **partilhado pasta Assistente para criar um** toocreate uma partilha.</span><span class="sxs-lookup"><span data-stu-id="5752d-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="5752d-262">No **caminho da pasta**, clique em **procurar** e localizem ou criar um caminho de pasta partilhada do Olá da base de dados cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="5752d-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="5752d-263">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-263">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-264">No **nome, descrição e as definições** verificar Olá partilha nome e caminho.</span><span class="sxs-lookup"><span data-stu-id="5752d-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="5752d-265">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-265">Click **Next**.</span></span>

1. <span data-ttu-id="5752d-266">No **as permissões da pasta partilhada** definir **personalizar permissões**.</span><span class="sxs-lookup"><span data-stu-id="5752d-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="5752d-267">Clique em **personalizados...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="5752d-268">No **personalizar permissões**, clique em **adicionar...** .</span><span class="sxs-lookup"><span data-stu-id="5752d-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="5752d-269">Certifique-se de que as contas de serviço de SQL Server e SQL Server Agent Olá para ambos os servidores têm controlo total.</span><span class="sxs-lookup"><span data-stu-id="5752d-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nova partilha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="5752d-271">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5752d-271">Click **OK**.</span></span>

1. <span data-ttu-id="5752d-272">No **as permissões da pasta partilhada**, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="5752d-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="5752d-273">Clique em **concluir** novamente.</span><span class="sxs-lookup"><span data-stu-id="5752d-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="5752d-274">Criar um completo cópia de segurança da base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-274">Take a full backup of hello database</span></span>

<span data-ttu-id="5752d-275">É necessário tooback segurança Olá nova base de dados tooinitialize Olá da cadeia de registos.</span><span class="sxs-lookup"><span data-stu-id="5752d-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="5752d-276">Se não efetuar uma cópia de segurança da base de dados nova Olá, não pode ser incluído num grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5752d-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="5752d-277">No **Object Explorer**, faça duplo clique de base de dados de Olá, aponte demasiado**tarefas...** , clique em **cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="5752d-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="5752d-278">Clique em **OK** tootake uma localização de cópia de segurança predefinida toohello cópia de segurança completa.</span><span class="sxs-lookup"><span data-stu-id="5752d-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="5752d-279">Criar grupo de disponibilidade de Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-279">Create hello Availability Group</span></span>
<span data-ttu-id="5752d-280">Agora, está pronto tooconfigure um grupo de disponibilidade com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5752d-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="5752d-281">Criar uma base de dados Olá primeiro o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="5752d-282">Coloque uma cópia de segurança completa e uma cópia de segurança do registo de transações da base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="5752d-283">Olá de restauro completa e toohello de cópias de segurança de registo segundo do SQL Server com Olá **NORECOVERY** opção</span><span class="sxs-lookup"><span data-stu-id="5752d-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="5752d-284">Criar grupo de disponibilidade de Olá (**AG1**) com consolidação síncrona, ativação pós-falha automática e as réplicas secundárias legíveis</span><span class="sxs-lookup"><span data-stu-id="5752d-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="5752d-285">Crie grupo de disponibilidade de Olá:</span><span class="sxs-lookup"><span data-stu-id="5752d-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="5752d-286">Na sessão de ambiente de trabalho remoto toohello primeiro o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="5752d-287">No **Object Explorer** no SSMS, faça duplo clique **elevada disponibilidade do AlwaysOn** e clique em **Assistente de novo grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="5752d-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Iniciar o Assistente de novo grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="5752d-289">No Olá **introdução** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="5752d-290">No Olá **Especificar nome do grupo de disponibilidade** , escreva um nome para Olá grupo de disponibilidade, por exemplo **AG1**, na **nome do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="5752d-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="5752d-291">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-291">Click **Next**.</span></span>

    ![Assistente de nova AG, especifique o nome de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="5752d-293">No Olá **selecionar bases de dados** página, selecione a base de dados e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5752d-294">base de dados de Olá cumpre Olá pré-requisitos para um grupo de disponibilidade como efetuou, pelo menos, uma cópia de segurança completa em Olá pretendido, réplica primária.</span><span class="sxs-lookup"><span data-stu-id="5752d-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Assistente de nova AG, selecione as bases de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="5752d-296">No Olá **especificar réplicas** página, clique em **Adicionar réplica**.</span><span class="sxs-lookup"><span data-stu-id="5752d-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Assistente de nova AG, especifique as réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="5752d-298">Olá **ligar tooServer** aparece a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5752d-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="5752d-299">Nome do tipo Olá de Olá segundo servidor **nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="5752d-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="5752d-300">Clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-300">Click **Connect**.</span></span>

   <span data-ttu-id="5752d-301">Novamente no Olá **especificar réplicas** página, deverá ver segundo servidor de Olá listado no **réplicas de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="5752d-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="5752d-302">Configure réplicas de Olá da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="5752d-302">Configure hello replicas as follows.</span></span>

   ![Assistente de nova AG, especifique as réplicas (completa)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="5752d-304">Clique em **pontos finais** toosee Olá ponto final de espelhamento para este grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5752d-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="5752d-305">Olá utilize mesma porta que utilizou quando definiu Olá [regra de firewall para pontos finais de espelhamento da base de dados](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="5752d-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Assistente de nova AG, selecione a sincronização inicial de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="5752d-307">No Olá **selecionar sincronização de dados inicial** página, selecione **completa** e especifique uma localização de rede partilhada.</span><span class="sxs-lookup"><span data-stu-id="5752d-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="5752d-308">Para a localização de Olá, utilize Olá [partilha de cópia de segurança que criou](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="5752d-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="5752d-309">Exemplo de Olá estava, **\\\\\<primeiro o SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="5752d-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="5752d-310">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5752d-311">Sincronização completa demora uma cópia de segurança completa da base de dados de Olá na primeira instância de Olá do SQL Server e restaura-toohello segunda instância.</span><span class="sxs-lookup"><span data-stu-id="5752d-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="5752d-312">Sincronização completa não é recomendada para bases de dados grandes, porque poderá demorar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="5752d-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="5752d-313">Pode reduzir este tempo manualmente fazer uma cópia de segurança da base de dados de Olá e restaurado com `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="5752d-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="5752d-314">Se a base de dados de Olá já for restaurada com `NO RECOVERY` no Olá segundo do SQL Server antes de configurar Olá grupo de disponibilidade, escolha **apenas junção**.</span><span class="sxs-lookup"><span data-stu-id="5752d-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="5752d-315">Se pretender que a cópia de segurança do tootake Olá depois de configurar Olá grupo de disponibilidade, escolha **ignorar sincronização de dados inicial**.</span><span class="sxs-lookup"><span data-stu-id="5752d-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Assistente de nova AG, selecione a sincronização inicial de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="5752d-317">No Olá **validação** página, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="5752d-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="5752d-318">Esta página deve ter um aspeto semelhante toohello seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="5752d-318">This page should look similar toohello following image:</span></span>

    ![Assistente de nova AG, validação](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="5752d-320">Não há um aviso para a configuração do serviço de escuta de Olá porque não tiver configurado um serviço de escuta do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5752d-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="5752d-321">Pode ignorar este aviso porque em máquinas virtuais do Azure cria serviço de escuta de Olá depois de criar Balanceador de carga do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="5752d-322">No Olá **resumo** página, clique em **concluir**, em seguida, aguarde enquanto o Assistente de Olá configura Olá novo grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5752d-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="5752d-323">No Olá **progresso** página, pode clicar **mais detalhes** tooview Olá detalhadas progresso.</span><span class="sxs-lookup"><span data-stu-id="5752d-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="5752d-324">Assim que o Assistente de Olá estiver concluído, Inspecione Olá **resultados** tooverify de página que Olá o grupo de disponibilidade é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="5752d-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Assistente de novo AG resulta](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="5752d-326">Clique em **fechar** Assistente de Olá tooexit.</span><span class="sxs-lookup"><span data-stu-id="5752d-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="5752d-327">Olá de verificação de grupo de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5752d-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="5752d-328">No **Object Explorer**, expanda **elevada disponibilidade do AlwaysOn**, em seguida, expanda **grupos de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="5752d-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="5752d-329">Deverá ver Olá novo grupo de disponibilidade neste contentor.</span><span class="sxs-lookup"><span data-stu-id="5752d-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="5752d-330">Faça duplo clique Olá grupo de disponibilidade e clique em **Mostrar Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="5752d-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Mostrar AG Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="5752d-332">O **AlwaysOn Dashboard** deverá ter um aspeto semelhante toothis.</span><span class="sxs-lookup"><span data-stu-id="5752d-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Dashboard de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="5752d-334">Pode ver réplicas Olá, modo de ativação pós-falha de Olá cada réplica e Olá do Estado de sincronização.</span><span class="sxs-lookup"><span data-stu-id="5752d-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="5752d-335">No **Gestor de clusters de ativação pós-falha**, clique em cluster.</span><span class="sxs-lookup"><span data-stu-id="5752d-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="5752d-336">Selecione **funções**.</span><span class="sxs-lookup"><span data-stu-id="5752d-336">Select **Roles**.</span></span> <span data-ttu-id="5752d-337">o nome do grupo de disponibilidade Olá utilizou é uma função em cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="5752d-338">Se o grupo de disponibilidade não tem um endereço IP para ligações de cliente, porque não foi possível configurar um serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="5752d-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="5752d-339">Irá configurar o serviço de escuta de Olá depois de criar um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![AG no Gestor de clusters de ativação pós-falha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="5752d-341">Não tente toofail através de Olá grupo de disponibilidade de Olá Gestor de clusters de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="5752d-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="5752d-342">Todas as operações de ativação pós-falha devem ser efetuadas a partir do **AlwaysOn Dashboard** no SSMS.</span><span class="sxs-lookup"><span data-stu-id="5752d-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="5752d-343">Para obter mais informações, consulte [restrições Using Olá Gestor de clusters de ativação pós-falha com grupos de disponibilidade](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="5752d-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="5752d-344">Neste momento, tem um grupo de disponibilidade com réplicas em duas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5752d-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="5752d-345">Pode mover o grupo de disponibilidade de Olá entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="5752d-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="5752d-346">Não é possível ligar toohello grupo de disponibilidade ainda porque não dispõe de um serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="5752d-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="5752d-347">Nas máquinas virtuais do Azure, o serviço de escuta de Olá requer um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5752d-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="5752d-348">Olá passo seguinte consiste em Balanceador de carga Olá toocreate no Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="5752d-349">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="5752d-349">Create an Azure load balancer</span></span>

<span data-ttu-id="5752d-350">Máquinas virtuais do Azure, um grupo de disponibilidade do SQL Server necessita de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5752d-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="5752d-351">Balanceador de carga Olá contém o endereço IP Olá para o serviço de escuta do grupo de disponibilidade Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="5752d-352">Esta secção resume como toocreate Olá carregar balanceador no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="5752d-353">Olá portal do Azure, aceda toohello grupo de recursos em que os servidores do SQL Server estão e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="5752d-354">Procurar **Balanceador de carga**.</span><span class="sxs-lookup"><span data-stu-id="5752d-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="5752d-355">Escolha o Balanceador de carga Olá publicado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5752d-355">Choose hello load balancer published by Microsoft.</span></span>

   ![AG no Gestor de clusters de ativação pós-falha](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="5752d-357">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-357">Click **Create**.</span></span>
3. <span data-ttu-id="5752d-358">Configure Olá seguir os parâmetros Olá Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5752d-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="5752d-359">Definição</span><span class="sxs-lookup"><span data-stu-id="5752d-359">Setting</span></span> | <span data-ttu-id="5752d-360">Campo</span><span class="sxs-lookup"><span data-stu-id="5752d-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="5752d-361">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5752d-361">**Name**</span></span> |<span data-ttu-id="5752d-362">Utilizar um nome de texto para o Balanceador de carga Olá, por exemplo **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="5752d-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="5752d-363">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="5752d-363">**Type**</span></span> |<span data-ttu-id="5752d-364">Interno</span><span class="sxs-lookup"><span data-stu-id="5752d-364">Internal</span></span> |
   | <span data-ttu-id="5752d-365">**Rede virtual**</span><span class="sxs-lookup"><span data-stu-id="5752d-365">**Virtual network**</span></span> |<span data-ttu-id="5752d-366">Utilize o nome de Olá de Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="5752d-367">**Sub-rede**</span><span class="sxs-lookup"><span data-stu-id="5752d-367">**Subnet**</span></span> |<span data-ttu-id="5752d-368">Utilize o nome de Olá da sub-rede Olá que Olá máquina virtual está a ser.</span><span class="sxs-lookup"><span data-stu-id="5752d-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="5752d-369">**Atribuição de endereços IP**</span><span class="sxs-lookup"><span data-stu-id="5752d-369">**IP address assignment**</span></span> |<span data-ttu-id="5752d-370">Estático</span><span class="sxs-lookup"><span data-stu-id="5752d-370">Static</span></span> |
   | <span data-ttu-id="5752d-371">**Endereço IP**</span><span class="sxs-lookup"><span data-stu-id="5752d-371">**IP address**</span></span> |<span data-ttu-id="5752d-372">Utilize um endereço disponível da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5752d-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="5752d-373">**Subscrição**</span><span class="sxs-lookup"><span data-stu-id="5752d-373">**Subscription**</span></span> |<span data-ttu-id="5752d-374">Utilize Olá mesmo subscrição como máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="5752d-375">**Localização**</span><span class="sxs-lookup"><span data-stu-id="5752d-375">**Location**</span></span> |<span data-ttu-id="5752d-376">Utilize Olá mesma localização da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="5752d-377">Olá painel do portal do Azure deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="5752d-377">hello Azure portal blade should look like this:</span></span>

   ![Criar Balanceador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="5752d-379">Clique em **criar**, Balanceador de carga de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="5752d-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="5752d-380">Balanceador de carga do tooconfigure Olá, terá de toocreate um conjunto de back-end, uma pesquisa e regras de balanceamento de carga de Olá de conjunto.</span><span class="sxs-lookup"><span data-stu-id="5752d-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="5752d-381">Efetue estes no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="5752d-382">Adicionar o conjunto de back-end</span><span class="sxs-lookup"><span data-stu-id="5752d-382">Add backend pool</span></span>

1. <span data-ttu-id="5752d-383">No portal do Azure Olá, visite tooyour grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5752d-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="5752d-384">Poderá ter de Balanceador de carga do toorefresh Olá vista toosee Olá recentemente criado.</span><span class="sxs-lookup"><span data-stu-id="5752d-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Localizar o Balanceador de carga no grupo de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="5752d-386">Clique em Balanceador de carga Olá, clique em **conjuntos back-end**e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="5752d-387">Defina o conjunto de back-end Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5752d-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="5752d-388">Definição</span><span class="sxs-lookup"><span data-stu-id="5752d-388">Setting</span></span> | <span data-ttu-id="5752d-389">Descrição</span><span class="sxs-lookup"><span data-stu-id="5752d-389">Description</span></span> | <span data-ttu-id="5752d-390">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5752d-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5752d-391">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5752d-391">**Name**</span></span> | <span data-ttu-id="5752d-392">Escreva um nome de texto</span><span class="sxs-lookup"><span data-stu-id="5752d-392">Type a text name</span></span> | <span data-ttu-id="5752d-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="5752d-393">SQLLBBE</span></span>
   | <span data-ttu-id="5752d-394">**Associado a**</span><span class="sxs-lookup"><span data-stu-id="5752d-394">**Associated to**</span></span> | <span data-ttu-id="5752d-395">Escolha a partir da lista</span><span class="sxs-lookup"><span data-stu-id="5752d-395">Pick from list</span></span> | <span data-ttu-id="5752d-396">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5752d-396">Availability set</span></span>
   | <span data-ttu-id="5752d-397">**Conjunto de disponibilidade**</span><span class="sxs-lookup"><span data-stu-id="5752d-397">**Availability set**</span></span> | <span data-ttu-id="5752d-398">Utilize um nome de conjunto de disponibilidade de Olá que as suas VMs do SQL Server estão em</span><span class="sxs-lookup"><span data-stu-id="5752d-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="5752d-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="5752d-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="5752d-400">**Máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="5752d-400">**Virtual machines**</span></span> |<span data-ttu-id="5752d-401">Olá, dois nomes de VM do Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="5752d-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="5752d-402">SQLServer-0, sqlserver 1</span><span class="sxs-lookup"><span data-stu-id="5752d-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="5752d-403">Nome do conjunto de back-end Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="5752d-404">Clique em **+ adicionar uma máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="5752d-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="5752d-405">Olá para conjunto de disponibilidade, escolha o conjunto de disponibilidade de Olá esse Olá servidores SQL Server estão em.</span><span class="sxs-lookup"><span data-stu-id="5752d-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="5752d-406">Para máquinas virtuais, incluem ambos Olá SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="5752d-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="5752d-407">Não inclua o servidor de testemunho de partilha de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="5752d-408">Clique em **OK** pool de back-end de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="5752d-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="5752d-409">Conjunto Olá sonda</span><span class="sxs-lookup"><span data-stu-id="5752d-409">Set hello probe</span></span>

1. <span data-ttu-id="5752d-410">Clique em Balanceador de carga Olá, clique em **sondas de estado de funcionamento**e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="5752d-411">Defina a sonda de estado de funcionamento de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5752d-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="5752d-412">Definição</span><span class="sxs-lookup"><span data-stu-id="5752d-412">Setting</span></span> | <span data-ttu-id="5752d-413">Descrição</span><span class="sxs-lookup"><span data-stu-id="5752d-413">Description</span></span> | <span data-ttu-id="5752d-414">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5752d-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5752d-415">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5752d-415">**Name**</span></span> | <span data-ttu-id="5752d-416">Texto</span><span class="sxs-lookup"><span data-stu-id="5752d-416">Text</span></span> | <span data-ttu-id="5752d-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5752d-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="5752d-418">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="5752d-418">**Protocol**</span></span> | <span data-ttu-id="5752d-419">Escolha TCP</span><span class="sxs-lookup"><span data-stu-id="5752d-419">Choose TCP</span></span> | <span data-ttu-id="5752d-420">TCP</span><span class="sxs-lookup"><span data-stu-id="5752d-420">TCP</span></span> |
   | <span data-ttu-id="5752d-421">**Porta**</span><span class="sxs-lookup"><span data-stu-id="5752d-421">**Port**</span></span> | <span data-ttu-id="5752d-422">Qualquer porta não utilizada</span><span class="sxs-lookup"><span data-stu-id="5752d-422">Any unused port</span></span> | <span data-ttu-id="5752d-423">59999</span><span class="sxs-lookup"><span data-stu-id="5752d-423">59999</span></span> |
   | <span data-ttu-id="5752d-424">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="5752d-424">**Interval**</span></span>  | <span data-ttu-id="5752d-425">Olá período de tempo entre sonda tenta em segundos</span><span class="sxs-lookup"><span data-stu-id="5752d-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="5752d-426">5</span><span class="sxs-lookup"><span data-stu-id="5752d-426">5</span></span> |
   | <span data-ttu-id="5752d-427">**Limiar de mau estado de funcionamento**</span><span class="sxs-lookup"><span data-stu-id="5752d-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="5752d-428">Olá, número de falhas de sonda consecutivas que deve ocorrer para toobe uma máquina virtual considerado em mau estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="5752d-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="5752d-429">2</span><span class="sxs-lookup"><span data-stu-id="5752d-429">2</span></span> |

1. <span data-ttu-id="5752d-430">Clique em **OK** sonda de estado de funcionamento de Olá tooset.</span><span class="sxs-lookup"><span data-stu-id="5752d-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="5752d-431">Definir regras de balanceamento de carga Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="5752d-432">Clique em Balanceador de carga Olá, clique em **as regras de balanceamento de carga**e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="5752d-433">Definir a forma de regras de balanceamento de carga de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="5752d-434">Definição</span><span class="sxs-lookup"><span data-stu-id="5752d-434">Setting</span></span> | <span data-ttu-id="5752d-435">Descrição</span><span class="sxs-lookup"><span data-stu-id="5752d-435">Description</span></span> | <span data-ttu-id="5752d-436">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5752d-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5752d-437">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5752d-437">**Name**</span></span> | <span data-ttu-id="5752d-438">Texto</span><span class="sxs-lookup"><span data-stu-id="5752d-438">Text</span></span> | <span data-ttu-id="5752d-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="5752d-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="5752d-440">**Endereço IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="5752d-440">**Frontend IP address**</span></span> | <span data-ttu-id="5752d-441">Escolha um endereço</span><span class="sxs-lookup"><span data-stu-id="5752d-441">Choose an address</span></span> |<span data-ttu-id="5752d-442">Utilize o endereço de Olá que criou quando criou o Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="5752d-443">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="5752d-443">**Protocol**</span></span> | <span data-ttu-id="5752d-444">Escolha TCP</span><span class="sxs-lookup"><span data-stu-id="5752d-444">Choose TCP</span></span> |<span data-ttu-id="5752d-445">TCP</span><span class="sxs-lookup"><span data-stu-id="5752d-445">TCP</span></span> |
   | <span data-ttu-id="5752d-446">**Porta**</span><span class="sxs-lookup"><span data-stu-id="5752d-446">**Port**</span></span> | <span data-ttu-id="5752d-447">Utilizar a porta de Olá para a instância do SQL Server Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="5752d-448">1433</span><span class="sxs-lookup"><span data-stu-id="5752d-448">1433</span></span> |
   | <span data-ttu-id="5752d-449">**Porta de back-end**</span><span class="sxs-lookup"><span data-stu-id="5752d-449">**Backend Port**</span></span> | <span data-ttu-id="5752d-450">Este campo não é utilizado quando o IP flutuante está definido para direta do servidor retorno</span><span class="sxs-lookup"><span data-stu-id="5752d-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="5752d-451">1433</span><span class="sxs-lookup"><span data-stu-id="5752d-451">1433</span></span> |
   | <span data-ttu-id="5752d-452">**Sonda**</span><span class="sxs-lookup"><span data-stu-id="5752d-452">**Probe**</span></span> |<span data-ttu-id="5752d-453">nome de Olá especificado para a sonda de Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="5752d-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5752d-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="5752d-455">**Persistência da sessão**</span><span class="sxs-lookup"><span data-stu-id="5752d-455">**Session Persistence**</span></span> | <span data-ttu-id="5752d-456">Na lista pendente</span><span class="sxs-lookup"><span data-stu-id="5752d-456">Drop down list</span></span> | <span data-ttu-id="5752d-457">**Nenhum**</span><span class="sxs-lookup"><span data-stu-id="5752d-457">**None**</span></span> |
   | <span data-ttu-id="5752d-458">**Tempo limite de inatividade**</span><span class="sxs-lookup"><span data-stu-id="5752d-458">**Idle Timeout**</span></span> | <span data-ttu-id="5752d-459">Tookeep minutos abrir uma ligação de TCP</span><span class="sxs-lookup"><span data-stu-id="5752d-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="5752d-460">4</span><span class="sxs-lookup"><span data-stu-id="5752d-460">4</span></span> |
   | <span data-ttu-id="5752d-461">**Vírgula flutuante (devolução direta do servidor) de IP**</span><span class="sxs-lookup"><span data-stu-id="5752d-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="5752d-462">Ativado</span><span class="sxs-lookup"><span data-stu-id="5752d-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="5752d-463">Devolução direta do servidor é definida durante a criação.</span><span class="sxs-lookup"><span data-stu-id="5752d-463">Direct server return is set during creation.</span></span> <span data-ttu-id="5752d-464">Não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="5752d-464">It cannot be changed.</span></span>

1. <span data-ttu-id="5752d-465">Clique em **OK** regras de balanceamento de carga na Olá tooset.</span><span class="sxs-lookup"><span data-stu-id="5752d-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="5752d-466"><a name="configure-listener"></a>Configurar o serviço de escuta de Olá</span><span class="sxs-lookup"><span data-stu-id="5752d-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="5752d-467">Olá seguinte coisa toodo é tooconfigure um serviço de escuta do grupo de disponibilidade no cluster de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5752d-468">Este tutorial mostra como endereço toocreate um único serviço de escuta - um IP do ILB.</span><span class="sxs-lookup"><span data-stu-id="5752d-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="5752d-469">toocreate um ou mais serviços de escuta com um ou mais endereços IP, consulte [Balanceador de carga e do serviço de escuta do grupo de disponibilidade criar | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5752d-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="5752d-470">Porta do serviço de escuta de conjunto</span><span class="sxs-lookup"><span data-stu-id="5752d-470">Set listener port</span></span>

<span data-ttu-id="5752d-471">No SQL Server Management Studio, defina a porta de serviço de escuta de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="5752d-472">Inicie o SQL Server Management Studio e ligue a réplica primária toohello.</span><span class="sxs-lookup"><span data-stu-id="5752d-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="5752d-473">Navegue demasiado**elevada disponibilidade do AlwaysOn** | **grupos de disponibilidade** | **escuta do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="5752d-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="5752d-474">Deverá ver agora o nome do serviço de escuta de Olá que criou no Gestor de clusters de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="5752d-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="5752d-475">Clique no nome do serviço de escuta de Olá e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5752d-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="5752d-476">No Olá **porta** caixa, especifique o número da porta de escuta do grupo de disponibilidade de Olá Olá utilizando Olá $EndpointPort que utilizou anteriormente (1433 foi predefinido Olá), em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5752d-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="5752d-477">Tem agora um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure em execução no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5752d-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="5752d-478">Toolistener de ligação de teste</span><span class="sxs-lookup"><span data-stu-id="5752d-478">Test connection toolistener</span></span>

<span data-ttu-id="5752d-479">ligação de Olá tootest:</span><span class="sxs-lookup"><span data-stu-id="5752d-479">tootest hello connection:</span></span>

1. <span data-ttu-id="5752d-480">RDP tooa SQL Server que está a ser Olá mesmo virtual de rede, mas não réplica Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="5752d-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="5752d-481">Pode utilizar Olá outro servidor de SQL no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="5752d-482">Utilize **sqlcmd** ligação do utilitário tootest Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="5752d-483">Por exemplo, o seguinte script de Olá estabelece uma **sqlcmd** réplica primária de toohello ligação através do serviço de escuta de Olá com autenticação do Windows:</span><span class="sxs-lookup"><span data-stu-id="5752d-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="5752d-484">Se o serviço de escuta de Olá é utilizar uma porta diferente de Olá predefinido (1433) de porta, especifique a porta de Olá na cadeia de ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="5752d-485">Por exemplo, hello seguinte comando sqlcmd liga tooa escuta na porta 1435:</span><span class="sxs-lookup"><span data-stu-id="5752d-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="5752d-486">Olá ligação SQLCMD liga automaticamente toowhichever instância da réplica primária do SQL Server anfitriões Olá.</span><span class="sxs-lookup"><span data-stu-id="5752d-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="5752d-487">Certifique-se de que a porta de Olá que especificar está aberta na firewall de Olá de ambos os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="5752d-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="5752d-488">Ambos os servidores necessitam de uma regra de entrada para Olá a porta TCP que utiliza.</span><span class="sxs-lookup"><span data-stu-id="5752d-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="5752d-489">Para obter mais informações, consulte [adicionar ou Editar regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="5752d-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="5752d-490">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5752d-490">Next steps</span></span>

- <span data-ttu-id="5752d-491">[Adicionar um balanceador de carga do tooa de endereço IP para um segundo grupo de disponibilidade](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="5752d-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
