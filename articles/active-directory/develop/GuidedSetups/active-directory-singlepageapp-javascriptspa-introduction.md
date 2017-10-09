---
title: "aaaAzure AD v2 JS SPA orientado configuração - introdução | Microsoft Docs"
description: "Como aplicações de JavaScript SPA podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Chamar Olá Microsoft Graph API a partir de um JavaScript única página aplicação (SPA)

Este guia demonstra como uma aplicação JavaScript página única (SPA) pode iniciar sessão no trabalhos pessoais e contas escolares, obter um token de acesso e chamar Olá Microsoft Graph API ou outras APIs que necessitam de tokens de acesso de Olá ponto final do Azure Active Directory v2.

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona a aplicação de exemplo de Olá gerada por este guia](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Mais Informações

aplicação de exemplo de Olá criada por este guia permite um Olá tooquery de JavaScript SPA Microsoft Graph API ou uma API Web que aceita tokens de ponto final do Azure Active Directory v2. Para este cenário, depois de um utilizador inicia sessão, um token de acesso é pedidos tooHTTP pedida e foram adicionados através do cabeçalho de autorização de Olá. Aquisição do token e a renovação são processados pela Olá biblioteca de autenticação da Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliotecas

Este guia utiliza Olá biblioteca os seguintes:

|Biblioteca|Descrição|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Biblioteca de autenticação da Microsoft para a pré-visualização de JavaScript|

> [!NOTE]
> *msal.js* Olá destinos *ponto final do Azure Active Directory v2* -que permite a contas pessoal, profissional e escolar toosign no e adquirir tokens. Olá *ponto final do Azure Active Directory v2* tem [algumas limitações](..\active-directory-v2-limitations.md). Se estiver interessado apenas em contas profissional e escolar, utilize *adal.js* e Olá *V1 endpoint*. toounderstand diferenças entre os pontos finais v1 e v2 de Olá ler Olá [v1 v2 comparação](..\active-directory-v2-compare.md).

<!--end-collapse-->
