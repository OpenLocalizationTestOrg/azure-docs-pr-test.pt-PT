---
title: aaaMonitor e gerir tarefas do Stream Analytics com o PowerShell | Microsoft Docs
description: Saiba como toouse Azure PowerShell e cmdlets toomonitor e gerir tarefas do Stream Analytics.
keywords: o Azure powershell, o cmdlets do powershell do azure, o comando do powershell, scripts do powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="9a4a7-104">Monitorizar e gerir tarefas do Stream Analytics com cmdlets do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="9a4a7-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="9a4a7-105">Saiba como toomonitor e gerir os recursos de Stream Analytics com cmdlets do Azure PowerShell e scripts do powershell que executar tarefas do Stream Analytics básicas.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="9a4a7-106">Pré-requisitos para executar cmdlets do Azure PowerShell para o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="9a4a7-107">Crie um grupo de recursos do Azure na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="9a4a7-108">Olá segue-se um exemplo de script do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="9a4a7-109">Para obter informações do Azure PowerShell, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="9a4a7-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="9a4a7-110">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="9a4a7-111">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="9a4a7-112">Tarefas do Stream Analytics criadas através de programação não dispõe de monitorização ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="9a4a7-113">Pode ativar manualmente a monitorização em Olá Portal do Azure, aceda a página de Monitor da tarefa toohello e clicar no botão Ativar de Olá ou pode fazê-lo através de programação, seguindo os passos de Olá localizados em [Azure Stream Analytics - sequência de Monitor Análise de tarefas X509securitytokenparameters](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="9a4a7-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="9a4a7-114">Cmdlets do PowerShell do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="9a4a7-115">Olá, os seguintes cmdlets do Azure PowerShell pode ser utilizado toomonitor e gerir tarefas do Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="9a4a7-116">Tenha em atenção que o Azure PowerShell tem versões diferentes.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="9a4a7-117">**Nos exemplos de Olá é primeiro comando de Olá listados para o Azure PowerShell 0.9.8, o segundo comando de Olá é para o Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="9a4a7-118">comandos de Olá Azure PowerShell 1.0 terão sempre no comando Olá "AzureRM".</span><span class="sxs-lookup"><span data-stu-id="9a4a7-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="9a4a7-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9a4a7-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9a4a7-120">Apresenta uma lista de todas as tarefas do Stream Analytics definidas num Olá subscrição do Azure ou o grupo de recursos especificado ou obtém as informações da tarefa sobre uma tarefa específica dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="9a4a7-121">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-121">**Example 1**</span></span>

<span data-ttu-id="9a4a7-122">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="9a4a7-123">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="9a4a7-124">Este comando PowerShell devolve informações sobre todas as tarefas do Stream Analytics Olá Olá subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="9a4a7-125">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-125">**Example 2**</span></span>

<span data-ttu-id="9a4a7-126">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="9a4a7-127">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="9a4a7-128">Este comando PowerShell devolve informações sobre todas as tarefas do Stream Analytics Olá no grupo de recursos de Olá StreamAnalytics-predefinição-Central-US.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="9a4a7-129">**Exemplo 3**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-129">**Example 3**</span></span>

<span data-ttu-id="9a4a7-130">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="9a4a7-131">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="9a4a7-132">Este comando PowerShell devolve informações sobre a tarefa de Stream Analytics Olá StreamingJob no grupo de recursos de Olá StreamAnalytics-predefinição-Central-US.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="9a4a7-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9a4a7-134">Apresenta uma lista de todas as entradas de Olá que são definidas numa tarefa do Stream Analytics especificada ou obtém informações sobre uma entrada específica.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="9a4a7-135">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-135">**Example 1**</span></span>

<span data-ttu-id="9a4a7-136">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9a4a7-137">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9a4a7-138">Este comando PowerShell devolve informações sobre todas as entradas de Olá definidos na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="9a4a7-139">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-139">**Example 2**</span></span>

<span data-ttu-id="9a4a7-140">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="9a4a7-141">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="9a4a7-142">Este comando PowerShell devolve informações sobre a entrada de Olá denominada EntryStream definido na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="9a4a7-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9a4a7-144">Apresenta uma lista de todas as saídas de Olá que são definidas numa tarefa do Stream Analytics especificada ou obtém informações sobre uma saída específica.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="9a4a7-145">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-145">**Example 1**</span></span>

<span data-ttu-id="9a4a7-146">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9a4a7-147">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9a4a7-148">Este comando PowerShell devolve informações sobre as saídas de Olá definidos na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="9a4a7-149">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-149">**Example 2**</span></span>

<span data-ttu-id="9a4a7-150">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="9a4a7-151">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="9a4a7-152">Este comando PowerShell devolve informações sobre a saída de Olá com o nome de saída definida na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="9a4a7-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="9a4a7-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="9a4a7-154">Obtém informações sobre a quota de Olá de transmissão em fluxo unidades numa região especificada.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="9a4a7-155">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-155">**Example 1**</span></span>

<span data-ttu-id="9a4a7-156">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="9a4a7-157">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="9a4a7-158">Este comando PowerShell devolve informações sobre a quota de Olá e a utilização de unidades de transmissão em fluxo na região de EUA Central Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="9a4a7-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="9a4a7-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="9a4a7-160">Obtém informações sobre uma transformação específica definida numa tarefa de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="9a4a7-161">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-161">**Example 1**</span></span>

<span data-ttu-id="9a4a7-162">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="9a4a7-163">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="9a4a7-164">Este comando PowerShell devolve informações sobre a transformação Olá chamada StreamingJob na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="9a4a7-165">Novo AzureStreamAnalyticsInput | Novo AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9a4a7-166">Cria uma nova entrada dentro de uma tarefa de Stream Analytics ou atualiza uma entrada existente especificada.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="9a4a7-167">Olá nome da entrada de Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="9a4a7-168">Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="9a4a7-169">Se especificar uma entrada que já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá perguntar se pretende ou não tooreplace Olá entrada existente.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="9a4a7-170">Se especificar Olá – parâmetro Force e especifique existente introduzir o nome, será substituída Olá entrada sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="9a4a7-171">Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [entrada criar (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] secção Olá [API de REST de gestão do Stream Analytics Biblioteca de referência][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9a4a7-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9a4a7-172">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-172">**Example 1**</span></span>

<span data-ttu-id="9a4a7-173">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="9a4a7-174">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="9a4a7-175">Este comando PowerShell cria uma nova entrada de ficheiro Olá Input.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="9a4a7-176">Se já está definida uma entrada existente com o nome de Olá especificado no ficheiro de definição de entrada de Olá, Olá cmdlet irá perguntar se pretende ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="9a4a7-177">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-177">**Example 2**</span></span>

<span data-ttu-id="9a4a7-178">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="9a4a7-179">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="9a4a7-180">Este comando PowerShell cria uma nova entrada na tarefa de Olá chamada EntryStream.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="9a4a7-181">Se uma entrada existente com este nome já está definida, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="9a4a7-182">**Exemplo 3**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-182">**Example 3**</span></span>

<span data-ttu-id="9a4a7-183">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="9a4a7-184">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="9a4a7-185">Este comando PowerShell substitui a definição de Olá Olá existente de origens de entrada chamada EntryStream com a definição do ficheiro de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="9a4a7-186">Novo AzureStreamAnalyticsJob | Novo AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9a4a7-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9a4a7-187">Cria uma nova tarefa de Stream Analytics no Microsoft Azure ou de atualizações de definição de Olá de uma tarefa especificada existente.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="9a4a7-188">nome de Olá da tarefa de Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="9a4a7-189">Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="9a4a7-190">Se especificar um nome de tarefa já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá perguntar se pretende ou não tooreplace Olá tarefa existente.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="9a4a7-191">Se especificar Olá – parâmetro Force e especifique um nome de tarefa existente, definição de tarefa Olá será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="9a4a7-192">Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [criar tarefa do Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] secção Olá [referência de API do REST de gestão do Stream Analytics Biblioteca][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9a4a7-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9a4a7-193">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-193">**Example 1**</span></span>

<span data-ttu-id="9a4a7-194">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="9a4a7-195">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="9a4a7-196">Este comando PowerShell cria uma nova tarefa da definição de Olá no JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="9a4a7-197">Se uma tarefa existente com o nome de Olá especificado no ficheiro de definição de tarefa Olá já está definida, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="9a4a7-198">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-198">**Example 2**</span></span>

<span data-ttu-id="9a4a7-199">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="9a4a7-200">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="9a4a7-201">Este comando PowerShell substitui a definição de tarefa Olá para StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="9a4a7-202">Novo AzureStreamAnalyticsOutput | Novo AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9a4a7-203">Cria uma saída de novo dentro de uma tarefa de Stream Analytics ou atualiza uma saída existente.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="9a4a7-204">nome de Olá da saída de Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="9a4a7-205">Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="9a4a7-206">Se especificar um resultado que já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá pedir-se ou não tooreplace Olá saída existente.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="9a4a7-207">Se especificar Olá – parâmetro Force e especifique o nome de saída de um existente, saída Olá será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="9a4a7-208">Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [saída criar (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] secção Olá [API de REST de gestão do Stream Analytics Biblioteca de referência][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9a4a7-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9a4a7-209">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-209">**Example 1**</span></span>

<span data-ttu-id="9a4a7-210">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="9a4a7-211">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="9a4a7-212">Este comando PowerShell cria uma nova saída chamada de "saída" na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="9a4a7-213">Se uma saída existente com este nome já está definida, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="9a4a7-214">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-214">**Example 2**</span></span>

<span data-ttu-id="9a4a7-215">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="9a4a7-216">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="9a4a7-217">Este comando PowerShell substitui a definição de Olá de "saída" na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="9a4a7-218">Novo AzureStreamAnalyticsTransformation | Novo AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="9a4a7-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="9a4a7-219">Cria uma transformação de novo dentro de uma tarefa de Stream Analytics ou atualiza a transformação existente Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="9a4a7-220">nome de Olá da transformação Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="9a4a7-221">Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="9a4a7-222">Se especificar uma transformação que já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá pedir-se ou não tooreplace Olá transformação existente.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="9a4a7-223">Se especificar Olá – parâmetro Force e especifique um nome de transformação existente será substituída transformação Olá sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="9a4a7-224">Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [criar transformação (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] secção Olá [Stream Analytics Management Biblioteca de referência de API de REST][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9a4a7-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9a4a7-225">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-225">**Example 1**</span></span>

<span data-ttu-id="9a4a7-226">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="9a4a7-227">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="9a4a7-228">Este comando PowerShell cria uma nova transformação chamada StreamingJobTransform na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="9a4a7-229">Se uma transformação existente já está definida com este nome, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="9a4a7-230">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-230">**Example 2**</span></span>

<span data-ttu-id="9a4a7-231">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="9a4a7-232">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="9a4a7-233">Este comando PowerShell substitui a definição de Olá de StreamingJobTransform na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="9a4a7-234">Remover AzureStreamAnalyticsInput | Remover AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9a4a7-235">No modo assíncrono elimina uma entrada específica de uma tarefa de Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="9a4a7-236">Se especificar hello – parâmetro Force, Olá entrada será eliminado sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="9a4a7-237">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-237">**Example 1**</span></span>

<span data-ttu-id="9a4a7-238">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="9a4a7-239">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="9a4a7-240">Este comando PowerShell remove Olá EventStream entrada na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="9a4a7-241">Remover AzureStreamAnalyticsJob | Remover AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9a4a7-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9a4a7-242">No modo assíncrono elimina uma tarefa de Stream Analytics específica no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="9a4a7-243">Se especificar hello – parâmetro Force, Olá tarefa irá ser eliminado sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="9a4a7-244">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-244">**Example 1**</span></span>

<span data-ttu-id="9a4a7-245">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9a4a7-246">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9a4a7-247">Este comando PowerShell remove tarefa Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="9a4a7-248">Remover AzureStreamAnalyticsOutput | Remover AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9a4a7-249">No modo assíncrono elimina uma saída específica de uma tarefa de Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="9a4a7-250">Se especificar hello – parâmetro Force, Olá resultado será eliminado sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="9a4a7-251">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-251">**Example 1**</span></span>

<span data-ttu-id="9a4a7-252">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9a4a7-253">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9a4a7-254">Este Olá de remove de comando do PowerShell de saída do resultado na tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="9a4a7-255">Início AzureStreamAnalyticsJob | Início AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9a4a7-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9a4a7-256">No modo assíncrono implementa e inicia uma tarefa de Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="9a4a7-257">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-257">**Example 1**</span></span>

<span data-ttu-id="9a4a7-258">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="9a4a7-259">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="9a4a7-260">Este comando PowerShell inicia Olá tarefa StreamingJob com uma hora de início de saída personalizado Definir tooDecember 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="9a4a7-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9a4a7-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9a4a7-262">No modo assíncrono para uma tarefa de Stream Analytics sejam executadas no Microsoft Azure e anula a alocação recursos que foram que estavam a ser utilizados.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="9a4a7-263">Olá definição de tarefa e metadados permanecerá disponíveis na sua subscrição através de Olá portal do Azure e APIs, de gestão de forma a que hello tarefa pode ser editada e reiniciada.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="9a4a7-264">Não será cobrada para uma tarefa no estado de Olá parado.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="9a4a7-265">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-265">**Example 1**</span></span>

<span data-ttu-id="9a4a7-266">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9a4a7-267">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9a4a7-268">Este comando do PowerShell para a tarefa de Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="9a4a7-269">Teste AzureStreamAnalyticsInput | Teste AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9a4a7-270">Capacidade de Olá testes do Stream Analytics tooconnect tooa especificada entrada.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="9a4a7-271">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-271">**Example 1**</span></span>

<span data-ttu-id="9a4a7-272">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="9a4a7-273">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="9a4a7-274">Este estado de ligação de Olá de testes de comando do PowerShell da Olá EntryStream no StreamingJob de entrada.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="9a4a7-275">Teste AzureStreamAnalyticsOutput | Teste AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9a4a7-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9a4a7-276">Capacidade de Olá testes do Stream Analytics tooconnect tooa especificado saída.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="9a4a7-277">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9a4a7-277">**Example 1**</span></span>

<span data-ttu-id="9a4a7-278">O Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9a4a7-279">O Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9a4a7-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9a4a7-280">Este estado de ligação de Olá de testes de comando do PowerShell da Olá saída no StreamingJob de saída.</span><span class="sxs-lookup"><span data-stu-id="9a4a7-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="9a4a7-281">Obter suporte</span><span class="sxs-lookup"><span data-stu-id="9a4a7-281">Get support</span></span>
<span data-ttu-id="9a4a7-282">Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="9a4a7-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9a4a7-283">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a4a7-283">Next steps</span></span>
* [<span data-ttu-id="9a4a7-284">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9a4a7-285">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9a4a7-286">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9a4a7-287">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9a4a7-288">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9a4a7-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

