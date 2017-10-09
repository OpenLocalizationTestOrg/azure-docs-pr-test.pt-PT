---
title: problemas de Azure Data Factory aaaTroubleshoot
description: "Saiba como tootroubleshoot problemas com a utilização do Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="55e01-103">Resolver Problemas do Data Factory</span><span class="sxs-lookup"><span data-stu-id="55e01-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="55e01-104">Este artigo fornece sugestões de resolução de problemas para problemas ao utilizar o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="55e01-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="55e01-105">Este artigo não listar todos os problemas de possíveis Olá ao utilizar o serviço de Olá, mas abrange alguns problemas e sugestões de resolução de problemas gerais.</span><span class="sxs-lookup"><span data-stu-id="55e01-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="55e01-106">Sugestões de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="55e01-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="55e01-107">Erro: a subscrição de Olá não está registado toouse espaço de nomes 'Microsoft. DataFactory'</span><span class="sxs-lookup"><span data-stu-id="55e01-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="55e01-108">Se receber este erro, o fornecedor de recursos do Azure Data Factory Olá não foi registado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="55e01-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="55e01-109">Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="55e01-109">Do hello following:</span></span>

1. <span data-ttu-id="55e01-110">Inicie o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55e01-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="55e01-111">Inicie sessão no tooyour conta do Azure utilizando Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="55e01-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="55e01-112">Execute Olá seguir o fornecedor do comando tooregister Olá do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="55e01-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="55e01-113">Problema: Não autorizado Ocorreu um erro ao executar um cmdlet de fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="55e01-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="55e01-114">Provavelmente não estiver a utilizar o direito de Olá conta do Azure ou de subscrição com Olá Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55e01-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="55e01-115">Utilize Olá os seguintes cmdlets tooselect Olá direito toouse de conta e subscrição do Azure com Olá Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55e01-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="55e01-116">Login-AzureRmAccount - ID de utilizador correto de Olá de utilização e a palavra-passe</span><span class="sxs-lookup"><span data-stu-id="55e01-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="55e01-117">Get-AzureRmSubscription - vista Olá todas as subscrições da conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="55e01-118">SELECT-AzureRmSubscription &lt;nome da subscrição&gt; -selecionar a subscrição correta Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="55e01-119">Utilize Olá mesmo utilizar toocreate uma fábrica de dados no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55e01-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="55e01-120">Problema: Falha toolaunch Express programa de configuração do Gateway do gestão de dados a partir do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="55e01-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="55e01-121">a configuração de Express de Olá para Olá Data Management Gateway requer o Internet Explorer ou um Microsoft ClickOnce browser compatível com.</span><span class="sxs-lookup"><span data-stu-id="55e01-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="55e01-122">Se Olá configuração Express falhar toostart, efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="55e01-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="55e01-123">Utilize o Internet Explorer ou um ClickOnce da Microsoft compatível browser.</span><span class="sxs-lookup"><span data-stu-id="55e01-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="55e01-124">Se estiver a utilizar o Chrome, aceda toohello [arquivo da web de Chrome](https://chrome.google.com/webstore/), pesquise com palavra-chave de "ClickOnce", escolha uma das extensões de ClickOnce Olá e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="55e01-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="55e01-125">Olá, mesmo para Firefox (instalação suplemento).</span><span class="sxs-lookup"><span data-stu-id="55e01-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="55e01-126">Clique no botão de abrir Menu na barra de ferramentas Olá (nas três linhas horizontais no canto superior direito de Olá), clique em suplementos, procurar com palavra-chave de "ClickOnce", escolha uma das extensões de ClickOnce Olá e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="55e01-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="55e01-127">Olá utilize **configuração Manual** ligação apresentada na Olá mesmo painel no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="55e01-128">Pode utiliza este ficheiro de instalação de toodownload abordagem e executá-la manualmente.</span><span class="sxs-lookup"><span data-stu-id="55e01-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="55e01-129">Após a instalação de Olá for bem sucedida, verá a caixa de diálogo de configuração do Gateway de gestão de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="55e01-130">Olá cópia **chave** no ecrã de portal de Olá e utilize-a no Olá configuration manager toomanually registar o gateway de Olá com o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="55e01-131">Problema: Falha tooconnect tooon local do SQL Server</span><span class="sxs-lookup"><span data-stu-id="55e01-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="55e01-132">Iniciar **Gestor de configuração do Data Management Gateway** no Olá computador gateway e utilize Olá **resolução de problemas** separador tootest Olá ligação tooSQL servidor da máquina do gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="55e01-133">Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.</span><span class="sxs-lookup"><span data-stu-id="55e01-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="55e01-134">Problema: Setores de entrada estão a aguardar estado por alguma vez</span><span class="sxs-lookup"><span data-stu-id="55e01-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="55e01-135">setores Olá dever-se no **a aguardar** Estado devido a razões toovarious.</span><span class="sxs-lookup"><span data-stu-id="55e01-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="55e01-136">É uma das razões comuns Olá esse Olá **externo** propriedade não está definida demasiado**verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="55e01-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="55e01-137">Qualquer conjunto de dados que é o âmbito de produzidos Olá fora do Azure Data Factory deve ser marcado com **externo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="55e01-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="55e01-138">Esta propriedade indica que os dados de Olá são externos e não é efetuada por qualquer pipelines dentro da fábrica de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="55e01-139">setores de dados de Olá estão marcados como **pronto** depois Olá os dados estão disponíveis no arquivo respetivos Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="55e01-140">Consulte Olá seguinte o exemplo de utilização de Olá de Olá **externo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="55e01-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="55e01-141">Pode especificar opcionalmente **externalData*** quando configurar tootrue externo.</span><span class="sxs-lookup"><span data-stu-id="55e01-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="55e01-142">Consulte [conjuntos de dados](data-factory-create-datasets.md) artigo para obter mais detalhes sobre esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="55e01-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="55e01-143">tooresolve Olá erro, adicione Olá **externo** propriedade e Olá opcional **externalData** secção toohello definição de JSON da tabela de entrada Olá e recrie a tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e01-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="55e01-144">Problema: Falha de operação de cópia híbrida</span><span class="sxs-lookup"><span data-stu-id="55e01-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="55e01-145">Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para passos tootroubleshoot problemas com a cópia de um dados no local/arquivo utiliza Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="55e01-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="55e01-146">Problema: HDInsight a pedido falha de aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="55e01-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="55e01-147">Quando utilizar um serviço ligado do tipo HDInsightOnDemand, terá de toospecify um linkedServiceName que aponta tooan Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="55e01-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="55e01-148">Serviço de fábrica de dados utiliza este armazenamento toostore registos e ficheiros de suporte para o cluster de HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="55e01-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="55e01-149">Por vezes, o aprovisionamento de um cluster do HDInsight a pedido falha com Olá seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="55e01-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="55e01-150">Este erro normalmente indica que a localização de Olá Olá da conta de armazenamento especificada na Olá linkedServiceName não está a ser Olá localização onde Olá HDInsight aprovisionamento está a acontecer do Centro de dados do mesmos.</span><span class="sxs-lookup"><span data-stu-id="55e01-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="55e01-151">Exemplo: se a fábrica de dados está nos EUA oeste e Olá storage do Azure está nos EUA leste, Olá a pedido falha aprovisionamento nos EUA oeste.</span><span class="sxs-lookup"><span data-stu-id="55e01-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="55e01-152">Além disso, existe um segundo additionalLinkedServiceNames de propriedade JSON onde é possível especificar contas de armazenamento adicionais no HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="55e01-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="55e01-153">Essas contas de armazenamento ligado adicional devem estar no Olá falha a mesma localização que o cluster do HDInsight hello, ou com Olá mesmo erro.</span><span class="sxs-lookup"><span data-stu-id="55e01-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="55e01-154">Problema: Personalizado não for possível atividade de .NET</span><span class="sxs-lookup"><span data-stu-id="55e01-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="55e01-155">Consulte [depurar um pipeline com atividade personalizada](data-factory-use-custom-activities.md#troubleshoot-failures) para obter passos detalhados.</span><span class="sxs-lookup"><span data-stu-id="55e01-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="55e01-156">Utilizar tootroubleshoot portal do Azure</span><span class="sxs-lookup"><span data-stu-id="55e01-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="55e01-157">Com os painéis do portais</span><span class="sxs-lookup"><span data-stu-id="55e01-157">Using portal blades</span></span>
<span data-ttu-id="55e01-158">Consulte [monitorizar o pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para obter os passos.</span><span class="sxs-lookup"><span data-stu-id="55e01-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="55e01-159">Com a Aplicação Monitorizar e Gerir</span><span class="sxs-lookup"><span data-stu-id="55e01-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="55e01-160">Consulte [monitorizar e gerir pipelines de fábrica de dados com a monitorizar e gerir aplicações](data-factory-monitor-manage-app.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="55e01-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="55e01-161">Utilizar o Azure PowerShell tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="55e01-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="55e01-162">Utilizar o Azure PowerShell tootroubleshoot um erro</span><span class="sxs-lookup"><span data-stu-id="55e01-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="55e01-163">Consulte [Monitor Data Factory pipelines com o Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="55e01-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
