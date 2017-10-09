---
title: "aaaAzure AD v2 Android introdução - introdução | Microsoft Docs"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Chamar Olá Microsoft Graph API a partir de uma aplicação Android

Este guia demonstra como uma aplicação Android nativa pode obter um token de acesso e chamar outras APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2 ou Microsoft Graph API.

No final de Olá deste guia, a aplicação irá ser capaz de toocall uma API protegida com contas pessoais (incluindo outlook.com, live.com e outros), bem como de trabalho e as contas de profissional de qualquer da empresa ou organização que tenha o Azure Active Directory.  

### <a name="how-this-sample-works"></a>Como funciona este exemplo
![Como funciona este exemplo](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

exemplo de Olá criado por este guia baseia-se um cenário onde uma aplicação Android é utilizado tooquery uma API Web que aceita tokens a partir do Azure Active Directory v2 endpoint – neste caso, Microsoft Graph API. Neste cenário, um token é adicionado tooHTTP pedidos através do cabeçalho de autorização de Olá. Aquisição do token e a renovação é processado pelo Olá biblioteca de autenticação da Microsoft (MSAL).

### <a name="pre-requisites"></a>Pré-requisitos
* Esta configuração orientada concentra-se no Android Studio, mas qualquer outro ambiente de desenvolvimento de uma aplicação Android também é aceitável. 
* É necessário o Android SDK 21 ou mais recente (recomenda-se SDK 25).
* Google Chrome ou um browser utilizando separadores personalizada é necessário para esta versão da biblioteca de autenticação da Microsoft (MSAL) para Android.

> Nota: Google Chrome não está incluído no Visual Studio emulador do Android. Recomendamos que tootest este código um emulador com API 25 ou uma imagem com API 21 ou mais recente que tem com o Google Chrome instalada.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Como toohandle token aquisição tooaccess uma API Web protegida

Depois do utilizador Olá efetua a autenticação, a aplicação de exemplo de Olá recebe um token que pode ser utilizado tooquery Microsoft Graph API ou uma API Web protegida pelo Microsoft Azure Active Directory v2.

APIs, tais como o Microsoft Graph requerem um tooallow de token de acesso a aceder a recursos específicos – por exemplo, tooread um perfil de utilizador, aceder ao calendário do utilizador ou enviem um e-mail. A aplicação pode pedir um token de acesso utilizando MSAL tooaccess estes recursos especificar âmbitos de API. Este token de acesso é, em seguida, adicionado toohello cabeçalho de autorização de HTTP para cada chamada realizada em Olá recurso protegido. 

MSAL gere a colocação em cache e atualizar os tokens de acesso para si, pelo que não tem da aplicação.

### <a name="libraries"></a>Bibliotecas

Este guia utiliza Olá bibliotecas os seguintes:

|Biblioteca|Descrição|
|---|---|
|[com.microsoft.Identity.Client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Biblioteca de autenticação da Microsoft (MSAL)|
