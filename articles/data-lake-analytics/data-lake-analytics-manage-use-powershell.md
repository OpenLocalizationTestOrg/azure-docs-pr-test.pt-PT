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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Gerir a Análise do Azure Data Lake com o Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Saiba como toomanage contas de Azure Data Lake Analytics, origens de dados, tarefas e itens de catálogo com o Azure PowerShell. 

## <a name="prerequisites"></a>Pré-requisitos

Quando criar uma conta de Data Lake Analytics, terá de tooknow:

* **ID de subscrição**: Olá ID de subscrição do Azure no qual reside a conta de Data Lake Analytics.
* **Grupo de recursos**: nome de Olá Olá do Azure do grupo de recursos que contém a sua conta do Data Lake Analytics.
* **O nome de conta do Data Lake Analytics**: Olá conta nome só pode conter letras minúsculas e números.
* **Conta do Data Lake Store predefinida**: cada conta do Data Lake Analytics tem uma conta do Data Lake Store predefinida. Estas contas tem de constar Olá mesma localização.
* **Localização**: localização Olá da sua conta do Data Lake Analytics, por exemplo, "EUA Leste 2" ou outro suportado localizações. Localizações suportadas podem ser vistas no nosso [página de preços](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

fragmentos de PowerShell Olá neste tutorial, utilize estas variáveis toostore estas informações

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Iniciar sessão

Inicie sessão com um id de subscrição.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Inicie sessão com um nome de subscrição.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Olá `Login-AzureRmAccount` cmdlet sempre pede-lhe credenciais. Pode evitar pedidos utilizando Olá os seguintes cmdlets:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Gerir contas

### <a name="create-a-data-lake-analytics-account"></a>Criar uma conta de Data Lake Analytics

Se ainda não tiver um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, crie uma. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Cada conta de Data Lake Analytics requer uma conta de Data Lake Store predefinida que utiliza para armazenar registos. Pode reutilizar uma conta existente ou criar uma conta. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Assim que um Grupo de Recursos e uma conta de Data Lake Store estiverem disponíveis, crie uma conta de Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Obter informações sobre uma conta

Obter informações sobre a uma conta.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Verificar a existência de Olá de uma conta de Data Lake Analytics específica. Olá cmdlet devolve um `True` ou `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Verificar a existência de Olá de uma conta de Data Lake Store específica. Olá cmdlet devolve um `True` ou `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Contas de listagem

Contas de análise do Data Lake da lista na subscrição atual Olá.

```powershell
Get-AdlAnalyticsAccount
```

Contas de análise do Data Lake da lista dentro de um grupo de recursos específico.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Gerir regras de firewall

Lista de regras de firewall.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Adicione uma regra de firewall.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Altere uma regra de firewall.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Remova uma regra de firewall.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Permitir que os endereços IP do Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Gerir origens de dados
Atualmente, o Azure Data Lake Analytics suporta Olá as seguintes origens de dados:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Armazenamento do Azure](../storage/common/storage-introduction.md)

Quando cria uma conta de análise, tem de designar uma origem de dados do Data Lake Store conta toobe Olá predefinido. Olá conta do Data Lake Store predefinida é utilizada registos de auditoria de metadados de tarefa toostore e tarefa. Depois de criar uma conta de Data Lake Analytics, pode adicionar mais contas de Data Lake Store e/ou as contas de armazenamento. 

### <a name="find-hello-default-data-lake-store-account"></a>Localizar a conta de Data Lake Store predefinida Olá

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Pode encontrar a conta de Data Lake Store predefinida Olá por filtrar a lista de Olá de origens de dados por Olá `IsDefault` propriedade:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Adicionar uma origem de dados

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Origens de dados de lista

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Submeter tarefas U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Submeter uma cadeia como um script U-SQL

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Submeter um ficheiro como um script U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Lista de tarefas numa conta

### <a name="list-all-hello-jobs-in-hello-account"></a>Liste todas as tarefas de Olá na conta de Olá. 

saída de Olá inclui Olá atualmente em execução de tarefas e essas tarefas que tenham sido concluído recentemente.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Lista de um número específico de tarefas

Por predefinição a lista de Olá de tarefas é ordenada submeter no tempo. Para que mais recentemente submetido Olá tarefas são apresentados primeiro. Por predefinição, Olá conta ADLA memorizou tarefas durante 180 dias, mas Olá Ge AdlJob cmdlet por predefinição devolve apenas Olá 500 primeiro. Utilize o - toolist parâmetro superior num número específico de tarefas.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Tarefas de lista com base no valor de Olá da propriedade de tarefa

Utilizar Olá `-State` parâmetro. Pode combinar qualquer um destes valores:

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

Olá utilize `-Result` parâmetro toodetect se terminada tarefas foi concluída com êxito. Tem estes valores:

* Foi cancelada
* Falha
* Nenhuma
* Bem-sucedido

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Olá `-Submitter` parâmetro ajuda-o a identificar quem submetida uma tarefa.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Olá `-SubmittedAfter` é útil em filtragem tooa intervalo de tempo.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Cenários comuns para listar as tarefas


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

## <a name="filtering-a-list-of-jobs"></a>Filtragem de uma lista de tarefas

Assim que tiver uma lista de tarefas na sua sessão atual do PowerShell. Pode utilizar normal lista de Olá do toofilter de cmdlets do PowerShell.

Filtro de uma lista de tarefas toohello tarefas submetidas no Olá últimas 24 horas

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filtrar uma lista de tarefas toohello tarefas que terminado em Olá últimas 24 horas

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filtre uma lista de tarefas de toohello de Tarefas iniciou a execução. Uma tarefa pode falhar no momento da compilação - e, por isso, nunca inicia. Vamos ver tarefas de Olá falhada que realmente começou a ser executada e, em seguida, falhou.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Analisar uma lista de tarefas

Olá utilize `Group-Object` cmdlet tooanalyze uma lista de tarefas.

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
Quando efetuar uma análise, pode ser útil tooadd propriedades toohello tarefa objetos toomake filtragem e mais simples de agrupamento. Olá fragmento a seguir mostra como tooannotate uma JobInfo com calculada propriedades.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Obter informações sobre pipelines e recurrences

Olá utilize `Get-AdlJobPipeline` informações de pipeline do cmdlet toosee Olá previamente submetido tarefas.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Olá utilize `Get-AdlJobRecurrence` cmdlet toosee Olá periodicidade as informações de tarefas anteriormente submetidas.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Obter informações sobre uma tarefa

### <a name="get-job-status"></a>Obter estado da tarefa

Obter o estado de Olá de uma tarefa específica.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Examine Olá saídas de tarefa

Depois de terminou a tarefa de Olá, verifique se o ficheiro de saída Olá existe por listar ficheiros Olá numa pasta.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Gerir tarefas em execução

### <a name="cancel-a-job"></a>Cancelar uma tarefa

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Aguarde um toofinish de tarefa

Em vez de repetir `Get-AdlAnalyticsJob` até que seja uma tarefa concluída, pode utilizar Olá `Wait-AdlJob` toowait de cmdlet para Olá tarefa tooend.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Gerir políticas de computação

### <a name="list-existing-compute-policies"></a>Lista as políticas existentes de computação

Olá `Get-AdlAnalyticsComputePolicy` cmdlet obtém informações sobre as políticas de computação para uma conta de Data Lake Analytics.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Criar uma política de computação

Olá `New-AdlAnalyticsComputePolicy` cmdlet cria uma nova política de computação para uma conta de Data Lake Analytics. Neste exemplo conjuntos Olá toohello disponível de AUs máximo especificado too50 de utilizador e Olá tarefa mínimo prioridade too250.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Verifique a existência de Olá de um ficheiro.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Carregar e transferir

Carregar um ficheiro.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Carregar um recursivamente pasta inteira.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Transferir um ficheiro.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Transferir um recursivamente pasta inteira.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Se hello carregar ou processo de transferência seja interrompido, pode tentar processo de Olá tooresume em execução Olá o cmdlet novamente com Olá ``-Resume`` sinalizador.

## <a name="manage-catalog-items"></a>Gerir itens de catálogo

o catálogo de Olá U-SQL é utilizado toostructure dados e o código para que possa ser partilhados por scripts U-SQL. catálogo de Olá permite Olá mais elevado desempenho possível com os dados no Azure Data Lake. Para obter mais informações, veja [Utilizar catálogo U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Itens de lista no catálogo de Olá U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Liste todas as assemblagens de Olá em todas as bases de dados de Olá numa conta ADLA.

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

### <a name="get-details-about-a-catalog-item"></a>Obter detalhes sobre um item de catálogo

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Criar as credenciais no catálogo

Dentro de uma base de dados do U-SQL, crie um objeto de credencial para uma base de dados alojado no Azure. Atualmente, as credenciais de U-SQL são tipo apenas de Olá de item de catálogo que pode criar através do PowerShell.

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

### <a name="get-basic-information-about-an-adla-account"></a>Obter informações básicas sobre uma conta ADLA

Olá seguinte código procura informações básicas sobre a conta de Olá fornecido um nome de conta

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

## <a name="working-with-azure"></a>Trabalhar com o Azure

### <a name="get-details-of-azurerm-errors"></a>Obter os detalhes de erros de AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Certifique-se de que se estiver a executar como administrador

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Localizar um TenantID

A partir de um nome de subscrição:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

A partir de um id de subscrição:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

De um endereço de domínio, como "contoso.com"


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Listar todas as subscrições e ids de inquilino

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Criar uma conta de Data Lake Analytics utilizando um modelo

Também pode utilizar um modelo de grupo de recursos do Azure utilizando Olá seguinte script do PowerShell:

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

Para obter mais informações, consulte [implementar uma aplicação com o modelo Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) e [modelos Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Modelo de exemplo**

Guardar Olá seguir texto como um `.json` de ficheiros e, em seguida, utilizar Olá precedente modelo de Olá de toouse de script do PowerShell. 

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

## <a name="next-steps"></a>Passos seguintes
* [Descrição geral do Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* Introdução ao Data Lake Analytics com [portal do Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Gerir o Azure Data Lake Analytics com [portal do Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 
