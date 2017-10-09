---
title: aaaAnalyze dados do Twitter com o Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Hive tooanalyze dados do Twitter do Hadoop no HDInsight toofind Olá frequência de utilização de uma palavra específica."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="7aa2a-103">Analisar dados do Twitter utilizando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7aa2a-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="7aa2a-104">Web sites sociais são um dos força despertar principais Olá para a adoção de macrodados.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="7aa2a-105">APIs públicas fornecidas por sites como Twitter são uma origem de dados para analisar e compreender as tendências populares útil.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="7aa2a-106">Neste tutorial, irá obter tweets utilizando a API de transmissão em fluxo do Twitter e, em seguida, utilizar o Apache Hive no Azure HDInsight tooget uma lista de utilizadores do Twitter que enviou Olá tweets maioria dos que continha um determinado word.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7aa2a-107">Olá passos neste documento exigem um cluster do HDInsight baseados em Windows.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="7aa2a-108">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7aa2a-109">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="7aa2a-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="7aa2a-110">Para o cluster do baseado em Linux tooa específico de passos, consulte [Twitter analisar dados, utilizando o Hive no HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7aa2a-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7aa2a-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7aa2a-111">Prerequisites</span></span>
<span data-ttu-id="7aa2a-112">Antes de começar este tutorial, tem de ter o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="7aa2a-113">**Uma estação de trabalho** com o Azure PowerShell instalada e configurada.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="7aa2a-114">scripts do Windows PowerShell tooexecute, tem de executar o Azure PowerShell como administrador e definir a política de execução de Olá demasiado*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="7aa2a-115">Consulte [scripts de executar o Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="7aa2a-116">Antes de executar scripts do Windows PowerShell, certifique-se de que está ligado tooyour subscrição do Azure utilizando o seguinte cmdlet de Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="7aa2a-117">Se tiver várias subscrições do Azure, utilize Olá subscrição atual do cmdlet tooset Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7aa2a-118">O suporte do Azure PowerShell para gerir recursos do HDInsight com o Gestor de Serviços do Azure está **preterido**, e foi removido a 1 de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="7aa2a-119">Olá passos neste documento utilize Olá novos cmdlets do HDInsight que funcionam com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="7aa2a-120">Siga os passos de Olá em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall versão mais recente do Olá do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="7aa2a-121">Se tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Azure Resource Manager, consulte [das ferramentas de migração tooAzure desenvolvimento baseadas no Resource Manager para clusters do HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="7aa2a-122">**Um cluster do Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="7aa2a-123">Para obter instruções sobre o aprovisionamento de cluster, consulte [começar a utilizar o HDInsight] [ hdinsight-get-started] ou [aprovisionar clusters do HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="7aa2a-124">É necessário o nome do cluster Olá mais tarde no tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="7aa2a-125">Olá tabela seguinte lista os ficheiros de Olá utilizados neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="7aa2a-126">Ficheiros</span><span class="sxs-lookup"><span data-stu-id="7aa2a-126">Files</span></span> | <span data-ttu-id="7aa2a-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="7aa2a-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7aa2a-128">/Tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="7aa2a-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="7aa2a-129">dados de origem de Olá de tarefa do Hive Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="7aa2a-130">/Tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="7aa2a-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="7aa2a-131">Olá a pasta de saída para a tarefa do Hive Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="7aa2a-132">Olá nome de ficheiro de saída de tarefa do Hive predefinido é **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="7aa2a-133">Tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="7aa2a-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="7aa2a-134">ficheiro de script de HiveQL Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="7aa2a-135">/Tutorials/twitter/JobStatus</span><span class="sxs-lookup"><span data-stu-id="7aa2a-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="7aa2a-136">Olá Hadoop estado da tarefa.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="7aa2a-137">Feed do Twitter Get</span><span class="sxs-lookup"><span data-stu-id="7aa2a-137">Get Twitter feed</span></span>
<span data-ttu-id="7aa2a-138">Neste tutorial, irá utilizar Olá [Twitter APIs de transmissão em fluxo][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="7aa2a-139">Olá Twitter específico API utilizará de transmissão em fluxo é [Estados/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="7aa2a-140">Um ficheiro que contenha 10 000 tweets e ficheiro de script de ramo de registo de Olá (abrangido na secção seguinte, Olá) tiverem sido carregados num contentor de Blob público.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="7aa2a-141">Pode ignorar esta secção se quiser toouse Olá carregado ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="7aa2a-142">[Tweets dados](https://dev.twitter.com/docs/platform-objects/tweets) são armazenadas em formato do Olá JavaScript Object Notation (JSON) que contém uma estrutura aninhada complexa.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="7aa2a-143">Em vez de escrever várias linhas de código ao utilizar uma linguagem de programação convencional, pode transformar esta estrutura aninhada numa tabela do Hive, para que podem ser consultada por uma linguagem SQL (Structured Query)-como linguagem denominada HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="7aa2a-144">Twitter utiliza OAuth tooprovide autorizado acesso tooits API.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="7aa2a-145">OAuth é um protocolo de autenticação que permite que os utilizadores tooapprove aplicações tooact em nome sem partilha a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="7aa2a-146">Podem encontrar mais informações em [oauth.net](http://oauth.net/) ou em Olá excelente [tooOAuth de guia do Beginner](http://hueniverse.com/oauth/) de Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="7aa2a-147">Olá primeiro passo toouse OAuth é toocreate uma nova aplicação no site de programador Twitter Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="7aa2a-148">**toocreate uma aplicação do Twitter**</span><span class="sxs-lookup"><span data-stu-id="7aa2a-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="7aa2a-149">A iniciar sessão demasiado[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="7aa2a-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="7aa2a-150">Clique em Olá **inscrever-se agora** ligação se não tiver uma conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="7aa2a-151">Clique em **criar nova aplicação**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="7aa2a-152">Introduza **nome**, **Descrição**, **Web site**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="7aa2a-153">Pode efetuar cópias de segurança um URL para Olá **Web site** campo.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="7aa2a-154">Olá, a tabela seguinte mostra algumas toouse de valores de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="7aa2a-155">Campo</span><span class="sxs-lookup"><span data-stu-id="7aa2a-155">Field</span></span> | <span data-ttu-id="7aa2a-156">Valor</span><span class="sxs-lookup"><span data-stu-id="7aa2a-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7aa2a-157">Nome</span><span class="sxs-lookup"><span data-stu-id="7aa2a-157">Name</span></span> |<span data-ttu-id="7aa2a-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="7aa2a-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="7aa2a-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="7aa2a-159">Description</span></span> |<span data-ttu-id="7aa2a-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="7aa2a-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="7aa2a-161">Site</span><span class="sxs-lookup"><span data-stu-id="7aa2a-161">Website</span></span> |<span data-ttu-id="7aa2a-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="7aa2a-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="7aa2a-163">Verifique **Sim, aceita**e, em seguida, clique em **criar a sua aplicação Twitter**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="7aa2a-164">Clique em Olá **permissões** permissão do separador. Olá predefinida é **só de leitura**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="7aa2a-165">Isto é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="7aa2a-166">Clique em Olá **chaves e os Tokens de acesso** separador.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="7aa2a-167">Clique em **crie minha token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="7aa2a-168">Clique em **teste OAuth** no canto superior direito de Olá da página Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="7aa2a-169">Anote **chave de consumidor**, **segredo de consumidor**, **token de acesso**, e **secreta de token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="7aa2a-170">Precisa de valores de Olá mais tarde no tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="7aa2a-171">Neste tutorial, irá utilizar a chamada de serviço web do Windows PowerShell toomake Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="7aa2a-172">Para um exemplo .NET c#, consulte [analisar dados de sentimento do Twitter em tempo real com o HBase no HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="7aa2a-173">Olá outras chamadas de serviço web do ferramenta populares toomake é [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="7aa2a-174">Curl pode ser transferido do [aqui][curl-download].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="7aa2a-175">Quando utilizar o comando de curl Olá no Windows, utilize aspas duplas em vez de plicas para os valores de opção Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="7aa2a-176">**tooget tweets**</span><span class="sxs-lookup"><span data-stu-id="7aa2a-176">**tooget tweets**</span></span>

1. <span data-ttu-id="7aa2a-177">Abra Olá Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="7aa2a-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="7aa2a-178">(No ecrã Iniciar do Windows 8 Olá, escreva **PowerShell_ISE** e, em seguida, clique em **ISE do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="7aa2a-179">Consulte [iniciar o Windows PowerShell no Windows 8 e Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="7aa2a-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="7aa2a-180">Copie Olá seguinte script no painel de script de Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="7aa2a-181">Defina variáveis de tooeight primeiro cinco Olá no script de Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="7aa2a-182">Variável</span><span class="sxs-lookup"><span data-stu-id="7aa2a-182">Variable</span></span>|<span data-ttu-id="7aa2a-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="7aa2a-183">Description</span></span>
    ---|---
    <span data-ttu-id="7aa2a-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="7aa2a-184">$clusterName</span></span>|<span data-ttu-id="7aa2a-185">Este é o nome de Olá de cluster do HDInsight olá onde pretende que a aplicação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="7aa2a-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="7aa2a-186">$oauth_consumer_key</span></span>|<span data-ttu-id="7aa2a-187">Esta é a aplicação de Twitter Olá **chave de consumidor** escreveu anteriormente quando criou a aplicação do Olá Twitter.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="7aa2a-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="7aa2a-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="7aa2a-189">Esta é a aplicação de Twitter Olá **segredo de consumidor** escrevemos anteriormente para baixo.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="7aa2a-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="7aa2a-190">$oauth_token</span></span>|<span data-ttu-id="7aa2a-191">Esta é a aplicação de Twitter Olá **token de acesso** escrevemos anteriormente para baixo.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="7aa2a-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="7aa2a-192">$oauth_token_secret</span></span>|<span data-ttu-id="7aa2a-193">Esta é a aplicação de Twitter Olá **secreta de token de acesso** escrevemos anteriormente para baixo.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="7aa2a-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="7aa2a-194">$destBlobName</span></span>|<span data-ttu-id="7aa2a-195">Este é o nome do blob de saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-195">This is hello output blob name.</span></span> <span data-ttu-id="7aa2a-196">valor predefinido de Olá é **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="7aa2a-197">Se alterar o valor predefinido de Olá, precisa de scripts do tooupdate Olá do Windows PowerShell em conformidade.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="7aa2a-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="7aa2a-198">$trackString</span></span>|<span data-ttu-id="7aa2a-199">serviço web de Olá irá devolver as de palavras-chave tweets toothese relacionados.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="7aa2a-200">valor predefinido de Olá é **do Azure, nuvem, o HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="7aa2a-201">Se alterar o valor predefinido de Olá, atualizar scripts do Windows PowerShell de Olá em conformidade.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="7aa2a-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="7aa2a-202">$lineMax</span></span>|<span data-ttu-id="7aa2a-203">valor de Olá determina quantos script de Olá tweets serão lidos.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="7aa2a-204">Demora cerca de três minutos tooread 100 tweets.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="7aa2a-205">Pode definir um número maior, mas irá demorar mais toodownload de tempo.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="7aa2a-206">Prima **F5** script de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="7aa2a-207">Caso se depare com problemas, como solução, selecione todas as linhas de Olá e, em seguida, prima **F8**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="7aa2a-208">Deverá ver "Concluir"!</span><span class="sxs-lookup"><span data-stu-id="7aa2a-208">You shall see "Complete!"</span></span> <span data-ttu-id="7aa2a-209">no final de Olá da saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-209">at hello end of hello output.</span></span> <span data-ttu-id="7aa2a-210">As mensagens de erro serão apresentadas vermelho.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="7aa2a-211">Como um procedimento de validação, pode verificar o ficheiro de saída Olá, **/tutorials/twitter/data/tweets.txt**, no seu armazenamento de Blobs do Azure ao utilizar um Explorador de armazenamento do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="7aa2a-212">Para um script do Windows PowerShell de exemplo para listar os ficheiros, consulte [utilizar o Blob storage com o HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="7aa2a-213">Criar script de HiveQL</span><span class="sxs-lookup"><span data-stu-id="7aa2a-213">Create HiveQL script</span></span>
<span data-ttu-id="7aa2a-214">Com o Azure PowerShell, pode executar várias declarações HiveQL um uma hora ou Olá pacote instrução HiveQL para um ficheiro de script.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="7aa2a-215">Neste tutorial, irá criar um script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="7aa2a-216">ficheiro de script de Olá tem de ser carregados tooAzure o Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="7aa2a-217">Na secção seguinte, Olá, irá executar o ficheiro de script de Olá utilizando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="7aa2a-218">ficheiro de script de ramo de registo Olá e um ficheiro que contenha 10 000 tweets tiverem sido carregados num contentor de Blob público.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="7aa2a-219">Pode ignorar esta secção se quiser toouse Olá carregado ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="7aa2a-220">Olá script de HiveQL executará o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="7aa2a-221">**Largar a tabela de tweets_raw Olá** no caso de Olá tabela já existe.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="7aa2a-222">**Criar a tabela de Hive Olá tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="7aa2a-223">Esta tabela estruturada temporária do ramo de registo contém dados de Olá para ainda mais a extração, transformação e carregamento processamento (ETL).</span><span class="sxs-lookup"><span data-stu-id="7aa2a-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="7aa2a-224">Para obter informações sobre as partições, consulte [Hive tutorial][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="7aa2a-225">**Carregar dados** da pasta de origem Olá, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="7aa2a-226">Olá tweets grande conjunto de dados aninhado formato JSON agora ter sido transformado numa estrutura de tabela do Hive temporária.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="7aa2a-227">**Largar Olá tweets tabela** no caso de Olá tabela já existe.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="7aa2a-228">**Criar a tabela de tweets Olá**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-228">**Create hello tweets table**.</span></span> <span data-ttu-id="7aa2a-229">Antes de pode consultar contra o conjunto de dados do Olá tweets através do Hive, terá de toorun outro processo ETL.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="7aa2a-230">Este processo ETL define um esquema de tabela mais detalhado para dados de Olá que tem de ser armazenados na tabela de "twitter_raw" Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="7aa2a-231">**Inserir a tabela de substituição**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-231">**Insert overwrite table**.</span></span> <span data-ttu-id="7aa2a-232">Este script de ramo de registo complexa irá iniciar um conjunto de tarefas de MapReduce longas pelo cluster de Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="7aa2a-233">Dependendo do seu tamanho de conjunto de dados e Olá do seu cluster, isto pode demorar cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="7aa2a-234">**Diretório de substituição de inserção**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="7aa2a-235">Execute um ficheiro de tooa do conjunto de dados do Olá consulta e de saída.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="7aa2a-236">Esta consulta irá devolver uma lista de utilizadores do Twitter que enviou a maioria das tweets que continha word Olá "Azure".</span><span class="sxs-lookup"><span data-stu-id="7aa2a-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="7aa2a-237">**toocreate um ramo de registo de script e carregá-la tooAzure**</span><span class="sxs-lookup"><span data-stu-id="7aa2a-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="7aa2a-238">Abra o ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="7aa2a-239">Copie Olá seguinte script no painel de script de Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-239">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="7aa2a-240">Defina Olá primeiro duas variáveis no script de Olá:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="7aa2a-241">Variável</span><span class="sxs-lookup"><span data-stu-id="7aa2a-241">Variable</span></span> | <span data-ttu-id="7aa2a-242">Descrição</span><span class="sxs-lookup"><span data-stu-id="7aa2a-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="7aa2a-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="7aa2a-243">$clusterName</span></span> |<span data-ttu-id="7aa2a-244">Introduza o nome do cluster HDInsight olá onde pretende que a aplicação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="7aa2a-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="7aa2a-245">$subscriptionID</span></span> |<span data-ttu-id="7aa2a-246">Introduza o seu ID de subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="7aa2a-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="7aa2a-247">$sourceDataPath</span></span> |<span data-ttu-id="7aa2a-248">Olá onde consultas do Hive de Olá irão ler os dados de Olá da localização de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="7aa2a-249">Não precisa de toochange esta variável.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="7aa2a-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="7aa2a-250">$outputPath</span></span> |<span data-ttu-id="7aa2a-251">localização de armazenamento de Blobs do Azure onde as consultas do Hive Olá irão enviar os resultados de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="7aa2a-252">Não precisa de toochange esta variável.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="7aa2a-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="7aa2a-253">$hqlScriptFile</span></span> |<span data-ttu-id="7aa2a-254">Olá localização e o nome de ficheiro Olá do ficheiro de script de HiveQL Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="7aa2a-255">Não precisa de toochange esta variável.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="7aa2a-256">Prima **F5** script de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="7aa2a-257">Caso se depare com problemas, como solução, selecione todas as linhas de Olá e, em seguida, prima **F8**.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="7aa2a-258">Deverá ver "Concluir"!</span><span class="sxs-lookup"><span data-stu-id="7aa2a-258">You shall see "Complete!"</span></span> <span data-ttu-id="7aa2a-259">no final de Olá da saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-259">at hello end of hello output.</span></span> <span data-ttu-id="7aa2a-260">As mensagens de erro serão apresentadas vermelho.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="7aa2a-261">Como um procedimento de validação, pode verificar o ficheiro de saída Olá, **/tutorials/twitter/twitter.hql**, no seu armazenamento de Blobs do Azure ao utilizar um Explorador de armazenamento do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="7aa2a-262">Para um script do Windows PowerShell de exemplo para listar os ficheiros, consulte [utilizar o Blob storage com o HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="7aa2a-263">Processar os dados do Twitter através do Hive</span><span class="sxs-lookup"><span data-stu-id="7aa2a-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="7aa2a-264">Terminar o trabalho de preparação de Olá todos os.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="7aa2a-265">Agora, pode invocar o script de ramo de registo Olá e Olá resultados da verificação.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="7aa2a-266">Submeter uma tarefa do Hive</span><span class="sxs-lookup"><span data-stu-id="7aa2a-266">Submit a Hive job</span></span>
<span data-ttu-id="7aa2a-267">Utilize Olá seguinte script de ramo de registo do Windows PowerShell script toorun Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="7aa2a-268">Terá de variável de primeiro tooset Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="7aa2a-269">Olá toouse tweets e Olá script de HiveQL que carregou no Olá últimas duas secções, conjunto $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="7aa2a-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="7aa2a-270">Olá toouse aqueles que tenham sido carregados blob público tooa para si, defina $hqlScriptFile demasiado"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="7aa2a-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="7aa2a-271">Resultados da verificação de Olá</span><span class="sxs-lookup"><span data-stu-id="7aa2a-271">Check hello results</span></span>
<span data-ttu-id="7aa2a-272">Utilize Olá seguir Olá de toocheck de script do Windows PowerShell resultado da tarefa do Hive.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="7aa2a-273">Terá das primeiras duas variáveis de tooset Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabela de Hive Olá utiliza \001 como Olá delimitador de campos. <span data-ttu-id="7aa2a-275">delimitador Olá não estiver visível na saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="7aa2a-276">Depois de resultados de análise Olá foram colocados no Blob storage do Azure, pode exportar o servidor de base de dados/SQL Olá dados tooan SQL do Azure, exportar Olá dados tooExcel utilizando o Power Query ou ligar os dados da aplicação toohello utilizando Olá controlador ODBC do Hive.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="7aa2a-277">Para obter mais informações, consulte [utilize Sqoop com o HDInsight][hdinsight-use-sqoop], [analisar dados de atraso de voo utilizando HDInsight][hdinsight-analyze-flight-delay-data], [ Ligar o Excel tooHDInsight com o Power Query][hdinsight-power-query], e [tooHDInsight de ligar o Excel com Olá controlador ODBC do Hive Microsoft][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="7aa2a-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7aa2a-278">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7aa2a-278">Next steps</span></span>
<span data-ttu-id="7aa2a-279">Neste tutorial, iremos ter visto como tootransform um conjunto de dados JSON não estruturado para um estruturados tooquery de tabela do Hive, explorar e analisar dados do Twitter com o HDInsight no Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa2a-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="7aa2a-280">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="7aa2a-280">toolearn more, see:</span></span>

* <span data-ttu-id="7aa2a-281">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7aa2a-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="7aa2a-282">[Analisar dados de sentimento do Twitter em tempo real com o HBase no HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="7aa2a-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="7aa2a-283">[Analisar dados de atraso de voo utilizar o HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="7aa2a-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="7aa2a-284">[Ligar o Excel tooHDInsight com o Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="7aa2a-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="7aa2a-285">[Ligar o Excel tooHDInsight com Olá controlador ODBC do Hive Microsoft][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="7aa2a-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="7aa2a-286">[Utilizar o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="7aa2a-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
