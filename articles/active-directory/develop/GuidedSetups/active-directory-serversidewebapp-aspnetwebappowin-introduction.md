---
title: "aaaAzure AD v2 ASP.NET Web Server introdução - introdução | Microsoft Docs"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Adicionar início de sessão com o Microsoft tooan ASP.NET web app

Este guia demonstra como tooimplement início de sessão com a Microsoft através de uma solução de ASP.NET MVC com uma aplicação de baseada no browser tradicional web com OpenID Connect. 

No final de Olá deste guia, a aplicação irá ser tooaccept capazes sessão ins do pessoal contas (incluindo outlook.com, live.com e outros), bem como funcionam contas escolares ou profissionais de qualquer da empresa ou organização que tem integrado com o Azure Active Directory. 

> Este guia requer o Visual Studio 2015 Update 3 ou Visual Studio 2017.  Não o tiver?  [Transferir o Visual Studio 2017 gratuitamente](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona este guia](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Este guia baseia-se num cenário de olá onde um browser acede a um web site do ASP.NET, pedindo uma tooauthenticate de utilizador através de um botão de início de sessão. Neste cenário, a maioria Olá trabalho toorender Olá web página ocorre no lado do servidor de Olá.

## <a name="libraries"></a>Bibliotecas

Este guia utiliza Olá bibliotecas os seguintes:

|Biblioteca|Descrição|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Middleware que permite uma aplicação toouse OpenIdConnect para autenticação|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Middleware que permite uma sessão de utilizador de toomaintain de aplicação a utilização de cookies|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Permite que aplicações baseadas em OWIN toorun no IIS através do pipeline de pedido do ASP.NET Olá|

