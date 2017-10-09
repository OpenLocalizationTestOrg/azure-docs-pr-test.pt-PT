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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Adicionar a aplicação de tooyour de informações de registo da aplicação Olá

Neste passo, terá de projeto de tooyour tooadd Olá ID de cliente.

1.  Abra `MainActivity` (em `app`  >  `java`  >   *`{host}.{namespace}`* )
2.  Substitua a partir de linha de Olá `final static String CLIENT_ID` com:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Abra:`app` > `manifests` > `AndroidManifest.xml`
4. Adicionar Olá seguir atividade demasiado`manifest\application` nós. Este registo um `BrowserTabActivity` tooallow Olá tooresume SO a aplicação depois de concluir a autenticação de Olá:

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

### <a name="what-is-next"></a>O que é o seguinte

[Testar e validar](active-directory-mobileanddesktopapp-android-test.md)
