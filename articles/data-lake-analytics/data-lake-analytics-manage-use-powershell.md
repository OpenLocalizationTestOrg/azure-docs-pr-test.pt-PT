---
title: aaaManage Azure Data Lake Analytics com o Azure PowerShell | Microsoft Docs
description: "Saiba como toomanage contas de Data Lake Analytics, origens de dados, tarefas e itens de catálogo. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="00439-103">Gerir a Análise do Azure Data Lake com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="00439-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="00439-104">Saiba como toomanage contas de Azure Data Lake Analytics, origens de dados, tarefas e itens de catálogo com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00439-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="00439-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00439-105">Prerequisites</span></span>

<span data-ttu-id="00439-106">Quando criar uma conta de Data Lake Analytics, terá de tooknow:</span><span class="sxs-lookup"><span data-stu-id="00439-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="00439-107">**ID de subscrição**: Olá ID de subscrição do Azure no qual reside a conta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="00439-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="00439-108">**Grupo de recursos**: nome de Olá Olá do Azure do grupo de recursos que contém a sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="00439-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="00439-109">**O nome de conta do Data Lake Analytics**: Olá conta nome só pode conter letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="00439-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="00439-110">**Conta do Data Lake Store predefinida**: cada conta do Data Lake Analytics tem uma conta do Data Lake Store predefinida.</span><span class="sxs-lookup"><span data-stu-id="00439-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="00439-111">Estas contas tem de constar Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="00439-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="00439-112">**Localização**: localização Olá da sua conta do Data Lake Analytics, por exemplo, "EUA Leste 2" ou outro suportado localizações.</span><span class="sxs-lookup"><span data-stu-id="00439-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="00439-113">Localizações suportadas podem ser vistas no nosso [página de preços](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="00439-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="00439-114">fragmentos de PowerShell Olá neste tutorial, utilize estas variáveis toostore estas informações</span><span class="sxs-lookup"><span data-stu-id="00439-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="00439-115">Iniciar sessão</span><span class="sxs-lookup"><span data-stu-id="00439-115">Log in</span></span>

<span data-ttu-id="00439-116">Inicie sessão com um id de subscrição.</span><span class="sxs-lookup"><span data-stu-id="00439-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="00439-117">Inicie sessão com um nome de subscrição.</span><span class="sxs-lookup"><span data-stu-id="00439-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="00439-118">Olá `Login-AzureRmAccount` cmdlet sempre pede-lhe credenciais.</span><span class="sxs-lookup"><span data-stu-id="00439-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="00439-119">Pode evitar pedidos utilizando Olá os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="00439-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="00439-120">Gerir contas</span><span class="sxs-lookup"><span data-stu-id="00439-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="00439-121">Criar uma conta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="00439-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="00439-122">Se ainda não tiver um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, crie uma.</span><span class="sxs-lookup"><span data-stu-id="00439-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="00439-123">Cada conta de Data Lake Analytics requer uma conta de Data Lake Store predefinida que utiliza para armazenar registos.</span><span class="sxs-lookup"><span data-stu-id="00439-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="00439-124">Pode reutilizar uma conta existente ou criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="00439-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="00439-125">Assim que um Grupo de Recursos e uma conta de Data Lake Store estiverem disponíveis, crie uma conta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="00439-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="00439-126">Obter informações sobre uma conta</span><span class="sxs-lookup"><span data-stu-id="00439-126">Get information about an account</span></span>

<span data-ttu-id="00439-127">Obter informações sobre a uma conta.</span><span class="sxs-lookup"><span data-stu-id="00439-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="00439-128">Verificar a existência de Olá de uma conta de Data Lake Analytics específica.</span><span class="sxs-lookup"><span data-stu-id="00439-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="00439-129">Olá cmdlet devolve um `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="00439-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="00439-130">Verificar a existência de Olá de uma conta de Data Lake Store específica.</span><span class="sxs-lookup"><span data-stu-id="00439-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="00439-131">Olá cmdlet devolve um `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="00439-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="00439-132">Contas de listagem</span><span class="sxs-lookup"><span data-stu-id="00439-132">Listing accounts</span></span>

<span data-ttu-id="00439-133">Contas de análise do Data Lake da lista na subscrição atual Olá.</span><span class="sxs-lookup"><span data-stu-id="00439-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="00439-134">Contas de análise do Data Lake da lista dentro de um grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="00439-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="00439-135">Gerir regras de firewall</span><span class="sxs-lookup"><span data-stu-id="00439-135">Managing firewall rules</span></span>

<span data-ttu-id="00439-136">Lista de regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="00439-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="00439-137">Adicione uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="00439-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="00439-138">Altere uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="00439-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="00439-139">Remova uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="00439-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="00439-140">Permitir que os endereços IP do Azure.</span><span class="sxs-lookup"><span data-stu-id="00439-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="00439-141">Gerir origens de dados</span><span class="sxs-lookup"><span data-stu-id="00439-141">Managing data sources</span></span>
<span data-ttu-id="00439-142">Atualmente, o Azure Data Lake Analytics suporta Olá as seguintes origens de dados:</span><span class="sxs-lookup"><span data-stu-id="00439-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="00439-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="00439-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="00439-144">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="00439-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="00439-145">Quando cria uma conta de análise, tem de designar uma origem de dados do Data Lake Store conta toobe Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="00439-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="00439-146">Olá conta do Data Lake Store predefinida é utilizada registos de auditoria de metadados de tarefa toostore e tarefa.</span><span class="sxs-lookup"><span data-stu-id="00439-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="00439-147">Depois de criar uma conta de Data Lake Analytics, pode adicionar mais contas de Data Lake Store e/ou as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="00439-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="00439-148">Localizar a conta de Data Lake Store predefinida Olá</span><span class="sxs-lookup"><span data-stu-id="00439-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="00439-149">Pode encontrar a conta de Data Lake Store predefinida Olá por filtrar a lista de Olá de origens de dados por Olá `IsDefault` propriedade:</span><span class="sxs-lookup"><span data-stu-id="00439-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="00439-150">Adicionar uma origem de dados</span><span class="sxs-lookup"><span data-stu-id="00439-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="00439-151">Origens de dados de lista</span><span class="sxs-lookup"><span data-stu-id="00439-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="00439-152">Submeter tarefas U-SQL</span><span class="sxs-lookup"><span data-stu-id="00439-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="00439-153">Submeter uma cadeia como um script U-SQL</span><span class="sxs-lookup"><span data-stu-id="00439-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="00439-154">Submeter um ficheiro como um script U-SQL</span><span class="sxs-lookup"><span data-stu-id="00439-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="00439-155">Lista de tarefas numa conta</span><span class="sxs-lookup"><span data-stu-id="00439-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="00439-156">Liste todas as tarefas de Olá na conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="00439-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="00439-157">saída de Olá inclui Olá atualmente em execução de tarefas e essas tarefas que tenham sido concluído recentemente.</span><span class="sxs-lookup"><span data-stu-id="00439-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="00439-158">Lista de um número específico de tarefas</span><span class="sxs-lookup"><span data-stu-id="00439-158">List a specific number of jobs</span></span>

<span data-ttu-id="00439-159">Por predefinição a lista de Olá de tarefas é ordenada submeter no tempo.</span><span class="sxs-lookup"><span data-stu-id="00439-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="00439-160">Para que mais recentemente submetido Olá tarefas são apresentados primeiro.</span><span class="sxs-lookup"><span data-stu-id="00439-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="00439-161">Por predefinição, Olá conta ADLA memorizou tarefas durante 180 dias, mas Olá Ge AdlJob cmdlet por predefinição devolve apenas Olá 500 primeiro.</span><span class="sxs-lookup"><span data-stu-id="00439-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="00439-162">Utilize o - toolist parâmetro superior num número específico de tarefas.</span><span class="sxs-lookup"><span data-stu-id="00439-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="00439-163">Tarefas de lista com base no valor de Olá da propriedade de tarefa</span><span class="sxs-lookup"><span data-stu-id="00439-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="00439-164">Utilizar Olá `-State` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="00439-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="00439-165">Pode combinar qualquer um destes valores:</span><span class="sxs-lookup"><span data-stu-id="00439-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="00439-166">Olá utilize `-Result` parâmetro toodetect se terminada tarefas foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="00439-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="00439-167">Tem estes valores:</span><span class="sxs-lookup"><span data-stu-id="00439-167">It has these values:</span></span>

* <span data-ttu-id="00439-168">Foi cancelada</span><span class="sxs-lookup"><span data-stu-id="00439-168">Cancelled</span></span>
* <span data-ttu-id="00439-169">Falha</span><span class="sxs-lookup"><span data-stu-id="00439-169">Failed</span></span>
* <span data-ttu-id="00439-170">Nenhuma</span><span class="sxs-lookup"><span data-stu-id="00439-170">None</span></span>
* <span data-ttu-id="00439-171">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="00439-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="00439-172">Olá `-Submitter` parâmetro ajuda-o a identificar quem submetida uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="00439-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="00439-173">Olá `-SubmittedAfter` é útil em filtragem tooa intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="00439-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="00439-174">Cenários comuns para listar as tarefas</span><span class="sxs-lookup"><span data-stu-id="00439-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="00439-175">Filtragem de uma lista de tarefas</span><span class="sxs-lookup"><span data-stu-id="00439-175">Filtering a list of jobs</span></span>

<span data-ttu-id="00439-176">Assim que tiver uma lista de tarefas na sua sessão atual do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00439-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="00439-177">Pode utilizar normal lista de Olá do toofilter de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00439-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="00439-178">Filtro de uma lista de tarefas toohello tarefas submetidas no Olá últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="00439-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="00439-179">Filtrar uma lista de tarefas toohello tarefas que terminado em Olá últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="00439-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="00439-180">Filtre uma lista de tarefas de toohello de Tarefas iniciou a execução.</span><span class="sxs-lookup"><span data-stu-id="00439-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="00439-181">Uma tarefa pode falhar no momento da compilação - e, por isso, nunca inicia.</span><span class="sxs-lookup"><span data-stu-id="00439-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="00439-182">Vamos ver tarefas de Olá falhada que realmente começou a ser executada e, em seguida, falhou.</span><span class="sxs-lookup"><span data-stu-id="00439-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="00439-183">Analisar uma lista de tarefas</span><span class="sxs-lookup"><span data-stu-id="00439-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="00439-184">Olá utilize `Group-Object` cmdlet tooanalyze uma lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="00439-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="00439-185">Quando efetuar uma análise, pode ser útil tooadd propriedades toohello tarefa objetos toomake filtragem e mais simples de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="00439-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="00439-186">Olá fragmento a seguir mostra como tooannotate uma JobInfo com calculada propriedades.</span><span class="sxs-lookup"><span data-stu-id="00439-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="00439-187">Obter informações sobre pipelines e recurrences</span><span class="sxs-lookup"><span data-stu-id="00439-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="00439-188">Olá utilize `Get-AdlJobPipeline` informações de pipeline do cmdlet toosee Olá previamente submetido tarefas.</span><span class="sxs-lookup"><span data-stu-id="00439-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="00439-189">Olá utilize `Get-AdlJobRecurrence` cmdlet toosee Olá periodicidade as informações de tarefas anteriormente submetidas.</span><span class="sxs-lookup"><span data-stu-id="00439-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="00439-190">Obter informações sobre uma tarefa</span><span class="sxs-lookup"><span data-stu-id="00439-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="00439-191">Obter estado da tarefa</span><span class="sxs-lookup"><span data-stu-id="00439-191">Get job status</span></span>

<span data-ttu-id="00439-192">Obter o estado de Olá de uma tarefa específica.</span><span class="sxs-lookup"><span data-stu-id="00439-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="00439-193">Examine Olá saídas de tarefa</span><span class="sxs-lookup"><span data-stu-id="00439-193">Examine hello job outputs</span></span>

<span data-ttu-id="00439-194">Depois de terminou a tarefa de Olá, verifique se o ficheiro de saída Olá existe por listar ficheiros Olá numa pasta.</span><span class="sxs-lookup"><span data-stu-id="00439-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="00439-195">Gerir tarefas em execução</span><span class="sxs-lookup"><span data-stu-id="00439-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="00439-196">Cancelar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="00439-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="00439-197">Aguarde um toofinish de tarefa</span><span class="sxs-lookup"><span data-stu-id="00439-197">Wait for a job toofinish</span></span>

<span data-ttu-id="00439-198">Em vez de repetir `Get-AdlAnalyticsJob` até que seja uma tarefa concluída, pode utilizar Olá `Wait-AdlJob` toowait de cmdlet para Olá tarefa tooend.</span><span class="sxs-lookup"><span data-stu-id="00439-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="00439-199">Gerir políticas de computação</span><span class="sxs-lookup"><span data-stu-id="00439-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="00439-200">Lista as políticas existentes de computação</span><span class="sxs-lookup"><span data-stu-id="00439-200">List existing compute policies</span></span>

<span data-ttu-id="00439-201">Olá `Get-AdlAnalyticsComputePolicy` cmdlet obtém informações sobre as políticas de computação para uma conta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="00439-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="00439-202">Criar uma política de computação</span><span class="sxs-lookup"><span data-stu-id="00439-202">Create a compute policy</span></span>

<span data-ttu-id="00439-203">Olá `New-AdlAnalyticsComputePolicy` cmdlet cria uma nova política de computação para uma conta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="00439-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="00439-204">Neste exemplo conjuntos Olá toohello disponível de AUs máximo especificado too50 de utilizador e Olá tarefa mínimo prioridade too250.</span><span class="sxs-lookup"><span data-stu-id="00439-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="00439-205">Verifique a existência de Olá de um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="00439-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="00439-206">Carregar e transferir</span><span class="sxs-lookup"><span data-stu-id="00439-206">Uploading and downloading</span></span>

<span data-ttu-id="00439-207">Carregar um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="00439-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="00439-208">Carregar um recursivamente pasta inteira.</span><span class="sxs-lookup"><span data-stu-id="00439-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="00439-209">Transferir um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="00439-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="00439-210">Transferir um recursivamente pasta inteira.</span><span class="sxs-lookup"><span data-stu-id="00439-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="00439-211">Se hello carregar ou processo de transferência seja interrompido, pode tentar processo de Olá tooresume em execução Olá o cmdlet novamente com Olá ``-Resume`` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="00439-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="00439-212">Gerir itens de catálogo</span><span class="sxs-lookup"><span data-stu-id="00439-212">Manage catalog items</span></span>

<span data-ttu-id="00439-213">o catálogo de Olá U-SQL é utilizado toostructure dados e o código para que possa ser partilhados por scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="00439-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="00439-214">catálogo de Olá permite Olá mais elevado desempenho possível com os dados no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="00439-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="00439-215">Para obter mais informações, veja [Utilizar catálogo U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="00439-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="00439-216">Itens de lista no catálogo de Olá U-SQL</span><span class="sxs-lookup"><span data-stu-id="00439-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="00439-217">Liste todas as assemblagens de Olá em todas as bases de dados de Olá numa conta ADLA.</span><span class="sxs-lookup"><span data-stu-id="00439-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="00439-218">Obter detalhes sobre um item de catálogo</span><span class="sxs-lookup"><span data-stu-id="00439-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="00439-219">Criar as credenciais no catálogo</span><span class="sxs-lookup"><span data-stu-id="00439-219">Create credentials in a catalog</span></span>

<span data-ttu-id="00439-220">Dentro de uma base de dados do U-SQL, crie um objeto de credencial para uma base de dados alojado no Azure.</span><span class="sxs-lookup"><span data-stu-id="00439-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="00439-221">Atualmente, as credenciais de U-SQL são tipo apenas de Olá de item de catálogo que pode criar através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00439-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="00439-222">Obter informações básicas sobre uma conta ADLA</span><span class="sxs-lookup"><span data-stu-id="00439-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="00439-223">Olá seguinte código procura informações básicas sobre a conta de Olá fornecido um nome de conta</span><span class="sxs-lookup"><span data-stu-id="00439-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="00439-224">Trabalhar com o Azure</span><span class="sxs-lookup"><span data-stu-id="00439-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="00439-225">Obter os detalhes de erros de AzureRm</span><span class="sxs-lookup"><span data-stu-id="00439-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="00439-226">Certifique-se de que se estiver a executar como administrador</span><span class="sxs-lookup"><span data-stu-id="00439-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="00439-227">Localizar um TenantID</span><span class="sxs-lookup"><span data-stu-id="00439-227">Find a TenantID</span></span>

<span data-ttu-id="00439-228">A partir de um nome de subscrição:</span><span class="sxs-lookup"><span data-stu-id="00439-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="00439-229">A partir de um id de subscrição:</span><span class="sxs-lookup"><span data-stu-id="00439-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="00439-230">De um endereço de domínio, como "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="00439-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="00439-231">Listar todas as subscrições e ids de inquilino</span><span class="sxs-lookup"><span data-stu-id="00439-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="00439-232">Criar uma conta de Data Lake Analytics utilizando um modelo</span><span class="sxs-lookup"><span data-stu-id="00439-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="00439-233">Também pode utilizar um modelo de grupo de recursos do Azure utilizando Olá seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="00439-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="00439-234">Para obter mais informações, consulte [implementar uma aplicação com o modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) e [modelos Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="00439-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="00439-235">**Modelo de exemplo**</span><span class="sxs-lookup"><span data-stu-id="00439-235">**Example template**</span></span>

<span data-ttu-id="00439-236">Guardar Olá seguir texto como um `.json` de ficheiros e, em seguida, utilizar Olá precedente modelo de Olá de toouse de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00439-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="00439-237">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="00439-237">Next steps</span></span>
* [<span data-ttu-id="00439-238">Descrição geral do Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="00439-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="00439-239">Introdução ao Data Lake Analytics com [portal do Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="00439-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="00439-240">Gerir o Azure Data Lake Analytics com [portal do Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="00439-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
