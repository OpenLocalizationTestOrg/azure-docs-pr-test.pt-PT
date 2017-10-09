---
title: "aaaAzure AD v2 Android introdução - configurar | Microsoft Docs"
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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar uma aplicação (rápida)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Introduza um nome para a aplicação e o seu correio eletrónico
3.  Certifique-se a opção de Olá para a configuração orientado está marcada
4.  Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação
2. Introduza um nome para a aplicação e o seu correio eletrónico 
3. Certifique-se a opção de Olá para a configuração orientado está desmarcada
4. Clique em `Add Platform`, em seguida, selecione `Native Application` e clique em Guardar
5.  Abra `MainActivity` (em `app`  >  `java`  >   *`{host}.{namespace}`* )
6.  Substitua Olá *[Introduza Olá aplicação Id aqui]* na linha de Olá começadas `final static String CLIENT_ID` com o ID da aplicação Olá apenas registado:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Abra `AndroidManifest.xml` (em `app`  >  `manifests`) Olá adicionar seguir atividade demasiado`manifest\application` nós. Este procedimento regista um `BrowserTabActivity` tooallow Olá tooresume SO a aplicação depois de concluir a autenticação de Olá:
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
No Olá `BrowserTabActivity`, substitua `[Enter hello application Id here]` com o ID da aplicação Olá.
</li>
</ol>
