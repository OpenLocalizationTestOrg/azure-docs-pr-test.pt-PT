---
title: "aaaGet à Azure Search no Node.js | Microsoft Docs"
description: "Instruções sobre a compilação de uma aplicação de pesquisa num serviço de pesquisa na cloud alojado no Azure utilizando Node.js como linguagem de programação."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="96104-103">Introdução à Azure Search no Node.js</span><span class="sxs-lookup"><span data-stu-id="96104-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96104-104">Portal</span><span class="sxs-lookup"><span data-stu-id="96104-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="96104-105">.NET</span><span class="sxs-lookup"><span data-stu-id="96104-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="96104-106">Saiba como toobuild um Node.js personalizado procure a aplicação que utiliza a Azure Search pela sua experiência de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="96104-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="96104-107">Este tutorial utiliza Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Olá objetos e as operações utilizados neste exercício.</span><span class="sxs-lookup"><span data-stu-id="96104-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="96104-108">Utilizámos [Node.js](https://Nodejs.org) e NPM, [Sublime Text 3](http://www.sublimetext.com/3)e o Windows PowerShell no Windows 8.1 toodevelop e testar este código.</span><span class="sxs-lookup"><span data-stu-id="96104-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="96104-109">toorun neste exemplo, tem de ter um serviço de pesquisa do Azure, pode inscrever-se no Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96104-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="96104-110">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="96104-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="96104-111">Sobre os dados de Olá</span><span class="sxs-lookup"><span data-stu-id="96104-111">About hello data</span></span>
<span data-ttu-id="96104-112">Esta aplicação de exemplo utiliza dados dos Olá [serviços geológicos dos Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)filtrados no tamanho de conjunto de dados do Olá estado da Rhode Island tooreduce Olá.</span><span class="sxs-lookup"><span data-stu-id="96104-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="96104-113">Utilizaremos esta toobuild dados de uma aplicação de pesquisa que devolve edifícios históricos, tais como hospitais e escolas, assim como características funcionalidades, como rios, lagos e cumes.</span><span class="sxs-lookup"><span data-stu-id="96104-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="96104-114">Nesta aplicação, Olá **DataIndexer** programa compila e carrega Olá índice utilizando uma [indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construção, obter Olá filtrado de dados USGS de uma base de dados de SQL pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="96104-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="96104-115">As credenciais e ligação de origem de dados online toohello informações é fornecida no código do programa de Olá.</span><span class="sxs-lookup"><span data-stu-id="96104-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="96104-116">Não é necessária qualquer configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="96104-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="96104-117">Aplicamos um filtro toostay este conjunto de dados no limite de 10 000 documentos Olá de Olá escalão de preço gratuito.</span><span class="sxs-lookup"><span data-stu-id="96104-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="96104-118">Se utilizar o escalão standard Olá, este limite não é aplicável.</span><span class="sxs-lookup"><span data-stu-id="96104-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="96104-119">Para obter detalhes sobre a capacidade para cada escalão de preço, consulte [limites do Serviço de Pesquisa](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="96104-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="96104-120">Localizar o nome do serviço Olá e chave de api do serviço da Azure Search</span><span class="sxs-lookup"><span data-stu-id="96104-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="96104-121">Depois de criar serviço Olá, devolver toohello portal tooget Olá URL ou `api-key`.</span><span class="sxs-lookup"><span data-stu-id="96104-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="96104-122">Ligações tooyour serviço Search requerem que tenha o URL Olá e um `api-key` chamada de Olá tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="96104-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="96104-123">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96104-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="96104-124">Na barra de índice de Olá, clique em **serviço de pesquisa** toolist todos os serviços da Azure Search aprovisionados para a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="96104-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="96104-125">Selecione Olá serviço toouse.</span><span class="sxs-lookup"><span data-stu-id="96104-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="96104-126">No dashboard do serviço de Olá, verá os mosaicos com informações essenciais, tais como o ícone da chave Olá para aceder às chaves de administração de Olá.</span><span class="sxs-lookup"><span data-stu-id="96104-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="96104-127">Copie o URL do serviço Olá, uma chave de administração e uma chave de consulta.</span><span class="sxs-lookup"><span data-stu-id="96104-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="96104-128">Precisa de três mais tarde quando os adicionar ficheiro de config.js toohello.</span><span class="sxs-lookup"><span data-stu-id="96104-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="96104-129">Transferir ficheiros de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="96104-129">Download hello sample files</span></span>
<span data-ttu-id="96104-130">Utilize uma das Olá seguinte exemplo de Olá toodownload de abordagens.</span><span class="sxs-lookup"><span data-stu-id="96104-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="96104-131">Aceda demasiado[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="96104-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="96104-132">Clique em **transferir ZIP**, guarde o ficheiro. zip de Olá e, em seguida, extraia todos os ficheiros de Olá nele contidos.</span><span class="sxs-lookup"><span data-stu-id="96104-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="96104-133">Todas as modificações do ficheiro e instruções de execução subsequentes são realizadas em ficheiros nesta pasta.</span><span class="sxs-lookup"><span data-stu-id="96104-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="96104-134">Atualize Olá config.js.</span><span class="sxs-lookup"><span data-stu-id="96104-134">Update hello config.js.</span></span> <span data-ttu-id="96104-135">com o seu URL do serviço Search e a chave de API</span><span class="sxs-lookup"><span data-stu-id="96104-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="96104-136">Utilizar Olá URL e a chave de api que copiou anteriormente, especifique o URL de Olá, chave de administrador e a chave de consulta no ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="96104-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="96104-137">As chaves de administração concedem um controlo total sobre as operações de serviço, incluindo criar ou eliminar um índice e carregar documentos.</span><span class="sxs-lookup"><span data-stu-id="96104-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="96104-138">Em contrapartida, as chaves de consulta são para operações só de leitura, normalmente utilizadas por aplicações cliente que se ligam tooAzure pesquisa.</span><span class="sxs-lookup"><span data-stu-id="96104-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="96104-139">Neste exemplo, incluímos consulta Olá toohelp chave impor Olá melhor prática em utilizar a chave de consulta de Olá em aplicações cliente.</span><span class="sxs-lookup"><span data-stu-id="96104-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="96104-140">Olá seguinte captura de ecrã mostra **config.js** aberto num editor de texto, com Olá entradas relevantes demarcadas para que possa ver onde o ficheiro de Olá tooupdate com Olá valores que do são válidas para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="96104-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="96104-141">Alojar um ambiente de tempo de execução para o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="96104-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="96104-142">exemplo de Olá requer um servidor HTTP, o que pode instalar globalmente utilizando npm.</span><span class="sxs-lookup"><span data-stu-id="96104-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="96104-143">Utilize uma janela do PowerShell para Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="96104-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="96104-144">Navegue toohello pasta que contém Olá **Package. JSON** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="96104-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="96104-145">Digite `npm install`.</span><span class="sxs-lookup"><span data-stu-id="96104-145">Type `npm install`.</span></span>
3. <span data-ttu-id="96104-146">Digite `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="96104-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="96104-147">Criar o índice de Olá e executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="96104-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="96104-148">Digite `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="96104-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="96104-149">Digite `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="96104-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="96104-150">Digite `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="96104-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="96104-151">Direcione o seu browser para `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="96104-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="96104-152">Pesquisar nos dados USGS</span><span class="sxs-lookup"><span data-stu-id="96104-152">Search on USGS data</span></span>
<span data-ttu-id="96104-153">conjunto de dados do Olá USGS inclui registos que são relevante toohello estado da Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="96104-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="96104-154">Se clicar em **pesquisa** numa caixa de pesquisa em branco, a obter entradas de principais 50 de Olá, Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="96104-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="96104-155">Introduzir um termo de pesquisa dá-motor de busca Olá algo toogo no.</span><span class="sxs-lookup"><span data-stu-id="96104-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="96104-156">Tente introduzir um nome regional.</span><span class="sxs-lookup"><span data-stu-id="96104-156">Try entering a regional name.</span></span> <span data-ttu-id="96104-157">"Roger Williams" foi o primeiro Governador de Olá de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="96104-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="96104-158">Existem vários parques, edifícios e escolas com o seu nome.</span><span class="sxs-lookup"><span data-stu-id="96104-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="96104-159">Também pode tentar qualquer um destes termos:</span><span class="sxs-lookup"><span data-stu-id="96104-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="96104-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="96104-160">Pawtucket</span></span>
* <span data-ttu-id="96104-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="96104-161">Pembroke</span></span>
* <span data-ttu-id="96104-162">ganso +cabo</span><span class="sxs-lookup"><span data-stu-id="96104-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="96104-163">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="96104-163">Next steps</span></span>
<span data-ttu-id="96104-164">Este é Olá primeiro tutorial da Azure Search com base no Node.js e Olá dados USGS.</span><span class="sxs-lookup"><span data-stu-id="96104-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="96104-165">Ao longo do tempo, iremos irá expandir este tutorial toodemonstrate funcionalidades adicionais de pesquisa é aconselhável toouse nas suas soluções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="96104-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="96104-166">Se já tiver algum conhecimento sobre a Azure Search, pode utilizar este exemplo como ponto de partida para tentar sugestores (escrita antecipada ou consultas de conclusão automática), filtros e navegação por facetas.</span><span class="sxs-lookup"><span data-stu-id="96104-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="96104-167">Também pode melhorar Olá página de resultados de pesquisa ao adicionar contagens e criação de batches de documentos para que os utilizadores possam percorrer os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="96104-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="96104-168">TooAzure nova pesquisa?</span><span class="sxs-lookup"><span data-stu-id="96104-168">New tooAzure Search?</span></span> <span data-ttu-id="96104-169">Recomendamos que tentar toodevelop outros tutoriais compreender de que pode criar.</span><span class="sxs-lookup"><span data-stu-id="96104-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="96104-170">Visite a nossa [página de documentação](https://azure.microsoft.com/documentation/services/search/) toofind mais recursos.</span><span class="sxs-lookup"><span data-stu-id="96104-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="96104-171">Também pode ver as ligações de Olá no nosso [lista de vídeos e tutoriais](search-video-demo-tutorial-list.md) tooaccess obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="96104-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
