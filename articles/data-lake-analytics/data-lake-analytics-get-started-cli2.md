---
title: "aaaGet começar a utilizar o Azure CLI 2.0 do Azure Data Lake Analytics | Microsoft Docs"
description: "Saiba como criar uma tarefa de Data Lake Analytics, utilizando U-SQL toouse Olá 2.0 de Interface de linha de comandos do Azure toocreate uma conta de Data Lake Analytics e submeter a tarefa de Olá. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="ef357-103">Introdução ao Azure Data Lake Analytics com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ef357-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="ef357-104">Neste tutorial, vai desenvolver uma tarefa que lê um ficheiro de valores separados por tabulações (TSV) e converte-o num ficheiro de valores separados por vírgulas (CSV).</span><span class="sxs-lookup"><span data-stu-id="ef357-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="ef357-105">toogo através de Olá suportado mesmo tutorial, utilizando outras ferramentas, utilize Olá na lista pendente na parte superior de Olá desta secção.</span><span class="sxs-lookup"><span data-stu-id="ef357-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef357-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ef357-106">Prerequisites</span></span>
<span data-ttu-id="ef357-107">Antes de começar este tutorial, tem de ter Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ef357-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="ef357-108">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ef357-108">**An Azure subscription**.</span></span> <span data-ttu-id="ef357-109">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef357-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ef357-110">**CLI 2.0 do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ef357-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="ef357-111">Consulte [instalar e configurar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ef357-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="ef357-112">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="ef357-112">Log in tooAzure</span></span>

<span data-ttu-id="ef357-113">toolog no tooyour subscrição do Azure:</span><span class="sxs-lookup"><span data-stu-id="ef357-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="ef357-114">São o URL do pedido toobrowse tooa e introduza um código de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ef357-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="ef357-115">E, em seguida, siga Olá instruções tooenter as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="ef357-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="ef357-116">Depois de ter sessão iniciada, o comando de início de sessão de Olá lista as suas subscrições.</span><span class="sxs-lookup"><span data-stu-id="ef357-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="ef357-117">toouse uma subscrição específica:</span><span class="sxs-lookup"><span data-stu-id="ef357-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="ef357-118">Criar conta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ef357-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="ef357-119">Tem de ter uma conta de Data Lake Analytics antes de poder executar quaisquer tarefas.</span><span class="sxs-lookup"><span data-stu-id="ef357-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="ef357-120">toocreate uma conta de Data Lake Analytics, tem de especificar Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ef357-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="ef357-121">**Grupo de Recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ef357-121">**Azure Resource Group**.</span></span> <span data-ttu-id="ef357-122">Uma conta do Data Lake Analytics tem de ser criada dentro de um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef357-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="ef357-123">[O Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permite-lhe toowork com recursos de Olá na sua aplicação como um grupo.</span><span class="sxs-lookup"><span data-stu-id="ef357-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="ef357-124">Pode implementar, atualizar ou eliminar todos os recursos de Olá para a sua aplicação numa operação única e coordenada.</span><span class="sxs-lookup"><span data-stu-id="ef357-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="ef357-125">toolist Olá existente grupos de recursos na sua subscrição:</span><span class="sxs-lookup"><span data-stu-id="ef357-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="ef357-126">toocreate um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="ef357-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="ef357-127">**Nome da conta do Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ef357-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="ef357-128">Cada conta do Data Lake Analytics tem um nome.</span><span class="sxs-lookup"><span data-stu-id="ef357-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="ef357-129">**Localização**.</span><span class="sxs-lookup"><span data-stu-id="ef357-129">**Location**.</span></span> <span data-ttu-id="ef357-130">Utilize um dos centros de dados do Azure de Olá que suporta o Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ef357-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="ef357-131">**Conta do Data Lake Store predefinida**: cada conta do Data Lake Analytics tem uma conta do Data Lake Store predefinida.</span><span class="sxs-lookup"><span data-stu-id="ef357-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="ef357-132">toolist Olá Data Lake Store conta existente:</span><span class="sxs-lookup"><span data-stu-id="ef357-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="ef357-133">toocreate uma nova conta de Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="ef357-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="ef357-134">Utilize Olá seguindo a sintaxe toocreate uma conta de Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="ef357-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="ef357-135">Depois de criar uma conta, pode utilizar Olá seguintes contas de Olá toolist de comandos e mostrar os detalhes da conta:</span><span class="sxs-lookup"><span data-stu-id="ef357-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="ef357-136">Carregar dados tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="ef357-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="ef357-137">Neste tutorial, vai processar alguns registos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ef357-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="ef357-138">registo de pesquisa de Olá pode ser armazenado no Data Lake store ou armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef357-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="ef357-139">Olá portal do Azure fornece uma interface de utilizador para copiar alguns exemplo dados ficheiros toohello Data Lake Store conta predefinida, que incluem um ficheiro de registo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ef357-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="ef357-140">Consulte [preparar dados de origem](data-lake-analytics-get-started-portal.md) conta de Data Lake Store do tooupload Olá dados toohello predefinido.</span><span class="sxs-lookup"><span data-stu-id="ef357-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="ef357-141">ficheiros de tooupload utilizando CLI 2.0, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ef357-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="ef357-142">A Data Lake Analytics também pode aceder ao armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef357-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="ef357-143">Para carregar o armazenamento de BLOBs de tooAzure de dados, consulte [Using Olá CLI do Azure com o Storage do Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ef357-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="ef357-144">Submeter tarefas de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ef357-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="ef357-145">tarefas de Data Lake Analytics Olá são escritas em linguagem U-SQL de Olá.</span><span class="sxs-lookup"><span data-stu-id="ef357-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="ef357-146">toolearn mais sobre U-SQL, consulte [introdução à linguagem U-SQL](data-lake-analytics-u-sql-get-started.md) e [eence de linguagem U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="ef357-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="ef357-147">**toocreate um script de tarefa do Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="ef357-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="ef357-148">Crie um ficheiro de texto com o seguinte script U-SQL e guarde a estação de trabalho do Olá texto ficheiro tooyour:</span><span class="sxs-lookup"><span data-stu-id="ef357-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="ef357-149">Este script U-SQL lê Olá origem ficheiro de dados utilizando **extractors**e, em seguida, cria um ficheiro csv, utilizando **outputters**.</span><span class="sxs-lookup"><span data-stu-id="ef357-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="ef357-150">Não modifique os dois caminhos de Olá, exceto se copiar o ficheiro de origem Olá para uma localização diferente.</span><span class="sxs-lookup"><span data-stu-id="ef357-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="ef357-151">O Data Lake Analytics cria a pasta de saída Olá se não existir.</span><span class="sxs-lookup"><span data-stu-id="ef357-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="ef357-152">É mais simples toouse de caminhos relativos para ficheiros armazenados em contas do Data Lake Store predefinida.</span><span class="sxs-lookup"><span data-stu-id="ef357-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="ef357-153">Também pode utilizar caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="ef357-153">You can also use absolute paths.</span></span>  <span data-ttu-id="ef357-154">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ef357-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="ef357-155">Tem de utilizar os ficheiros de tooaccess caminhos absolutos em contas de armazenamento ligadas.</span><span class="sxs-lookup"><span data-stu-id="ef357-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="ef357-156">Olá sintaxe para ficheiros armazenados numa conta de armazenamento do Azure ligada é:</span><span class="sxs-lookup"><span data-stu-id="ef357-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="ef357-157">O contentor de Blobs do Azure com blobs públicos não é suportado.</span><span class="sxs-lookup"><span data-stu-id="ef357-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="ef357-158">O contentor de Blobs do Azure com contentores públicos não é suportado.</span><span class="sxs-lookup"><span data-stu-id="ef357-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="ef357-159">**tarefas de toosubmit**</span><span class="sxs-lookup"><span data-stu-id="ef357-159">**toosubmit jobs**</span></span>

<span data-ttu-id="ef357-160">Utilize Olá seguindo a sintaxe toosubmit uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="ef357-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="ef357-161">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ef357-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="ef357-162">**tarefas de toolist e mostrar os detalhes da tarefa**</span><span class="sxs-lookup"><span data-stu-id="ef357-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="ef357-163">**tarefas de toocancel**</span><span class="sxs-lookup"><span data-stu-id="ef357-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="ef357-164">Obter resultados de tarefa</span><span class="sxs-lookup"><span data-stu-id="ef357-164">Retrieve job results</span></span>

<span data-ttu-id="ef357-165">Depois de uma tarefa é concluída, pode utilizar Olá os seguintes comandos toolist Olá ficheiros de saída e transferir ficheiros Olá:</span><span class="sxs-lookup"><span data-stu-id="ef357-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="ef357-166">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ef357-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="ef357-167">Pipelines e recorrências</span><span class="sxs-lookup"><span data-stu-id="ef357-167">Pipelines and recurrences</span></span>

<span data-ttu-id="ef357-168">**Obter informações sobre pipelines e recorrências**</span><span class="sxs-lookup"><span data-stu-id="ef357-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="ef357-169">Olá utilize `az dla job pipeline` comandos informações de pipeline de Olá toosee previamente submetido tarefas.</span><span class="sxs-lookup"><span data-stu-id="ef357-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="ef357-170">Olá utilize `az dla job recurrence` comandos toosee Olá periodicidade relativas tarefas anteriormente submetidas.</span><span class="sxs-lookup"><span data-stu-id="ef357-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="ef357-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ef357-171">Next steps</span></span>

* <span data-ttu-id="ef357-172">Olá toosee documento de referência do Data Lake Analytics CLI 2.0, consulte [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="ef357-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="ef357-173">Olá toosee documento de referência do Data Lake Store CLI 2.0, consulte [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="ef357-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="ef357-174">toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="ef357-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
