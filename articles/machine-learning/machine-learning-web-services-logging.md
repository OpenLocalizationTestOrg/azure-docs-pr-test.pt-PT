---
title: "aaaLogging para serviços web do Machine Learning | Microsoft Docs"
description: "Saiba como os serviços web tooenable registo para o Machine Learning. O registo fornece informações adicionais toohelp Olá APIs de resolução de problemas."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="857f3-104">Ativar o registo para os serviços Web do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="857f3-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="857f3-105">Este documento fornece informações sobre Olá registo a capacidade de serviços web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="857f3-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="857f3-106">O registo fornece informações adicionais, para além de apenas um número de erro e uma mensagem, que pode ajudar a resolver o toohello chamadas APIs do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="857f3-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="857f3-107">Como tooenable o registo para um serviço Web</span><span class="sxs-lookup"><span data-stu-id="857f3-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="857f3-108">Ativar o registo de Olá [serviços Web do Azure Machine Learning](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="857f3-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="857f3-109">Inicie sessão no portal de serviços Web do Azure Machine Learning toohello em [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="857f3-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="857f3-110">Para um serviço web clássico, também pode obter toohello portal clicando **nova experiência de serviços Web** na página de serviços Web Machine Learning Olá no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="857f3-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nova ligação de experiência de serviços Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="857f3-112">Na barra de menu superior Olá, clique em **serviços Web** para um novo serviço web, ou clique em **serviços Web clássicos** para um clássico de serviço web.</span><span class="sxs-lookup"><span data-stu-id="857f3-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selecione o novo ou clássico serviços web](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="857f3-114">Para um novo serviço web, clique em nome do serviço web Olá.</span><span class="sxs-lookup"><span data-stu-id="857f3-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="857f3-115">Para um serviço web clássico, clique em nome do serviço web Olá e, em seguida, na página seguinte Olá, clique em ponto final adequado de Olá.</span><span class="sxs-lookup"><span data-stu-id="857f3-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="857f3-116">Na barra de menu superior Olá, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="857f3-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="857f3-117">Conjunto Olá **ativar registo** opção demasiado*erro* (toolog apenas erros) ou *todos os* (para o registo completo).</span><span class="sxs-lookup"><span data-stu-id="857f3-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Selecione o nível de registo](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="857f3-119">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="857f3-119">Click **Save**.</span></span>

7. <span data-ttu-id="857f3-120">Para os serviços web clássico, crie Olá **ml diagnóstico** contentor.</span><span class="sxs-lookup"><span data-stu-id="857f3-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="857f3-121">Todos os registos do serviço web são mantidos num contentor do blob denominado **ml diagnóstico** na conta do storage Olá associada ao serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="857f3-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="857f3-122">Para novos serviços web, este contentor é criado Olá pela primeira vez, aceder ao serviço web Olá.</span><span class="sxs-lookup"><span data-stu-id="857f3-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="857f3-123">Para os serviços web clássico, terá de contentor de Olá toocreate se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="857f3-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="857f3-124">No Olá [portal do Azure](https://portal.azure.com), aceda a conta de armazenamento de toohello associada ao serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="857f3-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="857f3-125">Em **serviço Blob**, clique em **contentores**.</span><span class="sxs-lookup"><span data-stu-id="857f3-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="857f3-126">Se contentor Olá **ml diagnóstico** não existe, clique em **+ contentor**, dê Olá contentor Olá nome "ml-diagnóstico" e selecione Olá **aceder tipo** como "Blob".</span><span class="sxs-lookup"><span data-stu-id="857f3-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="857f3-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="857f3-127">Click **OK**.</span></span>

      ![Selecione o nível de registo](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="857f3-129">Para um serviço web clássico, Olá Dashboard de serviços Web do Machine Learning Studio também tem um registo de tooenable comutador.</span><span class="sxs-lookup"><span data-stu-id="857f3-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="857f3-130">No entanto, porque o registo está agora gerido através do portal de serviços Web Olá, terá de tooenable registo através do portal de Olá, tal como descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="857f3-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="857f3-131">Se já tiver ativado o registo no Studio, em seguida, no Portal de serviços Web Olá, desative o registo e volte a ativar.</span><span class="sxs-lookup"><span data-stu-id="857f3-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="857f3-132">efeitos de Olá de ativar o registo</span><span class="sxs-lookup"><span data-stu-id="857f3-132">hello effects of enabling logging</span></span>
<span data-ttu-id="857f3-133">Quando o registo está ativado, Olá diagnóstico e de erros de ponto final de serviço do Olá web são registados no Olá **ml diagnóstico** contentor do blob no Olá conta do Storage do Azure ligado com área de trabalho do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="857f3-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="857f3-134">Este contentor contém todas as informações de diagnóstico de Olá para todos os Olá web pontos finais de serviço para todas as áreas de trabalho Olá associados a esta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="857f3-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="857f3-135">Olá registos podem ser vistos utilizando qualquer um dos Olá tooexplore disponíveis várias ferramentas uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="857f3-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="857f3-136">Olá mais fácil poderá ser a conta de armazenamento de toohello toonavigate no Olá portal do Azure, clique em **contentores**e, em seguida, clique em contentor Olá **ml diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="857f3-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="857f3-137">Informações de detalhe do registo blob</span><span class="sxs-lookup"><span data-stu-id="857f3-137">Log blob detail information</span></span>
<span data-ttu-id="857f3-138">Cada blob no contentor de Olá contém informações de diagnóstico de Olá para exactamente um Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="857f3-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="857f3-139">Uma execução do método de Olá execução de lote</span><span class="sxs-lookup"><span data-stu-id="857f3-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="857f3-140">Uma execução do método de Olá resposta-pedido</span><span class="sxs-lookup"><span data-stu-id="857f3-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="857f3-141">Inicialização de um contentor de resposta-pedido</span><span class="sxs-lookup"><span data-stu-id="857f3-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="857f3-142">nome de Olá de cada blob tem um prefixo de Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="857f3-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="857f3-143">Onde _tipo de registo_ é um dos seguintes valores de Olá:</span><span class="sxs-lookup"><span data-stu-id="857f3-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="857f3-144">Batch</span><span class="sxs-lookup"><span data-stu-id="857f3-144">batch</span></span>  
* <span data-ttu-id="857f3-145">pontuação/pedidos</span><span class="sxs-lookup"><span data-stu-id="857f3-145">score/requests</span></span>  
* <span data-ttu-id="857f3-146">pontuação/init</span><span class="sxs-lookup"><span data-stu-id="857f3-146">score/init</span></span>  

