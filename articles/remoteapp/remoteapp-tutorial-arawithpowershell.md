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
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Utilizar cmdlets do Windows PowerShell com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

 Pode utilizar tooadminister de cmdlets do Azure RemoteApp PowerShell Olá e manter as coleções. Utilize Olá seguir tooget de informações foi iniciado.

## <a name="get-hello-cmdlets"></a>Obter Olá cmdlets
- - -
Transfira primeiro os cmdlets do Azure Powershell Olá [aqui](http://go.microsoft.com/?linkid=9811175), Olá RemoteApp cmdlets estão incluídos na mesma. 

Veja Olá [ajuda do cmdlet do Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Configurar a sua subscrição toouse de cmdlets do Azure
- - -
Siga [neste guia](/powershell/azure/overview) para poder utilizar os cmdlets de Olá contra a sua subscrição do Azure.

Pode utilizar estes tooget passos a trabalhar rapidamente:

1. Transfira e instale Olá [cmdlets Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Inicie o Microsoft Azure PowerShell.
3. Executar **Add-AzureAccount** tooauthenticate tooyour subscrição do Azure. Quando lhe for pedido, introduza Olá o mesmo nome de utilizador e palavra-passe que utilizam toosign no portal de tooAzure.  
4. Executar **Get-AzureSubscription** subscrições de Olá toolist associadas à sua conta de utilizador. 
5. Executar **Select-AzureSubscription - SubscriptionName &lt;nome da subscrição&gt;**  ou **Select-AzureSubscription - SubscriptionId &lt;ID de subscrição&gt;**  toospecify Olá subscrição toouse.

Parabéns, a consola do PowerShell do Azure está configurado e pronto toouse. Lembre-se de que precisa de toorepeate os passos 2 a 5 sempre que iniciar a consola do Olá Olá Azure PowerShell.  


## <a name="list-all-collections"></a>Lista todas as coleções
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Elimina uma coleção
- - -
    Remover AzureRemoteAppCollection<enter collection name>

Exemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Criar uma coleção na nuvem
- - -
É simple, execute Olá os seguintes comandos:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Olá acima comando publica automaticamente as aplicações do Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e o Word).

A criação de coleção pode demorar 30 minutos ou mais toocomplete. Por conseguinte, este comando devolve um ID de controlo que pode utilizar o seguinte:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Depois da conclusão da recolha de Olá, pode adicionar coleção toohello de utilizadores com Olá os seguintes comandos:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

E estiver pronto! Esse utilizador deve ser capaz de tooconnect toohello aplicação utilizando o cliente do Azure RemoteApp Olá encontrado [aqui](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Cmdlets disponíveis
Existem muitos outros comandos que temos, documentação de Olá para os mesmos estará disponível em breve:

Cmdlets de coleção do RemoteApp básicos: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Cmdlets de rede virtual do RemoteApp:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get - AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Cmdlets de imagem de modelo do RemoteApp:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Outros cmdlets do RemoteApp:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

