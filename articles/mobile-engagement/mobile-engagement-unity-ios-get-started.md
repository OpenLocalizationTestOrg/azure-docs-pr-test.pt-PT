---
title: "aaaGet iniciado com o Azure Mobile Engagement para implementação do Unity iOS"
description: "Saiba como toouse Azure Mobile Engagement com notificações Push e de análise para aplicações Unity tooiOS dispositivos."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Introdução ao Azure Mobile Engagement para implementação do Unity iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse Azure Mobile Engagement toounderstand a utilização da aplicação e como toosend push a utilizadores de toosegmented notificações de uma aplicação Unity quando implementar o dispositivo iOS tooan.
Este tutorial utiliza Olá clássico Unity Roll um tutorial Ball como Olá ponto de partida. Deve seguir os passos de Olá neste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar com Olá integração do Mobile Engagement que demonstramos no tutorial Olá abaixo. 

Este tutorial requer o seguinte Olá:

* [Unity Editor](http://unity3d.com/get-unity)
* [SDK Unity do Mobile Engagement](https://aka.ms/azmeunitysdk)
* XCode Editor

> [!NOTE]
> toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para a aplicação iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Ligar o back-end da aplicação toohello Mobile Engagement
### <a name="import-hello-unity-package"></a>Importar o pacote do Unity Olá
1. Transferir Olá [pacote Unity do Mobile Engagement](https://aka.ms/azmeunitysdk) e guarde-o computador local tooyour. 
2. Aceda demasiado**elementos -> Importar pacote -> pacote personalizado** e selecione Olá do pacote transferido no Olá passos acima. 
   
    ![][70] 
3. Certifique-se de que todos os ficheiros estão selecionados e clique no botão **Importar**. 
   
    ![][71] 
4. Assim que importar com êxito, verá os ficheiros do SDK de Olá importado no seu projeto.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Atualizar Olá EngagementConfiguration
1. Abra Olá **EngagementConfiguration** ficheiro de script de Olá de pasta e a atualização do SDK de Olá **IOS\_ligação\_cadeia** com a cadeia de ligação de Olá que obteve anteriormente de Olá portal do Azure.  
   
    ![][73]
2. Guarde o ficheiro de Olá. 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurar aplicação Olá para controlo básico
1. Abra Olá **PlayerController** script anexado toohello o objeto de leitor para edição. 
2. Adicione Olá seguinte utilizando a instrução:
   
        using Microsoft.Azure.Engagement.Unity;
3. Adicionar Olá seguir toohello `Start()` método
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implementar e executar a aplicação de Olá
1. Ligar uma máquina de tooyour do dispositivo iOS. 
2. Abra **Ficheiro -> Definições de Criação** 
   
    ![][40]
3. Selecione **iOS** e, em seguida, clique em **Alternar Plataforma**
   
    ![][41]
   
    ![][42]
4. Clique em **Definições de leitor** e faculte um Identificador de Pacote válido. 
   
    ![][53]
5. Finalmente, clique em **Criar e Executar**
   
    ![][54]
6. Poderá ser-lhe pedido tooprovide um pacote de iOS Olá de toostore de nome de pasta. 
   
    ![][43]
7. Se tudo correr bem, Olá projeto será compilado e deve abri-lo cópias de segurança na sua aplicação XCode. 
8. Certifique-se de que Olá **identificador de pacote** está correto no projeto Olá.  
   
    ![][75]
9. Agora, execute Olá aplicação no XCode para que o pacote de Olá é o dispositivo ligado tooyour implementado e deverá ver o seu jogo Unity no seu telemóvel! 

## <a id="monitor"></a>Ligar a aplicação com a monitorização em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Ativar as notificações push e mensagens na aplicação
O Mobile Engagement permite-lhe toointeract com os seus utilizadores e ao alcance com notificações push e mensagens no contexto de Olá das campanhas na aplicação. Este módulo é designado alcance no portal de Mobile Engagement Olá.
Toodo não tem qualquer configuração adicional na sua tooreceive notificações da aplicação e já está configurada para tal.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
