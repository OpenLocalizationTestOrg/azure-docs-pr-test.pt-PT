---
title: aaaUse cmdlets do PowerShell com o Azure RemoteApp | Microsoft Docs
description: Saiba como toouse cmdlets do Windows PowerShell no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="1a50b-103">Utilizar cmdlets do Windows PowerShell com o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1a50b-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a50b-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="1a50b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1a50b-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1a50b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="1a50b-106">Pode utilizar tooadminister de cmdlets do Azure RemoteApp PowerShell Olá e manter as coleções.</span><span class="sxs-lookup"><span data-stu-id="1a50b-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="1a50b-107">Utilize Olá seguir tooget de informações foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="1a50b-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="1a50b-108">Obter Olá cmdlets</span><span class="sxs-lookup"><span data-stu-id="1a50b-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="1a50b-109">Transfira primeiro os cmdlets do Azure Powershell Olá [aqui](http://go.microsoft.com/?linkid=9811175), Olá RemoteApp cmdlets estão incluídos na mesma.</span><span class="sxs-lookup"><span data-stu-id="1a50b-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="1a50b-110">Veja Olá [ajuda do cmdlet do Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="1a50b-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="1a50b-111">Configurar a sua subscrição toouse de cmdlets do Azure</span><span class="sxs-lookup"><span data-stu-id="1a50b-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="1a50b-112">Siga [neste guia](/powershell/azure/overview) para poder utilizar os cmdlets de Olá contra a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a50b-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="1a50b-113">Pode utilizar estes tooget passos a trabalhar rapidamente:</span><span class="sxs-lookup"><span data-stu-id="1a50b-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="1a50b-114">Transfira e instale Olá [cmdlets Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="1a50b-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="1a50b-115">Inicie o Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a50b-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="1a50b-116">Executar **Add-AzureAccount** tooauthenticate tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a50b-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="1a50b-117">Quando lhe for pedido, introduza Olá o mesmo nome de utilizador e palavra-passe que utilizam toosign no portal de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1a50b-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="1a50b-118">Executar **Get-AzureSubscription** subscrições de Olá toolist associadas à sua conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="1a50b-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="1a50b-119">Executar **Select-AzureSubscription - SubscriptionName &lt;nome da subscrição&gt;**  ou **Select-AzureSubscription - SubscriptionId &lt;ID de subscrição&gt;**  toospecify Olá subscrição toouse.</span><span class="sxs-lookup"><span data-stu-id="1a50b-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="1a50b-120">Parabéns, a consola do PowerShell do Azure está configurado e pronto toouse.</span><span class="sxs-lookup"><span data-stu-id="1a50b-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="1a50b-121">Lembre-se de que precisa de toorepeate os passos 2 a 5 sempre que iniciar a consola do Olá Olá Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a50b-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="1a50b-122">Lista todas as coleções</span><span class="sxs-lookup"><span data-stu-id="1a50b-122">List all collections</span></span>
- - -
     <span data-ttu-id="1a50b-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1a50b-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="1a50b-124">Elimina uma coleção</span><span class="sxs-lookup"><span data-stu-id="1a50b-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="1a50b-125">Remover AzureRemoteAppCollection<enter collection name></span><span class="sxs-lookup"><span data-stu-id="1a50b-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="1a50b-126">Exemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="1a50b-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="1a50b-127">Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="1a50b-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="1a50b-128">É simple, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1a50b-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="1a50b-129">Olá acima comando publica automaticamente as aplicações do Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e o Word).</span><span class="sxs-lookup"><span data-stu-id="1a50b-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="1a50b-130">A criação de coleção pode demorar 30 minutos ou mais toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1a50b-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="1a50b-131">Por conseguinte, este comando devolve um ID de controlo que pode utilizar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1a50b-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="1a50b-132">Depois da conclusão da recolha de Olá, pode adicionar coleção toohello de utilizadores com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1a50b-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="1a50b-133">E estiver pronto!</span><span class="sxs-lookup"><span data-stu-id="1a50b-133">And you're done!</span></span> <span data-ttu-id="1a50b-134">Esse utilizador deve ser capaz de tooconnect toohello aplicação utilizando o cliente do Azure RemoteApp Olá encontrado [aqui](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1a50b-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="1a50b-135">Cmdlets disponíveis</span><span class="sxs-lookup"><span data-stu-id="1a50b-135">Available cmdlets</span></span>
<span data-ttu-id="1a50b-136">Existem muitos outros comandos que temos, documentação de Olá para os mesmos estará disponível em breve:</span><span class="sxs-lookup"><span data-stu-id="1a50b-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="1a50b-137">Cmdlets de coleção do RemoteApp básicos:</span><span class="sxs-lookup"><span data-stu-id="1a50b-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="1a50b-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1a50b-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1a50b-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1a50b-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1a50b-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1a50b-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1a50b-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1a50b-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1a50b-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1a50b-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1a50b-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1a50b-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1a50b-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1a50b-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1a50b-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1a50b-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1a50b-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="1a50b-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="1a50b-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="1a50b-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="1a50b-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="1a50b-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="1a50b-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="1a50b-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="1a50b-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1a50b-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1a50b-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="1a50b-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="1a50b-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1a50b-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1a50b-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1a50b-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1a50b-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="1a50b-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="1a50b-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="1a50b-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="1a50b-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="1a50b-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="1a50b-157">Cmdlets de rede virtual do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="1a50b-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="1a50b-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1a50b-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1a50b-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1a50b-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1a50b-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1a50b-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1a50b-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1a50b-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1a50b-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="1a50b-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="1a50b-163">Get - AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="1a50b-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="1a50b-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="1a50b-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="1a50b-165">Cmdlets de imagem de modelo do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="1a50b-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="1a50b-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1a50b-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1a50b-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1a50b-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1a50b-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1a50b-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1a50b-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1a50b-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="1a50b-170">Outros cmdlets do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="1a50b-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="1a50b-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="1a50b-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="1a50b-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="1a50b-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="1a50b-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="1a50b-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="1a50b-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="1a50b-174">Get-AzureRemoteAppOperationResult</span></span>

