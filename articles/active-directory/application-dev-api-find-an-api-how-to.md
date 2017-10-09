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
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="35dcb-103">Como toofind uma API específica necessária para uma aplicação desenvolvida personalizada</span><span class="sxs-lookup"><span data-stu-id="35dcb-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="35dcb-104">TooAPIs de acesso necessita de configuração de âmbitos de acesso e de funções.</span><span class="sxs-lookup"><span data-stu-id="35dcb-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="35dcb-105">Se quiser tooexpose seu recurso aplicação APIs tooclient as aplicações web, tem de funções e âmbitos de acesso de tooconfigure Olá API.</span><span class="sxs-lookup"><span data-stu-id="35dcb-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="35dcb-106">Se pretender que um tooaccess de aplicação de cliente uma API web, terá de tooconfigure permissões tooaccess Olá API no registo de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="35dcb-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="35dcb-107">Configurar uma web do recurso aplicação tooexpose APIs</span><span class="sxs-lookup"><span data-stu-id="35dcb-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="35dcb-108">Quando expor API, web Olá API apresentado no Olá **selecionar um API** lista ao adicionar o registo de aplicação de tooan de permissões.</span><span class="sxs-lookup"><span data-stu-id="35dcb-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="35dcb-109">âmbitos de acesso de tooadd, siga os passos de Olá descritos em [adicionar acesso âmbitos de aplicação de recurso tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="35dcb-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="35dcb-110">Configurar uma APIs cliente aplicação tooaccess web</span><span class="sxs-lookup"><span data-stu-id="35dcb-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="35dcb-111">Quando adicionar o registo de aplicação de tooyour de permissões, pode **adicionar acesso à API** tooexposed web APIs.</span><span class="sxs-lookup"><span data-stu-id="35dcb-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="35dcb-112">tooaccess web APIs, siga os passos de Olá descritos em [adicionar credenciais ou permissões tooaccess APIs web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="35dcb-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="35dcb-113">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="35dcb-113">Next steps</span></span>

-   [<span data-ttu-id="35dcb-114">Integração de aplicações com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35dcb-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="35dcb-115">Compreender o manifesto da aplicação Olá do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35dcb-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


