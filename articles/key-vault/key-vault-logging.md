---
title: Registo do Cofre de chave de aaaAzure | Microsoft Docs
description: "Utilize este tutorial toohelp começar com o Cofre de chaves do Azure registo."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="03cef-103">Registo do Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="03cef-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="03cef-104">O Cofre de Chaves do Azure chave está disponível na maior parte das regiões.</span><span class="sxs-lookup"><span data-stu-id="03cef-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="03cef-105">Para obter mais informações, consulte Olá [Cofre de chaves página de preços](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="03cef-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="03cef-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="03cef-106">Introduction</span></span>
<span data-ttu-id="03cef-107">Depois de criar um ou mais cofres de chaves, irá provavelmente pretender toomonitor como e quando a sua chave de cofres dos são acedidos e por quem.</span><span class="sxs-lookup"><span data-stu-id="03cef-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="03cef-108">Esta ação é possível ao ativar o registo do Cofre de Chaves, que guarda as informações numa conta de armazenamento do Azure que indicar.</span><span class="sxs-lookup"><span data-stu-id="03cef-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="03cef-109">É automaticamente criado um novo contentor designado **insights-logs-auditevent** na sua conta de armazenamento especificada, sendo que também pode utilizar essa mesma conta de armazenamento para recolher registos para vários cofres de chaves.</span><span class="sxs-lookup"><span data-stu-id="03cef-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="03cef-110">Pode aceder às suas informações de registo no máximo, 10 minutos após a chave de Olá operação do cofre.</span><span class="sxs-lookup"><span data-stu-id="03cef-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="03cef-111">Na maioria dos casos, o processo será ainda mais rápido.</span><span class="sxs-lookup"><span data-stu-id="03cef-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="03cef-112">Está a funcionar tooyou toomanage os seus registos na sua conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="03cef-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="03cef-113">Utilize toosecure de métodos de controlo de acesso do Azure standard os seus registos, restringindo quem pode aceder a eles.</span><span class="sxs-lookup"><span data-stu-id="03cef-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="03cef-114">Elimine registos que já não pretende que tookeep na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="03cef-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="03cef-115">Utilize este tutorial toohelp começar com o cofre do Azure chave de registo, toocreate a conta de armazenamento, ativar o registo e interpretar as informações de registo de Olá recolhidas.</span><span class="sxs-lookup"><span data-stu-id="03cef-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="03cef-116">Este tutorial não inclui instruções sobre como toocreate chave cofres, chaves ou segredos.</span><span class="sxs-lookup"><span data-stu-id="03cef-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="03cef-117">Para obter estas informações, consulte o artigo [Introdução ao Cofre de Chaves do Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="03cef-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="03cef-118">Ou, para obter instruções sobre a Interface de Linha de Comandos de várias plataformas, veja o [tutorial equivalente](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="03cef-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="03cef-119">Atualmente, não é possível configurar o Cofre de chaves do Azure no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03cef-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="03cef-120">Em alternativa, utilize estas instruções do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03cef-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="03cef-121">Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte o artigo [O que é o Cofre de Chaves do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="03cef-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03cef-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="03cef-122">Prerequisites</span></span>
<span data-ttu-id="03cef-123">toocomplete neste tutorial, tem de ter Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="03cef-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="03cef-124">Um cofre de chaves que tiver utilizado.</span><span class="sxs-lookup"><span data-stu-id="03cef-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="03cef-125">Azure PowerShell, **versão mínima 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="03cef-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="03cef-126">tooinstall Azure PowerShell e associá-lo à sua subscrição do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="03cef-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="03cef-127">Se já tiver instalado o Azure PowerShell e não souber a versão de Olá, a partir da consola do Azure PowerShell Olá, escreva `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="03cef-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="03cef-128">Armazenamento suficiente no Azure para os seus registos do Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="03cef-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="03cef-129"><a id="connect"></a>Ligar a subscrições tooyour</span><span class="sxs-lookup"><span data-stu-id="03cef-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="03cef-130">Iniciar uma sessão do Azure PowerShell e inicie sessão tooyour conta do Azure com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="03cef-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="03cef-131">Na janela de pop-up do browser de Olá, introduza o nome de utilizador da conta do Azure e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="03cef-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="03cef-132">Azure PowerShell irá obter todas as subscrições de Olá que estão associadas esta conta e, por predefinição, utiliza Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="03cef-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="03cef-133">Se tiver várias subscrições, poderá ter toospecify uma definição específica que foi utilizado toocreate seu Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="03cef-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="03cef-134">Escreva Olá subscrições de Olá toosee da sua conta os seguintes:</span><span class="sxs-lookup"><span data-stu-id="03cef-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="03cef-135">Em seguida, toospecify Olá subscrição associado ao seu Cofre de chaves que irá registar, tipo:</span><span class="sxs-lookup"><span data-stu-id="03cef-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="03cef-136">Isto é um passo importante e especialmente útil se tiver várias subscrições associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="03cef-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="03cef-137">Poderá receber um erro tooregister insights se este passo é ignorado.</span><span class="sxs-lookup"><span data-stu-id="03cef-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="03cef-138">Para obter mais informações sobre como configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="03cef-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="03cef-139"><a id="storage"></a>Criar uma nova conta de armazenamento para os seus registos</span><span class="sxs-lookup"><span data-stu-id="03cef-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="03cef-140">Apesar de poder utilizar uma conta de armazenamento existente para os seus registos, vamos criar uma nova conta de armazenamento que serão os registos do cofre tooKey dedicado.</span><span class="sxs-lookup"><span data-stu-id="03cef-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="03cef-141">Para sua comodidade que poderemos ter toospecify isto mais tarde, iremos guardar Olá detalhes numa variável designada **sa**.</span><span class="sxs-lookup"><span data-stu-id="03cef-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="03cef-142">Para facilitar ainda mais a gestão, também iremos utilizar Olá mesmo grupo de recursos como Olá que contém o nosso Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="03cef-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="03cef-143">De Olá [tutorial de introdução](key-vault-get-started.md), este grupo de recursos será designado **ContosoResourceGroup** e continuaremos toouse Olá Oriental como localização.</span><span class="sxs-lookup"><span data-stu-id="03cef-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="03cef-144">Substitua estes valores pelos seus próprios valores, conforme aplicável:</span><span class="sxs-lookup"><span data-stu-id="03cef-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="03cef-145">Se decidir toouse uma conta de armazenamento existente, tem de utilizar Olá mesma subscrição, como o seu Cofre de chaves e devem utilizar o modelo de implementação do Resource Manager Olá, em vez de modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="03cef-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="03cef-146"><a id="identify"></a>Identificar o Cofre de chaves Olá para os seus registos</span><span class="sxs-lookup"><span data-stu-id="03cef-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="03cef-147">No nosso tutorial de introdução, o nome do nosso Cofre de chaves era **ContosoKeyVault**, por isso, continuaremos toouse que atribua um nome e armazenar os detalhes de Olá numa variável designada **kv**:</span><span class="sxs-lookup"><span data-stu-id="03cef-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="03cef-148"><a id="enable"></a>Ativar registo</span><span class="sxs-lookup"><span data-stu-id="03cef-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="03cef-149">tooenable registo para o Cofre de chaves, iremos utilizar o cmdlet Olá Set-AzureRmDiagnosticSetting, juntamente com variáveis de Olá criadas para a nossa nova conta de armazenamento e o nosso Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="03cef-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="03cef-150">Também iremos definir Olá **-ativado** sinalizador demasiado**$true** e defina Olá categoria tooAuditEvent (Olá única categoria para o registo do Cofre de chaves):</span><span class="sxs-lookup"><span data-stu-id="03cef-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="03cef-151">Olá resultado inclui:</span><span class="sxs-lookup"><span data-stu-id="03cef-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="03cef-152">Isto confirma que o registo está agora ativado para o seu Cofre de chaves, guardar a conta de armazenamento de tooyour de informações.</span><span class="sxs-lookup"><span data-stu-id="03cef-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="03cef-153">Opcionalmente, pode também definir a política de retenção dos seus registos de forma a que os registos mais antigos sejam eliminados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="03cef-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="03cef-154">Por exemplo, definir a política de retenção utilizar **- RetentionEnabled** sinalizador demasiado**$true** e defina **- RetentionInDays** parâmetro demasiado**90** para Se os registos com mais de 90 dias serão automaticamente eliminados.</span><span class="sxs-lookup"><span data-stu-id="03cef-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="03cef-155">O que é registado:</span><span class="sxs-lookup"><span data-stu-id="03cef-155">What's logged:</span></span>

* <span data-ttu-id="03cef-156">Todos os pedidos de REST API autenticados são registados, o que inclui os pedidos falhados resultantes de erros de permissões de acesso, erros do sistema ou pedidos incorretos.</span><span class="sxs-lookup"><span data-stu-id="03cef-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="03cef-157">Operações na chave de Olá próprio, o que inclui a criação, eliminação, políticas de acesso do Cofre de chaves de definição, cofre e atualizar os atributos do Cofre de chaves, tais como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="03cef-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="03cef-158">Operações sobre chaves e segredos no Olá Cofre de chaves, que inclui a criação, modificação ou eliminação dessas chaves ou segredos; operações como assinar, verificar, encriptar, desencriptar, moldar e desenrolar chaves, obter segredos, listar e segredos e as respetivas versões.</span><span class="sxs-lookup"><span data-stu-id="03cef-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="03cef-159">Pedidos não autenticados que resultam numa resposta 401.</span><span class="sxs-lookup"><span data-stu-id="03cef-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="03cef-160">Por exemplo, pedidos que não têm um token de portador ou pedidos incorretamente formulados ou expirados ou com um token inválido.</span><span class="sxs-lookup"><span data-stu-id="03cef-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="03cef-161"><a id="access"></a>Aceder aos seus registos</span><span class="sxs-lookup"><span data-stu-id="03cef-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="03cef-162">Os registos do Cofre de chaves são armazenados na Olá **insights-logs-auditevent** contentor na conta de armazenamento de Olá que indicou.</span><span class="sxs-lookup"><span data-stu-id="03cef-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="03cef-163">toolist todos os blobs Olá neste contentor, escreva:</span><span class="sxs-lookup"><span data-stu-id="03cef-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="03cef-164">Em primeiro lugar, crie uma variável de nome do contentor Olá.</span><span class="sxs-lookup"><span data-stu-id="03cef-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="03cef-165">Este será utilizado ao longo do resto Olá Olá percurso através de.</span><span class="sxs-lookup"><span data-stu-id="03cef-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="03cef-166">toolist todos os blobs Olá neste contentor, escreva:</span><span class="sxs-lookup"><span data-stu-id="03cef-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="03cef-167">saída de Olá procurará toothis algo semelhante:</span><span class="sxs-lookup"><span data-stu-id="03cef-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="03cef-168">**Uri do contentor: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="03cef-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="03cef-169">**Nome**</span><span class="sxs-lookup"><span data-stu-id="03cef-169">**Name**</span></span>

- - -
<span data-ttu-id="03cef-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="03cef-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="03cef-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="03cef-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="03cef-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="03cef-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="03cef-173">Como pode neste resultado, os blobs de Olá seguem uma convenção de nomenclatura: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="03cef-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="03cef-174">valores de data e hora Olá utilizam o UTC.</span><span class="sxs-lookup"><span data-stu-id="03cef-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="03cef-175">Como hello mesma conta de armazenamento pode ser utilizados toocollect registos para vários recursos, hello ID de recurso completo no nome do blob Olá é tooaccess muito útil ou blobs de Olá apenas de transferência que precisa.</span><span class="sxs-lookup"><span data-stu-id="03cef-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="03cef-176">Mas antes de podermos fazer isso, teremos primeiro de saber como toodownload Olá todos os blobs.</span><span class="sxs-lookup"><span data-stu-id="03cef-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="03cef-177">Em primeiro lugar, crie um Olá de toodownload pasta blobs.</span><span class="sxs-lookup"><span data-stu-id="03cef-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="03cef-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="03cef-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="03cef-179">Em seguida, obtenha uma lista de todos os blobs:</span><span class="sxs-lookup"><span data-stu-id="03cef-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="03cef-180">Encaminhe esta lista através de blobs de Olá toodownload de 'Get-AzureStorageBlobContent' para a nossa pasta de destino:</span><span class="sxs-lookup"><span data-stu-id="03cef-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="03cef-181">Quando executar este segundo comando, Olá  **/**  delimitador dos nomes de blob Olá criar uma estrutura de pasta completa sob a pasta de destino Olá, e esta estrutura serão utilizados toodownload e arquivo Olá os blobs como ficheiros.</span><span class="sxs-lookup"><span data-stu-id="03cef-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="03cef-182">tooselectively transferir blobs, utilize carateres universais.</span><span class="sxs-lookup"><span data-stu-id="03cef-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="03cef-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="03cef-183">For example:</span></span>

* <span data-ttu-id="03cef-184">Se tiver vários cofres de chaves e pretender obter registos toodownload de apenas um cofre de chaves, designado CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="03cef-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="03cef-185">Se tiver vários grupos de recursos e pretende registos toodownload para apenas um grupo de recursos, utilize `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="03cef-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="03cef-186">Se quiser toodownload todos os registos de Olá mês Olá de Janeiro de 2016, utilize `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="03cef-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="03cef-187">Está agora pronto toostart observar o que está a ser Olá registos.</span><span class="sxs-lookup"><span data-stu-id="03cef-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="03cef-188">Mas antes dessa, dois parâmetros adicionais para que poderá ter tooknow Get-AzureRmDiagnosticSetting:</span><span class="sxs-lookup"><span data-stu-id="03cef-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="03cef-189">Estado de Olá tooquery das definições de diagnóstico para o seu recurso do Cofre de chaves:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="03cef-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="03cef-190">registo de toodisable para o recurso do Cofre de chaves:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="03cef-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="03cef-191"><a id="interpret"></a>Interpretar os registos do seu Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="03cef-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="03cef-192">Os blobs individuais são armazenadas como texto, formatados como um blob JSON.</span><span class="sxs-lookup"><span data-stu-id="03cef-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="03cef-193">Esta é uma entrada de registo de exemplo em execução `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="03cef-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="03cef-194">Olá tabela seguinte lista os nomes de campo Olá e descrições.</span><span class="sxs-lookup"><span data-stu-id="03cef-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="03cef-195">Nome do campo</span><span class="sxs-lookup"><span data-stu-id="03cef-195">Field name</span></span> | <span data-ttu-id="03cef-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="03cef-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03cef-197">hora</span><span class="sxs-lookup"><span data-stu-id="03cef-197">time</span></span> |<span data-ttu-id="03cef-198">Data e hora (UTC).</span><span class="sxs-lookup"><span data-stu-id="03cef-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="03cef-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="03cef-199">resourceId</span></span> |<span data-ttu-id="03cef-200">ID do Recurso do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03cef-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="03cef-201">Para os registos do Cofre de chaves, o que é sempre ID de recurso do Olá Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="03cef-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="03cef-202">operationName</span><span class="sxs-lookup"><span data-stu-id="03cef-202">operationName</span></span> |<span data-ttu-id="03cef-203">Nome da operação de Olá, conforme documentada na tabela seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="03cef-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="03cef-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="03cef-204">operationVersion</span></span> |<span data-ttu-id="03cef-205">Esta é a versão de REST API de Olá solicitada pelo cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="03cef-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="03cef-206">categoria</span><span class="sxs-lookup"><span data-stu-id="03cef-206">category</span></span> |<span data-ttu-id="03cef-207">Para os registos do Cofre de chaves, AuditEvent é Olá único valor disponível.</span><span class="sxs-lookup"><span data-stu-id="03cef-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="03cef-208">resultType</span><span class="sxs-lookup"><span data-stu-id="03cef-208">resultType</span></span> |<span data-ttu-id="03cef-209">Resultado do pedido de API REST.</span><span class="sxs-lookup"><span data-stu-id="03cef-209">Result of REST API request.</span></span> |
| <span data-ttu-id="03cef-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="03cef-210">resultSignature</span></span> |<span data-ttu-id="03cef-211">Estado de HTTP.</span><span class="sxs-lookup"><span data-stu-id="03cef-211">HTTP status.</span></span> |
| <span data-ttu-id="03cef-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="03cef-212">resultDescription</span></span> |<span data-ttu-id="03cef-213">Descrição adicional sobre o resultado de Olá, quando disponível.</span><span class="sxs-lookup"><span data-stu-id="03cef-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="03cef-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="03cef-214">durationMs</span></span> |<span data-ttu-id="03cef-215">Tempo que demorou pedido de REST API do tooservice Olá, em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="03cef-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="03cef-216">Não inclui latência de rede Olá, pelo que o tempo de Olá que medir do lado do cliente de Olá poderá não corresponder a este período de tempo.</span><span class="sxs-lookup"><span data-stu-id="03cef-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="03cef-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="03cef-217">callerIpAddress</span></span> |<span data-ttu-id="03cef-218">Endereço IP do cliente de Olá que efetuou o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="03cef-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="03cef-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="03cef-219">correlationId</span></span> |<span data-ttu-id="03cef-220">Um GUID opcional que hello do cliente pode passar toocorrelate registos do lado do cliente com os registos do lado do serviço (Cofre de chaves).</span><span class="sxs-lookup"><span data-stu-id="03cef-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="03cef-221">identidade</span><span class="sxs-lookup"><span data-stu-id="03cef-221">identity</span></span> |<span data-ttu-id="03cef-222">Identidade do token de Olá apresentado aquando do pedido de API de REST Olá.</span><span class="sxs-lookup"><span data-stu-id="03cef-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="03cef-223">Trata-se geralmente de um "utilizador", um "principal de serviço" ou uma combinação "utilizador + appId", como no caso de um pedido resultante de um cmdlet do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03cef-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="03cef-224">propriedades</span><span class="sxs-lookup"><span data-stu-id="03cef-224">properties</span></span> |<span data-ttu-id="03cef-225">Este campo irá conter diversas informações com base na operação de Olá (Oeprationname).</span><span class="sxs-lookup"><span data-stu-id="03cef-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="03cef-226">Na maioria dos casos, contém informações de cliente (Olá cadeia useragent transmitida pelo cliente de Olá), Olá URI exato de pedido de REST API e código de estado HTTP.</span><span class="sxs-lookup"><span data-stu-id="03cef-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="03cef-227">Além disso, quando um objeto é devolvido como resultado de um pedido (por exemplo, KeyCreate ou VaultGet), também irá conter Olá URI de chave (como "id"), o cofre do URI ou o segredo do URI.</span><span class="sxs-lookup"><span data-stu-id="03cef-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="03cef-228">Olá **operationName** valores dos campos estão no formato ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="03cef-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="03cef-229">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="03cef-229">For example:</span></span>

* <span data-ttu-id="03cef-230">Todas as operações do Cofre de chaves têm Olá ' cofre`<action>`' Formatar, tais como `VaultGet` e `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="03cef-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="03cef-231">Todas as operações de chaves têm Olá ' chave`<action>`' Formatar, tais como `KeySign` e `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="03cef-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="03cef-232">Todas as operações de segredo têm Olá ' segredo`<action>`' Formatar, tais como `SecretGet` e `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="03cef-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="03cef-233">Olá, a tabela seguinte lista o operationName Olá e comando REST API correspondente.</span><span class="sxs-lookup"><span data-stu-id="03cef-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="03cef-234">operationName</span><span class="sxs-lookup"><span data-stu-id="03cef-234">operationName</span></span> | <span data-ttu-id="03cef-235">Comando API REST</span><span class="sxs-lookup"><span data-stu-id="03cef-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="03cef-236">Autenticação</span><span class="sxs-lookup"><span data-stu-id="03cef-236">Authentication</span></span> |<span data-ttu-id="03cef-237">Através do ponto final do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03cef-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="03cef-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="03cef-238">VaultGet</span></span> |[<span data-ttu-id="03cef-239">Obter informações sobre um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="03cef-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="03cef-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="03cef-240">VaultPut</span></span> |[<span data-ttu-id="03cef-241">Criar ou atualizar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="03cef-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="03cef-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="03cef-242">VaultDelete</span></span> |[<span data-ttu-id="03cef-243">Eliminar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="03cef-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="03cef-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="03cef-244">VaultPatch</span></span> |[<span data-ttu-id="03cef-245">Atualizar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="03cef-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="03cef-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="03cef-246">VaultList</span></span> |[<span data-ttu-id="03cef-247">Lista todos os cofres de chaves num grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="03cef-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="03cef-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="03cef-248">KeyCreate</span></span> |[<span data-ttu-id="03cef-249">Criar uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="03cef-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="03cef-250">KeyGet</span></span> |[<span data-ttu-id="03cef-251">Obter informações sobre uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="03cef-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="03cef-252">KeyImport</span></span> |[<span data-ttu-id="03cef-253">Importar uma chave para um cofre</span><span class="sxs-lookup"><span data-stu-id="03cef-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="03cef-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="03cef-254">KeyBackup</span></span> |<span data-ttu-id="03cef-255">[Fazer uma cópia de segurança de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="03cef-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="03cef-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="03cef-256">KeyDelete</span></span> |[<span data-ttu-id="03cef-257">Eliminar uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="03cef-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="03cef-258">KeyRestore</span></span> |[<span data-ttu-id="03cef-259">Restaurar uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="03cef-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="03cef-260">KeySign</span></span> |[<span data-ttu-id="03cef-261">Assinar com uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="03cef-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="03cef-262">KeyVerify</span></span> |[<span data-ttu-id="03cef-263">Verificar com uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="03cef-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="03cef-264">KeyWrap</span></span> |[<span data-ttu-id="03cef-265">Moldar uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="03cef-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="03cef-266">KeyUnwrap</span></span> |[<span data-ttu-id="03cef-267">Desenrolar uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="03cef-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="03cef-268">KeyEncrypt</span></span> |[<span data-ttu-id="03cef-269">Encriptar com uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="03cef-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="03cef-270">KeyDecrypt</span></span> |[<span data-ttu-id="03cef-271">Desencriptar com uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="03cef-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="03cef-272">KeyUpdate</span></span> |[<span data-ttu-id="03cef-273">Atualizar uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="03cef-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="03cef-274">KeyList</span></span> |[<span data-ttu-id="03cef-275">Lista Olá chaves num cofre</span><span class="sxs-lookup"><span data-stu-id="03cef-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="03cef-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="03cef-276">KeyListVersions</span></span> |[<span data-ttu-id="03cef-277">Lista as versões de Olá de uma chave</span><span class="sxs-lookup"><span data-stu-id="03cef-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="03cef-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="03cef-278">SecretSet</span></span> |[<span data-ttu-id="03cef-279">Criar um segredo</span><span class="sxs-lookup"><span data-stu-id="03cef-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="03cef-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="03cef-280">SecretGet</span></span> |[<span data-ttu-id="03cef-281">Obter um segredo</span><span class="sxs-lookup"><span data-stu-id="03cef-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="03cef-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="03cef-282">SecretUpdate</span></span> |[<span data-ttu-id="03cef-283">Atualizar um segredo</span><span class="sxs-lookup"><span data-stu-id="03cef-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="03cef-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="03cef-284">SecretDelete</span></span> |[<span data-ttu-id="03cef-285">Eliminar um segredo</span><span class="sxs-lookup"><span data-stu-id="03cef-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="03cef-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="03cef-286">SecretList</span></span> |[<span data-ttu-id="03cef-287">Lista os segredos num cofre</span><span class="sxs-lookup"><span data-stu-id="03cef-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="03cef-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="03cef-288">SecretListVersions</span></span> |[<span data-ttu-id="03cef-289">Lista as versões de um segredo</span><span class="sxs-lookup"><span data-stu-id="03cef-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="03cef-290"><a id="loganalytics"></a>Utilizar o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="03cef-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="03cef-291">Pode utilizar solução Cofre de chaves do Azure de Olá tooreview de análise de registos do Azure chave de cofre AuditEvent registos.</span><span class="sxs-lookup"><span data-stu-id="03cef-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="03cef-292">Para obter mais informações, incluindo como tooset esta cópia de segurança, consulte [solução Cofre de chaves do Azure na análise de registos](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="03cef-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="03cef-293">Este artigo também contém instruções se precisar de toomigrate da solução Cofre de chaves antiga Olá que foi fornecida durante a pré-visualização de análise de registos de Olá, onde primeiro encaminhados sua tooan registos de conta de armazenamento do Azure e configurado tooread de análise de registos a partir daí.</span><span class="sxs-lookup"><span data-stu-id="03cef-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="03cef-294"><a id="next"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="03cef-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="03cef-295">Para um tutorial que utiliza o Cofre de Chaves do Azure numa aplicação Web, consulte o artigo [Utilizar o Cofre de Chaves do Azure a partir de uma Aplicação Web](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="03cef-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="03cef-296">Para as referências de programação, consulte [Olá guia para programadores do Cofre de chaves do Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="03cef-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="03cef-297">Para obter uma lista dos cmdlets do Azure PowerShell 1.0 para o Cofre de Chaves do Azure, consulte o artigo [Cmdlets do Cofre de Chaves do Azure](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="03cef-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="03cef-298">Para um tutorial de rotação da chave e auditoria do registo com o Cofre de chaves do Azure, consulte [como toosetup Cofre de chaves com final tooend chave auditoria e rotação](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="03cef-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
