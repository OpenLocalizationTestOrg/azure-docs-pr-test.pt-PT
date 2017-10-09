---
title: origens de dados de perfil de tooData aaaHow
description: "Realce como dados de nível de tabela e coluna tooinclude perfis quando registar origens de dados no catálogo de dados do Azure e como os dados toouse perfis de origens de dados de toounderstand tooarticle como."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="1b0ec-103">Origens de dados de perfis de dados</span><span class="sxs-lookup"><span data-stu-id="1b0ec-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="1b0ec-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="1b0ec-104">Introduction</span></span>
<span data-ttu-id="1b0ec-105">**Catálogo de dados do Microsoft Azure** é um serviço em nuvem completamente gerido que funciona como um sistema de registo e de deteção de origens de dados empresariais.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="1b0ec-106">Por outras palavras, **catálogo de dados do Azure** está tudo sobre Ajuda pessoas detetar, compreender e utilizar origens de dados e ajudar as organizações tooget mais valor a partir da respetiva dados existentes.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="1b0ec-107">Quando uma origem de dados é registada com **catálogo de dados do Azure**, os metadados é copiado e indexado pelo serviço de Olá, mas o bloco de Olá não termina não existe.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="1b0ec-108">Olá **a criação de perfis de dados** funcionalidade do **catálogo de dados do Azure** analisa os dados de Olá de origens de dados suportados no seu catálogo e recolhe estatísticas e as informações sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="1b0ec-109">É fácil tooinclude um perfil dos seus recursos de dados.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="1b0ec-110">Ao registar um recurso de dados, escolha **incluir perfil de dados** na ferramenta de registo da origem de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="1b0ec-111">O que é a criação de perfis de dados</span><span class="sxs-lookup"><span data-stu-id="1b0ec-111">What is Data Profiling</span></span>
<span data-ttu-id="1b0ec-112">A criação de perfis de dados examina dados Olá na origem de dados de Olá a ser registado e recolhe estatísticas e as informações sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="1b0ec-113">Durante a deteção de origem de dados, estas estatísticas podem ajudar a determinar adequabilidade Olá de Olá dados toosolve seu problema empresarial.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="1b0ec-114">Olá seguintes origens de dados suportam a criação de perfis de dados:</span><span class="sxs-lookup"><span data-stu-id="1b0ec-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="1b0ec-115">SQL Server (incluindo BD SQL do Azure e Azure SQL Data Warehouse) tabelas e vistas</span><span class="sxs-lookup"><span data-stu-id="1b0ec-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="1b0ec-116">Oracle tabelas e vistas</span><span class="sxs-lookup"><span data-stu-id="1b0ec-116">Oracle tables and views</span></span>
* <span data-ttu-id="1b0ec-117">Teradata tabelas e vistas</span><span class="sxs-lookup"><span data-stu-id="1b0ec-117">Teradata tables and views</span></span>
* <span data-ttu-id="1b0ec-118">Tabelas do Hive</span><span class="sxs-lookup"><span data-stu-id="1b0ec-118">Hive tables</span></span>

<span data-ttu-id="1b0ec-119">Perfis de dados, incluindo quando registar recursos de dados ajuda os utilizadores a responder às perguntas sobre origens de dados, incluindo:</span><span class="sxs-lookup"><span data-stu-id="1b0ec-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="1b0ec-120">Este pode ser utilizado toosolve meu problema empresarial?</span><span class="sxs-lookup"><span data-stu-id="1b0ec-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="1b0ec-121">Dados Olá está em conformidade com as normas de tooparticular ou padrões?</span><span class="sxs-lookup"><span data-stu-id="1b0ec-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="1b0ec-122">Quais são alguns dos anomalias Olá Olá da origem de dados?</span><span class="sxs-lookup"><span data-stu-id="1b0ec-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="1b0ec-123">O que são possíveis desafios de integrar estes dados na minha aplicação?</span><span class="sxs-lookup"><span data-stu-id="1b0ec-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="1b0ec-124">Também pode adicionar documentação tooan asset toodescribe como dados podem ser integrados numa aplicação.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="1b0ec-125">Consulte [como origens de dados de toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="1b0ec-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="1b0ec-126">Como tooinclude dados de perfil ao registar uma origem de dados</span><span class="sxs-lookup"><span data-stu-id="1b0ec-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="1b0ec-127">É fácil tooinclude um perfil da sua origem de dados.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="1b0ec-128">Quando registar uma origem de dados no Olá **toobe objetos registado** painel do registo da origem de dados Olá ferramenta, escolha **incluir perfil de dados**.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="1b0ec-129">mais informações sobre como toolearn como tooregister origens de dados, consulte [como origens de dados de tooregister](data-catalog-how-to-register.md) e [introdução ao catálogo de dados do Azure](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b0ec-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="1b0ec-130">Filtragem de recursos de dados que incluem perfis de dados</span><span class="sxs-lookup"><span data-stu-id="1b0ec-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="1b0ec-131">recursos de dados de toodiscover que incluem um perfil de dados, pode incluir `has:tableDataProfiles` ou `has:columnsDataProfiles` como um dos seus termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="1b0ec-132">Selecionar **incluir perfil de dados** nos dados de Olá ferramenta de registo de origem inclui a tabela e as informações do perfil de nível de coluna.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="1b0ec-133">No entanto, hello API do catálogo de dados permite toobe de recursos de dados registados com apenas um conjunto de informações de perfil incluídas.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="1b0ec-134">Ver as informações de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="1b0ec-134">Viewing data profile information</span></span>
<span data-ttu-id="1b0ec-135">Depois de encontrar uma origem de dados adequado com um perfil, pode ver detalhes do perfil de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="1b0ec-136">dados de Olá tooview perfil, selecione um recurso de dados e escolha **dados perfil** na janela portal do catálogo de dados Olá.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="1b0ec-137">Um perfil de dados no **catálogo de dados do Azure** mostra tabela e informações de perfil de coluna, incluindo:</span><span class="sxs-lookup"><span data-stu-id="1b0ec-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="1b0ec-138">Perfil de dados de objeto</span><span class="sxs-lookup"><span data-stu-id="1b0ec-138">Object data profile</span></span>
* <span data-ttu-id="1b0ec-139">Número de linhas</span><span class="sxs-lookup"><span data-stu-id="1b0ec-139">Number of rows</span></span>
* <span data-ttu-id="1b0ec-140">Tamanho da tabela</span><span class="sxs-lookup"><span data-stu-id="1b0ec-140">Table size</span></span>
* <span data-ttu-id="1b0ec-141">Quando o objeto de Olá última atualização</span><span class="sxs-lookup"><span data-stu-id="1b0ec-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="1b0ec-142">Perfil de dados da coluna</span><span class="sxs-lookup"><span data-stu-id="1b0ec-142">Column data profile</span></span>
* <span data-ttu-id="1b0ec-143">Tipo de dados da coluna</span><span class="sxs-lookup"><span data-stu-id="1b0ec-143">Column data type</span></span>
* <span data-ttu-id="1b0ec-144">Número de valores distintos</span><span class="sxs-lookup"><span data-stu-id="1b0ec-144">Number of distinct values</span></span>
* <span data-ttu-id="1b0ec-145">Número de linhas com valores nulos</span><span class="sxs-lookup"><span data-stu-id="1b0ec-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="1b0ec-146">Mínimo, máximo, média e desvio padrão para valores da coluna</span><span class="sxs-lookup"><span data-stu-id="1b0ec-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="1b0ec-147">Resumo</span><span class="sxs-lookup"><span data-stu-id="1b0ec-147">Summary</span></span>
<span data-ttu-id="1b0ec-148">A criação de perfis de dados fornece estatísticas e informações sobre como registar dados ativos toohelp determinar adequabilidade Olá de Olá dados toosolve alguns dos problemas empresariais.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="1b0ec-149">Juntamente com anotar e documentar origens de dados, perfis de dados podem dar aos utilizadores uma compreensão mais aprofundada dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="1b0ec-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="1b0ec-150">Veja Também</span><span class="sxs-lookup"><span data-stu-id="1b0ec-150">See Also</span></span>
* [<span data-ttu-id="1b0ec-151">Como tooregister origens de dados</span><span class="sxs-lookup"><span data-stu-id="1b0ec-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="1b0ec-152">Introdução ao Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="1b0ec-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
