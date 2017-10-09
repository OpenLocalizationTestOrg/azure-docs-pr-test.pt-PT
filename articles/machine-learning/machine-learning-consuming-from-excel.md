---
title: "aaaConsume um serviço Web do Machine Learning a partir do Excel | Microsoft Docs"
description: "Consumir um serviço Web do Azure Machine Learning a partir do Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="4d2e1-103">Consumir um serviço Web do Azure Machine Learning a partir do Excel</span><span class="sxs-lookup"><span data-stu-id="4d2e1-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="4d2e1-104">Azure Machine Learning Studio facilita toocall fácil os serviços web diretamente a partir do Excel sem precisar de Olá toowrite qualquer código.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="4d2e1-105">Se estiver a utilizar o Excel 2013 (ou posterior) ou o Excel Online, em seguida, recomendamos que utilize Olá Excel [suplemento do Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="4d2e1-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="4d2e1-106">Passos</span><span class="sxs-lookup"><span data-stu-id="4d2e1-106">Steps</span></span>
<span data-ttu-id="4d2e1-107">Publica um serviço web.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-107">Publish a web service.</span></span> <span data-ttu-id="4d2e1-108">[Esta página](machine-learning-walkthrough-5-publish-web-service.md) explica como toodo-lo.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="4d2e1-109">A funcionalidade de livro do Excel Olá só é suportada para os serviços de pedido/resposta com uma saída único (ou seja, uma classificação simples).</span><span class="sxs-lookup"><span data-stu-id="4d2e1-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="4d2e1-110">Depois de ter um serviço web, clique em Olá **serviços WEB** secção esquerda Olá do studio Olá e, em seguida, selecione Olá web service tooconsume a partir do Excel.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="4d2e1-111">**Serviço Web clássico**</span><span class="sxs-lookup"><span data-stu-id="4d2e1-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="4d2e1-112">No Olá **DASHBOARD** separador para o serviço web de Olá é uma linha para Olá **pedido/resposta** serviço.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="4d2e1-113">Se este serviço tinha de saída única, deverá ver Olá **Transferir livro do Excel** ligação nessa linha.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="4d2e1-114">Clique em **transferir o livro do Excel**.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="4d2e1-115">**Novo serviço Web**</span><span class="sxs-lookup"><span data-stu-id="4d2e1-115">**New Web Service**</span></span>

1. <span data-ttu-id="4d2e1-116">No portal do serviço Web do Azure Machine Learning Olá, selecione **Consume**.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="4d2e1-117">Na página de Consume Olá, no Olá **Web opções de consumo do serviço** secção, clique em ícone do Excel Olá.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="4d2e1-118">**Utilizar Olá livro**</span><span class="sxs-lookup"><span data-stu-id="4d2e1-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="4d2e1-119">Livro Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-119">Open hello workbook.</span></span>
2. <span data-ttu-id="4d2e1-120">É apresentado um aviso de segurança; Clique em Olá **ativar editar** botão.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="4d2e1-121">É apresentado um aviso de segurança.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-121">A Security Warning appears.</span></span> <span data-ttu-id="4d2e1-122">Clique em Olá **ativar conteúdo** botão toorun macros no seu folha de cálculo.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="4d2e1-123">Depois de macros estiverem ativadas, é gerada uma tabela.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="4d2e1-124">As colunas na azul são necessárias como entrada para Olá serviço web RRS, ou **parâmetros**.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="4d2e1-125">Tenha em atenção resultado Olá Olá serviço RRS, **PREVER valores** verde.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="4d2e1-126">Quando todas as colunas para uma determinada linha estão preenchidas, Olá livro automaticamente chama Olá API de classificação e apresenta Olá classificada resultados.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="4d2e1-127">tooscore mais do que uma linha, a segunda linha da preenchimento Olá com dados e Olá prever valores são produzidos.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="4d2e1-128">Ainda pode colar linhas várias em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="4d2e1-129">Pode utilizar qualquer uma das funcionalidades de Excel Olá (gráficos, mapa de energia, condicional formatação, etc.) com Olá prever valores toohelp visualizar dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="4d2e1-130">Partilhar o seu livro</span><span class="sxs-lookup"><span data-stu-id="4d2e1-130">Sharing your workbook</span></span>
<span data-ttu-id="4d2e1-131">Para Olá macros toowork, a chave de API têm de constar da folha de cálculo de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="4d2e1-132">Isto significa que devem partilhar o livro Olá apenas com entidades/indivíduos que confia.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="4d2e1-133">Atualizações automáticas</span><span class="sxs-lookup"><span data-stu-id="4d2e1-133">Automatic updates</span></span>
<span data-ttu-id="4d2e1-134">É efetuada uma chamada RRS nestas duas situações:</span><span class="sxs-lookup"><span data-stu-id="4d2e1-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="4d2e1-135">Olá pela primeira vez uma linha possui conteúdo em todos os respetivos **parâmetros**</span><span class="sxs-lookup"><span data-stu-id="4d2e1-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="4d2e1-136">Sempre que qualquer um dos Olá **parâmetros** alterações numa linha que tinha todos os respetivos **parâmetros** introduzido.</span><span class="sxs-lookup"><span data-stu-id="4d2e1-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
