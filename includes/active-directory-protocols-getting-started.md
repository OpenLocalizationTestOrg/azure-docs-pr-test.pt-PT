---
title: "aaaAzure AD descrição geral de protocolo do .NET | Microsoft Docs"
description: "Como aceder aos toouse HTTP mensagens tooauthorize tooweb aplicações e APIs web no seu inquilino com o Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## Registar a aplicação com o inquilino do AD
Em primeiro lugar, precisa de tooregister a aplicação com o seu inquilino do Azure Active Directory (Azure AD). Isto irá dar-lhe um ID de aplicação para a sua aplicação, bem como ativá-la tooreceive tokens.

* Inicie sessão no toohello [Portal do Azure](https://portal.azure.com).
* Escolha o seu inquilino do Azure AD, clicando na sua conta no Olá canto superior direito da página Olá.
* No painel de navegação da esquerda de Olá, clique em **do Azure Active Directory**.
* Clique em **Registos de Aplicação** e clique em **Adicionar**.
* Siga as instruções de Olá e crie uma nova aplicação. Para este tutorial não importa se é uma aplicação Web ou uma aplicação nativa, mas se pretender exemplos específicos de aplicações Web ou aplicações nativas, veja os [inícios rápidos](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Para aplicações Web, forneça Olá **URL de início de sessão** que é Olá URL base da sua aplicação, onde os utilizadores podem iniciar sessão por exemplo `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicações nativas, forneça um **URI de redirecionamento**, o Azure AD irá utilizar tooreturn respostas de token. Introduza um valor tooyour específico de aplicação,. por exemplo`http://MyFirstAADApp`
* Depois de concluir o registo, do Azure AD irá atribuir um identificador de cliente exclusivos a sua aplicação, Olá ID da aplicação. Irá precisar deste valor nas secções seguintes Olá, por isso, copie-o partir da página de aplicação Olá.
