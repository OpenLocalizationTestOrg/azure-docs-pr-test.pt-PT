---
title: "aaaAzure Interface de utilizador do Mobile Engagement - definições"
description: "Saiba como toomanage Olá definições globais da sua aplicação utilizando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a>Como toomanage Olá definições globais da aplicação
Olá **definições** disponíveis para vary uma aplicação, dependendo da plataforma de Olá de aplicação Olá e permissões de Olá lhe foram concedidas para aplicação Olá de opções de menu. As definições incluem o seguinte Olá: detalhes, projetos, Push nativo, velocidade de Push, etiqueta (app-info) e que a pressão comercial. Olá opção do menu (as informações da aplicação) Tag da secção de definições de Olá pode ser gerido pela sua aplicação (utilizando Olá SDK) ou pelo seu back-end (através de Olá Device API). 

> [!NOTE]
> Muitos secções Olá **Mobile Engagement** portal IU conter Olá **Mostrar ajudar** botão. Prima este botão tooget mais contextuais informações sobre uma secção.
> 
> 

## <a name="details"></a>Detalhes
Permite-lhe nome de Olá toochange e descrição da sua aplicação, o proprietário de Olá de vista da sua aplicação e as permissões de função. 

Configuração de análise permite-lhe tooview ou alteração dia Olá semanas iniciar no e Olá tempo de retenção em dias.

  ![settings1][46]

## <a name="projects"></a>Projetos
Permite-lhe tooselect todos os projetos pretende tooappear sua aplicação. 

Também pode procurar um nome de Olá do projeto e vista, a descrição, o proprietário e as permissões de função de qualquer projeto a aplicação faz parte.

Para obter mais informações, consulte: [documentação de IU – home page][Link 13]

  ![settings3][48]

## <a name="native-push"></a>Push nativo
Permite-lhe tooregister um novo certificado ou a eliminação e o certificado existente para utilizam com o push nativo. Push nativo permite que a aplicação de tooyour do Azure Mobile Engagement toopush em qualquer altura, mesmo quando não está em execução. 

Depois de fornecer as credenciais ou certificados para, pelo menos, um serviço de Push nativo, pode selecionar "Sempre" quando criar campanhas de alcance bem como o parâmetro de "notifier" Olá de utilização no Olá PUSH API.

### <a name="apple-push-notification-service-apns"></a>Serviço Apple Push Notification (APNS)
tooenable Push nativo com Olá serviço Apple Push Notification, terá de tooregister o certificado. Terá de tipo de Olá toospecify do certificado como desenvolvimento (desenvolvimento) ou de produção (PROD). Em seguida, irá precisar de carregar a palavra-passe do certificado e Olá.

Para obter mais informações, consulte: [documentação do SDK - iOS - como tooPrepare a aplicação para notificações Push da Apple][Link 5]

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a>Serviço de notificações de Push do Windows (WPNS)
tooenable Push nativo com o serviço de notificação do Windows, tem de fornecer credenciais da sua aplicação. Terá do identificador de segurança (SID) do seu pacote e a chave secreta.

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a>Google Cloud Messaging para Android (GCM)
tooenable Push nativo com GCM, tem de instruções de Olá toofollow do Google. Em seguida, tem de colar uma chave de API simple de servidor, configurada sem restrições IP. Requer uma integração com Olá SDK para Android v1.12.0 +.

Para obter mais informações, consulte: 

* [SDK documentação Android como tooIntegrate GCM][Link 5]
* [Guia do programador da Google GCM](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a>Dispositivo Amazon Messaging para Android (ADM)
tooenable nativo Push utilizando ADM, tem de fornecer o Amazon <OAuth credentials> constituída por um ID de cliente e o segredo do cliente (requer uma integração com o SDK para Android v2.1.0 +).

Para obter mais informações, consulte: 

* [SDK documentação Android como tooIntegrate ADM][Link 5]
* [Documentação de programador da Amazon ADM](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a>Velocidade de push
Mostra Olá atual velocidade de push da aplicação e permite-lhe toodefine Olá velocidade de push da aplicação.

  ![settings7][52]

## <a name="tag-app-info"></a>Etiqueta (app-info)
![settings11][56]

## <a name="commercial-pressure"></a>Pressão comercial
![settings12][57]

## <a name="see-also"></a>Consultar também
* [Conceitos][Link 6]
* [Serviço de guia de resolução de problemas][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

