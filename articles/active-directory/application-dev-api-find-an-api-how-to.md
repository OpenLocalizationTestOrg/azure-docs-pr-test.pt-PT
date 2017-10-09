---
title: "aaaHow toofind uma API específica necessária para uma aplicação desenvolvida personalizado | Microsoft Docs"
description: "Como as permissões de Olá tooconfigure necessita tooaccess uma API específica no seu personalizadas desenvolvidas aplicação do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Como toofind uma API específica necessária para uma aplicação desenvolvida personalizada

TooAPIs de acesso necessita de configuração de âmbitos de acesso e de funções. Se quiser tooexpose seu recurso aplicação APIs tooclient as aplicações web, tem de funções e âmbitos de acesso de tooconfigure Olá API. Se pretender que um tooaccess de aplicação de cliente uma API web, terá de tooconfigure permissões tooaccess Olá API no registo de aplicação Olá.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configurar uma web do recurso aplicação tooexpose APIs

Quando expor API, web Olá API apresentado no Olá **selecionar um API** lista ao adicionar o registo de aplicação de tooan de permissões. âmbitos de acesso de tooadd, siga os passos de Olá descritos em [adicionar acesso âmbitos de aplicação de recurso tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurar uma APIs cliente aplicação tooaccess web

Quando adicionar o registo de aplicação de tooyour de permissões, pode **adicionar acesso à API** tooexposed web APIs. tooaccess web APIs, siga os passos de Olá descritos em [adicionar credenciais ou permissões tooaccess APIs web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Passos seguintes

-   [Integração de aplicações com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Compreender o manifesto da aplicação Olá do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


