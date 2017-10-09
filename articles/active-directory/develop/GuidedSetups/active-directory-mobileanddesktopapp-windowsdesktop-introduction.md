---
title: "aaaAzure AD v2 Windows Desktop introdução - introdução | Microsoft Docs"
description: "Como aplicações de .NET de ambiente de trabalho do Windows (XAML) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Chamar Olá Microsoft Graph API a partir de uma aplicação de ambiente de trabalho do Windows

Este guia demonstra como uma aplicação .NET de ambiente de trabalho do Windows (XAML) nativo pode obter um token de acesso e chamar outras APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2 ou Microsoft Graph API.

No final de Olá deste guia, a aplicação irá ser capaz de toocall uma API protegida com contas pessoais (incluindo outlook.com, live.com e outros), bem como de trabalho e as contas de profissional de qualquer da empresa ou organização que tenha o Azure Active Directory.  

> Este guia requer o Visual Studio 2015 Update 3 ou Visual Studio 2017.  Não o tiver? [Transferir o Visual Studio 2017 gratuitamente](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona este guia](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

permite que a aplicação de exemplo de Olá criada por este guia tooquery uma aplicação de ambiente de trabalho do Windows Microsoft Graph API ou uma API Web que aceita tokens de ponto final do Azure Active Directory v2. Neste cenário, um token é adicionado tooHTTP pedidos através do cabeçalho de autorização de Olá. Aquisição do token e a renovação é processado pelo Olá biblioteca de autenticação da Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Processamento de aquisição de token para aceder ao protegidos APIs da Web

Depois do utilizador Olá efetua a autenticação, a aplicação de exemplo de Olá recebe um token que pode ser utilizado tooquery Microsoft Graph API ou uma API Web protegida pelo Microsoft Azure Active Directory v2.

APIs, tais como o Microsoft Graph requerem um tooallow de token de acesso a aceder a recursos específicos – por exemplo, tooread um perfil de utilizador, aceder ao calendário do utilizador ou enviem um e-mail. A aplicação pode pedir um token de acesso utilizando MSAL tooaccess estes recursos especificar âmbitos de API. Este token de acesso é, em seguida, adicionado toohello cabeçalho de autorização de HTTP para cada chamada realizada em Olá recurso protegido. 

MSAL gere a colocação em cache e atualizar os tokens de acesso para si, pelo que não tem da aplicação.


### <a name="nuget-packages"></a>Pacotes NuGet

Este guia utiliza Olá pacotes NuGet os seguintes:

|Biblioteca|Descrição|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Biblioteca de autenticação da Microsoft (MSAL)|

