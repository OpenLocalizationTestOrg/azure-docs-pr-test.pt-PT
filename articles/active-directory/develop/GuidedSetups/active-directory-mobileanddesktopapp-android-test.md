---
title: "aaaAzure AD v2 Android introdução - teste | Microsoft Docs"
description: "Como uma aplicação Android pode obter um token de acesso e chamar Graph API do Microsoft ou de APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testar o seu código

1. Implemente o código tooyour dispositivos/emulador.
2. Quando estiver pronto tootest, utilize (conta institucional) um Microsoft Azure Active Directory ou uma toosign de conta Account Microsoft (live.com, outlook.com) no. 

![Captura de ecrã de exemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Início de sessão](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Consentimento
Olá pela primeira vez que um utilizador inicia sessão numa aplicação tooyour, estes serão apresentados com um ecrã consentimento com semelhante toohello de abaixo, onde têm de aceitar tooexplicitly: 

![Consentimento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Resultados esperados
Deverá ver resultados de Olá de uma chamada de tooMicrosoft Graph API 'me' ponto final utilizado o perfil de utilizador de Olá tootooobtain - https://graph.microsoft.com/v1.0/me. Para obter uma lista de pontos finais de Microsoft Graph comuns, consulte este [artigo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Mais informações sobre âmbitos e as permissões delegadas

Olá Microsoft Graph API requer Olá `user.read` âmbito tooread Olá perfil. Este âmbito é adicionado automaticamente por predefinição em todas as aplicações que está a ser registada no nosso portal de registo. Algumas outras APIs para o Microsoft Graph, bem como APIs personalizadas para o servidor de back-end poderá exigir âmbitos adicionais. Por exemplo, para o Microsoft Graph, Olá âmbito `Calendars.Read` é calendários do utilizador Olá toolist necessária. Ordem tooaccess Olá calendário do utilizador num contexto de uma aplicação, terá de tooadd Olá `Calendars.Read` delegados informações do registo de permissão, toohello aplicação e, em seguida, adicionar Olá `Calendars.Read` âmbito toohello `acquireTokenSilentAsync` chamada. Olá poderá ser solicitado ao utilizador consents adicionais como aumentar o número de Olá de âmbitos.

<!--end-collapse-->
