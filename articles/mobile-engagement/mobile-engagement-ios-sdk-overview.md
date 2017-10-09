---
title: "aaaAzure descrição geral do SDK do iOS do Mobile Engagement | Microsoft Docs"
description: "Mais recentes atualizações e procedimentos para o SDK do iOS do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>SDK do iOS do Azure Mobile Engagement
Comece por aqui tooget todos os detalhes de Olá sobre toointegrate Azure Mobile Engagement numa aplicação iOS. Se quiser toogive, tente novamente em primeiro lugar, certifique-se de que fazer nosso [tutorial de 15 minutos](mobile-engagement-ios-get-started.md).

Clique em toosee Olá [SDK conteúdo](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Procedimentos de integração
1. Comece por aqui: [como toointegrate Mobile Engagement na sua aplicação iOS](mobile-engagement-ios-integrate-engagement.md)
2. Para obter notificações: [como toointegrate alcance (notificações) na sua aplicação iOS](mobile-engagement-ios-integrate-engagement-reach.md)
3. Implementação do plano de etiqueta: [como toouse Olá avançadas etiquetagem API na sua aplicação iOS do Mobile Engagement](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Notas de versão
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Destaques fixos limpo em segundo plano.
* Avisos fixos no XCode 9 sobre APIs não chamadas na fila principal.
* Fixo uma fuga de memória em inquéritos de alcance.
* Remover o suporte para iOS 6. x. A partir de destino da implementação Olá esta versão da aplicação tem de ser, pelo menos, o iOS 7.

Para versão anterior, consulte Olá [concluir notas de versão](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimentos de atualização
Se já tiver integrado uma versão antiga do Engagement na sua aplicação, terá de Olá tooconsider seguintes pontos ao atualizar Olá SDK.

Poderá ter toofollow vários procedimentos se omitido várias versões do Olá SDK Consulte Olá concluída [atualizar procedimentos](mobile-engagement-ios-upgrade-procedure.md).

Para cada versão nova do SDK de Olá tem de substituir primeiro (remover e voltar a importar no xcode) Olá pastas EngagementSDK e EngagementReach.

### <a name="from-300-too400"></a>De 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 é obrigatório iniciados a partir da versão 4.0.0 de Olá SDK.

> [!NOTE]
> Se é realmente depende do XCode 7, em seguida, pode utilizar Olá [iOS o Engagement SDK v3.2.4](https://aka.ms/r6oouh). Não há um erro conhecido no módulo de alcance Olá com esta versão anterior ao executar em dispositivos iOS 10: as notificações do sistema não estão alvo de ação. toofix isto, terá de tooimplement Olá preterido API `application:didReceiveRemoteNotification:` na sua aplicação delegar da seguinte forma:
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Não recomendamos esta solução** como este comportamento pode alterar qualquer atualização de versão futura iOS (mesmo secundárias) porque esta API do iOS foi preterido. Deverá mudar tooXCode 8 logo que possível.
>
>

#### <a name="usernotifications-framework"></a>UserNotifications framework
Terá de tooadd Olá `UserNotifications` framework nas fases de criação.

no Explorador de projeto Olá, abra o painel do projeto e selecione Olá de destino correto. Em seguida, abra Olá **"Fases de compilação"** separador e no Olá **"Binário com bibliotecas de ligação"** menu, adicionar framework `UserNotifications.framework` -ligação Olá conjunto`Optional`

#### <a name="application-push-capability"></a>Capacidade de push da aplicação
XCode 8 pode repor a sua aplicação push capacidade, volte a verificar no Olá `capability` separador de destino selecionado.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Adicione o código de registo de notificação 10 Olá novo iOS
Olá mais antiga código fragmento tooregister Olá aplicação toonotifications ainda funciona, mas está a utilizar preterido APIs ao executar o iOS 10.

Olá importação `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>

No seu delegado de aplicação `application:didFinishLaunchingWithOptions` substituição de método:

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

por:

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolver conflitos de delegado UNUserNotificationCenter

*Se não a aplicação ou uma das suas bibliotecas de terceiros implementa um `UNUserNotificationCenterDelegate` , em seguida, pode ignorar esta parte.*

A `UNUserNotificationCenter` delegado é utilizado pelo Olá SDK toomonitor Olá do ciclo de vida de notificações de envolvimento em dispositivos com IOS 10 ou superior. Olá SDK tem a seus próprios uma implementação de Olá `UNUserNotificationCenterDelegate` protocolo, mas pode existir apenas uma `UNUserNotificationCenter` delegar por aplicação. Quaisquer outro delegado adicionado toohello `UNUserNotificationCenter` objeto entram em conflito com Olá o Engagement um. Se Olá SDK Deteta delegado do ou quaisquer outras terceiros, em seguida, não irá utilizar o seu próprio toogive de implementação é uma oportunidade tooresolve Olá conflitos. Terá tooadd Olá Engagement lógica tooyour conflitos de Olá tooresolve o proprietário do delegado por ordem.

Existem duas formas tooachieve isto.

Proposta 1, basta pelo seu delegado de reencaminhamento chama toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Ou proposta 2, ao herdar de Olá `AEUserNotificationHandler` classe

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Pode determinar se uma notificação provém do Engagement ou não transferindo o `userInfo` dicionário toohello agente `isEngagementPushPayload:` método de classe.

Certifique-se de que Olá `UNUserNotificationCenter` delegado do objeto está definido tooyour delegado dentro ou Olá `application:willFinishLaunchingWithOptions:` ou Olá `application:didFinishLaunchingWithOptions:` método de delegado de aplicação.
Por exemplo, se tiver implementado a Olá acima proposta 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
