---
title: "Introdução de aaaAzure AD v2 iOS - configurar | Microsoft Docs"
description: "Como as aplicações do iOS (Swift) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar uma aplicação (rápida)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Introduza um nome para a aplicação e o seu correio eletrónico
3.  Certifique-se a opção de Olá para a configuração orientado está marcada
4.  Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)

1.  Aceda demasiado[Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Introduza um nome para a aplicação e o seu correio eletrónico
3.  Certifique-se a opção de Olá para a configuração orientado está desmarcada
4.  Clique em `Add Platform`, em seguida, selecione `Native Application` e clique em`Save`
5.  Volte tooXcode. No `ViewController.swift`, substitua a linha de Olá que começa por '`let kClientID`' com o ID da aplicação Olá apenas registado:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Controlar + clique <code>Info.plist</code> toobring configurar menu contextuais Olá e, em seguida, clique em: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
Em Olá <code>dict</code> nó raiz, adicione Olá seguinte:
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
Substitua <i> <code>[Your_Application_Id_Here]</code> </i> com Olá Id da aplicação que acabou de ser registado
</li>
</ol>
