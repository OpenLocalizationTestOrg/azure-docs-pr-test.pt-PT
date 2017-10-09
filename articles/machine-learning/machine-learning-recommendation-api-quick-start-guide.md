---
title: "Início rápido: Azure recomendações API do Machine Learning (ver. 1) | Microsoft Docs"
description: "Do Azure Machine Learning recomendações - guia de introdução"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="0c060-104">Guia de introdução para Olá API do Machine Learning recomendações (versão 1)</span><span class="sxs-lookup"><span data-stu-id="0c060-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="0c060-105">Deve começar a utilizar Olá [recomendações API cognitivos serviço](https://www.microsoft.com/cognitive-services/recommendations-api) em vez de nesta versão.</span><span class="sxs-lookup"><span data-stu-id="0c060-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="0c060-106">Olá serviço cognitivos recomendações irá substituir este serviço e todas as novas funcionalidades de Olá irão ser desenvolvidas não existe.</span><span class="sxs-lookup"><span data-stu-id="0c060-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="0c060-107">Tem novas capacidades, como a criação de batches de suporte, melhor Explorador de API, uma experiência de inscrição/faturação superfície, mais consistente de API limpeza, etc.</span><span class="sxs-lookup"><span data-stu-id="0c060-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="0c060-108">Saiba mais sobre [migrar toohello novo serviço cognitivos](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="0c060-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="0c060-109">Este documento descreve como tooonboard toouse a aplicação ou serviço Microsoft Azure Machine Learning recomendações.</span><span class="sxs-lookup"><span data-stu-id="0c060-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="0c060-110">Pode encontrar mais detalhes sobre Olá API de recomendações na Olá [galeria da Cortana Intelligence](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="0c060-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="0c060-111">Descrição geral do geral</span><span class="sxs-lookup"><span data-stu-id="0c060-111">General overview</span></span>
<span data-ttu-id="0c060-112">toouse recomendações do Azure Machine Learning, terá de Olá tootake os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0c060-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="0c060-113">Criar um modelo - um modelo é um contentor dos seus dados de utilização, dados do catálogo e modelo de recomendação Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="0c060-114">Importar dados de catálogo - um catálogo contém informações de metadados em itens de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="0c060-115">Importar dados de utilização - dados de utilização podem ser carregados uma de duas formas (ou ambos):</span><span class="sxs-lookup"><span data-stu-id="0c060-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="0c060-116">Através do carregamento de um ficheiro que contém dados de utilização de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="0c060-117">Através do envio de eventos de aquisição de dados.</span><span class="sxs-lookup"><span data-stu-id="0c060-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="0c060-118">Normalmente, pode carregar um ficheiro de utilização na ordem toobe capaz de toocreate um modelo de recomendação inicial (arranque de configuração) e utilizá-lo até que o sistema de Olá reúne dados suficientes utilizando o formato de aquisição de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="0c060-119">Criar um modelo de recomendação - esta é uma operação assíncrona no qual Olá sistema recomendação demora todos os dados de utilização de Olá e cria um modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="0c060-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="0c060-120">Esta operação pode demorar alguns minutos ou várias horas, consoante Olá tamanho dos dados de Olá e Olá compilar parâmetros de configuração.</span><span class="sxs-lookup"><span data-stu-id="0c060-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="0c060-121">Quando a acionar a compilação de Olá, receberá um ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="0c060-122">Utilizá-lo toocheck quando o processo de compilação de Olá terminou antes de iniciar tooconsume recomendações.</span><span class="sxs-lookup"><span data-stu-id="0c060-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="0c060-123">Consuma recomendações - Get recomendações para um item específico ou a lista de itens.</span><span class="sxs-lookup"><span data-stu-id="0c060-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="0c060-124">Todos os passos de Olá acima são efetuados através de Olá API do Azure Machine Learning recomendações.</span><span class="sxs-lookup"><span data-stu-id="0c060-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="0c060-125">Pode transferir uma aplicação de exemplo que implementa cada um destes passos de Olá [Galeria bem.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="0c060-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="0c060-126">Limitações</span><span class="sxs-lookup"><span data-stu-id="0c060-126">Limitations</span></span>
* <span data-ttu-id="0c060-127">Olá número máximo de modelos por subscrição é 10.</span><span class="sxs-lookup"><span data-stu-id="0c060-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="0c060-128">Olá o número máximo de itens que pode conter um catálogo é 100 000.</span><span class="sxs-lookup"><span data-stu-id="0c060-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="0c060-129">número máximo de Olá de pontos de utilização que são mantidos é ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="0c060-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="0c060-130">Olá mais antigo será eliminado se novos serão carregados ou comunicados.</span><span class="sxs-lookup"><span data-stu-id="0c060-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="0c060-131">tamanho máximo do Olá dos dados que podem ser enviados em POST (por exemplo, importar dados do catálogo, importar dados de utilização) é 200MB.</span><span class="sxs-lookup"><span data-stu-id="0c060-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="0c060-132">Olá número de transações por segundo para uma compilação de modelo de recomendação que não está ativa é ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="0c060-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="0c060-133">Uma compilação de modelo de recomendação está ativa pode manter cópias de segurança too20TPS.</span><span class="sxs-lookup"><span data-stu-id="0c060-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="0c060-134">Integração</span><span class="sxs-lookup"><span data-stu-id="0c060-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="0c060-135">Autenticação</span><span class="sxs-lookup"><span data-stu-id="0c060-135">Authentication</span></span>
<span data-ttu-id="0c060-136">Microsoft Azure Marketplace suporta qualquer um dos Olá método de autenticação básica ou de OAuth.</span><span class="sxs-lookup"><span data-stu-id="0c060-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="0c060-137">Pode localizar facilmente Olá chaves de conta, navegando toohello chaves no marketplace, Olá em [definições da sua conta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="0c060-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="0c060-138">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="0c060-138">Basic Authentication</span></span>
<span data-ttu-id="0c060-139">Adicione cabeçalho de autorização de Olá:</span><span class="sxs-lookup"><span data-stu-id="0c060-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="0c060-140">Converter tooBase64 (c#)</span><span class="sxs-lookup"><span data-stu-id="0c060-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="0c060-141">Converter tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="0c060-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="0c060-142">URI do serviço</span><span class="sxs-lookup"><span data-stu-id="0c060-142">Service URI</span></span>
<span data-ttu-id="0c060-143">URI de raiz de serviço Olá para Olá recomendações APIs do Azure Machine Learning é [aqui.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="0c060-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="0c060-144">URI do serviço completo Olá é expresso utilizando os elementos de especificação do OData Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="0c060-145">Versão de API</span><span class="sxs-lookup"><span data-stu-id="0c060-145">API version</span></span>
<span data-ttu-id="0c060-146">Cada chamada à API será de ter, no final de Olá, um parâmetro de consulta denominado apiVersion que deve ser definido demasiado "1.0".</span><span class="sxs-lookup"><span data-stu-id="0c060-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="0c060-147">Os iDs de são sensíveis a maiúsculas</span><span class="sxs-lookup"><span data-stu-id="0c060-147">IDs are case-sensitive</span></span>
<span data-ttu-id="0c060-148">IDs, devolvidos por qualquer um dos Olá APIs, são maiúsculas e minúsculas e devem ser utilizados como tal, ao transmitido como parâmetros subsequentes chamadas de API.</span><span class="sxs-lookup"><span data-stu-id="0c060-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="0c060-149">Por exemplo, IDs de modelo e os IDs de catálogo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0c060-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="0c060-150">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="0c060-150">Create a model</span></span>
<span data-ttu-id="0c060-151">Criar um pedido de "Criar modelo de":</span><span class="sxs-lookup"><span data-stu-id="0c060-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="0c060-152">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-152">HTTP Method</span></span> | <span data-ttu-id="0c060-153">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-154">POST</span><span class="sxs-lookup"><span data-stu-id="0c060-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-155">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-156">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-156">Parameter Name</span></span> | <span data-ttu-id="0c060-157">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-158">modelName</span><span class="sxs-lookup"><span data-stu-id="0c060-158">modelName</span></span> |<span data-ttu-id="0c060-159">Apenas letras (A-Z, a-z), números (0-9), hífenes (-) e caráter de sublinhado (_) são permitidos.</span><span class="sxs-lookup"><span data-stu-id="0c060-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="0c060-160">Comprimento máximo: 20</span><span class="sxs-lookup"><span data-stu-id="0c060-160">Max length: 20</span></span> |
| <span data-ttu-id="0c060-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-161">apiVersion</span></span> |<span data-ttu-id="0c060-162">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-162">1.0</span></span> |
|  | |
| <span data-ttu-id="0c060-163">Corpo do Pedido</span><span class="sxs-lookup"><span data-stu-id="0c060-163">Request Body</span></span> |<span data-ttu-id="0c060-164">NENHUM</span><span class="sxs-lookup"><span data-stu-id="0c060-164">NONE</span></span> |

<span data-ttu-id="0c060-165">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="0c060-165">**Response**:</span></span>

<span data-ttu-id="0c060-166">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="0c060-167">`feed/entry/content/properties/id`-Contém o ID de modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="0c060-168">Tenha em atenção que o ID de modelo de Olá maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0c060-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="0c060-169">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="0c060-170">Importar dados de catálogo</span><span class="sxs-lookup"><span data-stu-id="0c060-170">Import catalog data</span></span>
<span data-ttu-id="0c060-171">Se carregar várias catálogo ficheiros toohello mesmo modelo com várias chamadas, iremos irá inserir apenas Olá novos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="0c060-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="0c060-172">Itens existentes permanecerá com valores originais Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="0c060-173">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-173">HTTP Method</span></span> | <span data-ttu-id="0c060-174">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-175">POST</span><span class="sxs-lookup"><span data-stu-id="0c060-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-176">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-177">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-177">Parameter Name</span></span> | <span data-ttu-id="0c060-178">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-179">modelId</span><span class="sxs-lookup"><span data-stu-id="0c060-179">modelId</span></span> |<span data-ttu-id="0c060-180">Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="0c060-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="0c060-181">nome de ficheiro</span><span class="sxs-lookup"><span data-stu-id="0c060-181">filename</span></span> |<span data-ttu-id="0c060-182">Identificador de textual do catálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="0c060-183">Apenas letras (A-Z, a-z), números (0-9), hífenes (-) e caráter de sublinhado (_) são permitidos.</span><span class="sxs-lookup"><span data-stu-id="0c060-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="0c060-184">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="0c060-184">Max length: 50</span></span> |
| <span data-ttu-id="0c060-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-185">apiVersion</span></span> |<span data-ttu-id="0c060-186">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-186">1.0</span></span> |
|  | |
| <span data-ttu-id="0c060-187">Corpo do Pedido</span><span class="sxs-lookup"><span data-stu-id="0c060-187">Request Body</span></span> |<span data-ttu-id="0c060-188">Catálogo de dados.</span><span class="sxs-lookup"><span data-stu-id="0c060-188">Catalog data.</span></span> <span data-ttu-id="0c060-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="0c060-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="0c060-190">Nome</span><span class="sxs-lookup"><span data-stu-id="0c060-190">Name</span></span></th><th><span data-ttu-id="0c060-191">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0c060-191">Mandatory</span></span></th><th><span data-ttu-id="0c060-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="0c060-192">Type</span></span></th><th><span data-ttu-id="0c060-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c060-193">Description</span></span></th></tr><tr><td><span data-ttu-id="0c060-194">Id do item</span><span class="sxs-lookup"><span data-stu-id="0c060-194">Item Id</span></span></td><td><span data-ttu-id="0c060-195">Sim</span><span class="sxs-lookup"><span data-stu-id="0c060-195">Yes</span></span></td><td><span data-ttu-id="0c060-196">Comprimento máximo, alfanumérico 50</span><span class="sxs-lookup"><span data-stu-id="0c060-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="0c060-197">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="0c060-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="0c060-198">Nome do item</span><span class="sxs-lookup"><span data-stu-id="0c060-198">Item Name</span></span></td><td><span data-ttu-id="0c060-199">Sim</span><span class="sxs-lookup"><span data-stu-id="0c060-199">Yes</span></span></td><td><span data-ttu-id="0c060-200">Comprimento máximo, alfanumérico 255</span><span class="sxs-lookup"><span data-stu-id="0c060-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="0c060-201">Nome do item</span><span class="sxs-lookup"><span data-stu-id="0c060-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="0c060-202">Categoria do item</span><span class="sxs-lookup"><span data-stu-id="0c060-202">Item Category</span></span></td><td><span data-ttu-id="0c060-203">Sim</span><span class="sxs-lookup"><span data-stu-id="0c060-203">Yes</span></span></td><td><span data-ttu-id="0c060-204">Comprimento máximo, alfanumérico 255</span><span class="sxs-lookup"><span data-stu-id="0c060-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="0c060-205">Toowhich categoria que este item pertence (por exemplo, Cooking Books, Drama...)</span><span class="sxs-lookup"><span data-stu-id="0c060-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="0c060-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c060-206">Description</span></span></td><td><span data-ttu-id="0c060-207">Não</span><span class="sxs-lookup"><span data-stu-id="0c060-207">No</span></span></td><td><span data-ttu-id="0c060-208">Comprimento máximo, alfanumérico 4000</span><span class="sxs-lookup"><span data-stu-id="0c060-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="0c060-209">Descrição deste item</span><span class="sxs-lookup"><span data-stu-id="0c060-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="0c060-210">Tamanho máximo do ficheiro é de 200MB.</span><span class="sxs-lookup"><span data-stu-id="0c060-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="0c060-211">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="0c060-212">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="0c060-212">**Response**:</span></span>

<span data-ttu-id="0c060-213">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="0c060-214">`Feed\entry\content\properties\LineCount`-Aceite número de linhas.</span><span class="sxs-lookup"><span data-stu-id="0c060-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="0c060-215">`Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridos devido a erro de tooan.</span><span class="sxs-lookup"><span data-stu-id="0c060-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="0c060-216">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="0c060-217">Importar dados de utilização</span><span class="sxs-lookup"><span data-stu-id="0c060-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="0c060-218">Carregar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="0c060-218">Uploading a file</span></span>
<span data-ttu-id="0c060-219">Esta secção mostra como dados de utilização de tooupload utilizando um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="0c060-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="0c060-220">Pode chamar esta API várias vezes com dados de utilização.</span><span class="sxs-lookup"><span data-stu-id="0c060-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="0c060-221">Todos os dados de utilização serão guardados para todas as chamadas.</span><span class="sxs-lookup"><span data-stu-id="0c060-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="0c060-222">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-222">HTTP Method</span></span> | <span data-ttu-id="0c060-223">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-224">POST</span><span class="sxs-lookup"><span data-stu-id="0c060-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-225">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-226">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-226">Parameter Name</span></span> | <span data-ttu-id="0c060-227">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-228">modelId</span><span class="sxs-lookup"><span data-stu-id="0c060-228">modelId</span></span> |<span data-ttu-id="0c060-229">Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="0c060-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="0c060-230">nome de ficheiro</span><span class="sxs-lookup"><span data-stu-id="0c060-230">filename</span></span> |<span data-ttu-id="0c060-231">Identificador de textual do catálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="0c060-232">Apenas letras (A-Z, a-z), números (0-9), hífenes (-) e caráter de sublinhado (_) são permitidos.</span><span class="sxs-lookup"><span data-stu-id="0c060-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="0c060-233">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="0c060-233">Max length: 50</span></span> |
| <span data-ttu-id="0c060-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-234">apiVersion</span></span> |<span data-ttu-id="0c060-235">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-235">1.0</span></span> |
|  | |
| <span data-ttu-id="0c060-236">Corpo do Pedido</span><span class="sxs-lookup"><span data-stu-id="0c060-236">Request Body</span></span> |<span data-ttu-id="0c060-237">Dados de utilização.</span><span class="sxs-lookup"><span data-stu-id="0c060-237">Usage data.</span></span> <span data-ttu-id="0c060-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="0c060-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="0c060-239">Nome</span><span class="sxs-lookup"><span data-stu-id="0c060-239">Name</span></span></th><th><span data-ttu-id="0c060-240">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0c060-240">Mandatory</span></span></th><th><span data-ttu-id="0c060-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="0c060-241">Type</span></span></th><th><span data-ttu-id="0c060-242">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c060-242">Description</span></span></th></tr><tr><td><span data-ttu-id="0c060-243">Id de utilizador</span><span class="sxs-lookup"><span data-stu-id="0c060-243">User Id</span></span></td><td><span data-ttu-id="0c060-244">Sim</span><span class="sxs-lookup"><span data-stu-id="0c060-244">Yes</span></span></td><td><span data-ttu-id="0c060-245">Alfanumérica</span><span class="sxs-lookup"><span data-stu-id="0c060-245">Alphanumeric</span></span></td><td><span data-ttu-id="0c060-246">Identificador exclusivo de um utilizador</span><span class="sxs-lookup"><span data-stu-id="0c060-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="0c060-247">Id do item</span><span class="sxs-lookup"><span data-stu-id="0c060-247">Item Id</span></span></td><td><span data-ttu-id="0c060-248">Sim</span><span class="sxs-lookup"><span data-stu-id="0c060-248">Yes</span></span></td><td><span data-ttu-id="0c060-249">Comprimento máximo, alfanumérico 50</span><span class="sxs-lookup"><span data-stu-id="0c060-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="0c060-250">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="0c060-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="0c060-251">Hora</span><span class="sxs-lookup"><span data-stu-id="0c060-251">Time</span></span></td><td><span data-ttu-id="0c060-252">Não</span><span class="sxs-lookup"><span data-stu-id="0c060-252">No</span></span></td><td><span data-ttu-id="0c060-253">Data no formato: aaaa/MM/ddTHH (por exemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="0c060-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="0c060-254">Hora de dados</span><span class="sxs-lookup"><span data-stu-id="0c060-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="0c060-255">Evento</span><span class="sxs-lookup"><span data-stu-id="0c060-255">Event</span></span></td><td><span data-ttu-id="0c060-256">Não, se for fornecido, em seguida, também deve colocar data</span><span class="sxs-lookup"><span data-stu-id="0c060-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="0c060-257">Um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="0c060-257">One of hello following:</span></span><br><span data-ttu-id="0c060-258">• Clique</span><span class="sxs-lookup"><span data-stu-id="0c060-258">• Click</span></span><br><span data-ttu-id="0c060-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="0c060-259">• RecommendationClick</span></span><br><span data-ttu-id="0c060-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="0c060-260">•    AddShopCart</span></span><br><span data-ttu-id="0c060-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="0c060-261">• RemoveShopCart</span></span><br><span data-ttu-id="0c060-262">• Compra</span><span class="sxs-lookup"><span data-stu-id="0c060-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="0c060-263">Tamanho máximo do ficheiro é de 200MB.</span><span class="sxs-lookup"><span data-stu-id="0c060-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="0c060-264">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="0c060-265">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="0c060-265">**Response**:</span></span>

<span data-ttu-id="0c060-266">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="0c060-267">`Feed\entry\content\properties\LineCount`-Aceite número de linhas.</span><span class="sxs-lookup"><span data-stu-id="0c060-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="0c060-268">`Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridos devido a erro de tooan.</span><span class="sxs-lookup"><span data-stu-id="0c060-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="0c060-269">`Feed\entry\content\properties\FileId`-Identificador do ficheiro.</span><span class="sxs-lookup"><span data-stu-id="0c060-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="0c060-270">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="0c060-271">Utilizar a aquisição de dados</span><span class="sxs-lookup"><span data-stu-id="0c060-271">Using data acquisition</span></span>
<span data-ttu-id="0c060-272">Esta secção mostra como eventos toosend real tempo tooAzure Machine Learning as recomendações, normalmente, a partir do seu Web site.</span><span class="sxs-lookup"><span data-stu-id="0c060-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="0c060-273">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-273">HTTP Method</span></span> | <span data-ttu-id="0c060-274">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-275">POST</span><span class="sxs-lookup"><span data-stu-id="0c060-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-276">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-276">Parameter Name</span></span> | <span data-ttu-id="0c060-277">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-278">apiVersion</span></span> |<span data-ttu-id="0c060-279">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-279">1.0</span></span> |
|  | |
| <span data-ttu-id="0c060-280">Corpo do pedido</span><span class="sxs-lookup"><span data-stu-id="0c060-280">Request body</span></span> |<span data-ttu-id="0c060-281">Entrada de dados de eventos para cada evento pretende toosend.</span><span class="sxs-lookup"><span data-stu-id="0c060-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="0c060-282">Deve enviar para hello mesma sessão de utilizador ou browser Olá mesmo ID no campo de SessionId Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="0c060-283">(Consulte o exemplo de corpo de evento abaixo).</span><span class="sxs-lookup"><span data-stu-id="0c060-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="0c060-284">Exemplo para o evento 'Clique':</span><span class="sxs-lookup"><span data-stu-id="0c060-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="0c060-285">Exemplo para o evento 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="0c060-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="0c060-286">Exemplo para o evento 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="0c060-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="0c060-287">Exemplo para o evento 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="0c060-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="0c060-288">Exemplo para o evento 'Compra':</span><span class="sxs-lookup"><span data-stu-id="0c060-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="0c060-289">Exemplo a enviar 2 eventos, 'clique em' e 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="0c060-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="0c060-290">**Resposta**: código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="0c060-291">Criar um modelo de recomendação</span><span class="sxs-lookup"><span data-stu-id="0c060-291">Build a recommendation model</span></span>
| <span data-ttu-id="0c060-292">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-292">HTTP Method</span></span> | <span data-ttu-id="0c060-293">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-294">POST</span><span class="sxs-lookup"><span data-stu-id="0c060-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-295">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-296">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-296">Parameter Name</span></span> | <span data-ttu-id="0c060-297">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-298">modelId</span><span class="sxs-lookup"><span data-stu-id="0c060-298">modelId</span></span> |<span data-ttu-id="0c060-299">Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="0c060-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="0c060-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="0c060-300">userDescription</span></span> |<span data-ttu-id="0c060-301">Identificador de textual do catálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="0c060-302">Tenha em atenção que se utilizar os espaços de tem codificá-lo com o % 20 em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0c060-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="0c060-303">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="0c060-303">See example above.</span></span><br><span data-ttu-id="0c060-304">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="0c060-304">Max length: 50</span></span> |
| <span data-ttu-id="0c060-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-305">apiVersion</span></span> |<span data-ttu-id="0c060-306">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-306">1.0</span></span> |
|  | |
| <span data-ttu-id="0c060-307">Corpo do Pedido</span><span class="sxs-lookup"><span data-stu-id="0c060-307">Request Body</span></span> |<span data-ttu-id="0c060-308">NENHUM</span><span class="sxs-lookup"><span data-stu-id="0c060-308">NONE</span></span> |

<span data-ttu-id="0c060-309">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="0c060-309">**Response**:</span></span>

<span data-ttu-id="0c060-310">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-310">HTTP Status code: 200</span></span>

<span data-ttu-id="0c060-311">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="0c060-311">This is an asynchronous API.</span></span> <span data-ttu-id="0c060-312">Irá obter um ID de compilação como resposta.</span><span class="sxs-lookup"><span data-stu-id="0c060-312">You will get a build ID as a response.</span></span> <span data-ttu-id="0c060-313">tooknow quando terminou compilação Olá, deve chamar a API de "Obter compilações do Estado de um modelo" Olá e localizar este ID de compilação na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="0c060-314">Tenha em atenção que uma compilação pode demorar entre toohours minutos consoante o tamanho dos dados de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="0c060-315">Não é possível consumir recomendações até Olá criar termina.</span><span class="sxs-lookup"><span data-stu-id="0c060-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="0c060-316">Estado de compilação válido:</span><span class="sxs-lookup"><span data-stu-id="0c060-316">Valid build status:</span></span>

* <span data-ttu-id="0c060-317">Criar – modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="0c060-317">Create – Model was created.</span></span>
* <span data-ttu-id="0c060-318">Em fila – compilação do modelo foi acionada e é colocada na fila.</span><span class="sxs-lookup"><span data-stu-id="0c060-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="0c060-319">Edifício – modelo está a ser criado.</span><span class="sxs-lookup"><span data-stu-id="0c060-319">Building – Model is being built.</span></span>
* <span data-ttu-id="0c060-320">Êxito – compilação terminada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0c060-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="0c060-321">Erro-compilação terminou com uma falha.</span><span class="sxs-lookup"><span data-stu-id="0c060-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="0c060-322">Compilação cancelada – foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="0c060-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="0c060-323">Cancelar – compilação que está a ser cancelada.</span><span class="sxs-lookup"><span data-stu-id="0c060-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="0c060-324">Tenha em atenção que compilação Olá que ID pode ser encontrado em Olá seguinte caminho:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="0c060-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="0c060-325">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="0c060-326">Obter o estado de compilação de um modelo</span><span class="sxs-lookup"><span data-stu-id="0c060-326">Get build status of a model</span></span>
| <span data-ttu-id="0c060-327">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-327">HTTP Method</span></span> | <span data-ttu-id="0c060-328">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-329">INTRODUÇÃO</span><span class="sxs-lookup"><span data-stu-id="0c060-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-330">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-331">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-331">Parameter Name</span></span> | <span data-ttu-id="0c060-332">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-333">modelId</span><span class="sxs-lookup"><span data-stu-id="0c060-333">modelId</span></span> |<span data-ttu-id="0c060-334">Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="0c060-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="0c060-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="0c060-335">onlyLastBuild</span></span> |<span data-ttu-id="0c060-336">Indica se o tooreturn todas Olá criar histórico do modelo de Olá ou apenas Olá estado de compilação mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="0c060-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-337">apiVersion</span></span> |<span data-ttu-id="0c060-338">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-338">1.0</span></span> |

<span data-ttu-id="0c060-339">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="0c060-339">**Response**:</span></span>

<span data-ttu-id="0c060-340">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-340">HTTP Status code: 200</span></span>

<span data-ttu-id="0c060-341">resposta Olá inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-341">hello response includes one entry per build.</span></span> <span data-ttu-id="0c060-342">Cada entrada tem Olá dados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0c060-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="0c060-343">`feed/entry/content/properties/UserName`– O nome de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="0c060-344">`feed/entry/content/properties/ModelName`– O nome do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="0c060-345">`feed/entry/content/properties/ModelId`– Identificador exclusivo modelo.</span><span class="sxs-lookup"><span data-stu-id="0c060-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="0c060-346">`feed/entry/content/properties/IsDeployed`– Indica se a compilação de Olá é implementada (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="0c060-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="0c060-347">compilação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0c060-347">active build).</span></span>
* <span data-ttu-id="0c060-348">`feed/entry/content/properties/BuildId`– Crie Identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0c060-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="0c060-349">`feed/entry/content/properties/BuildType`-Tipo de compilação de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="0c060-350">`feed/entry/content/properties/Status`– Estado de compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="0c060-351">Pode ser um dos seguintes Olá: erro de criação, em fila, Canceling, cancelado, êxito</span><span class="sxs-lookup"><span data-stu-id="0c060-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="0c060-352">`feed/entry/content/properties/StatusMessage`– Mensagem de estado detalhado (aplica-se apenas toospecific Estados).</span><span class="sxs-lookup"><span data-stu-id="0c060-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="0c060-353">`feed/entry/content/properties/Progress`– Crie progresso (%).</span><span class="sxs-lookup"><span data-stu-id="0c060-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="0c060-354">`feed/entry/content/properties/StartTime`– Hora de início de compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="0c060-355">`feed/entry/content/properties/EndTime`– Hora de fim de compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="0c060-356">`feed/entry/content/properties/ExecutionTime`– Crie duração.</span><span class="sxs-lookup"><span data-stu-id="0c060-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="0c060-357">`feed/entry/content/properties/ProgressStep`– Detalhes sobre a fase de atual Olá que está a ser uma compilação em curso.</span><span class="sxs-lookup"><span data-stu-id="0c060-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="0c060-358">Estado de compilação válido:</span><span class="sxs-lookup"><span data-stu-id="0c060-358">Valid build status:</span></span>

* <span data-ttu-id="0c060-359">Criado – foi criada a entrada de pedido de compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="0c060-360">Em fila – compilação pedido foi acionado e é colocada na fila.</span><span class="sxs-lookup"><span data-stu-id="0c060-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="0c060-361">Edifício – compilação está em curso.</span><span class="sxs-lookup"><span data-stu-id="0c060-361">Building – Build is in process.</span></span>
* <span data-ttu-id="0c060-362">Êxito – compilação terminada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0c060-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="0c060-363">Erro-compilação terminou com uma falha.</span><span class="sxs-lookup"><span data-stu-id="0c060-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="0c060-364">Compilação cancelada – foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="0c060-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="0c060-365">Cancelar – compilação que está a ser cancelada.</span><span class="sxs-lookup"><span data-stu-id="0c060-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="0c060-366">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="0c060-366">Valid values for build type:</span></span>

* <span data-ttu-id="0c060-367">Classificação - a posição da compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-367">Rank - Rank build.</span></span> <span data-ttu-id="0c060-368">(Para a posição da compilação detalhes, consulte o documento de "Documentação de Machine Learning recomendação API" toohello.)</span><span class="sxs-lookup"><span data-stu-id="0c060-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="0c060-369">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="0c060-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="0c060-370">Fbt - comprou com frequência, em conjunto compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="0c060-371">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="0c060-372">Obtenha recomendações</span><span class="sxs-lookup"><span data-stu-id="0c060-372">Get recommendations</span></span>
| <span data-ttu-id="0c060-373">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-373">HTTP Method</span></span> | <span data-ttu-id="0c060-374">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-375">INTRODUÇÃO</span><span class="sxs-lookup"><span data-stu-id="0c060-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-376">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-377">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-377">Parameter Name</span></span> | <span data-ttu-id="0c060-378">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-379">modelId</span><span class="sxs-lookup"><span data-stu-id="0c060-379">modelId</span></span> |<span data-ttu-id="0c060-380">Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="0c060-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="0c060-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="0c060-381">itemIds</span></span> |<span data-ttu-id="0c060-382">Lista separada por vírgulas de Olá itens toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="0c060-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="0c060-383">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="0c060-383">Max length: 1024</span></span> |
| <span data-ttu-id="0c060-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0c060-384">numberOfResults</span></span> |<span data-ttu-id="0c060-385">Número de resultados necessários</span><span class="sxs-lookup"><span data-stu-id="0c060-385">Number of required results</span></span> |
| <span data-ttu-id="0c060-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0c060-386">includeMetatadata</span></span> |<span data-ttu-id="0c060-387">Utilização futura, sempre falsa</span><span class="sxs-lookup"><span data-stu-id="0c060-387">Future use, always false</span></span> |
| <span data-ttu-id="0c060-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-388">apiVersion</span></span> |<span data-ttu-id="0c060-389">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-389">1.0</span></span> |

<span data-ttu-id="0c060-390">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="0c060-390">**Response:**</span></span>

<span data-ttu-id="0c060-391">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-391">HTTP Status code: 200</span></span>

<span data-ttu-id="0c060-392">resposta Olá inclui uma entrada por item recomendada.</span><span class="sxs-lookup"><span data-stu-id="0c060-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="0c060-393">Cada entrada tem Olá dados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0c060-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="0c060-394">`Feed\entry\content\properties\Id`-ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="0c060-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0c060-395">`Feed\entry\content\properties\Name`-Nome do item de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c060-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="0c060-396">`Feed\entry\content\properties\Rating`-Classificação recomendação Olá; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="0c060-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0c060-397">`Feed\entry\content\properties\Reasoning`-Raciocínio recomendação (por exemplo, explicações recomendação).</span><span class="sxs-lookup"><span data-stu-id="0c060-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="0c060-398">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-398">OData XML</span></span>

<span data-ttu-id="0c060-399">resposta de exemplo de Olá abaixo inclui 10 itens recomendados:</span><span class="sxs-lookup"><span data-stu-id="0c060-399">hello example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="0c060-400">Modelo de atualização</span><span class="sxs-lookup"><span data-stu-id="0c060-400">Update model</span></span>
<span data-ttu-id="0c060-401">Pode atualizar a descrição do modelo Olá ou Olá ID de compilação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c060-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="0c060-402">*ID de compilação do Active Directory* -cada compilação para cada modelo tem um ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="0c060-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="0c060-403">ID de compilação do Active Directory Olá é compilação efetuada com êxito primeiro Olá de cada novo modelo.</span><span class="sxs-lookup"><span data-stu-id="0c060-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="0c060-404">Depois de ter um ID de compilação do Active Directory e fazer compilações adicionais para Olá mesmo modelo, terá de tooexplicitly defini-lo como hello predefinido criar ID se pretender.</span><span class="sxs-lookup"><span data-stu-id="0c060-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="0c060-405">Quando consumir recomendações, se não especificar ID de compilação de Olá que pretende que sejam toouse, Olá um será utilizado o predefinido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0c060-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="0c060-406">Este mecanismo permite-lhe - depois de ter um modelo de recomendação em produção - modelos novo toobuild e testá-los antes de promovê-los tooproduction.</span><span class="sxs-lookup"><span data-stu-id="0c060-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="0c060-407">Método de HTTP</span><span class="sxs-lookup"><span data-stu-id="0c060-407">HTTP Method</span></span> | <span data-ttu-id="0c060-408">URI</span><span class="sxs-lookup"><span data-stu-id="0c060-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-409">COLOCAR</span><span class="sxs-lookup"><span data-stu-id="0c060-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0c060-410">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c060-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0c060-411">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0c060-411">Parameter Name</span></span> | <span data-ttu-id="0c060-412">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="0c060-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c060-413">ID</span><span class="sxs-lookup"><span data-stu-id="0c060-413">id</span></span> |<span data-ttu-id="0c060-414">Identificador exclusivo do modelo de Olá (maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="0c060-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="0c060-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0c060-415">apiVersion</span></span> |<span data-ttu-id="0c060-416">1.0</span><span class="sxs-lookup"><span data-stu-id="0c060-416">1.0</span></span> |
|  | |
| <span data-ttu-id="0c060-417">Corpo do Pedido</span><span class="sxs-lookup"><span data-stu-id="0c060-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="0c060-418">Tenha em atenção que a descrição de etiquetas de Olá XML e ActiveBuildId são opcionais.</span><span class="sxs-lookup"><span data-stu-id="0c060-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="0c060-419">Se não pretender tooset descrição ou ActiveBuildId, remova etiqueta Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="0c060-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="0c060-420">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="0c060-420">**Response**:</span></span>

<span data-ttu-id="0c060-421">Código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="0c060-421">HTTP Status code: 200</span></span>

<span data-ttu-id="0c060-422">XML de OData</span><span class="sxs-lookup"><span data-stu-id="0c060-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="0c060-423">Informações Legais</span><span class="sxs-lookup"><span data-stu-id="0c060-423">Legal</span></span>
<span data-ttu-id="0c060-424">Este documento é fornecido "como-é".</span><span class="sxs-lookup"><span data-stu-id="0c060-424">This document is provided "as-is".</span></span> <span data-ttu-id="0c060-425">As informações e opiniões expressados neste documento, incluindo URLs e outras referências de Web site da Internet, podem ser alteradas sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="0c060-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="0c060-426">Alguns exemplos aqui demonstrados são fornecidos para apenas ilustração e são fictícios.</span><span class="sxs-lookup"><span data-stu-id="0c060-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="0c060-427">Nenhuma associação ou ligação é intencional nem deve ser inferida.</span><span class="sxs-lookup"><span data-stu-id="0c060-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="0c060-428">Este documento não fornece-lhe direitos de propriedade intelectual de tooany em qualquer produto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0c060-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="0c060-429">Pode copiar e utilizar este documento interna, para efeitos de consulta.</span><span class="sxs-lookup"><span data-stu-id="0c060-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="0c060-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0c060-430">© 2014 Microsoft.</span></span> <span data-ttu-id="0c060-431">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="0c060-431">All rights reserved.</span></span> 

