---
title: "aaaAzure AD v2 Windows Desktop introdução - Config | Microsoft Docs"
description: "Como uma aplicação .NET de ambiente de trabalho do Windows (XAML) pode obter um token de acesso e chamar uma API protegida pelo ponto final do Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar uma aplicação (rápida)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Introduza um nome para a aplicação e o seu correio eletrónico
3.  Certifique-se a opção de Olá para a configuração orientado está marcada
4.  Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação
2. Introduza um nome para a aplicação e o seu correio eletrónico 
3. Certifique-se a opção de Olá para a configuração orientado está desmarcada
4. Clique em `Add Platform`, em seguida, selecione `Native Application` e clique em Guardar
5. Copiar Olá GUID no ID da aplicação, volte atrás tooVisual Studio, abra `App.xaml.cs` e substitua `your_client_id_here` com Olá ID da aplicação que acabou de ser registado:

```csharp
private static string ClientId = "your_application_id_here";
```
