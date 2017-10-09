---
title: "aaaBuild a primeira fábrica de dados (REST) | Microsoft Docs"
description: Neste tutorial, vai criar um exemplo de pipeline do Azure Data Factory com a API REST do Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="72cff-103">Tutorial: Criar a primeira fábrica de dados do Azure com a API REST do Data Factory</span><span class="sxs-lookup"><span data-stu-id="72cff-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72cff-104">Descrição geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72cff-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="72cff-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="72cff-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="72cff-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72cff-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="72cff-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72cff-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="72cff-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="72cff-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="72cff-109">API REST</span><span class="sxs-lookup"><span data-stu-id="72cff-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="72cff-110">Neste artigo, utilize toocreate de API de REST de fábrica de dados a primeira fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="72cff-111">toodo Olá tutorial, utilizando outras ferramentas/SDKs, selecione uma das opções de Olá Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="72cff-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="72cff-112">pipeline de Olá neste tutorial tem uma atividade: **atividade do ramo de registo do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="72cff-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="72cff-113">Esta atividade executa um script de ramo de registo num cluster do Azure HDInsight transformações dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="72cff-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="72cff-114">pipeline de Olá é agendada toorun depois de um mês entre Olá especificado tempos de início e de fim.</span><span class="sxs-lookup"><span data-stu-id="72cff-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="72cff-115">Este artigo não abrange todos os Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="72cff-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="72cff-116">Para obter a documentação completa sobre a API REST, veja [Data Factory REST API Reference](/rest/api/datafactory/) (Referência da API REST do Data Factory).</span><span class="sxs-lookup"><span data-stu-id="72cff-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="72cff-117">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="72cff-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="72cff-118">Além disso, pode encadeiam duas atividades (executadas uma atividade após outro) definindo o conjunto de dados de saída de Olá de uma atividade como Olá de entrada de conjunto de dados de Olá outra atividade.</span><span class="sxs-lookup"><span data-stu-id="72cff-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="72cff-119">Para obter mais informações, veja [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) (agendamento e execução no Data Factory).</span><span class="sxs-lookup"><span data-stu-id="72cff-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="72cff-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72cff-120">Prerequisites</span></span>
* <span data-ttu-id="72cff-121">Leia [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e Olá concluída **pré-requisito** passos.</span><span class="sxs-lookup"><span data-stu-id="72cff-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="72cff-122">Instale o [Curl](https://curl.haxx.se/dlwiz/) no seu computador.</span><span class="sxs-lookup"><span data-stu-id="72cff-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="72cff-123">É utilizar a ferramenta CURL Olá com REST comandos toocreate uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="72cff-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="72cff-124">Siga as instruções [neste artigo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:</span><span class="sxs-lookup"><span data-stu-id="72cff-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="72cff-125">Criar uma aplicação Web com o nome **ADFGetStartedApp** no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72cff-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="72cff-126">Obter o **ID de cliente** e a **chave secreta**.</span><span class="sxs-lookup"><span data-stu-id="72cff-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="72cff-127">Obter o **ID de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="72cff-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="72cff-128">Atribuir Olá **ADFGetStartedApp** aplicação toohello **contribuinte da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="72cff-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="72cff-129">Instale o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72cff-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="72cff-130">Iniciar **PowerShell** e Olá execute os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="72cff-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="72cff-131">Mantenha o Azure PowerShell aberto até Olá fim deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="72cff-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="72cff-132">Se fechar e reabrir, terá de comandos de Olá toorun novamente.</span><span class="sxs-lookup"><span data-stu-id="72cff-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="72cff-133">Executar **Login-AzureRmAccount** e introduza o nome de utilizador de Olá e a palavra-passe que utilizam toosign no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="72cff-134">Executar **Get-AzureRmSubscription** tooview Olá todas as subscrições para esta conta.</span><span class="sxs-lookup"><span data-stu-id="72cff-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="72cff-135">Executar **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** subscrição de Olá tooselect que pretende que sejam toowork com.</span><span class="sxs-lookup"><span data-stu-id="72cff-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="72cff-136">Substitua **NameOfAzureSubscription** com o nome de Olá da sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="72cff-137">Criar um grupo de recursos do Azure com o nome **ADFTutorialResourceGroup** executando Olá seguinte comando na Olá do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="72cff-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="72cff-138">Alguns dos passos de Olá neste tutorial partem do princípio de que utiliza o grupo de recursos de Olá com o nome ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="72cff-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="72cff-139">Se utilizar um grupo de recursos diferente, terá de nome de Olá toouse do seu grupo de recursos em vez de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="72cff-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="72cff-140">Criar definições JSON</span><span class="sxs-lookup"><span data-stu-id="72cff-140">Create JSON definitions</span></span>
<span data-ttu-id="72cff-141">Crie os seguintes ficheiros JSON na pasta de olá onde curl.exe está localizado.</span><span class="sxs-lookup"><span data-stu-id="72cff-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="72cff-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="72cff-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="72cff-143">Nome deve ser globalmente exclusivo, pelo que poderá ser útil tooprefix/sufixo ADFCopyTutorialDF toomake-um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="72cff-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="72cff-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="72cff-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="72cff-145">Substitua **accountname** e **accountkey** pelo nome e chave da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="72cff-146">toolearn como tooget o armazenamento de acesso da chave, consulte Olá obter informações sobre como tooview, copiar e voltar a gerar armazenamento aceder às chaves na [gerir a sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="72cff-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="72cff-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="72cff-147">hdinsightondemandlinkedservice.json</span></span>

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="72cff-148">Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:</span><span class="sxs-lookup"><span data-stu-id="72cff-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="72cff-149">Propriedade</span><span class="sxs-lookup"><span data-stu-id="72cff-149">Property</span></span> | <span data-ttu-id="72cff-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="72cff-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="72cff-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="72cff-151">ClusterSize</span></span> |<span data-ttu-id="72cff-152">Tamanho do cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="72cff-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="72cff-153">TimeToLive</span></span> |<span data-ttu-id="72cff-154">Especifica esse tempo de inatividade Olá para o cluster do HDInsight Olá, antes de ser eliminado.</span><span class="sxs-lookup"><span data-stu-id="72cff-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="72cff-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="72cff-155">linkedServiceName</span></span> |<span data-ttu-id="72cff-156">Especifica a conta de armazenamento Olá, que é utilizado toostore os registos de Olá que são gerados pelo HDInsight</span><span class="sxs-lookup"><span data-stu-id="72cff-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="72cff-157">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="72cff-157">Note hello following points:</span></span>

* <span data-ttu-id="72cff-158">Olá Data Factory cria um **baseado em Linux** cluster do HDInsight com Olá acima JSON.</span><span class="sxs-lookup"><span data-stu-id="72cff-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="72cff-159">Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="72cff-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="72cff-160">Também pode utilizar o **seu próprio cluster do HDInsight** em vez de utilizar um cluster do HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="72cff-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="72cff-161">Veja [HDInsight Linked Service (Serviço Ligado do HDInsight)](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="72cff-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="72cff-162">cluster do HDInsight Olá cria um **contentor predefinido** no armazenamento de BLOBs de Olá especificado na Olá JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="72cff-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="72cff-163">HDInsight não é eliminado deste contentor quando cluster Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="72cff-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="72cff-164">Este comportamento é propositado.</span><span class="sxs-lookup"><span data-stu-id="72cff-164">This behavior is by design.</span></span> <span data-ttu-id="72cff-165">Com o serviço de ligado de HDInsight a pedido, é criado um cluster de HDInsight sempre que um setor é processado, exceto se houver um cluster existente em direto (**timeToLive**) e é eliminado quando o processamento de Olá terminar.</span><span class="sxs-lookup"><span data-stu-id="72cff-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="72cff-166">À medida que são processados mais setores, verá muitos contentores no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="72cff-167">Se não precisar deles para resolução de problemas de tarefas Olá, poderá ser útil toodelete-los armazenamento de Olá tooreduce custo.</span><span class="sxs-lookup"><span data-stu-id="72cff-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="72cff-168">os nomes de Olá destes contentores seguem um padrão: "adf**nomedafábricadedados**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="72cff-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="72cff-169">Utilize ferramentas como [Explorador de armazenamento do Microsoft](http://storageexplorer.com/) toodelete contentores no seu Azure armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="72cff-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="72cff-170">Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="72cff-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="72cff-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="72cff-171">inputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

<span data-ttu-id="72cff-172">Olá JSON define um conjunto de dados com o nome **AzureBlobInput**, que representa dados de entrada para uma atividade no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="72cff-173">Além disso, especifica que os dados de entrada de Olá estão localizados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="72cff-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="72cff-174">Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:</span><span class="sxs-lookup"><span data-stu-id="72cff-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="72cff-175">Propriedade</span><span class="sxs-lookup"><span data-stu-id="72cff-175">Property</span></span> | <span data-ttu-id="72cff-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="72cff-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="72cff-177">tipo</span><span class="sxs-lookup"><span data-stu-id="72cff-177">type</span></span> |<span data-ttu-id="72cff-178">propriedade de tipo de Olá está definida tooAzureBlob porque os dados que residem no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="72cff-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="72cff-179">linkedServiceName</span></span> |<span data-ttu-id="72cff-180">refere-se toohello StorageLinkedService que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="72cff-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="72cff-181">fileName</span><span class="sxs-lookup"><span data-stu-id="72cff-181">fileName</span></span> |<span data-ttu-id="72cff-182">Esta propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="72cff-182">This property is optional.</span></span> <span data-ttu-id="72cff-183">Se omitir esta propriedade, serão escolhidos todos os ficheiros de Olá de Olá folderPath.</span><span class="sxs-lookup"><span data-stu-id="72cff-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="72cff-184">Neste caso, apenas Olá input.log é processado.</span><span class="sxs-lookup"><span data-stu-id="72cff-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="72cff-185">tipo</span><span class="sxs-lookup"><span data-stu-id="72cff-185">type</span></span> |<span data-ttu-id="72cff-186">ficheiros de registo de Olá estão no formato de texto, pelo que iremos utilizar TextFormat.</span><span class="sxs-lookup"><span data-stu-id="72cff-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="72cff-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="72cff-187">columnDelimiter</span></span> |<span data-ttu-id="72cff-188">colunas nos ficheiros de registo Olá são delimitadas por vírgula ()</span><span class="sxs-lookup"><span data-stu-id="72cff-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="72cff-189">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="72cff-189">frequency/interval</span></span> |<span data-ttu-id="72cff-190">a frequência definida tooMonth e o intervalo é 1, o que significa que os setores de entrada Olá estão disponíveis mensalmente.</span><span class="sxs-lookup"><span data-stu-id="72cff-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="72cff-191">externo</span><span class="sxs-lookup"><span data-stu-id="72cff-191">external</span></span> |<span data-ttu-id="72cff-192">Esta propriedade é definida tootrue se os dados de entrada de Olá não forem gerados pelo serviço do Data Factory Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="72cff-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="72cff-193">outputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="72cff-194">Olá JSON define um conjunto de dados com o nome **AzureBlobOutput**, que representa dados de saída para uma atividade no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="72cff-195">Além disso, especifica que os resultados de Olá são armazenados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="72cff-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="72cff-196">Olá **disponibilidade** secção especifica o conjunto de dados de saída que Olá é produzido mensalmente.</span><span class="sxs-lookup"><span data-stu-id="72cff-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="72cff-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="72cff-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="72cff-198">Substitua **storageaccountname** pelo nome da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "HDInsightOnDemandLinkedService"
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="72cff-199">No fragmento JSON de Olá, está a criar um pipeline que consiste numa única atividade que utiliza o ramo de registo tooprocess dados num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72cff-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="72cff-200">ficheiro de script de ramo de registo de Olá **partitionweblogs.hql**, é armazenada no Olá conta do storage do Azure (especificado pelo scriptLinkedService Olá, denominado **StorageLinkedService**) e, em **script**  pasta no contentor de Olá **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="72cff-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="72cff-201">Olá **define** secção especifica as definições de tempo de execução que são transmitidas toohello script de ramo de registo como valores de configuração do ramo de registo (por exemplo ${hiveconf: inputtable}, ${hiveconf}).</span><span class="sxs-lookup"><span data-stu-id="72cff-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="72cff-202">Olá **iniciar** e **final** propriedades de pipeline de Olá Especifica o período ativo de Olá de pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="72cff-203">No JSON de atividade de Olá, especifique esse Olá script de ramo de registo é executado na computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="72cff-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="72cff-204">Consulte "JSON do Pipeline" em [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON utilizadas no Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="72cff-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="72cff-205">Definir variáveis globais</span><span class="sxs-lookup"><span data-stu-id="72cff-205">Set global variables</span></span>
<span data-ttu-id="72cff-206">No Azure PowerShell, execute Olá depois de substituir os valores de Olá com os seus próprios os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="72cff-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72cff-207">Consulte a secção [Pré-requisitos](#prerequisites) para instruções sobre como obter o ID de cliente, o segredo do cliente, o ID de inquilino e o ID da subscrição.</span><span class="sxs-lookup"><span data-stu-id="72cff-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="72cff-208">Autenticar com o AAD</span><span class="sxs-lookup"><span data-stu-id="72cff-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="72cff-209">Criar fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="72cff-209">Create data factory</span></span>
<span data-ttu-id="72cff-210">Neste passo, irá criar uma fábrica de dados do Azure com o nome **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="72cff-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="72cff-211">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="72cff-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="72cff-212">Um pipeline pode conter uma atividade ou mais.</span><span class="sxs-lookup"><span data-stu-id="72cff-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="72cff-213">Por exemplo, um atividade de cópia toocopy dados de um arquivo de dados de destino de tooa de origem e um toorun de atividade do ramo de registo do HDInsight tootransform dados de script de ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="72cff-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="72cff-214">Execute Olá fábrica de dados do comandos toocreate Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="72cff-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="72cff-215">Atribuir Olá comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="72cff-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="72cff-216">Confirme que o nome da fábrica de dados de Olá que especificar aqui (ADFCopyTutorialDF) correspondências Olá nome especificado no Olá Olá **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="72cff-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="72cff-217">Execute o comando de Olá utilizando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="72cff-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="72cff-218">Ver os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-218">View hello results.</span></span> <span data-ttu-id="72cff-219">Se Olá a fábrica de dados foi criada com êxito, verá Olá JSON Olá fábrica de dados no Olá **resultados**; caso contrário, verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="72cff-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="72cff-220">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="72cff-220">Note hello following points:</span></span>

* <span data-ttu-id="72cff-221">nome de Olá de Olá do Azure Data Factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="72cff-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="72cff-222">Se vir Olá erro nos resultados: **nome da fábrica de dados "FirstDataFactoryREST" não está disponível**, Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="72cff-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="72cff-223">O nome de Olá alteração (por exemplo, yournameFirstDataFactoryREST) no Olá **datafactory.json** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="72cff-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="72cff-224">Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="72cff-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="72cff-225">No comando primeiro olá onde Olá **$cmd** variável é atribuída um valor, substitua o novo nome de Olá FirstDataFactoryREST e execute o comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="72cff-226">Execute Olá dois comandos tooinvoke Olá REST API toocreate Olá data factory e de impressão Olá resultados da operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="72cff-227">instâncias do Data Factory toocreate, terá de toobe um Contribuidor/administrador da Olá subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="72cff-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="72cff-228">nome de Olá da fábrica de dados de Olá pode ser registado como um nome DNS no futuro Olá e, por conseguinte, ficar publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="72cff-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="72cff-229">Se receber o erro de Olá: "**esta subscrição não está registado toouse espaço de nomes Microsoft. DataFactory**", efetue um dos seguintes Olá e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="72cff-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="72cff-230">No Azure PowerShell, execute Olá fornecedor do Data Factory comando tooregister Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="72cff-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="72cff-231">Pode executar Olá tooconfirm de comando a seguir que Olá é registado o fornecedor do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="72cff-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="72cff-232">Utilizar o início de sessão Olá a subscrição do Azure no Olá [portal do Azure](https://portal.azure.com) e navegue até o painel do Data Factory tooa (ou) crie uma fábrica de dados no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="72cff-233">Esta ação regista automaticamente o fornecedor de Olá por si.</span><span class="sxs-lookup"><span data-stu-id="72cff-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="72cff-234">Antes de criar um pipeline, terá de toocreate algumas entidades do Data Factory primeiro.</span><span class="sxs-lookup"><span data-stu-id="72cff-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="72cff-235">Primeiro criar serviços ligados toolink dados arquivos/computações tooyour armazenar, definir a entrada e saída de dados de toorepresent de conjuntos de dados nos arquivos de dados ligados.</span><span class="sxs-lookup"><span data-stu-id="72cff-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="72cff-236">Criar serviços ligados</span><span class="sxs-lookup"><span data-stu-id="72cff-236">Create linked services</span></span>
<span data-ttu-id="72cff-237">Neste passo, pode liga a sua conta do Storage do Azure e uma fábrica de dados a pedido do Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="72cff-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="72cff-238">Olá contém Olá dados de entrada e de saída do pipeline de Olá neste exemplo de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="72cff-239">Olá serviço ligado do HDInsight é toorun utilizado um script de ramo de registo especificado na atividade de Olá de pipeline de Olá neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="72cff-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="72cff-240">Criar o serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="72cff-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="72cff-241">Neste passo, ligar a fábrica de dados de tooyour de conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="72cff-242">Com este tutorial utiliza Olá mesma conta de armazenamento do Azure ficheiro de script de dados de entrada/saída toostore e Olá HQL.</span><span class="sxs-lookup"><span data-stu-id="72cff-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="72cff-243">Atribuir Olá comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="72cff-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="72cff-244">Execute o comando de Olá utilizando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="72cff-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="72cff-245">Ver os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-245">View hello results.</span></span> <span data-ttu-id="72cff-246">Se ligado Olá o serviço foi criado com êxito, verá Olá JSON para o serviço de Olá ligado no Olá **resultados**; caso contrário, verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="72cff-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="72cff-247">Criar o serviço ligado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="72cff-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="72cff-248">Neste passo, pode liga a uma fábrica de dados a pedido HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="72cff-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="72cff-249">cluster do HDInsight Olá é automaticamente criada no tempo de execução e eliminado depois de ter é processado e ficado inativo para o período de tempo especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="72cff-250">Também pode utilizar o seu próprio cluster do HDInsight em vez de utilizar um cluster do HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="72cff-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="72cff-251">Veja [Compute Linked Services (Serviços Ligados de Computação)](data-factory-compute-linked-services.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="72cff-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="72cff-252">Atribuir Olá comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="72cff-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="72cff-253">Execute o comando de Olá utilizando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="72cff-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="72cff-254">Ver os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-254">View hello results.</span></span> <span data-ttu-id="72cff-255">Se ligado Olá o serviço foi criado com êxito, verá Olá JSON para o serviço de Olá ligado no Olá **resultados**; caso contrário, verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="72cff-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="72cff-256">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="72cff-256">Create datasets</span></span>
<span data-ttu-id="72cff-257">Neste passo, poderá criar conjuntos de dados toorepresent Olá entrada e saída dados para o processamento do ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="72cff-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="72cff-258">Estes conjuntos de dados Consulte toohello **StorageLinkedService** que criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="72cff-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="72cff-259">Olá tooan de pontos de serviço ligado conta de armazenamento do Azure e os conjuntos de dados especificam um contentor, pasta, nome de ficheiro no armazenamento de Olá que contém a entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="72cff-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="72cff-260">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="72cff-260">Create input dataset</span></span>
<span data-ttu-id="72cff-261">Neste passo, vai criar Olá conjunto de dados de entrada toorepresent entrada dados armazenados no Olá Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="72cff-262">Atribuir Olá comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="72cff-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="72cff-263">Execute o comando de Olá utilizando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="72cff-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="72cff-264">Ver os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-264">View hello results.</span></span> <span data-ttu-id="72cff-265">Se Olá conjunto de dados foi criado com êxito, verá Olá JSON para Olá conjunto de dados Olá **resultados**; caso contrário, verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="72cff-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="72cff-266">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="72cff-266">Create output dataset</span></span>
<span data-ttu-id="72cff-267">Neste passo, crie as dados de saída conjunto de dados de saída do Olá toorepresent armazenados no Olá Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="72cff-268">Atribuir Olá comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="72cff-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="72cff-269">Execute o comando de Olá utilizando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="72cff-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="72cff-270">Ver os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-270">View hello results.</span></span> <span data-ttu-id="72cff-271">Se Olá conjunto de dados foi criado com êxito, verá Olá JSON para Olá conjunto de dados Olá **resultados**; caso contrário, verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="72cff-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="72cff-272">Criar pipeline</span><span class="sxs-lookup"><span data-stu-id="72cff-272">Create pipeline</span></span>
<span data-ttu-id="72cff-273">Neste passo, irá criar o seu primeiro pipeline com uma atividade **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="72cff-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="72cff-274">Setor de entrada está disponível mensalmente (frequência: mês, intervalo: 1), o setor de saída é produzido mensalmente e propriedade do agendador Olá atividade Olá seja também definida toomonthly.</span><span class="sxs-lookup"><span data-stu-id="72cff-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="72cff-275">Olá as definições de conjunto de dados de saída de Olá e agendador de atividade Olá têm de corresponder.</span><span class="sxs-lookup"><span data-stu-id="72cff-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="72cff-276">Atualmente, o conjunto de dados de saída é que unidades Olá agenda, pelo que deve criar um conjunto de dados de saída, mesmo se Olá atividade não produzir qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="72cff-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="72cff-277">Se a atividade de Olá não incluir entradas, pode ignorar o conjunto de dados de entrada Olá criar.</span><span class="sxs-lookup"><span data-stu-id="72cff-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="72cff-278">Confirme que vê Olá **input.log** ficheiro Olá **adfgetstarted/inputdata** pasta Olá blob storage do Azure e execute Olá pipeline de Olá toodeploy de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="72cff-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="72cff-279">Desde Olá **iniciar** e **final** são definidas no passado Olá e **isPaused** é conjunto toofalse, pipeline Olá executa (atividade no pipeline de Olá) imediatamente depois da implementação.</span><span class="sxs-lookup"><span data-stu-id="72cff-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="72cff-280">Atribuir Olá comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="72cff-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="72cff-281">Execute o comando de Olá utilizando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="72cff-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="72cff-282">Ver os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-282">View hello results.</span></span> <span data-ttu-id="72cff-283">Se Olá conjunto de dados foi criado com êxito, verá Olá JSON para Olá conjunto de dados Olá **resultados**; caso contrário, verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="72cff-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="72cff-284">Parabéns, criou com êxito o seu primeiro pipeline com o Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="72cff-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="72cff-285">Monitorizar o pipeline</span><span class="sxs-lookup"><span data-stu-id="72cff-285">Monitor pipeline</span></span>
<span data-ttu-id="72cff-286">Neste passo, utiliza o setores de toomonitor de API de REST de fábrica de dados que está a ser produzidos pelo pipeline Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="72cff-287">A criação de um cluster do HDInsight a pedido demora, por norma, algum tempo (cerca de 20 minutos).</span><span class="sxs-lookup"><span data-stu-id="72cff-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="72cff-288">Por conseguinte, esperar Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá setor.</span><span class="sxs-lookup"><span data-stu-id="72cff-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="72cff-289">Executar Olá Invoke-Command e Olá seguinte até verá o setor de Olá no **pronto** Estado ou **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="72cff-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="72cff-290">Quando o setor Olá está no estado pronto, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contentor de armazenamento de BLOBs para Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="72cff-291">criação de Olá de um cluster do HDInsight a pedido demora, normalmente, algum tempo.</span><span class="sxs-lookup"><span data-stu-id="72cff-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![dados de saída](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="72cff-293">ficheiro de entrada Olá é eliminado quando o setor de Olá é processado com êxito.</span><span class="sxs-lookup"><span data-stu-id="72cff-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="72cff-294">Por conseguinte, se pretender setor de Olá toorerun ou Olá novamente o tutorial, carregue Olá ficheiro de entrada (input.log) toohello na pasta inputdata do contentor adfgetstarted de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="72cff-295">Também pode utilizar os setores de toomonitor portal do Azure e resolva quaisquer problemas.</span><span class="sxs-lookup"><span data-stu-id="72cff-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="72cff-296">Consulte os detalhes em [Monitorizar pipelines com o portal do Azure](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="72cff-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="72cff-297">Resumo</span><span class="sxs-lookup"><span data-stu-id="72cff-297">Summary</span></span>
<span data-ttu-id="72cff-298">Neste tutorial, criou um dados de tooprocess da fábrica de dados do Azure executando o script de ramo de registo num cluster de hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72cff-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="72cff-299">Utilizou Olá Editor do Data Factory no Olá toodo portal do Azure de Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="72cff-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="72cff-300">Criou uma **fábrica de dados** do Azure.</span><span class="sxs-lookup"><span data-stu-id="72cff-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="72cff-301">Criar dois **serviços ligados**:</span><span class="sxs-lookup"><span data-stu-id="72cff-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="72cff-302">**Armazenamento do Azure** ligado serviço toolink o armazenamento de Blobs do Azure que contém a fábrica de dados de toohello de ficheiros de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="72cff-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="72cff-303">**O Azure HDInsight** a pedido ligado serviço toolink uma fábrica de dados a pedido do HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="72cff-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="72cff-304">O Azure Data Factory cria do HDInsight Hadoop, dados de entrada do cluster just-in-time tooprocess e produzir dados de saída.</span><span class="sxs-lookup"><span data-stu-id="72cff-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="72cff-305">Criar dois **conjuntos de dados**, que descrevem dados de entrada e de saída para a atividade do ramo de registo do HDInsight no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="72cff-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="72cff-306">Criar um **pipeline** com uma atividade do **Ramo de Registo do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="72cff-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72cff-307">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="72cff-307">Next steps</span></span>
<span data-ttu-id="72cff-308">Neste artigo, criou um pipeline com uma atividade de transformação (Atividade do HDInsight) que executa um Script de ramo de registo num cluster do Azure HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="72cff-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="72cff-309">toosee como toouse um toocopy de dados de atividade de cópia de tooAzure um Blob do Azure SQL, consulte [Tutorial: copiar dados de tooAzure um Blob do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="72cff-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="72cff-310">Veja Também</span><span class="sxs-lookup"><span data-stu-id="72cff-310">See Also</span></span>
| <span data-ttu-id="72cff-311">Tópico</span><span class="sxs-lookup"><span data-stu-id="72cff-311">Topic</span></span> | <span data-ttu-id="72cff-312">Descrição</span><span class="sxs-lookup"><span data-stu-id="72cff-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="72cff-313">Referência da API REST do Data Factory</span><span class="sxs-lookup"><span data-stu-id="72cff-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="72cff-314">Consulte a documentação abrangente sobre os cmdlets do Data Factory</span><span class="sxs-lookup"><span data-stu-id="72cff-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="72cff-315">Pipelines</span><span class="sxs-lookup"><span data-stu-id="72cff-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="72cff-316">Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e como toouse-los tooconstruct ponto a ponto condicionados por dados fluxos de trabalho para o seu cenário ou empresa.</span><span class="sxs-lookup"><span data-stu-id="72cff-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="72cff-317">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="72cff-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="72cff-318">Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="72cff-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="72cff-319">Agendamento e Execução</span><span class="sxs-lookup"><span data-stu-id="72cff-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="72cff-320">Este artigo explica os aspetos de agendamento e execução de Olá do modelo de aplicação do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="72cff-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="72cff-321">Monitorizar e gerir pipelines com a Aplicação de Monitorização</span><span class="sxs-lookup"><span data-stu-id="72cff-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="72cff-322">Este artigo descreve como toomonitor, gerir e depurar pipelines utilizando Olá de monitorização e gestão de aplicações.</span><span class="sxs-lookup"><span data-stu-id="72cff-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
