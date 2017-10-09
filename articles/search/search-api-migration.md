---
title: "aaaUpgrading toohello API de REST do serviço do Azure Search versão 2016-09-01 | Microsoft Docs"
description: "Atualizar toohello API de REST do serviço do Azure Search versão 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="ae77f-103">Atualizar toohello API de REST do serviço do Azure Search versão 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="ae77f-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="ae77f-104">Se estiver a utilizar a versão 2015-02-28 ou de pré-visualização 2015-02-28-de Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artigo irá ajudar a atualizar a sua aplicação toouse Olá seguinte geralmente disponível versão da API, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="ae77f-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="ae77f-105">Versão 2016-09-01 das Olá REST API contém algumas alterações de versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="ae77f-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="ae77f-106">Estes são principalmente retrocompatível, para que alterar o seu código deverá ser preciso apenas esforço, consoante a versão que estava a utilizar antes.</span><span class="sxs-lookup"><span data-stu-id="ae77f-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="ae77f-107">Consulte [passos tooupgrade](#UpgradeSteps) para obter instruções sobre como toochange código toouse Olá nova versão da sua API.</span><span class="sxs-lookup"><span data-stu-id="ae77f-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="ae77f-108">A instância de serviço de pesquisa do Azure suporta várias versões de REST API, incluindo Olá mais recente.</span><span class="sxs-lookup"><span data-stu-id="ae77f-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="ae77f-109">Pode continuar toouse uma versão quando já não é hello mais recente, mas recomendamos que migrar a versão mais recente do código toouse Olá.</span><span class="sxs-lookup"><span data-stu-id="ae77f-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="ae77f-110">Novidades na versão 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="ae77f-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="ae77f-111">Versão 2016-09-01 é versão geralmente disponível segundo Olá de Olá API de REST do serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae77f-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="ae77f-112">Novas funcionalidades nesta versão de API incluem:</span><span class="sxs-lookup"><span data-stu-id="ae77f-112">New features in this API version include:</span></span>

* <span data-ttu-id="ae77f-113">[Analisadores personalizados](https://aka.ms/customanalyzers), que permitem tootake controlo sobre o processo de Olá de conversão de texto em tokens indexable e pesquisáveis.</span><span class="sxs-lookup"><span data-stu-id="ae77f-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="ae77f-114">[Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) e [Table Storage do Azure](search-howto-indexing-azure-tables.md) indexadores, que lhe permitem tooeasily importar dados de armazenamento do Azure na Azure Search num agendamento ou a pedido.</span><span class="sxs-lookup"><span data-stu-id="ae77f-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="ae77f-115">[Campo mapeamentos](search-indexer-field-mappings.md), que permitem toocustomize como indexadores importar dados na Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ae77f-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="ae77f-116">Etags são, que permite que as definições de Olá tooupdate de índices, indexadores e origens de dados de forma segura de concorrência.</span><span class="sxs-lookup"><span data-stu-id="ae77f-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="ae77f-117">Passos tooupgrade</span><span class="sxs-lookup"><span data-stu-id="ae77f-117">Steps tooupgrade</span></span>
<span data-ttu-id="ae77f-118">Se estiver a atualizar a partir da versão 2015-02-28, provavelmente, não terá toomake qualquer código tooyour alterações, que não seja o número de versão de Olá toochange.</span><span class="sxs-lookup"><span data-stu-id="ae77f-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="ae77f-119">situações apenas Olá na qual poderá ser necessário toochange código são quando:</span><span class="sxs-lookup"><span data-stu-id="ae77f-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="ae77f-120">O código de falha quando uma resposta de API, são devolvidas propriedades não reconhecidas.</span><span class="sxs-lookup"><span data-stu-id="ae77f-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="ae77f-121">Por predefinição, a aplicação deve ignorar propriedades que não compreender.</span><span class="sxs-lookup"><span data-stu-id="ae77f-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="ae77f-122">O código de persistir pedidos de API e tenta tooresend-los toohello nova versão de API.</span><span class="sxs-lookup"><span data-stu-id="ae77f-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="ae77f-123">Por exemplo, isto pode acontecer se a aplicação persistir tokens de continuação devolvidos de Olá API de pesquisa (para obter mais informações, procure `@search.nextPageParameters` no Olá [referência da API de pesquisa](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="ae77f-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="ae77f-124">Se qualquer uma destas situações aplicar tooyou, em seguida, poderá ter toochange código em conformidade.</span><span class="sxs-lookup"><span data-stu-id="ae77f-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="ae77f-125">Caso contrário, não existem alterações devem ser necessárias a menos que queira toostart utilizando Olá [novas funcionalidades](#WhatsNew) da versão 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="ae77f-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="ae77f-126">Se estiver a atualizar a partir da versão 2015-02-28-pré-visualização, também se aplica a Olá acima, mas deve também estar ciente de que algumas funcionalidades de pré-visualização não estão disponíveis na versão 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="ae77f-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="ae77f-127">Suporte do indexador de armazenamento de Blobs do Azure para blobs que contém matrizes JSON e de ficheiros CSV.</span><span class="sxs-lookup"><span data-stu-id="ae77f-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="ae77f-128">Sinónimos</span><span class="sxs-lookup"><span data-stu-id="ae77f-128">Synonyms</span></span>
* <span data-ttu-id="ae77f-129">Consultas de "Mais como"</span><span class="sxs-lookup"><span data-stu-id="ae77f-129">"More like this" queries</span></span>

<span data-ttu-id="ae77f-130">Se o seu código utiliza estas funcionalidades, não será capaz de tooupgrade too2016-09-01, sem remover a sua utilização dos mesmos.</span><span class="sxs-lookup"><span data-stu-id="ae77f-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae77f-131">. Lembre-se, pré-visualizar APIs foram concebidas para avaliação e de teste e não deve ser utilizadas em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="ae77f-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="ae77f-132">Conclusão</span><span class="sxs-lookup"><span data-stu-id="ae77f-132">Conclusion</span></span>
<span data-ttu-id="ae77f-133">Se precisar de mais detalhes sobre como utilizar Olá API de REST do serviço de pesquisa do Azure, consulte Olá recentemente atualizado [referência da API](https://msdn.microsoft.com/library/azure/dn798935.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ae77f-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="ae77f-134">Apreciamos os seus comentários na Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ae77f-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="ae77f-135">Se tiver problemas, sentir tooask livre-nos para obter ajuda na Olá [fórum MSDN de pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="ae77f-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="ae77f-136">Se está a solicitar uma pergunta sobre a Azure procura StackOverflow, tootag se marca-a com `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="ae77f-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="ae77f-137">Obrigado por utilizar a pesquisa do Azure!</span><span class="sxs-lookup"><span data-stu-id="ae77f-137">Thank you for using Azure Search!</span></span>

