---
title: "aaaAzure baseado no Resource Manager PowerShell comandos para a aplicação Web do Azure | Microsoft Docs"
description: "Saiba como toouse Olá novo toomanage de comandos baseada no Azure Resource Manager PowerShell as Web Apps do Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="9f035-103">Utilizar Web Apps do Azure Azure Resource Manager-Based PowerShell tooManage</span><span class="sxs-lookup"><span data-stu-id="9f035-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f035-104">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9f035-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="9f035-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f035-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="9f035-106">Com o Microsoft Azure PowerShell versão 1.0.0 novos comandos foram adicionados, que dê Olá utilizador Olá capacidade toouse baseado no Azure Resource Manager PowerShell comandos toomanage Web Apps.</span><span class="sxs-lookup"><span data-stu-id="9f035-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="9f035-107">toolearn sobre a gestão de grupos de recursos, consulte [utilizar o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9f035-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="9f035-108">toolearn sobre a lista completa de Olá de parâmetros e as opções para Olá cmdlets do PowerShell, consulte Olá [completa referência de Cmdlet baseado no Gestor de recursos do Azure de aplicação Web de Cmdlets do PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="9f035-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="9f035-109">Planos de gestão do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="9f035-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="9f035-110">Criar um plano de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="9f035-110">Create an App Service Plan</span></span>
<span data-ttu-id="9f035-111">toocreate um plano do app service, utilizar Olá **New-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f035-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="9f035-112">Seguem-se as descrições dos parâmetros diferentes de Olá:</span><span class="sxs-lookup"><span data-stu-id="9f035-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="9f035-113">**Nome**: nome do plano de serviço de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="9f035-114">**Localização**: localização do plano de serviço.</span><span class="sxs-lookup"><span data-stu-id="9f035-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="9f035-115">**ResourceGroupName**: grupo de recursos que inclui o plano de serviço de aplicação Olá recentemente criado.</span><span class="sxs-lookup"><span data-stu-id="9f035-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="9f035-116">**Camada**: Olá pretendido escalão de preço (a predefinição é gratuito, outras opções são partilhados, básico, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="9f035-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="9f035-117">**WorkerSize**: Olá tamanho dos trabalhadores (a predefinição é pequena se foi especificado o parâmetro de camada de Olá como básica, Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="9f035-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="9f035-118">Outras opções são médio e grande.)</span><span class="sxs-lookup"><span data-stu-id="9f035-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="9f035-119">**NumberofWorkers**: Olá o número de funcionários no plano de serviço de aplicação Olá (o valor predefinido é 1).</span><span class="sxs-lookup"><span data-stu-id="9f035-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="9f035-120">Exemplo toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9f035-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="9f035-121">Criar um plano de serviço de aplicações num ambiente de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="9f035-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="9f035-122">Planear a um serviço de aplicações toocreate num ambiente de serviço de aplicações, utilize Olá mesmo comando **New-AzureRmAppServicePlan** comando com o nome de Olá de toospecify parâmetros extra da ASE e nome de grupo de recursos do ASE.</span><span class="sxs-lookup"><span data-stu-id="9f035-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="9f035-123">Exemplo toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9f035-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="9f035-124">mais informações sobre o ambiente de serviço de aplicações, verifique toolearn [introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="9f035-125">Lista os planos de serviço de aplicações existentes</span><span class="sxs-lookup"><span data-stu-id="9f035-125">List Existing App Service Plans</span></span>
<span data-ttu-id="9f035-126">toolist Olá existente aplicação planos de serviço, utilize **Get-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f035-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="9f035-127">toolist todos os planos de serviço de aplicações na sua subscrição, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="9f035-128">toolist todos os planos de serviço de aplicações num grupo de recurso específico, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="9f035-129">tooget um plano de serviço de aplicação específica, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="9f035-130">Configurar um existente plano do App Service</span><span class="sxs-lookup"><span data-stu-id="9f035-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="9f035-131">definições de Olá toochange para um plano de serviço de aplicação existente, utilize Olá **conjunto AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f035-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="9f035-132">Pode alterar o escalão de Olá, o tamanho de trabalho e o número de Olá dos trabalhadores</span><span class="sxs-lookup"><span data-stu-id="9f035-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="9f035-133">Um plano de serviço de aplicações de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9f035-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="9f035-134">tooscale um existente plano do App Service, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="9f035-135">Alterar o tamanho de trabalho de Olá de um plano do App Service</span><span class="sxs-lookup"><span data-stu-id="9f035-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="9f035-136">tamanho de Olá toochange dos funcionários de um existente plano do App Service, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="9f035-137">Alterar Olá camada de um plano do App Service</span><span class="sxs-lookup"><span data-stu-id="9f035-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="9f035-138">camada de Olá toochange de um existente plano do App Service, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="9f035-139">Eliminar uma existente plano do App Service</span><span class="sxs-lookup"><span data-stu-id="9f035-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="9f035-140">toodelete um plano de serviço de aplicação existente, todos os atribuído toobe da necessidade de aplicações web moveu ou eliminou primeiro.</span><span class="sxs-lookup"><span data-stu-id="9f035-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="9f035-141">Em seguida, utilizar Olá **remover AzureRmAppServicePlan** cmdlet pode eliminar o plano de serviço de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="9f035-142">Gestão de aplicações do serviço de aplicações Web</span><span class="sxs-lookup"><span data-stu-id="9f035-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="9f035-143">Criar uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="9f035-143">Create a Web App</span></span>
<span data-ttu-id="9f035-144">toocreate uma aplicação web, utilize Olá **New-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f035-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="9f035-145">Seguem-se as descrições dos parâmetros diferentes de Olá:</span><span class="sxs-lookup"><span data-stu-id="9f035-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="9f035-146">**Nome**: nome da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="9f035-147">**AppServicePlan**: nome para o plano de serviço Olá utilizado toohost Olá web app.</span><span class="sxs-lookup"><span data-stu-id="9f035-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="9f035-148">**ResourceGroupName**: grupo de recursos que aloja o plano de serviço de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="9f035-149">**Localização**: Olá localização da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="9f035-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="9f035-150">Exemplo toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9f035-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="9f035-151">Criar uma aplicação Web num ambiente de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="9f035-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="9f035-152">toocreate uma aplicação web de ambiente no serviço de aplicações (ASE).</span><span class="sxs-lookup"><span data-stu-id="9f035-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="9f035-153">Utilize Olá mesmo **New-AzureRmWebApp** comando com o nome de Olá ASE de toospecify de parâmetros adicionais e nome de grupo de recursos de Olá Olá ASE pertence.</span><span class="sxs-lookup"><span data-stu-id="9f035-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="9f035-154">mais informações sobre o ambiente de serviço de aplicações, verifique toolearn [introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="9f035-155">Eliminar uma aplicação Web existente</span><span class="sxs-lookup"><span data-stu-id="9f035-155">Delete an existing Web App</span></span>
<span data-ttu-id="9f035-156">toodelete uma aplicação web existente, pode utilizar Olá **remover AzureRmWebApp** cmdlet, precisará de nome de Olá toospecify da aplicação web de Olá e nome do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="9f035-157">Lista de aplicações Web existentes</span><span class="sxs-lookup"><span data-stu-id="9f035-157">List existing Web Apps</span></span>
<span data-ttu-id="9f035-158">toolist Olá existente aplicações web, utilize Olá **Get-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f035-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="9f035-159">toolist todas as aplicações web na sua subscrição, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="9f035-160">toolist todas as aplicações web num grupo de recurso específico, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="9f035-161">tooget uma aplicação web específico, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="9f035-162">Configurar uma aplicação Web existente</span><span class="sxs-lookup"><span data-stu-id="9f035-162">Configure an existing Web App</span></span>
<span data-ttu-id="9f035-163">definições de Olá toochange e configurações para uma aplicação web existente, utilize Olá **conjunto AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f035-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="9f035-164">Para obter uma lista completa de parâmetros, consulte Olá [ligação de referência de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="9f035-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="9f035-165">Exemplo (1): Utilize esta cadeias de ligação de toochange do cmdlet</span><span class="sxs-lookup"><span data-stu-id="9f035-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="9f035-166">Exemplo (2): Adicionar ou alterar as definições de aplicação</span><span class="sxs-lookup"><span data-stu-id="9f035-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="9f035-167">(3) exemplo: Definir Olá web app toorun no modo de 64 bits</span><span class="sxs-lookup"><span data-stu-id="9f035-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="9f035-168">Alterar o estado de Olá de uma aplicação Web existente</span><span class="sxs-lookup"><span data-stu-id="9f035-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="9f035-169">Reiniciar uma aplicação web</span><span class="sxs-lookup"><span data-stu-id="9f035-169">Restart a web app</span></span>
<span data-ttu-id="9f035-170">toorestart uma aplicação web, tem de especificar o grupo de recursos e nome de Olá da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="9f035-171">Parar uma aplicação web</span><span class="sxs-lookup"><span data-stu-id="9f035-171">Stop a web app</span></span>
<span data-ttu-id="9f035-172">toostop uma aplicação web, tem de especificar o grupo de recursos e nome de Olá da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="9f035-173">Iniciar uma aplicação web</span><span class="sxs-lookup"><span data-stu-id="9f035-173">Start a web app</span></span>
<span data-ttu-id="9f035-174">toostart uma aplicação web, tem de especificar o grupo de recursos e nome de Olá da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="9f035-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="9f035-175">Gerir perfis de publicação de aplicações Web</span><span class="sxs-lookup"><span data-stu-id="9f035-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="9f035-176">Cada aplicação web tem um perfil de publicação que pode ser utilizado toopublish as suas aplicações, podem ser executadas várias operações sobre a publicação de perfis.</span><span class="sxs-lookup"><span data-stu-id="9f035-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="9f035-177">Obter o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="9f035-177">Get Publishing Profile</span></span>
<span data-ttu-id="9f035-178">tooget Olá publicação perfil para uma aplicação web, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="9f035-179">Este comando echoes Olá publicação de linha de comandos de toohello de perfil, bem como saída Olá ficheiro de texto de tooa do perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="9f035-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="9f035-180">Repor o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="9f035-180">Reset Publishing Profile</span></span>
<span data-ttu-id="9f035-181">tooreset ambos Olá publicação palavra-passe para implementar o FTP e web para uma aplicação web, utilize:</span><span class="sxs-lookup"><span data-stu-id="9f035-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="9f035-182">Gerir certificados de aplicação Web</span><span class="sxs-lookup"><span data-stu-id="9f035-182">Manage Web App Certificates</span></span>
<span data-ttu-id="9f035-183">toolearn sobre como toomanage web certificados de aplicação, consulte [enlace de certificados SSL com o PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="9f035-184">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="9f035-184">Next Steps</span></span>
* <span data-ttu-id="9f035-185">toolearn sobre o suporte do Azure Resource Manager PowerShell, consulte [utilizar o Azure PowerShell com o Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="9f035-186">toolearn sobre ambientes do App Service, consulte [introdução tooApp ambiente de serviço.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="9f035-187">toolearn sobre como gerir certificados SSL do serviço de aplicações através do PowerShell, consulte [enlace de certificados SSL com o PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="9f035-188">toolearn sobre a lista completa de Olá baseado no Azure Resource Manager de cmdlets do PowerShell para Web Apps do Azure, consulte [referência de cmdlets do Azure Web Apps do Azure Resource Manager de Cmdlets do PowerShell.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="9f035-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="9f035-189">toolearn sobre a gestão de serviço de aplicações ao utilizar a CLI, consulte [Using Azure Resource Manager-Based XPlat CLI para a aplicação Web do Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9f035-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

