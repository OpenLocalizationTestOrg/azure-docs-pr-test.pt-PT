---
title: "aaaGuide toocreating um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implementar um serviço de dados para comprar no Olá Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="045f6-103">Mapeamento de um existente tooOData de serviço web através de CSDL</span><span class="sxs-lookup"><span data-stu-id="045f6-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="045f6-104">**Neste momento, estamos já não integração qualquer nova editores de serviço de dados. Novo dataservices não irá obter aprovada para listagem.**</span><span class="sxs-lookup"><span data-stu-id="045f6-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="045f6-105">Se tiver uma aplicação de negócio de SaaS que gostaria de toopublish pode encontrar mais informações no AppSource [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="045f6-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="045f6-106">Se tiver um aplicações IaaS ou para programadores de serviço teria como toopublish no Azure Marketplace pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="045f6-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="045f6-107">Este artigo fornece uma descrição geral sobre como toouse um toomap CSDL um tooan de serviço existente serviço compatível de OData.</span><span class="sxs-lookup"><span data-stu-id="045f6-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="045f6-108">Explica como toocreate Olá mapeamento documento (CSDL) que transforma pedido de entrada hello do cliente Olá através de uma chamada de serviço e Olá saída do cliente de toohello (dados) volta através de um feed compatível de OData.</span><span class="sxs-lookup"><span data-stu-id="045f6-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="045f6-109">Microsoft Azure Marketplace expõe os utilizadores finais toohello de serviços através do protocolo OData Olá.</span><span class="sxs-lookup"><span data-stu-id="045f6-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="045f6-110">Serviços que são expostos pelos fornecedores de conteúdo (os proprietários de dados) são expostos numa variedade de formulários, tais como REST, SOAP, etc.</span><span class="sxs-lookup"><span data-stu-id="045f6-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="045f6-111">O que é um CSDL e a respetiva estrutura?</span><span class="sxs-lookup"><span data-stu-id="045f6-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="045f6-112">Um CSDL (linguagem de definição de esquema Concetual) é uma especificação de definir como serviço web de toodescribe ou a base de dados do serviço em comum XML verbiage toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="045f6-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="045f6-113">Descrição geral Simple do Olá **fluxo do pedido:**</span><span class="sxs-lookup"><span data-stu-id="045f6-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="045f6-114">Olá **fluxo de dados** está a ser Olá opposite direção:</span><span class="sxs-lookup"><span data-stu-id="045f6-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="045f6-115">**Figura 1** diagramas como um cliente obter dados de um fornecedor de conteúdo (o serviço) ao percorrer Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="045f6-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="045f6-116">Olá CSDL é utilizado por pedido de Olá Olá mapeamento/transformação componente toohandle e transmitir dados entre os serviços e Olá pedir cliente do Olá fornecedor de conteúdos.</span><span class="sxs-lookup"><span data-stu-id="045f6-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="045f6-117">*Figura 1: Fluxo de detalhado de pedir o fornecedor de toocontent de cliente através do Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="045f6-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="045f6-119">Para em segundo plano em Atom, do Atom Pub e protocolo de OData Olá após o qual Olá compilação de extensões do Azure Marketplace, consulte: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="045f6-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="045f6-120">Excerpt from above ligação: *"o objetivo de Olá do protocolo de Open Data Olá (tooas hereafter referenciado OData) é o protocolo de tooprovide um baseado em REST para operações CRUD estilo (criar, ler, atualizar e eliminar) relativamente aos recursos expostas como serviços de dados. "Serviço de dados" é um ponto final onde há dados expostos a partir de uma ou mais "coleções" cada com zero ou mais "entradas", que consistem em escreveu pares nome-valor. OData é publicado pela Microsoft em normas OASIS (organização para Olá Advancement of informações estruturados Standards) para que qualquer pessoa que pretende toocan criar servidores, clientes ou ferramentas sem restrições ou royalties."*</span><span class="sxs-lookup"><span data-stu-id="045f6-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="045f6-121">Três importantes que têm toobe definido pelo Olá CSDL são:</span><span class="sxs-lookup"><span data-stu-id="045f6-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="045f6-122">Olá **endpoint** de Olá fornecedor de serviços Olá endereço de Web (URI) de Olá serviço</span><span class="sxs-lookup"><span data-stu-id="045f6-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="045f6-123">Olá **parâmetros de dados** que está a ser transmitido como entrada toohello fornecedor de serviços de definições de Olá dos parâmetros de Olá enviados toohello do serviço do fornecedor de baixo toohello tipo de dados conteúdo.</span><span class="sxs-lookup"><span data-stu-id="045f6-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="045f6-124">**Esquema** de dados de Olá a ser devolvidos o esquema de Olá toohello pedir serviço de dados de Olá sejam entregues pelo serviço do fornecedor Olá conteúdo, incluindo os tipos de contentor, coleções/tabelas, colunas/variáveis e dados.</span><span class="sxs-lookup"><span data-stu-id="045f6-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="045f6-125">Olá seguinte diagrama mostra uma descrição geral do fluxo de Olá de onde o cliente de Olá introduz Olá OData instrução (chamada toohello conteúdo do serviço web fornecedor) toogetting Olá resultados/dados novamente.</span><span class="sxs-lookup"><span data-stu-id="045f6-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="045f6-127">passos:</span><span class="sxs-lookup"><span data-stu-id="045f6-127">Steps:</span></span>
1. <span data-ttu-id="045f6-128">O cliente envia o pedido através de chamada de serviço concluída com parâmetros de entrada definidos no XML toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="045f6-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="045f6-129">CSDL é utilizado toovalidate Olá chamada de serviço.</span><span class="sxs-lookup"><span data-stu-id="045f6-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="045f6-130">Olá formatado chamada de serviço é, em seguida, enviada toohello conteúdo de fornecedores de serviço por Olá Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="045f6-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="045f6-131">Olá Webservice executa e preforms ação Olá Olá verbo de Http (ou seja, obter) Olá os dados forem devolvidos tooAzure Marketplace onde Olá pedida dados (se aplicável) é expõe no formato XML toohello cliente Olá mapeamento definido no Olá CSDL a utilizar.</span><span class="sxs-lookup"><span data-stu-id="045f6-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="045f6-132">Olá cliente é enviado dados Olá (se existirem) no formato XML ou JSON</span><span class="sxs-lookup"><span data-stu-id="045f6-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="045f6-133">Definições</span><span class="sxs-lookup"><span data-stu-id="045f6-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="045f6-134">Do OData ATOM pub</span><span class="sxs-lookup"><span data-stu-id="045f6-134">OData ATOM pub</span></span>
<span data-ttu-id="045f6-135">Definir uma extensão toohello do ATOM pub onde cada entrada representa uma linha de um resultado.</span><span class="sxs-lookup"><span data-stu-id="045f6-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="045f6-136">Olá conteúdo parte entrada Olá é melhorado toocontain Olá valores de linha de Olá – como pares de valor de chave.</span><span class="sxs-lookup"><span data-stu-id="045f6-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="045f6-137">Encontrar mais informações aqui: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="045f6-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="045f6-138">CSDL - linguagem de definição de esquema Concetual</span><span class="sxs-lookup"><span data-stu-id="045f6-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="045f6-139">Permite definir funções (SPROCs) e as entidades que estão expostas através de uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="045f6-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="045f6-140">Obter mais informações, localizadas aqui: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="045f6-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="045f6-141">Clique em Olá **outras versões** pendente e selecione uma versão, se não vir artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="045f6-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="045f6-142">EDM - modelo de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="045f6-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="045f6-143">Descrição geral: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="045f6-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="045f6-144">Pré-visualização: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="045f6-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="045f6-145">Tipos de dados: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="045f6-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="045f6-146">seguinte Olá mostra Olá detalhadas fluxo tooRight esquerdo de onde o cliente de Olá introduz Olá OData instrução (chamada toohello conteúdo do serviço web fornecedor) toogetting Olá resultados/dados novamente:</span><span class="sxs-lookup"><span data-stu-id="045f6-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="045f6-148">Noções básicas CSDL</span><span class="sxs-lookup"><span data-stu-id="045f6-148">CSDL Basics</span></span>
<span data-ttu-id="045f6-149">Um CSDL (linguagem de definição de esquema Concetual) é uma especificação de definir como serviço web de toodescribe ou a base de dados do serviço em comum XML verbiage toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="045f6-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="045f6-150">Descreve CSDL Olá crítico pieces que **possibilita a transmissão de Olá dos dados da origem de dados de Olá toohello Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="045f6-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="045f6-151">partes principais Olá são descritas aqui:</span><span class="sxs-lookup"><span data-stu-id="045f6-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="045f6-152">Informações de interface que descrevem todas as funções publicamente disponíveis (FunctionImport nó)</span><span class="sxs-lookup"><span data-stu-id="045f6-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="045f6-153">Informações de tipo de dados para todas as mensagens requests(input) e responses(outputs) de mensagem (EntitySet/EntityContainer/EntityType nós)</span><span class="sxs-lookup"><span data-stu-id="045f6-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="045f6-154">Informações sobre toobe de protocolo de transporte de Olá de enlace utilizado (cabeçalho nó)</span><span class="sxs-lookup"><span data-stu-id="045f6-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="045f6-155">Informações de endereço para localizar Olá especificado serviço (BaseURI atributo)</span><span class="sxs-lookup"><span data-stu-id="045f6-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="045f6-156">Um nutshell, Olá CSDL representa um contrato e idiomas-independentes da plataforma entre o requerente do serviço de Olá e fornecedor de serviços de Olá.</span><span class="sxs-lookup"><span data-stu-id="045f6-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="045f6-157">Utilizar Olá CSDL, um cliente pode localizar um serviço de base de dados/serviço web e invocar qualquer uma das respetivas funções publicamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="045f6-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="045f6-158">Relacionado com uma base de dados de tooa CSDL ou uma coleção</span><span class="sxs-lookup"><span data-stu-id="045f6-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="045f6-159">**Olá especificação CSDL**</span><span class="sxs-lookup"><span data-stu-id="045f6-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="045f6-160">CSDL é a gramática XML para que descrevem um serviço web.</span><span class="sxs-lookup"><span data-stu-id="045f6-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="045f6-161">especificação de Olá propriamente dito está dividida em 4 elementos principais: EntitySet, FunctionImport; Espaço de nomes e EntityType.</span><span class="sxs-lookup"><span data-stu-id="045f6-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="045f6-162">toomake este toounderstand mais fácil de abstração permite referem-se de uma tabela de tooa CSDL.</span><span class="sxs-lookup"><span data-stu-id="045f6-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="045f6-163">Lembre-se;</span><span class="sxs-lookup"><span data-stu-id="045f6-163">Remember;</span></span>

  <span data-ttu-id="045f6-164">CSDL representa um contrato e idiomas-independentes da plataforma entre Olá **requerente serviço** e Olá **fornecedor de serviços**.</span><span class="sxs-lookup"><span data-stu-id="045f6-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="045f6-165">Utilizar CSDL, um **cliente** possam localizar um **serviço de base de dados/serviço web** e invocar qualquer um dos respetivos publicamente disponíveis **funções.**</span><span class="sxs-lookup"><span data-stu-id="045f6-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="045f6-166">Para um Olá do serviço de dados quatro partes de um CSDL podem considerar em termos de uma base de dados, tabela, coluna e de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="045f6-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="045f6-167">Relacionadas com estes da seguinte forma para um serviço de dados:</span><span class="sxs-lookup"><span data-stu-id="045f6-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="045f6-168">EntityContainer ~ = base de dados</span><span class="sxs-lookup"><span data-stu-id="045f6-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="045f6-169">EntitySet ~ = tabela</span><span class="sxs-lookup"><span data-stu-id="045f6-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="045f6-170">EntityType ~ = colunas</span><span class="sxs-lookup"><span data-stu-id="045f6-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="045f6-171">FunctionImport ~ = procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="045f6-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="045f6-172">**Verbos HTTP permitidos**</span><span class="sxs-lookup"><span data-stu-id="045f6-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="045f6-173">GET-devolve valores da base de dados de Olá (devolve um conjunto)</span><span class="sxs-lookup"><span data-stu-id="045f6-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="045f6-174">POST – utilizado toopass dados tooand opcional valores de retorno da base de dados Olá (criar uma nova entrada de coleção de Olá, id de retorno/URI)</span><span class="sxs-lookup"><span data-stu-id="045f6-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="045f6-175">ELIMINAR – elimina dados de Olá BD (elimina uma coleção)</span><span class="sxs-lookup"><span data-stu-id="045f6-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="045f6-176">COLOCAR – atualizar os dados para uma base de dados (substituir uma coleção ou crie um)</span><span class="sxs-lookup"><span data-stu-id="045f6-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="045f6-177">Documento de metadados/mapeamento</span><span class="sxs-lookup"><span data-stu-id="045f6-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="045f6-178">documento de metadados/mapeamento Olá é utilizado toomap serviços web de existente de um fornecedor de conteúdos, para que pode ser exposta como um serviço web OData pelo sistema do Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="045f6-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="045f6-179">Se baseia no CSDL e implementa algumas extensões tooCSDL tooaccommodate Olá necessidades de REST com base em serviços web expostos através do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="045f6-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="045f6-180">extensões de Olá encontram Olá [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="045f6-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="045f6-181">Segue-se um exemplo de Olá CSDL: (copiar e colar Olá abaixo exemplo CSDL para um editor de XML e alterar toomatch seu serviço.</span><span class="sxs-lookup"><span data-stu-id="045f6-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="045f6-182">Em seguida, cole CSDL mapeamento em DataService separador ao criar o seu serviço na Olá [Portal de publicação do Azure Marketplace](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="045f6-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="045f6-183">**Termos de licenciamento:** Relating Olá CSDL termos toohello [Portal publicação](https://publish.windowsazure.com) termos de IU (PPUI).</span><span class="sxs-lookup"><span data-stu-id="045f6-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="045f6-184">Oferecer "Title" Olá PPUI está relacionada com tooMyWebOffer</span><span class="sxs-lookup"><span data-stu-id="045f6-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="045f6-185">Aminhaempresa no Olá PPUI está relacionada com demasiado**nome a apresentar do publicador** no Olá [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) IU</span><span class="sxs-lookup"><span data-stu-id="045f6-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="045f6-186">A API está relacionada com tooa Web ou serviço de dados (um plano Olá PPUI)</span><span class="sxs-lookup"><span data-stu-id="045f6-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="045f6-187">**Hierarquia:** Offer(s) que têm Plan(s) é proprietário de uma empresa (fornecedor de conteúdos), nomeadamente service(s), que linha cópias de segurança com uma API.</span><span class="sxs-lookup"><span data-stu-id="045f6-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="045f6-188">Exemplo de WebService CSDL</span><span class="sxs-lookup"><span data-stu-id="045f6-188">WebService CSDL Example</span></span>
<span data-ttu-id="045f6-189">Estabelece ligação tooa serviço que está a expor um ponto final da aplicação web (por exemplo, uma aplicação c#)</span><span class="sxs-lookup"><span data-stu-id="045f6-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="045f6-190">Ver mais exemplos de serviço Web de CSDL artigo Olá [exemplos de mapeamento existente web tooOData de serviço através de CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="045f6-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="045f6-191">Exemplo de DataService CSDL</span><span class="sxs-lookup"><span data-stu-id="045f6-191">DataService CSDL Example</span></span>
<span data-ttu-id="045f6-192">Liga ao serviço de tooa que está a expor uma base de dados tabela ou vista como um ponto final de exemplo abaixo mostra duas APIs para a base de dados com base em CSDL de API (pode utilizar vistas em vez de tabelas).</span><span class="sxs-lookup"><span data-stu-id="045f6-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="045f6-193">Veja Também</span><span class="sxs-lookup"><span data-stu-id="045f6-193">See Also</span></span>
* <span data-ttu-id="045f6-194">Se estiver interessado em learning e nós específicos de Olá compreender e os respetivos parâmetros, leia este artigo [dados serviço OData mapeamento de nós](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para definições e uma explicação, exemplos e contexto de cenários de utilização.</span><span class="sxs-lookup"><span data-stu-id="045f6-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="045f6-195">Se estiver interessado em rever exemplos, leia este artigo [dados serviço OData mapeamento exemplos](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de exemplo e compreender a sintaxe de código e o contexto.</span><span class="sxs-lookup"><span data-stu-id="045f6-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="045f6-196">toohello tooreturn prescrita caminho para a publicação de um toohello de serviço de dados do Azure Marketplace, leia este artigo [dados serviço de publicação guia](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="045f6-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

