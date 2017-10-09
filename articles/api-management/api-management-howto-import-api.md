---
title: aaaImport uma API na API Management do Azure | Microsoft Docs
description: "Saiba como tooimport uma API e as suas operações na API Management do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="2080b-103">Como tooimport Olá a definição de uma API com operações em API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="2080b-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="2080b-104">Na API Management, podem ser criadas novas APIs e operações de Olá adicionadas manualmente ou Olá API pode ser importados juntamente com operações de Olá num único passo.</span><span class="sxs-lookup"><span data-stu-id="2080b-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="2080b-105">APIs e as respetivas operações podem ser importadas utilizando Olá seguintes formatos.</span><span class="sxs-lookup"><span data-stu-id="2080b-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="2080b-106">WADL</span><span class="sxs-lookup"><span data-stu-id="2080b-106">WADL</span></span>
* <span data-ttu-id="2080b-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="2080b-107">Swagger</span></span>

<span data-ttu-id="2080b-108">Este guia mostra como criar uma nova API e importar as respetivas operações num único passo.</span><span class="sxs-lookup"><span data-stu-id="2080b-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="2080b-109">Para informações sobre como criar manualmente uma API e adicionar operações, consulte [como toocreate APIs] [ How toocreate APIs] e [como tooadd operações tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="2080b-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="2080b-110"><a name="import-api"> </a>Importar uma API</span><span class="sxs-lookup"><span data-stu-id="2080b-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="2080b-111">As APIs são criadas e configuradas no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="2080b-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="2080b-112">tooaccess Olá clique portal, publicador **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="2080b-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="2080b-113">Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="2080b-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal do publicador][api-management-management-console]

<span data-ttu-id="2080b-115">Clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **importar API**.</span><span class="sxs-lookup"><span data-stu-id="2080b-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![API de importação][api-management-import-apis]

<span data-ttu-id="2080b-117">Olá **API de importação** janela tem três separadores que correspondem a especificação do toohello três formas tooprovide Olá API.</span><span class="sxs-lookup"><span data-stu-id="2080b-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="2080b-118">**Na área de transferência** permite a especificação de Olá API toopaste na caixa de texto designado de Olá.</span><span class="sxs-lookup"><span data-stu-id="2080b-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="2080b-119">**Ficheiro** permite-lhe toobrowse tooand Olá selecione ficheiro que contém a especificação de Olá API.</span><span class="sxs-lookup"><span data-stu-id="2080b-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="2080b-120">**Partir do URL** permite-lhe toosupply Olá URL toohello a especificação de Olá API.</span><span class="sxs-lookup"><span data-stu-id="2080b-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Formato de importar API][api-management-import-api-clipboard]

<span data-ttu-id="2080b-122">Depois de fornecer a especificação de Olá API, utilize os botões de opção de Olá no formato de especificação do Olá tooindicate direita Olá.</span><span class="sxs-lookup"><span data-stu-id="2080b-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="2080b-123">Olá seguintes formatos é suportada.</span><span class="sxs-lookup"><span data-stu-id="2080b-123">hello following formats are supported.</span></span>

* <span data-ttu-id="2080b-124">WADL</span><span class="sxs-lookup"><span data-stu-id="2080b-124">WADL</span></span>
* <span data-ttu-id="2080b-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="2080b-125">Swagger</span></span>

<span data-ttu-id="2080b-126">Em seguida, introduza um **sufixo do URL da API Web**.</span><span class="sxs-lookup"><span data-stu-id="2080b-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="2080b-127">Este é o URL de base de toohello anexado, para o seu serviço de gestão de API.</span><span class="sxs-lookup"><span data-stu-id="2080b-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="2080b-128">URL de base de Olá é comum para todos os APIs alojadas em cada instância de um serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="2080b-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="2080b-129">Gestão de API distingue APIs pelo respetivo sufixo e, por conseguinte, o sufixo de Olá tem de ser exclusivo para cada API numa instância de serviço de gestão de API específica.</span><span class="sxs-lookup"><span data-stu-id="2080b-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="2080b-130">Depois de todos os valores são introduzidos, clique em **guardar** toocreate Olá API e Olá associados operações.</span><span class="sxs-lookup"><span data-stu-id="2080b-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="2080b-131">Para obter um tutorial importar uma API de calculadora básica no formato Swagger, consulte [gerir a sua primeira API na API Management do Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2080b-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="2080b-132"><a name="export-api"></a> Exportar uma API</span><span class="sxs-lookup"><span data-stu-id="2080b-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="2080b-133">Na adição tooimporting novas APIs, pode exportar definições de Olá das suas APIs do portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="2080b-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="2080b-134">toodo por isso, clique em **exportar API** de Olá **separador Resumo** do seu **API**.</span><span class="sxs-lookup"><span data-stu-id="2080b-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Exportação de API][api-management-export-api]

<span data-ttu-id="2080b-136">APIs podem ser exportadas utilizando WADL ou Swagger.</span><span class="sxs-lookup"><span data-stu-id="2080b-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="2080b-137">Selecione formato pretendido Olá, clique em **guardar**e escolha a localização de Olá no qual o ficheiro Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="2080b-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Formato de API de exportação][api-management-export-api-format]

## <span data-ttu-id="2080b-139"><a name="next-steps"> </a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2080b-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="2080b-140">Depois de uma API é criada e operações de Olá importadas, pode rever e configurar as definições adicionais, adicione Olá API tooa produto e publicá-lo para que fique disponível para programadores.</span><span class="sxs-lookup"><span data-stu-id="2080b-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="2080b-141">Para obter mais informações, consulte Olá seguintes guias.</span><span class="sxs-lookup"><span data-stu-id="2080b-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="2080b-142">[Como as definições de tooconfigure API][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="2080b-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="2080b-143">[Como toocreate e publicar um produto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="2080b-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
