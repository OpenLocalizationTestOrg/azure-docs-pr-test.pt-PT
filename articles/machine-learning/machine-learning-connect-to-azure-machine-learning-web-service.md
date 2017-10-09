---
title: "aaaConnect tooa serviço Web do Machine Learning | Microsoft Docs"
description: "Com c# ou Python, ligar tooan serviço Web do Azure Machine Learning utilizando uma chave de autorização."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="27453-103">Ligar tooan serviço Web do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="27453-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="27453-104">Olá experiência de programação do Azure Machine Learning é um predições do Web service API toomake de dados de entrada em tempo real ou no modo de batch.</span><span class="sxs-lookup"><span data-stu-id="27453-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="27453-105">Utilizar predições toocreate do Azure Machine Learning Studio e implementar um serviço Web do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="27453-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="27453-106">toolearn sobre como toocreate e implementar um serviço Web do Machine Learning com Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="27453-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="27453-107">Para um tutorial sobre como toocreate uma experimentação no Machine Learning Studio, consulte o artigo [criar a sua primeira experimentação](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="27453-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="27453-108">Para obter detalhes sobre como toodeploy um serviço Web, consulte [implementar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="27453-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="27453-109">Para obter mais informações sobre o Machine Learning em geral, visite Olá [Centro de documentação do Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="27453-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="27453-110">Serviço Web do Machine Learning do Azure</span><span class="sxs-lookup"><span data-stu-id="27453-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="27453-111">Com o serviço Web do Azure Machine Learning Olá, uma aplicação externa comunica com um modelo de pontuação de fluxo de trabalho de Machine Learning em tempo real.</span><span class="sxs-lookup"><span data-stu-id="27453-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="27453-112">Uma chamada de serviço Web do Machine Learning devolve resultados de predição aplicação externa tooan.</span><span class="sxs-lookup"><span data-stu-id="27453-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="27453-113">toomake uma chamada de serviço Web do Machine Learning, passa uma chave de API que foi criada quando implementou uma predição.</span><span class="sxs-lookup"><span data-stu-id="27453-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="27453-114">Olá serviço Web do Machine Learning é baseado em REST, uma opção de arquitetura popular para projetos de programação web.</span><span class="sxs-lookup"><span data-stu-id="27453-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="27453-115">O Azure Machine Learning tem dois tipos de serviços:</span><span class="sxs-lookup"><span data-stu-id="27453-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="27453-116">O serviço de resposta-pedido (RRS) – A latência baixa, o serviço altamente dimensionável, que fornece uma interface toohello modelos sem monitorização de estado criados e implementados a partir de Olá Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="27453-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="27453-117">Execução serviço batch (BES) – um assíncrono que pontua um lote de registos de dados do serviço.</span><span class="sxs-lookup"><span data-stu-id="27453-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="27453-118">Para obter mais informações sobre os serviços Web do Machine Learning, consulte [implementar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="27453-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="27453-119">Obter uma chave de autorização do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="27453-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="27453-120">Ao implementar a sua experimentação, chaves de API são geradas para Olá serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="27453-121">Pode obter chaves Olá de várias localizações.</span><span class="sxs-lookup"><span data-stu-id="27453-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="27453-122">No portal de serviços Web do Microsoft Azure Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="27453-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="27453-123">Inicie sessão no toohello [serviços Web do Microsoft Azure Machine Learning](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="27453-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="27453-124">chave de Olá API tooretrieve para um serviço Web de aprendizagem máquina novo:</span><span class="sxs-lookup"><span data-stu-id="27453-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="27453-125">No portal de serviços Web do Azure Machine Learning Olá, clique em **serviços Web** menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="27453-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="27453-126">Clique em serviço Web de Olá para o qual pretende chave de Olá tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="27453-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="27453-127">No menu superior Olá, clique em **Consume**.</span><span class="sxs-lookup"><span data-stu-id="27453-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="27453-128">Copie e guarde Olá **chave primária**.</span><span class="sxs-lookup"><span data-stu-id="27453-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="27453-129">chave de API de Olá tooretrieve para um serviço Web de aprendizagem máquina clássico:</span><span class="sxs-lookup"><span data-stu-id="27453-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="27453-130">No portal de serviços Web do Azure Machine Learning Olá, clique em **serviços Web clássicos** menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="27453-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="27453-131">Clique em serviço Web de Olá com a qual está a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="27453-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="27453-132">Clique em ponto final de Olá para o qual pretende chave de Olá tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="27453-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="27453-133">No menu superior Olá, clique em **Consume**.</span><span class="sxs-lookup"><span data-stu-id="27453-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="27453-134">Copie e guarde Olá **chave primária**.</span><span class="sxs-lookup"><span data-stu-id="27453-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="27453-135">Serviço Web clássico</span><span class="sxs-lookup"><span data-stu-id="27453-135">Classic Web service</span></span>
 <span data-ttu-id="27453-136">Também pode obter uma chave para um serviço Web clássico de Machine Learning Studio ou Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="27453-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="27453-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="27453-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="27453-138">No Machine Learning Studio, clique em **serviços WEB** Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="27453-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="27453-139">Clique num serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-139">Click a Web service.</span></span> <span data-ttu-id="27453-140">Olá **chave de API** no Olá **DASHBOARD** separador.</span><span class="sxs-lookup"><span data-stu-id="27453-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="27453-141">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="27453-141">Azure classic portal</span></span>
1. <span data-ttu-id="27453-142">Clique em **MACHINE LEARNING** Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="27453-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="27453-143">Clique em área de trabalho Olá em que se encontra o seu serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="27453-144">Clique em **serviços WEB**.</span><span class="sxs-lookup"><span data-stu-id="27453-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="27453-145">Clique num serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-145">Click a Web service.</span></span>
5. <span data-ttu-id="27453-146">Clique num ponto final.</span><span class="sxs-lookup"><span data-stu-id="27453-146">Click an endpoint.</span></span> <span data-ttu-id="27453-147">Olá "Chave de API" está inativo em Olá inferior direita.</span><span class="sxs-lookup"><span data-stu-id="27453-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="27453-148"><a id="connect"></a>Ligar o serviço de Machine Learning Web tooa</span><span class="sxs-lookup"><span data-stu-id="27453-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="27453-149">Pode ligar tooa serviço Web do Machine Learning utilizando qualquer linguagem de programação que suporte o HTTP de pedido e resposta.</span><span class="sxs-lookup"><span data-stu-id="27453-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="27453-150">Pode ver exemplos em c#, Python e R de uma página de ajuda do serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="27453-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="27453-151">**Ajuda da API de aprendizagem do computador** ajuda de API do Machine Learning é criada quando implementar um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="27453-152">Consulte [instruções de aprendizagem do Azure - implementar o serviço Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="27453-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="27453-153">Olá ajuda de API do Machine Learning contém detalhes sobre uma predição do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="27453-154">Clique em serviço Web de Olá com a qual está a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="27453-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="27453-155">Clique em ponto final de Olá para o qual pretende tooview Olá página de ajuda de API.</span><span class="sxs-lookup"><span data-stu-id="27453-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="27453-156">No menu superior Olá, clique em **Consume**.</span><span class="sxs-lookup"><span data-stu-id="27453-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="27453-157">Clique em **página de ajuda de API** em Olá pedido-resposta ou pontos finais de execução de lote.</span><span class="sxs-lookup"><span data-stu-id="27453-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="27453-158">**ajudar a API do Machine Learning tooview para um serviço Web de novo**</span><span class="sxs-lookup"><span data-stu-id="27453-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="27453-159">No Portal de serviços Web do Azure Machine Learning Olá:</span><span class="sxs-lookup"><span data-stu-id="27453-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="27453-160">Clique em **serviços WEB** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="27453-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="27453-161">Clique em serviço Web de Olá para o qual pretende chave de Olá tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="27453-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="27453-162">Clique em **Consume** tooget hello URIs para Olá Reposonse pedido e o código de exemplo e serviços de execução do Batch em c#, R e Python.</span><span class="sxs-lookup"><span data-stu-id="27453-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="27453-163">Clique em **API do Swagger** tooget Swagger baseada em documentação para Olá APIs chamada a partir de Olá fornecido URIs.</span><span class="sxs-lookup"><span data-stu-id="27453-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="27453-164">Exemplo do c#</span><span class="sxs-lookup"><span data-stu-id="27453-164">C# Sample</span></span>
<span data-ttu-id="27453-165">tooconnect tooa serviço Web do Machine Learning, utilize um **HttpClient** transmitir ScoreData.</span><span class="sxs-lookup"><span data-stu-id="27453-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="27453-166">ScoreData contém um FeatureVector, um vetor n dimensional das funcionalidades numéricos que representa Olá ScoreData.</span><span class="sxs-lookup"><span data-stu-id="27453-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="27453-167">Autenticar o serviço de Machine Learning toohello com uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="27453-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="27453-168">Olá tooconnect tooa serviço Web do Machine Learning, **Microsoft.AspNet.WebApi.Client** pacote NuGet tem de estar instalado.</span><span class="sxs-lookup"><span data-stu-id="27453-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="27453-169">**Instalar Microsoft.AspNet.WebApi.Client NuGet no Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="27453-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="27453-170">Publicar o conjunto de dados de transferência de Olá de UCI: conjunto de dados de classe para adultos 2 serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="27453-171">clique em **Ferramentas** > **Gestor de Pacotes NuGet** > **Consola de Gestor de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="27453-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="27453-172">Escolha **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="27453-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="27453-173">**exemplo de código toorun Olá**</span><span class="sxs-lookup"><span data-stu-id="27453-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="27453-174">Publicar "exemplo 1: Transferir o conjunto de dados a partir de UCI: o conjunto de dados do adulto 2 classe" experimentação, parte Olá coleção de exemplo do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="27453-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="27453-175">Atribua apiKey com a chave de Olá um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="27453-176">Consulte **obter uma chave de autorização do Azure Machine Learning** acima.</span><span class="sxs-lookup"><span data-stu-id="27453-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="27453-177">Atribua serviceUri com Olá URI do pedido.</span><span class="sxs-lookup"><span data-stu-id="27453-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="27453-178">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="27453-178">Python Sample</span></span>
<span data-ttu-id="27453-179">tooconnect tooa serviço Web do Machine Learning, utilize Olá **urllib2** biblioteca transmitir ScoreData.</span><span class="sxs-lookup"><span data-stu-id="27453-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="27453-180">ScoreData contém um FeatureVector, um vetor n dimensional das funcionalidades numéricos que representa Olá ScoreData.</span><span class="sxs-lookup"><span data-stu-id="27453-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="27453-181">Autenticar o serviço de Machine Learning toohello com uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="27453-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="27453-182">**exemplo de código toorun Olá**</span><span class="sxs-lookup"><span data-stu-id="27453-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="27453-183">Implementar "exemplo 1: Transferir o conjunto de dados a partir de UCI: o conjunto de dados do adulto 2 classe" experimentação, parte Olá coleção de exemplo do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="27453-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="27453-184">Atribua apiKey com a chave de Olá um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="27453-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="27453-185">Consulte Olá **obter uma chave de autorização do Azure Machine Learning** secção quase início Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="27453-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="27453-186">Atribua serviceUri com Olá URI do pedido.</span><span class="sxs-lookup"><span data-stu-id="27453-186">Assign serviceUri with hello Request URI.</span></span>

