---
title: "pontos finais do serviço de Web aaaCreating no Machine Learning | Microsoft Docs"
description: "A criação de pontos finais do serviço Web no Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="dfc3f-103">Criar Pontos Finais</span><span class="sxs-lookup"><span data-stu-id="dfc3f-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="dfc3f-104">Este tópico descreve tooa aplicável técnicas **clássico** serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="dfc3f-105">Quando criar serviços Web que propor tooyour reencaminhar clientes, terá de tooprovide modelos de formação tooeach cliente que são experimentação toohello ainda ligado do qual Olá Web o serviço foi criado.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="dfc3f-106">Além disso, quaisquer atualizações toohello experimentação deve ser aplicadas seletivamente tooan endpoint sem substituir personalizações Olá.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="dfc3f-107">tooaccomplish, o Azure Machine Learning permite-lhe toocreate vários pontos finais para um serviço Web implementado.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="dfc3f-108">Cada ponto final no serviço Web de Olá independentemente é resolvido, limitado e gerido.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="dfc3f-109">Cada ponto final é uma chave exclusiva de autorização e de URL que pode distribuir tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="dfc3f-110">Adicionar pontos finais tooa Web serviço</span><span class="sxs-lookup"><span data-stu-id="dfc3f-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="dfc3f-111">Existem três formas tooadd um tooa ponto final de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="dfc3f-112">Através de Programação</span><span class="sxs-lookup"><span data-stu-id="dfc3f-112">Programmatically</span></span>
* <span data-ttu-id="dfc3f-113">Através do portal de serviços Web do Azure Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="dfc3f-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="dfc3f-114">Embora Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="dfc3f-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="dfc3f-115">Assim que for criado o ponto final de Olá, pode consumi-lo através de APIs síncronas, batch APIs e folhas de cálculo do excel.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="dfc3f-116">Além disso tooadding pontos finais através deste IU, também pode utilizar Olá APIs de gestão do ponto final tooprogrammatically adicionar pontos finais.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="dfc3f-117">Se tiver adicionado os pontos finais adicionais toohello serviço Web, não é possível eliminar o ponto final do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="dfc3f-118">Adicionar um ponto final através de programação</span><span class="sxs-lookup"><span data-stu-id="dfc3f-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="dfc3f-119">Pode adicionar um serviço Web do ponto final tooyour através de programação utilizando Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="dfc3f-120">Adicionar um ponto final com o portal de serviços Web do Azure Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="dfc3f-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="dfc3f-121">No Machine Learning Studio, na coluna de navegação esquerdo Olá, clique em serviços Web.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="dfc3f-122">Na parte inferior de Olá do dashboard de serviço Web de Olá, clique em **gerir pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="dfc3f-123">portal de serviços Web do Azure Machine Learning Olá abre a página de pontos finais de toohello para Olá serviço Web.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="dfc3f-124">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-124">Click **New**.</span></span>
4. <span data-ttu-id="dfc3f-125">Escreva um nome e descrição para o ponto final de nova Olá.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="dfc3f-126">Os nomes de ponto final tem de ser 24 caráter ou menos de comprimento e devem ser constituídos por europeus minúsculas ou números.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="dfc3f-127">Selecione o nível de registo Olá e se os dados de exemplo estão ativados.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="dfc3f-128">Para obter mais informações sobre o registo, consulte [ativar o registo de serviços Web do Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="dfc3f-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="dfc3f-129">Adicionar um ponto final com Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="dfc3f-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="dfc3f-130">Inicie sessão no toohello [portal clássico do Azure](http://manage.windowsazure.com), clique em **Machine Learning** na coluna esquerda Olá.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="dfc3f-131">Clique em área de trabalho de Olá que contém o serviço Web de Olá no qual está interessado.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Navegue tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="dfc3f-133">Clique em **serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-133">Click **Web Services**.</span></span>
   
    ![Navegue tooWeb serviços](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="dfc3f-135">Clique em serviço Web de Olá estiver interessado na lista de Olá toosee de pontos finais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Navegue tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="dfc3f-137">Na Olá parte inferior da página Olá, clique em **adicionar ponto final**.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="dfc3f-138">Escreva um nome e uma descrição, certifique-se de que existem não existem pontos finais com Olá mesmo nome neste serviço Web.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="dfc3f-139">Deixe o nível de limitação de Olá com o respetivo valor predefinido, salvo se tiver requisitos especiais.</span><span class="sxs-lookup"><span data-stu-id="dfc3f-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="dfc3f-140">toolearn mais informações sobre limitação, consulte [Dimensionar pontos finais da API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="dfc3f-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Criar o ponto final](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="dfc3f-142">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="dfc3f-142">Next Steps</span></span>
<span data-ttu-id="dfc3f-143">[Como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="dfc3f-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

