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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar uma aplicação (rápida)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Introduza um nome para a aplicação e o seu correio eletrónico
3.  Certifique-se a opção de Olá para a configuração orientado está marcada
4.  Siga as instruções de Olá tooadd uma aplicação de tooyour do URL de redirecionamento

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)
Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:
1. Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação
2. Introduza um nome para a aplicação e o seu correio eletrónico 
3.  Certifique-se a opção de Olá para a configuração orientado está desmarcada
4.  Clique em `Add Platform`, em seguida, selecione`Web`
5.  Voltar atrás tooVisual Studio, no Explorador de soluções, selecione o projeto de Olá e observe a janela de propriedades de Olá (se não for apresentada uma janela de propriedades, prima F4)
6.  Alterar demasiado SSL ativado`True`
7.  Copie o URL de SSL de Olá e adicionar esta lista de toohello do URL de redirecionamento URLs na lista de Portal de registo a Olá de URLs de redirecionamento:<br/><br/>![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Adicione o seguinte Olá no `web.config` localizado na pasta raiz de Olá na secção de Olá `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Substitua `ClientId` com Olá Id da aplicação que acabou de ser registado
</li>
<li>
Substitua `redirectUri` com Olá SSL URL do seu projeto
</li>
</ol>
<!-- End Docs -->
