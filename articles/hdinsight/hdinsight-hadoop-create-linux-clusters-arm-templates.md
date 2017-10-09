---
title: aaaCreate Hadoop clusters utilizando os modelos - Azure HDInsight | Microsoft Docs
description: Saiba como toocreate clusters para o HDInsight utilizando modelos do Resource Manager
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="619d8-103">Criar clusters do Hadoop no HDInsight com modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="619d8-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="619d8-104">Neste artigo, saiba mais formas de vários clusters toocreate Azure HDInsight com modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="619d8-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="619d8-105">Para obter mais informações, consulte [implementar uma aplicação com o modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="619d8-106">toolearn sobre outras ferramentas de criação do cluster e funcionalidades, clique em Seletor de separador Olá na parte superior de Olá deste página ou consulte [métodos de criação do Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="619d8-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="619d8-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="619d8-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="619d8-108">instruções de Olá toofollow neste artigo, precisa de:</span><span class="sxs-lookup"><span data-stu-id="619d8-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="619d8-109">Um [subscrição do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="619d8-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="619d8-110">CLI do Azure PowerShell e/ou do Azure.</span><span class="sxs-lookup"><span data-stu-id="619d8-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="619d8-111">Modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="619d8-111">Resource Manager templates</span></span>
<span data-ttu-id="619d8-112">Um modelo do Resource Manager permite Olá toocreate fácil para a sua aplicação numa operação única e coordenada os seguintes:</span><span class="sxs-lookup"><span data-stu-id="619d8-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="619d8-113">Clusters do HDInsight e os recursos dependentes (como conta de armazenamento predefinida de Olá)</span><span class="sxs-lookup"><span data-stu-id="619d8-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="619d8-114">Outros recursos (por exemplo, SQL Database do Azure toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="619d8-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="619d8-115">No modelo de Olá, é possível definir recursos Olá que são necessários para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="619d8-116">Também especificar valores de tooinput de parâmetros de implementação para os diferentes ambientes.</span><span class="sxs-lookup"><span data-stu-id="619d8-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="619d8-117">Olá modelo é constituído por JSON e expressões que utilize tooconstruct valores para a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="619d8-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="619d8-118">Pode encontrar exemplos de modelo do HDInsight em [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="619d8-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="619d8-119">Utilizar várias plataformas [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) com Olá [extensão do Gestor de recursos](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou um modelo de Olá de toosave ao editor de texto num ficheiro na sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="619d8-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="619d8-120">Pode saber como toocall Olá modelo através da utilização de métodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="619d8-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="619d8-121">Para obter mais informações sobre modelos do Resource Manager, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="619d8-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="619d8-122">Modelos do Azure Resource Manager autor</span><span class="sxs-lookup"><span data-stu-id="619d8-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="619d8-123">Implementar uma aplicação com modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="619d8-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="619d8-124">Gerar modelos</span><span class="sxs-lookup"><span data-stu-id="619d8-124">Generate templates</span></span>

<span data-ttu-id="619d8-125">Ao utilizar Olá portal do Azure, pode configurar todas as propriedades de Olá de um cluster e, em seguida, guardar o modelo de Olá antes de o implementar.</span><span class="sxs-lookup"><span data-stu-id="619d8-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="619d8-126">Em seguida, pode reutilizar o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-126">You can then reuse hello template.</span></span>

<span data-ttu-id="619d8-127">**toogenerate um modelo ao utilizar Olá portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="619d8-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="619d8-128">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="619d8-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="619d8-129">Clique em **novo** no menu à esquerda Olá, clique em **Intelligence + análise**e, em seguida, clique em **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="619d8-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="619d8-130">Siga as propriedades de tooenter Olá instruções.</span><span class="sxs-lookup"><span data-stu-id="619d8-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="619d8-131">Pode utilizar qualquer um dos Olá **criação rápida** ou Olá **personalizada** opção.</span><span class="sxs-lookup"><span data-stu-id="619d8-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="619d8-132">No Olá **resumo** separador, clique em **transferir modelo e os parâmetros**:</span><span class="sxs-lookup"><span data-stu-id="619d8-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop criar transferências de modelo de Gestor de recursos de cluster](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="619d8-134">É apresentada uma lista de ficheiro de modelo Olá, o ficheiro de parâmetros e o código amostras utilizadas toodeploy Olá modelo:</span><span class="sxs-lookup"><span data-stu-id="619d8-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![HDInsight Hadoop Criar cluster as opções de transferência do modelo do Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="619d8-136">Aqui, pode transferir o modelo de Olá, guardá-lo a biblioteca de modelos de tooyour ou implementar a modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="619d8-137">tooaccess um modelo na biblioteca, clique em **mais serviços** no menu à esquerda de Olá e, em seguida, clique em **modelos** (em Olá **outros** categoria).</span><span class="sxs-lookup"><span data-stu-id="619d8-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="619d8-138">ficheiro de modelo e os parâmetros de Olá tem de ser utilizado em conjunto.</span><span class="sxs-lookup"><span data-stu-id="619d8-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="619d8-139">Caso contrário, pode obter resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="619d8-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="619d8-140">Por exemplo, Olá predefinido **clusterKind** valor da propriedade é sempre **hadoop**, não obstante que especifique antes de transferir o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="619d8-141">Implementar com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="619d8-141">Deploy with PowerShell</span></span>

<span data-ttu-id="619d8-142">Este procedimento cria um cluster do Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="619d8-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="619d8-143">Guardar o ficheiro JSON Olá no Olá [apêndice](#appx-a-arm-template) tooyour estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="619d8-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="619d8-144">Olá script do PowerShell, nome de ficheiro Olá é `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="619d8-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="619d8-145">Definir Olá parâmetros e variáveis se for necessário.</span><span class="sxs-lookup"><span data-stu-id="619d8-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="619d8-146">Execute o modelo de Olá utilizando Olá seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="619d8-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="619d8-147">Olá script do PowerShell configura o nome do cluster apenas Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="619d8-148">o nome de conta do storage Olá é "hard-coded" no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="619d8-149">São palavra-passe de utilizador de cluster de Olá tooenter pedido.</span><span class="sxs-lookup"><span data-stu-id="619d8-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="619d8-150">(o nome de utilizador do Olá predefinido é **admin**.) Também são palavra-passe de utilizador SSH de Olá tooenter pedido.</span><span class="sxs-lookup"><span data-stu-id="619d8-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="619d8-151">(nome de utilizador SSH Olá predefinido é **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="619d8-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="619d8-152">Para obter mais informações, consulte [implementar com o PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="619d8-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="619d8-153">Implementar com a CLI</span><span class="sxs-lookup"><span data-stu-id="619d8-153">Deploy with CLI</span></span>
<span data-ttu-id="619d8-154">Olá exemplo a seguir utiliza a interface de linha de comandos (CLI) do Azure.</span><span class="sxs-lookup"><span data-stu-id="619d8-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="619d8-155">Cria um cluster e a conta do storage dependente e contentor ao chamar um modelo do Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="619d8-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="619d8-156">São tooenter pedido:</span><span class="sxs-lookup"><span data-stu-id="619d8-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="619d8-157">nome do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-157">hello cluster name.</span></span>
* <span data-ttu-id="619d8-158">palavra-passe utilizador cluster Olá</span><span class="sxs-lookup"><span data-stu-id="619d8-158">hello cluster user password.</span></span> <span data-ttu-id="619d8-159">(o nome de utilizador do Olá predefinido é **admin**.)</span><span class="sxs-lookup"><span data-stu-id="619d8-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="619d8-160">palavra-passe utilizador SSH Olá</span><span class="sxs-lookup"><span data-stu-id="619d8-160">hello SSH user password.</span></span> <span data-ttu-id="619d8-161">(nome de utilizador SSH Olá predefinido é **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="619d8-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="619d8-162">Olá código a seguir fornece parâmetros inline:</span><span class="sxs-lookup"><span data-stu-id="619d8-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="619d8-163">Implementar com Olá REST API</span><span class="sxs-lookup"><span data-stu-id="619d8-163">Deploy with hello REST API</span></span>
<span data-ttu-id="619d8-164">Consulte [implementar com Olá REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="619d8-165">Implementar com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="619d8-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="619d8-166">Utilizar o Visual Studio toocreate um projeto do grupo de recursos e implementá-la tooAzure através da interface de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="619d8-167">Seleciona o tipo de Olá de tooinclude de recursos no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="619d8-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="619d8-168">Esses recursos são adicionados automaticamente o modelo do Resource Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="619d8-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="619d8-169">projeto de Olá também fornece um modelo de Olá de toodeploy de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="619d8-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="619d8-170">Para um toousing introdução Visual Studio com grupos de recursos, consulte [criar e implementar grupos de recursos do Azure através do Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="619d8-171">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="619d8-171">Troubleshoot</span></span>

<span data-ttu-id="619d8-172">Caso se depare com problemas com a criação de clusters do HDInsight, veja [aceder aos requisitos de controlo](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="619d8-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="619d8-173">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="619d8-173">Next steps</span></span>
<span data-ttu-id="619d8-174">Neste artigo, aprendeu a várias formas toocreate um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="619d8-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="619d8-175">toolearn mais, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="619d8-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="619d8-176">Para obter um exemplo de implementação de recursos através da biblioteca de cliente .NET Olá, consulte [implementar recursos com bibliotecas .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="619d8-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="619d8-177">Para obter um exemplo detalhado para implementar uma aplicação, consulte [aprovisionar e implementar micro-serviços previsibilidade no Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="619d8-178">Para obter orientações sobre como implementar os seus ambientes de toodifferent solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="619d8-179">toolearn sobre Olá as secções do modelo do Azure Resource Manager Olá, consulte [criação de modelos](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="619d8-180">Para obter uma lista de funções de Olá, pode utilizar um modelo Azure Resource Manager, consulte [funções de modelo](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="619d8-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="619d8-181">Apêndice: Resource Manager modelo toocreate um cluster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="619d8-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="619d8-182">Olá modelo Azure Resource Manager seguinte cria um cluster do Hadoop baseados em Linux com Olá dependentes conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="619d8-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="619d8-183">Este exemplo inclui informações de configuração para o metastore do Hive e metastore do Oozie.</span><span class="sxs-lookup"><span data-stu-id="619d8-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="619d8-184">Remover a secção de Olá ou configurar secção Olá antes de utilizar o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="619d8-185">Apêndice: Resource Manager modelo toocreate um cluster do Spark</span><span class="sxs-lookup"><span data-stu-id="619d8-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="619d8-186">Esta secção fornece um modelo do Resource Manager que pode utilizar toocreate um cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="619d8-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="619d8-187">Este modelo inclui as configurações de `spark-defaults` e `spark-thrift-sparkconf` (para os clusters do Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (para os clusters do Spark 2).</span><span class="sxs-lookup"><span data-stu-id="619d8-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="619d8-188">Além disso toothis, HDInsight calcula e define as configurações, tais como `spark.executor.instances`, `spark.executor.memory`, e `spark.executor.cores` com base no tamanho de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="619d8-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="619d8-189">Se qualquer um parâmetro numa secção como parte do modelo de Olá próprio, HDInsight não calcular e definir Olá outros parâmetros de Olá mesma secção.</span><span class="sxs-lookup"><span data-stu-id="619d8-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="619d8-190">Por exemplo, o parâmetro `spark.executor.instances` está a ser Olá `spark-defaults` configuração.</span><span class="sxs-lookup"><span data-stu-id="619d8-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="619d8-191">Se definir o parâmetro outro (por exemplo, `spark.yarn.exector.memoryOverhead`) no Olá `spark-defaults` configuração, HDInsight não calcular e defina Olá `spark.executor.instances` , bem como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="619d8-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
