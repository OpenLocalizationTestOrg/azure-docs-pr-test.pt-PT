---
title: "Do Azure serviços Web Machine Learning: Implementação e o consumo | Microsoft Docs"
description: "Recursos para implementar e utilizar os serviços web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="cc17e-103">Serviços Web do Azure Machine Learning: implementação e consumo</span><span class="sxs-lookup"><span data-stu-id="cc17e-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="cc17e-104">Pode utilizar o Azure Machine Learning a fluxos de trabalho de machine-learning do toodeploy e modelos como serviços web.</span><span class="sxs-lookup"><span data-stu-id="cc17e-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="cc17e-105">Estes serviços web, em seguida, podem ser utilizados toocall Olá machine-learning modelos de aplicações por predições do Olá Internet toodo em tempo real ou no modo de batch.</span><span class="sxs-lookup"><span data-stu-id="cc17e-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="cc17e-106">Dado que os serviços web Olá RESTful, pode chamá-los de vários idiomas e plataformas, tal como .NET e Java, programação e de aplicações, como o Excel.</span><span class="sxs-lookup"><span data-stu-id="cc17e-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="cc17e-107">secções Olá fornecem ligações toowalkthroughs, códigos e documentação toohelp começar.</span><span class="sxs-lookup"><span data-stu-id="cc17e-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="cc17e-108">Implementar serviços Web</span><span class="sxs-lookup"><span data-stu-id="cc17e-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="cc17e-109">Com o Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="cc17e-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="cc17e-110">Machine Learning Studio e o portal de serviços Web do Microsoft Azure Machine Learning Olá ajudam a implementar e gerir um serviço web sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="cc17e-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="cc17e-111">Olá ligações seguintes fornecem informações gerais sobre como toodeploy um novo serviço web:</span><span class="sxs-lookup"><span data-stu-id="cc17e-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="cc17e-112">Para obter uma descrição geral sobre como toodeploy um novo serviço web que é baseado no Azure Resource Manager, consulte o artigo [implementar um novo serviço web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="cc17e-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="cc17e-113">Para obter instruções sobre como toodeploy um serviço web, consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="cc17e-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="cc17e-114">Para obter instruções completas sobre como toocreate e implementar um serviço web, consulte [instruções passo 1: criar uma área de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="cc17e-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="cc17e-115">Para obter exemplos específicos que implementar um serviço web, consulte:</span><span class="sxs-lookup"><span data-stu-id="cc17e-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="cc17e-116">Instruções passo 5: Implementar o serviço de web do Azure Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="cc17e-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="cc17e-117">Como toodeploy uma web service toomultiple regiões</span><span class="sxs-lookup"><span data-stu-id="cc17e-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="cc17e-118">Com o fornecedor de recursos de serviços web APIs (APIs do Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="cc17e-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="cc17e-119">fornecedor de recursos do Azure Machine Learning Olá para serviços web permite a implementação e gestão de serviços web através de chamadas da REST API.</span><span class="sxs-lookup"><span data-stu-id="cc17e-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="cc17e-120">Para obter mais detalhes, consulte o [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) referência.</span><span class="sxs-lookup"><span data-stu-id="cc17e-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="cc17e-121">Com os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc17e-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="cc17e-122">Fornecedor de recursos do Azure Machine Learning para serviços web permite a implementação e gestão de serviços web utilizando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc17e-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="cc17e-123">toouse Olá cmdlets, tem primeiro de iniciar sessão tooyour conta do Azure a partir do ambiente de PowerShell Olá utilizando Olá [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cc17e-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="cc17e-124">Se não estiver familiarizado com como toocall PowerShell comandos que são baseadas no Resource Manager, consulte [utilizar o Azure PowerShell com o Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="cc17e-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="cc17e-125">tooexport experimentar, utilize o preditiva [este código de exemplo](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="cc17e-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="cc17e-126">Depois de criar o ficheiro de .exe Olá a partir do código Olá, pode escrever:</span><span class="sxs-lookup"><span data-stu-id="cc17e-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="cc17e-127">Execução da aplicação Olá cria um modelo de JSON do serviço web.</span><span class="sxs-lookup"><span data-stu-id="cc17e-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="cc17e-128">toouse Olá modelo toodeploy um serviço web, tem de adicionar Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="cc17e-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="cc17e-129">Nome da conta de armazenamento e a chave</span><span class="sxs-lookup"><span data-stu-id="cc17e-129">Storage account name and key</span></span>

    <span data-ttu-id="cc17e-130">Pode obter o nome de conta do storage Olá e a chave de qualquer um dos Olá [portal do Azure](https://portal.azure.com/) ou Olá [portal clássico do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="cc17e-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="cc17e-131">ID de plano de compromisso</span><span class="sxs-lookup"><span data-stu-id="cc17e-131">Commitment plan ID</span></span>

    <span data-ttu-id="cc17e-132">Pode obter o ID de plano Olá de Olá [serviços Web do Azure Machine Learning](https://services.azureml.net) portal, iniciando sessão e clicar em nome do plano.</span><span class="sxs-lookup"><span data-stu-id="cc17e-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="cc17e-133">Adicionar modelo JSON toohello como elementos subordinados do Olá *propriedades* nó na Olá mesmo nível como Olá *MachineLearningWorkspace* nós.</span><span class="sxs-lookup"><span data-stu-id="cc17e-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="cc17e-134">Eis um exemplo:</span><span class="sxs-lookup"><span data-stu-id="cc17e-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="cc17e-135">Consulte Olá seguintes artigos e dar exemplos de código para obter detalhes adicionais:</span><span class="sxs-lookup"><span data-stu-id="cc17e-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="cc17e-136">[Cmdlets do Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) na MSDN</span><span class="sxs-lookup"><span data-stu-id="cc17e-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="cc17e-137">Exemplo [instruções](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) no GitHub</span><span class="sxs-lookup"><span data-stu-id="cc17e-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="cc17e-138">Consumir os serviços web de Olá</span><span class="sxs-lookup"><span data-stu-id="cc17e-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="cc17e-139">De Olá Azure Machine Learning serviços IU da Web (teste)</span><span class="sxs-lookup"><span data-stu-id="cc17e-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="cc17e-140">Pode testar o seu serviço web do portal de serviços Web do Azure Machine Learning Olá.</span><span class="sxs-lookup"><span data-stu-id="cc17e-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="cc17e-141">Isto inclui a testar o serviço de resposta-pedido Olá (RRS) e interfaces de serviço de execução de lote (BES).</span><span class="sxs-lookup"><span data-stu-id="cc17e-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="cc17e-142">Implementar um serviço Web novo</span><span class="sxs-lookup"><span data-stu-id="cc17e-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="cc17e-143">Implementar um serviço web do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cc17e-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="cc17e-144">Instruções passo 5: Implementar o serviço de web do Azure Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="cc17e-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="cc17e-145">A partir do Excel</span><span class="sxs-lookup"><span data-stu-id="cc17e-145">From Excel</span></span>
<span data-ttu-id="cc17e-146">Pode transferir um modelo do Excel que consome o serviço web de Olá:</span><span class="sxs-lookup"><span data-stu-id="cc17e-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="cc17e-147">Consumir um serviço web do Azure Machine Learning a partir do Excel</span><span class="sxs-lookup"><span data-stu-id="cc17e-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="cc17e-148">Suplemento do Excel para serviços Web do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cc17e-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="cc17e-149">De um cliente baseado em REST</span><span class="sxs-lookup"><span data-stu-id="cc17e-149">From a REST-based client</span></span>
<span data-ttu-id="cc17e-150">Serviços Web do Azure Machine Learning são RESTful APIs.</span><span class="sxs-lookup"><span data-stu-id="cc17e-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="cc17e-151">Pode consumir estas APIs de várias plataformas, tais como .NET, Python, R, Java, Olá etc. **Consume** página para o seu serviço web no Olá [portal de serviços Web do Microsoft Azure Machine Learning](https://services.azureml.net) tem de exemplo Introdução ao código que pode ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="cc17e-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="cc17e-152">Para obter mais informações, consulte [como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="cc17e-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
