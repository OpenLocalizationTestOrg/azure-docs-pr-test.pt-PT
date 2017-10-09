---
title: "aaaAzure AD v2 ASP.NET Web Server introdução - Config | Microsoft Docs"
description: "Implementar Microsoft início de sessão numa solução ASP.NET com uma aplicação de baseadas no browser web tradicional utilizando o padrão de OpenID Connect"
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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Configurar a sua aplicação Web do ASP.NET com as informações de registo da aplicação Olá

Neste passo, irá configurar o projeto toouse SSL e, em seguida, utilizar Olá SSL URL tooconfigure as informações de registo da aplicação. Depois da primeira, adicionar aplicação Olá ' solução tooyour de informações de registo através de *Web. config*.

1.  No Explorador de soluções, selecione o projeto de Olá e observe Olá `Properties` janela (se não for apresentada uma janela de propriedades, prima F4)
2.  Alteração `SSL Enabled` demasiado`True`
3.  Copie o valor Olá `SSL URL` acima e colá-lo na Olá `Redirect URL` campo na parte superior desta página Olá, em seguida, clique em *atualização*:<br/><br/>![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Adicione o seguinte Olá no `web.config` ficheiro localizado na pasta da raiz, na secção `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
