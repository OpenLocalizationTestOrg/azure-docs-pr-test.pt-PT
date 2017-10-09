---
title: "aaaAzure AD v2 iOS introdução - introdução | Microsoft Docs"
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
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Chamar Olá Microsoft Graph API a partir de uma aplicação iOS

Este guia demonstra como uma aplicação nativa do iOS (Swift) pode obter o token de acesso e chamar Olá Microsoft Graph API ou outras APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2.

No final de Olá deste guia, a aplicação irá ser capaz de toocall uma API protegida com contas pessoais (incluindo outlook.com, live.com e outros), bem como de trabalho e as contas de profissional de qualquer da empresa ou organização que tenha o Azure Active Directory.

> ### <a name="pre-requisites"></a>Pré-requisitos
> - XCode 8. x é necessário para este guia. Pode transferir o XCode [aqui](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode transferir URL").
> - [Carthage](https://github.com/Carthage/Carthage) para gestão de pacotes

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona este guia](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

aplicação de exemplo de Olá criada por este guia permite um Olá de tooquery de aplicação iOS Microsoft Graph API ou uma API Web que aceita tokens de ponto final do Azure Active Directory v2. Neste cenário, um token é adicionado tooHTTP pedidos através do cabeçalho de autorização de Olá. Aquisição do token e a renovação é processado pelo Olá biblioteca de autenticação da Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Processamento de aquisição de token para aceder ao protegidos APIs da Web

Depois do utilizador Olá efetua a autenticação, a aplicação de exemplo de Olá recebe um token que pode ser utilizados tooquery Olá Microsoft Graph API ou uma API Web protegida pelo Microsoft Azure Active Directory v2.

APIs, tais como o Microsoft Graph requerem um tooallow de token de acesso a aceder a recursos específicos – por exemplo, tooread um perfil de utilizador, aceder ao calendário do utilizador ou enviem um e-mail. A aplicação pode pedir um token de acesso utilizando MSAL especificando âmbitos de API. Este token de acesso é, em seguida, adicionado toohello cabeçalho de autorização de HTTP para cada chamada realizada em Olá recurso protegido.

MSAL gere a colocação em cache e atualizar os tokens de acesso para si, pelo que não tem da aplicação.


### <a name="nuget-packages"></a>Pacotes NuGet

Este guia utiliza Olá pacotes NuGet os seguintes:

|Biblioteca|Descrição|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Pré-visualização biblioteca de autenticação de Microsoft para iOS|

