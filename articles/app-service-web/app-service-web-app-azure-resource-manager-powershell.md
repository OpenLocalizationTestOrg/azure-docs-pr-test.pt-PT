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
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Utilizar Web Apps do Azure Azure Resource Manager-Based PowerShell tooManage
> [!div class="op_single_selector"]
> * [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Com o Microsoft Azure PowerShell versão 1.0.0 novos comandos foram adicionados, que dê Olá utilizador Olá capacidade toouse baseado no Azure Resource Manager PowerShell comandos toomanage Web Apps.

toolearn sobre a gestão de grupos de recursos, consulte [utilizar o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md). 

toolearn sobre a lista completa de Olá de parâmetros e as opções para Olá cmdlets do PowerShell, consulte Olá [completa referência de Cmdlet baseado no Gestor de recursos do Azure de aplicação Web de Cmdlets do PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Planos de gestão do serviço de aplicações
### <a name="create-an-app-service-plan"></a>Criar um plano de serviço de aplicações
toocreate um plano do app service, utilizar Olá **New-AzureRmAppServicePlan** cmdlet.

Seguem-se as descrições dos parâmetros diferentes de Olá:

* **Nome**: nome do plano de serviço de aplicação Olá.
* **Localização**: localização do plano de serviço.
* **ResourceGroupName**: grupo de recursos que inclui o plano de serviço de aplicação Olá recentemente criado.
* **Camada**: Olá pretendido escalão de preço (a predefinição é gratuito, outras opções são partilhados, básico, Standard e Premium).
* **WorkerSize**: Olá tamanho dos trabalhadores (a predefinição é pequena se foi especificado o parâmetro de camada de Olá como básica, Standard ou Premium. Outras opções são médio e grande.)
* **NumberofWorkers**: Olá o número de funcionários no plano de serviço de aplicação Olá (o valor predefinido é 1). 

Exemplo toouse este cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Criar um plano de serviço de aplicações num ambiente de serviço de aplicações
Planear a um serviço de aplicações toocreate num ambiente de serviço de aplicações, utilize Olá mesmo comando **New-AzureRmAppServicePlan** comando com o nome de Olá de toospecify parâmetros extra da ASE e nome de grupo de recursos do ASE.

Exemplo toouse este cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

mais informações sobre o ambiente de serviço de aplicações, verifique toolearn [introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Lista os planos de serviço de aplicações existentes
toolist Olá existente aplicação planos de serviço, utilize **Get-AzureRmAppServicePlan** cmdlet.

toolist todos os planos de serviço de aplicações na sua subscrição, utilize: 

    Get-AzureRmAppServicePlan

toolist todos os planos de serviço de aplicações num grupo de recurso específico, utilize:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget um plano de serviço de aplicação específica, utilize:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Configurar um existente plano do App Service
definições de Olá toochange para um plano de serviço de aplicação existente, utilize Olá **conjunto AzureRmAppServicePlan** cmdlet. Pode alterar o escalão de Olá, o tamanho de trabalho e o número de Olá dos trabalhadores 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Um plano de serviço de aplicações de dimensionamento
tooscale um existente plano do App Service, utilize:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Alterar o tamanho de trabalho de Olá de um plano do App Service
tamanho de Olá toochange dos funcionários de um existente plano do App Service, utilize:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Alterar Olá camada de um plano do App Service
camada de Olá toochange de um existente plano do App Service, utilize:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Eliminar uma existente plano do App Service
toodelete um plano de serviço de aplicação existente, todos os atribuído toobe da necessidade de aplicações web moveu ou eliminou primeiro. Em seguida, utilizar Olá **remover AzureRmAppServicePlan** cmdlet pode eliminar o plano de serviço de aplicação Olá.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Gestão de aplicações do serviço de aplicações Web
### <a name="create-a-web-app"></a>Criar uma aplicação Web
toocreate uma aplicação web, utilize Olá **New-AzureRmWebApp** cmdlet.

Seguem-se as descrições dos parâmetros diferentes de Olá:

* **Nome**: nome da aplicação web de Olá.
* **AppServicePlan**: nome para o plano de serviço Olá utilizado toohost Olá web app.
* **ResourceGroupName**: grupo de recursos que aloja o plano de serviço de aplicação Olá.
* **Localização**: Olá localização da aplicação web.

Exemplo toouse este cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Criar uma aplicação Web num ambiente de serviço de aplicações
toocreate uma aplicação web de ambiente no serviço de aplicações (ASE). Utilize Olá mesmo **New-AzureRmWebApp** comando com o nome de Olá ASE de toospecify de parâmetros adicionais e nome de grupo de recursos de Olá Olá ASE pertence.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

mais informações sobre o ambiente de serviço de aplicações, verifique toolearn [introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Eliminar uma aplicação Web existente
toodelete uma aplicação web existente, pode utilizar Olá **remover AzureRmWebApp** cmdlet, precisará de nome de Olá toospecify da aplicação web de Olá e nome do grupo de recursos de Olá.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Lista de aplicações Web existentes
toolist Olá existente aplicações web, utilize Olá **Get-AzureRmWebApp** cmdlet.

toolist todas as aplicações web na sua subscrição, utilize:

    Get-AzureRmWebApp

toolist todas as aplicações web num grupo de recurso específico, utilize:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget uma aplicação web específico, utilize:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Configurar uma aplicação Web existente
definições de Olá toochange e configurações para uma aplicação web existente, utilize Olá **conjunto AzureRmWebApp** cmdlet. Para obter uma lista completa de parâmetros, consulte Olá [ligação de referência de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)

Exemplo (1): Utilize esta cadeias de ligação de toochange do cmdlet

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Exemplo (2): Adicionar ou alterar as definições de aplicação

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


(3) exemplo: Definir Olá web app toorun no modo de 64 bits

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Alterar o estado de Olá de uma aplicação Web existente
#### <a name="restart-a-web-app"></a>Reiniciar uma aplicação web
toorestart uma aplicação web, tem de especificar o grupo de recursos e nome de Olá da aplicação web de Olá.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Parar uma aplicação web
toostop uma aplicação web, tem de especificar o grupo de recursos e nome de Olá da aplicação web de Olá.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Iniciar uma aplicação web
toostart uma aplicação web, tem de especificar o grupo de recursos e nome de Olá da aplicação web de Olá.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Gerir perfis de publicação de aplicações Web
Cada aplicação web tem um perfil de publicação que pode ser utilizado toopublish as suas aplicações, podem ser executadas várias operações sobre a publicação de perfis.

#### <a name="get-publishing-profile"></a>Obter o perfil de publicação
tooget Olá publicação perfil para uma aplicação web, utilize:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Este comando echoes Olá publicação de linha de comandos de toohello de perfil, bem como saída Olá ficheiro de texto de tooa do perfil de publicação.

#### <a name="reset-publishing-profile"></a>Repor o perfil de publicação
tooreset ambos Olá publicação palavra-passe para implementar o FTP e web para uma aplicação web, utilize:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Gerir certificados de aplicação Web
toolearn sobre como toomanage web certificados de aplicação, consulte [enlace de certificados SSL com o PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Passos Seguintes
* toolearn sobre o suporte do Azure Resource Manager PowerShell, consulte [utilizar o Azure PowerShell com o Azure Resource Manager.](../powershell-azure-resource-manager.md)
* toolearn sobre ambientes do App Service, consulte [introdução tooApp ambiente de serviço.](app-service-app-service-environment-intro.md)
* toolearn sobre como gerir certificados SSL do serviço de aplicações através do PowerShell, consulte [enlace de certificados SSL com o PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn sobre a lista completa de Olá baseado no Azure Resource Manager de cmdlets do PowerShell para Web Apps do Azure, consulte [referência de cmdlets do Azure Web Apps do Azure Resource Manager de Cmdlets do PowerShell.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn sobre a gestão de serviço de aplicações ao utilizar a CLI, consulte [Using Azure Resource Manager-Based XPlat CLI para a aplicação Web do Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

