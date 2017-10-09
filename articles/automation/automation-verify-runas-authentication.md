---
title: "configuração de conta de automatização do Azure aaaValidate | Microsoft Docs"
description: "Este artigo descreve como configuração de Olá tooconfirm da sua conta de automatização está configurada corretamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="6e046-103">Testar a autenticação da conta Run As de Automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="6e046-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="6e046-104">Depois de uma conta de automatização é criada com êxito, pode realizar uma tooconfirm de teste simples poderá toosuccessfully autenticar no Azure Resource Manager ou implementação clássica do Azure com a conta Run As de automatização recentemente criada ou actualizada.</span><span class="sxs-lookup"><span data-stu-id="6e046-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="6e046-105">Autenticação Run As de Automatização</span><span class="sxs-lookup"><span data-stu-id="6e046-105">Automation Run As authentication</span></span>
<span data-ttu-id="6e046-106">Utilizar o código de exemplo de Olá abaixo demasiado[criar um runbook de PowerShell](automation-creating-importing-runbook.md) autenticação tooverify utilizando Olá executado como conta e também no seu tooauthenticate runbooks personalizados e gerir recursos do Resource Manager com a sua conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="6e046-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="6e046-107">Tenha em atenção Olá cmdlet utilizado para autenticar no runbook Olá - **Add-AzureRmAccount**, utiliza Olá *ServicePrincipalCertificate* conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="6e046-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="6e046-108">Autentica utilizando o certificado de serviço principal, não as credenciais.</span><span class="sxs-lookup"><span data-stu-id="6e046-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="6e046-109">Quando a [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate a conta Run As, um [tarefa de runbook](automation-runbook-execution.md) é criado, é apresentado o painel de tarefas Olá e estado da tarefa Olá apresentados na Olá **resumo da tarefa**mosaico.</span><span class="sxs-lookup"><span data-stu-id="6e046-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="6e046-110">Estado da tarefa Olá começará como *em fila* indicando que está a aguardar para um runbook worker no Olá toobecome de nuvem disponível.</span><span class="sxs-lookup"><span data-stu-id="6e046-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="6e046-111">Em seguida, irá mudar demasiado*inicial* quando uma função de trabalho tarefa Olá e, em seguida, *executar* quando runbook Olá, na verdade, entra em execução.</span><span class="sxs-lookup"><span data-stu-id="6e046-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="6e046-112">Quando tiver concluído a tarefa de runbook Olá, vemos um Estado de **concluído**.</span><span class="sxs-lookup"><span data-stu-id="6e046-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="6e046-113">toosee Olá resultados detalhados do runbook Olá, clique em Olá **saída** mosaico.</span><span class="sxs-lookup"><span data-stu-id="6e046-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="6e046-114">No Olá **saída** painel, deverá ver que foi autenticado com êxito e devolve uma lista de todos os recursos em todos os grupos de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="6e046-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="6e046-115">Esqueça bloco de Olá tooremove de código de carateres começadas comentários de Olá `#Get all ARM resources from all resource groups` quando reutilizar o código de Olá para os runbooks.</span><span class="sxs-lookup"><span data-stu-id="6e046-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="6e046-116">Autenticação Run As clássica</span><span class="sxs-lookup"><span data-stu-id="6e046-116">Classic Run As authentication</span></span>
<span data-ttu-id="6e046-117">Utilizar o código de exemplo de Olá abaixo demasiado[criar um runbook de PowerShell](automation-creating-importing-runbook.md) tooverify autenticação utilizando Olá clássico executado como conta e também no seu tooauthenticate runbooks personalizados e gerir recursos no modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="6e046-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="6e046-118">Quando a [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate a conta Run As, um [tarefa de runbook](automation-runbook-execution.md) é criado, é apresentado o painel de tarefas Olá e estado da tarefa Olá apresentados na Olá **resumo da tarefa**mosaico.</span><span class="sxs-lookup"><span data-stu-id="6e046-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="6e046-119">Estado da tarefa Olá começará como *em fila* indicando que está a aguardar para um runbook worker no Olá toobecome de nuvem disponível.</span><span class="sxs-lookup"><span data-stu-id="6e046-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="6e046-120">Em seguida, irá mudar demasiado*inicial* quando uma função de trabalho tarefa Olá e, em seguida, *executar* quando runbook Olá, na verdade, entra em execução.</span><span class="sxs-lookup"><span data-stu-id="6e046-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="6e046-121">Quando tiver concluído a tarefa de runbook Olá, vemos um Estado de **concluído**.</span><span class="sxs-lookup"><span data-stu-id="6e046-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="6e046-122">toosee Olá resultados detalhados do runbook Olá, clique em Olá **saída** mosaico.</span><span class="sxs-lookup"><span data-stu-id="6e046-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="6e046-123">No Olá **saída** painel, deverá ver que foi autenticado com êxito e devolve uma lista de todas as VMs do Azure por VMName que são implementadas na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="6e046-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="6e046-124">Esqueça tooremove Olá cmdlet **Get-AzureVM** quando reutilizar o código de Olá para os runbooks.</span><span class="sxs-lookup"><span data-stu-id="6e046-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e046-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6e046-125">Next steps</span></span>
* <span data-ttu-id="6e046-126">tooget iniciado com runbooks do PowerShell, consulte [o meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6e046-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="6e046-127">toolearn mais informações sobre a criação de gráficos, consulte [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6e046-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
