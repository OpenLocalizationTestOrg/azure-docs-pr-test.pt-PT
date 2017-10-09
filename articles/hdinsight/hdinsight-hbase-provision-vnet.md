---
title: aaaCreate HBase clusters numa rede Virtual - Azure | Microsoft Docs
description: "Introdução ao hbase no Azure HDInsight. Saiba como clusters de toocreate HBase do HDInsight na Azure Virtual Network."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="5c4c2-104">Criar clusters de HBase no HDInsight na Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="5c4c2-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="5c4c2-105">Saiba como toocreate HBase do HDInsight Azure clusters num [Azure Virtual Network][1].</span><span class="sxs-lookup"><span data-stu-id="5c4c2-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="5c4c2-106">Com a integração de rede virtual, clusters de HBase podem ser implementado toohello mesmo virtual de rede como as suas aplicações, por isso, que aplicações podem comunicar diretamente com o HBase.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="5c4c2-107">Olá benefícios incluem:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-107">hello benefits include:</span></span>

* <span data-ttu-id="5c4c2-108">Ligação direta Olá web aplicação toohello nós Olá HBase cluster, que permite a comunicação através de procedimento remoto de HBase Java chamar APIs (RPC).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="5c4c2-109">Desempenho melhorado por não ter o tráfego aceda ao longo de vários gateways e Balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="5c4c2-110">Olá capacidade tooprocess informações confidenciais de forma mais segura sem a exposição de um ponto final público.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5c4c2-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c4c2-111">Prerequisites</span></span>
<span data-ttu-id="5c4c2-112">Antes de começar este tutorial, tem de ter Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="5c4c2-113">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-113">**An Azure subscription**.</span></span> <span data-ttu-id="5c4c2-114">Consulte [Obter versão de avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5c4c2-115">**Uma estação de trabalho com o Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="5c4c2-116">Consulte [instalar e utilizar o Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="5c4c2-117">Criar cluster HBase numa rede virtual</span><span class="sxs-lookup"><span data-stu-id="5c4c2-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="5c4c2-118">Nesta secção, cria um cluster HBase baseado em Linux com a conta do armazenamento do Azure dependente Olá uma rede virtual do Azure utilizando um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="5c4c2-119">Para outros métodos de criação do cluster e compreender as definições de Olá, consulte [criar clusters do HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="5c4c2-120">Para obter mais informações sobre como utilizar um modelo toocreate Hadoop clusters no HDInsight, consulte [clusters do Hadoop criar no HDInsight com modelos Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="5c4c2-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="5c4c2-121">Algumas propriedades estão hard-coded para o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="5c4c2-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-122">For example:</span></span>
>
> * <span data-ttu-id="5c4c2-123">**Localização**: EUA Leste 2</span><span class="sxs-lookup"><span data-stu-id="5c4c2-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="5c4c2-124">**Versão do cluster**: 3.5</span><span class="sxs-lookup"><span data-stu-id="5c4c2-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="5c4c2-125">**Número de nós de trabalho de cluster**: 2</span><span class="sxs-lookup"><span data-stu-id="5c4c2-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="5c4c2-126">**Conta de armazenamento de predefinido**: uma cadeia exclusiva</span><span class="sxs-lookup"><span data-stu-id="5c4c2-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="5c4c2-127">**Nome da rede virtual**: &lt;nome do Cluster >-vnet</span><span class="sxs-lookup"><span data-stu-id="5c4c2-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="5c4c2-128">**Espaço de endereços de rede virtual**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5c4c2-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="5c4c2-129">**Nome da sub-rede**: subnet1</span><span class="sxs-lookup"><span data-stu-id="5c4c2-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="5c4c2-130">**Intervalo de endereços da sub-rede**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5c4c2-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="5c4c2-131">&lt;Nome do cluster > é substituído pelo nome do cluster Olá fornecer ao utilizar o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="5c4c2-132">Clique em Olá seguinte imagem tooopen Olá o modelo de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="5c4c2-133">modelo de Olá está localizado num [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="5c4c2-134">De Olá **implementação personalizada** painel, introduza Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="5c4c2-135">**Subscrição**: selecione o cluster do HDInsight toocreate Olá uma subscrição do Azure utilizado, Olá conta do Storage dependente e Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="5c4c2-136">**Grupo de recursos**: selecione **criar nova**e especifique um nome do novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="5c4c2-137">**Localização**: selecione uma localização para o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="5c4c2-138">**ClusterName**: introduza um nome para toobe de cluster de Hadoop Olá criado.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="5c4c2-139">**Nome de início de sessão e palavra-passe do cluster**: nome de início de sessão predefinido Olá é **admin**.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="5c4c2-140">**Nome de utilizador do SSH e a palavra-passe**: é o nome de utilizador do Olá predefinido **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="5c4c2-141">Pode alterá-lo.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-141">You can rename it.</span></span>
   * <span data-ttu-id="5c4c2-142">**Concordo toohello termos e condições de Olá indicadas acima**: (selecionar)</span><span class="sxs-lookup"><span data-stu-id="5c4c2-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="5c4c2-143">Clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-143">Click **Purchase**.</span></span> <span data-ttu-id="5c4c2-144">Demora cerca de 20 minutos toocreate um cluster.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="5c4c2-145">Depois de Olá cluster for criado, pode clicar em Painel de cluster Olá no tooopen portal Olá-lo.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="5c4c2-146">Depois de concluir o tutorial Olá, pode querer cluster de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="5c4c2-147">Com o HDInsight, os dados são armazenados no Storage do Azure, pelo que pode eliminar um cluster em segurança quando este não está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="5c4c2-148">Também lhe é cobrado o valor de um cluster do HDInsight mesmo quando não o está a utilizar.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="5c4c2-149">Uma vez que os custos de Olá de cluster Olá são muitas vezes mais do que os custos de Olá de armazenamento, faz sentido em termos económicos toodelete clusters quando não estão em utilização.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="5c4c2-150">Para obter instruções de Olá da eliminação de um cluster, consulte [Olá de clusters de gerir Hadoop no HDInsight utilizando o portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="5c4c2-151">toobegin trabalhar com o novo cluster de HBase, pode utilizar os procedimentos de Olá encontrados no [introdução ao hbase com o Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="5c4c2-152">Ligar o cluster de HBase toohello com APIs de RPC de Java de HBase</span><span class="sxs-lookup"><span data-stu-id="5c4c2-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="5c4c2-153">Criar uma infraestrutura como uma máquina virtual de serviço (IaaS) para Olá a mesma rede virtual do Azure e Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="5c4c2-154">Para obter instruções sobre como criar uma nova máquina virtual de IaaS, consulte [criar uma Máquina Virtual a executar o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="5c4c2-155">Quando os seguintes passos de Olá neste documento, tem de utilizar Olá os seguintes valores para a configuração de rede Olá:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="5c4c2-156">**Rede virtual**: &lt;nome do Cluster >-vnet</span><span class="sxs-lookup"><span data-stu-id="5c4c2-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="5c4c2-157">**Sub-rede**: subnet1</span><span class="sxs-lookup"><span data-stu-id="5c4c2-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5c4c2-158">Substitua &lt;nome do Cluster > com o nome de Olá utilizado ao criar o cluster do HDInsight Olá nos passos anteriores.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="5c4c2-159">Utilizar estes valores, Olá máquina virtual está colocada em Olá mesma rede virtual e sub-rede que o cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="5c4c2-160">Esta configuração permite-lhes toodirectly comunicam entre si.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="5c4c2-161">Há um toocreate de forma um cluster do HDInsight com um nó de extremidade vazio.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="5c4c2-162">nó de extremidade Olá pode ser o cluster de Olá de toomanage utilizados.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="5c4c2-163">Para obter mais informações, consulte [utilizar nós edge vazio no HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="5c4c2-164">Quando utilizar um tooHBase de tooconnect de aplicação Java remotamente, tem de utilizar o nome de domínio completamente qualificado (FQDN) do Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="5c4c2-165">toodetermine, tem de obter o sufixo DNS de específico da ligação de Olá do cluster de HBase Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="5c4c2-166">toodo, pode utilizar um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="5c4c2-167">Utilize um toomake de browser Web uma chamada do Ambari:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="5c4c2-168">Procurar toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / aloja? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="5c4c2-169">Transforma um ficheiro JSON com os sufixos DNS por Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="5c4c2-170">Utilize Olá Ambari site:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="5c4c2-171">Procurar demasiado https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="5c4c2-172">Clique em **anfitriões** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="5c4c2-173">Utilize chamadas REST de toomake Curl:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="5c4c2-174">No Olá devolveu dados de JavaScript Object Notation (JSON), localizar a entrada de "host_name" Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="5c4c2-175">Contém Olá FQDN para nós de Olá no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="5c4c2-176">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="5c4c2-177">parte de Olá do Olá domínio nome que começa com o nome do cluster Olá é o sufixo DNS de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="5c4c2-178">Por exemplo, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="5c4c2-179">Utilizar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c4c2-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="5c4c2-180">Olá de utilização seguintes Olá do Azure PowerShell script tooregister **Get-ClusterDetail** função, o que pode ser o sufixo DNS de Olá tooreturn utilizado:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="5c4c2-181">Após a execução Olá Azure o script do PowerShell seguinte de Olá utilize comando sufixo DNS de Olá tooreturn utilizando Olá **Get-ClusterDetail** função.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="5c4c2-182">Especifique o nome do cluster HBase do HDInsight, o nome de administrador e a palavra-passe de administrador ao utilizar este comando.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="5c4c2-183">Este comando devolve o sufixo DNS de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="5c4c2-184">Por exemplo, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="5c4c2-185">tooverify Olá máquina virtual pode comunicar com Olá HBase cluster, utilize o comando de Olá `ping headnode0.<dns suffix>` da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="5c4c2-186">Por exemplo, executar um ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="5c4c2-187">toouse estas informações numa aplicação Java, pode seguir passos Olá [utilizar Maven toobuild Java aplicações que utilizam o HBase com o HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="5c4c2-188">aplicação de Olá toohave ligar tooa remoto HBase servidor, modifique Olá **hbase site.xml** ficheiro Olá de toouse este exemplo FQDN para Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="5c4c2-189">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="5c4c2-190">Para obter mais informações sobre resolução de nomes em redes virtuais do Azure, incluindo como toouse o próprio servidor DNS, consulte [resolução de nomes (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5c4c2-191">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5c4c2-191">Next steps</span></span>
<span data-ttu-id="5c4c2-192">Neste tutorial, aprendeu como toocreate um cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="5c4c2-193">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-193">toolearn more, see:</span></span>

* [<span data-ttu-id="5c4c2-194">Introdução ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c4c2-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="5c4c2-195">Utilize nós de limite vazio no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c4c2-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="5c4c2-196">Configurar a replicação do HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c4c2-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="5c4c2-197">Criar clusters do Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c4c2-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="5c4c2-198">Introdução ao hbase com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c4c2-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="5c4c2-199">Analisar dados de sentimento do Twitter com o HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c4c2-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="5c4c2-200">[Descrição geral da rede virtual][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="5c4c2-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalhes de aprovisionamento para o novo cluster de HBase Olá"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Utilize a ação de Script toocustomize um cluster HBase"

[azure-preview-portal]: https://portal.azure.com
