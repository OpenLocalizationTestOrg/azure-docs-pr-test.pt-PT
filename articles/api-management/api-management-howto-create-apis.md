---
title: aaaHow toocreate APIs na API Management do Azure
description: Saiba como toocreate e configure APIs na API Management do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="a1f39-103">Como toocreate APIs na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="a1f39-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="a1f39-104">Uma API na API Management representa um conjunto de operações que podem ser invocados por aplicações cliente.</span><span class="sxs-lookup"><span data-stu-id="a1f39-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="a1f39-105">Novas APIs são criadas no portal do publicador Olá e, em seguida, Olá pretendido operações são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="a1f39-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="a1f39-106">Assim que forem adicionadas operações Olá, Olá API é adicionada tooa produto e pode ser publicado.</span><span class="sxs-lookup"><span data-stu-id="a1f39-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="a1f39-107">Depois de uma API for publicada, pode ser subscrito tooand utilizado pelos programadores.</span><span class="sxs-lookup"><span data-stu-id="a1f39-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="a1f39-108">Este guia mostra o primeiro passo de Olá no processo de Olá: como toocreate e configurar uma nova API na API Management.</span><span class="sxs-lookup"><span data-stu-id="a1f39-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="a1f39-109">Para obter mais informações sobre a adição de operações e publicar um produto, consulte [como tooadd operações tooan API] [ How tooadd operations tooan API] e [como toocreate e publicar um produto] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="a1f39-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="a1f39-110"><a name="create-new-api"></a>Criar uma nova API</span><span class="sxs-lookup"><span data-stu-id="a1f39-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="a1f39-111">As APIs são criadas e configuradas no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="a1f39-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="a1f39-112">tooaccess Olá clique portal, publicador **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="a1f39-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal do publicador][api-management-management-console]

> <span data-ttu-id="a1f39-114">Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1f39-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a1f39-115">Clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="a1f39-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Criar API][api-management-create-api]

<span data-ttu-id="a1f39-117">Olá utilize **Adicionar nova API** janela tooconfigure Olá nova API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Adicionar nova API][api-management-add-new-api]

<span data-ttu-id="a1f39-119">Olá seguintes campos é utilizados tooconfigure Olá nova API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="a1f39-120">**Nome da Web API** fornece um nome único e descritivo para Olá API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="a1f39-121">Será apresentado em portais de programador e o publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="a1f39-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="a1f39-122">**URL do serviço Web** referências Olá implementar Olá API de serviço HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1f39-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="a1f39-123">API de gestão reencaminha pedidos toothis endereço.</span><span class="sxs-lookup"><span data-stu-id="a1f39-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="a1f39-124">**Sufixo do URL da API Web** é anexado toohello URL base do serviço de gestão de Olá API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="a1f39-125">URL de base de Olá é comum para todos os APIs alojadas por uma instância de serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="a1f39-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="a1f39-126">Gestão de API distingue APIs pelo respetivo sufixo e, por conseguinte, o sufixo de Olá tem de ser exclusivo para cada API para um determinado publicador.</span><span class="sxs-lookup"><span data-stu-id="a1f39-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="a1f39-127">**Esquema de URL de API Web** determina quais protocolos podem ser utilizados tooaccess Olá API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="a1f39-128">HTTPs é especificado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="a1f39-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="a1f39-129">toooptionally adicionar este novo tooa produto da API, clique em Olá **produtos (opcionais)** pendente e escolha um produto.</span><span class="sxs-lookup"><span data-stu-id="a1f39-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="a1f39-130">Este passo pode ser repetida múltiplas vezes tooadd Olá API toomultiple produtos.</span><span class="sxs-lookup"><span data-stu-id="a1f39-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="a1f39-131">Depois de Olá pretendido valores estão configurados, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="a1f39-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="a1f39-132">Assim que for criado Olá nova API, hello página de resumo para a API de Olá é apresentada no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="a1f39-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Resumo da API][api-management-api-summary]

## <span data-ttu-id="a1f39-134"><a name="configure-api-settings"></a>As definições da API de configurar</span><span class="sxs-lookup"><span data-stu-id="a1f39-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="a1f39-135">Pode utilizar Olá **definições** separador tooverify e editar Olá configuração de uma API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="a1f39-136">**Nome da Web API**, **URL do serviço Web**, e **sufixo do URL da API Web** são inicialmente definido quando Olá API é criado e pode ser modificado aqui.</span><span class="sxs-lookup"><span data-stu-id="a1f39-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="a1f39-137">**Descrição** fornece uma descrição opcional e **esquema de URL de API Web** determina quais protocolos podem ser utilizados tooaccess Olá API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![Definições da API][api-management-api-settings]

<span data-ttu-id="a1f39-139">autenticação de gateway tooconfigure por hello back-end do serviço implementar Olá API, selecione Olá **segurança** Olá separador **com credenciais** pendente pode ser utilizado tooconfigure **HTTP básico** ou **certificados de cliente** autenticação.</span><span class="sxs-lookup"><span data-stu-id="a1f39-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="a1f39-140">autenticação básica toouse HTTP, basta introduzir credenciais de Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="a1f39-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="a1f39-141">Para obter informações sobre como utilizar a autenticação de certificado de cliente, consulte [como serviços de back-end toosecure utilizando o cliente de certificado de autenticação na API Management do Azure][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a1f39-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="a1f39-142">Olá **segurança** separador também pode ser utilizado tooconfigure **autorização do utilizador** utilizando OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a1f39-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="a1f39-143">Para obter mais informações, consulte [como programador tooauthorize contas com OAuth 2.0 na API Management do Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a1f39-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Definições de autenticação básica][api-management-api-settings-credentials]

<span data-ttu-id="a1f39-145">Clique em **guardar** toosave quaisquer alterações que efetuar toohello as definições da API.</span><span class="sxs-lookup"><span data-stu-id="a1f39-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="a1f39-146"><a name="next-steps"> </a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a1f39-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a1f39-147">Assim que é criada uma API e definições de Olá configuradas, passos Olá são tooadd Olá operações toohello API, adicionar Olá API tooa produto e publicá-lo para que fique disponível para programadores.</span><span class="sxs-lookup"><span data-stu-id="a1f39-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="a1f39-148">Para obter mais informações, consulte Olá seguintes artigos.</span><span class="sxs-lookup"><span data-stu-id="a1f39-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="a1f39-149">[Como tooadd operações tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="a1f39-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="a1f39-150">[Como toocreate e publicar um produto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="a1f39-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
