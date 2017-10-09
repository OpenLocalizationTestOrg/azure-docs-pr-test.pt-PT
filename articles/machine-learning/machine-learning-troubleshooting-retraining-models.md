---
title: "serviço web de aaaTroubleshoot reparametrização um clássico do Azure Machine Learning | Microsoft Docs"
description: "Identificar e corrigir encontrou de problemas comuns quando são reparametrização modelo Olá para um serviço Web do Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="5c9fd-103">Resolução de problemas Olá reparametrização de um serviço Web clássico do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5c9fd-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="5c9fd-104">Reparametrização descrição geral</span><span class="sxs-lookup"><span data-stu-id="5c9fd-104">Retraining overview</span></span>
<span data-ttu-id="5c9fd-105">Ao implementar uma experimentação preditiva como um serviço web classificação é um modelo estático.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="5c9fd-106">Modelo de Olá tem toobe retrained como novos dados ficarem disponíveis ou quando consumidor Olá de Olá API tem os seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="5c9fd-107">Para instruções completas de Olá reparametrização o processo de um serviço Web clássico, consulte [reparametrização dos Machine Learning modelos através de programação](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="5c9fd-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="5c9fd-108">Reparametrização processo</span><span class="sxs-lookup"><span data-stu-id="5c9fd-108">Retraining process</span></span>
<span data-ttu-id="5c9fd-109">Quando precisar de tooretrain Olá serviço Web, tem de adicionar algumas partes adicionais:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="5c9fd-110">Um serviço Web implementado de Olá experimentação de preparação.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="5c9fd-111">experimentação Olá tem de ter um **saída de serviço Web** módulo ligado resultado toohello Olá **preparar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Anexe o modelo de formação do toohello de saída do Olá web service.][image1]
* <span data-ttu-id="5c9fd-113">Um novo ponto final adicionado tooyour da classificação de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="5c9fd-114">Pode adicionar ponto final de Olá programaticamente com o código de exemplo de Olá referenciado no Olá Machine Learning reparametrização dos modelos programáticos do tópico ou através de Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="5c9fd-115">Em seguida, pode utilizar Olá c# código de exemplo do modelo de tooretrain de página de ajuda API do serviço de Olá, formação Web.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="5c9fd-116">Depois de o ter avaliado resultados Olá e estiver satisfeito com os mesmos, atualizar modelo treinado Olá da classificação de serviço web utilizando Olá novo ponto final que adicionou.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="5c9fd-117">Com todas as partes de Olá no local, passos principais Olá tem de ter o modelo de Olá tooretrain são:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="5c9fd-118">Chamar Olá serviço Web de formação: chamada de Olá é toohello serviço de execução de lote (BES), não Olá serviço de resposta de pedido (RRS).</span><span class="sxs-lookup"><span data-stu-id="5c9fd-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="5c9fd-119">Pode utilizar Olá c# código de exemplo na chamada de Olá de toomake de página de ajuda de Olá API.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="5c9fd-120">Localizar os valores de Olá de Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken*: estes valores são apresentados no resultado de Olá da sua toohello chamada formação Web Serviço.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="5c9fd-121">![Mostrar resultado Olá Olá reparametrização valores de exemplo e Olá BaseLocation, RelativeLocation e SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="5c9fd-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="5c9fd-122">Atualização Olá adicionado ponto final de Olá a classificação de serviço web com Olá novo modelo de preparação: utilizando o código de exemplo de Olá fornecido no Olá Machine Learning reparametrização dos modelos através de programação, atualizar o ponto final de nova Olá adicionou toohello classificação modelo com Olá recentemente modelo treinado do Olá formação Web Service.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="5c9fd-123">Obstacles comuns</span><span class="sxs-lookup"><span data-stu-id="5c9fd-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="5c9fd-124">Verifique toosee se tiver Olá, corrija o URL de correção</span><span class="sxs-lookup"><span data-stu-id="5c9fd-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="5c9fd-125">Olá URL de aplicar o PATCH de mensagens em fila estão a utilizar tem de ser Olá um associados Olá novo ponto final da classificação adicionou toohello da classificação de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="5c9fd-126">Existem diversas formas tooobtain Olá PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="5c9fd-127">**Opção 1: X509securitytokenparameters**</span><span class="sxs-lookup"><span data-stu-id="5c9fd-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="5c9fd-128">Olá tooget corrigir PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="5c9fd-129">Executar Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="5c9fd-130">Da saída de Olá de AddEndpoint, determinar Olá *HelpLocation* valor e copie o URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation na saída de Olá de exemplo de addEndpoint Olá.][image2]
3. <span data-ttu-id="5c9fd-132">Cole o URL de Olá uma página tooa toonavigate de browser que fornece ligações de ajuda para Olá serviço Web.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="5c9fd-133">Clique em Olá **atualização recursos** página de ajuda do ligação tooopen Olá patch.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="5c9fd-134">**Opção 2: Utilizar Olá portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="5c9fd-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="5c9fd-135">Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5c9fd-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5c9fd-136">Separador de Machine Learning Olá aberta. ![Separador leaning da máquina.][image4]</span><span class="sxs-lookup"><span data-stu-id="5c9fd-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="5c9fd-137">Clique no nome de área de trabalho, em seguida, **serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="5c9fd-138">Clique em Olá serviço Web que estiver a trabalhar com a classificação.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="5c9fd-139">(Se não tiver modificado o nome predefinido de Olá do serviço web de Olá, vai terminar dentro de [classificação Exp]..)</span><span class="sxs-lookup"><span data-stu-id="5c9fd-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="5c9fd-140">Clique em **adicionar ponto final**.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="5c9fd-141">Depois de é adicionado ponto final de Olá, clique em nome do ponto final Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="5c9fd-142">Em seguida, clique em **atualização recursos** tooopen Olá página de ajuda de aplicação de patches.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="5c9fd-143">Se tiver adicionado Olá endpoint toohello serviço Web de formação em vez de Olá preditiva serviço Web, receberá Olá seguinte erro ao clicar em Olá **atualização recursos** ligação: Lamentamos, mas esta funcionalidade não é suportada ou está disponível neste contexto.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="5c9fd-144">Este serviço Web tem não existem recursos atualizáveis.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="5c9fd-145">Iremos desculpa pelo incómodo do Olá e a trabalhar para melhorar este fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Dashboard de ponto final de novo.][image3]

<span data-ttu-id="5c9fd-147">página de ajuda de PATCH Olá contém Olá PATCH URL tem de utilizar e fornece o código de exemplo, pode utilizar toocall-lo.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![URL de patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="5c9fd-149">Verifique toosee que estão a atualizar o ponto final de classificação corretos Olá</span><span class="sxs-lookup"><span data-stu-id="5c9fd-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="5c9fd-150">Não aplicar o patch Olá serviço Web de formação: operação de patch Olá deve ser executada no Olá da classificação de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="5c9fd-151">Não aplicar o patch ponto final predefinido de Olá no serviço Web: tem de efetuar a operação de patch de Olá no Olá nova classificação de ponto final do serviço Web que adicionou.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="5c9fd-152">Pode verificar o ponto final do Web service Olá está ativada por Olá visitando o portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c9fd-153">Lembre-se de que está a adicionar o ponto final de Olá toohello serviço Web preditiva, Olá formação Web Service.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="5c9fd-154">Se tiver implementado corretamente uma formação e um serviço Web preditiva, deverá ver dois serviços Web separados listados.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="5c9fd-155">Olá preditiva serviço Web deve terminar com "[exp preditiva.]".</span><span class="sxs-lookup"><span data-stu-id="5c9fd-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="5c9fd-156">Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5c9fd-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5c9fd-157">Separador de Machine Learning Olá aberta. ![Machine learning área de trabalho da IU.][image4]</span><span class="sxs-lookup"><span data-stu-id="5c9fd-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="5c9fd-158">Selecione a sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-158">Select your workspace.</span></span>
4. <span data-ttu-id="5c9fd-159">Clique em **serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="5c9fd-160">Selecione o seu serviço Web preditiva.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="5c9fd-161">Certifique-se de que o novo ponto final foi adicionado o serviço Web de toohello.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="5c9fd-162">Verifique a área de trabalho de Olá que o serviço web está a ser tooensure está numa região corretos Olá</span><span class="sxs-lookup"><span data-stu-id="5c9fd-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="5c9fd-163">Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5c9fd-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5c9fd-164">Selecione o Machine Learning a partir do menu de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="5c9fd-165">![Machine learning região da IU.][image4]</span><span class="sxs-lookup"><span data-stu-id="5c9fd-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="5c9fd-166">Certifique-se a localização de Olá da sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
