---
title: "aaaConsume um serviço web do Machine Learning com um modelo de aplicação web | Microsoft Docs"
description: "Utilize um modelo de aplicação web no Azure Marketplace tooconsume um serviço web preditiva no Azure Machine Learning."
keywords: "serviço Web, operationalization, REST API, machine learning"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="96841-104">Consumir um serviço Web do Azure Machine Learning com um modelo de aplicação Web</span><span class="sxs-lookup"><span data-stu-id="96841-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="96841-105">Uma vez que já desenvolveu o seu modelo preditivo e implementado como um serviço web do Azure utilizando o Machine Learning Studio, ou utilizando ferramentas como R ou Python, pode aceder ao modelo operacionalizado Olá utilizando uma API REST.</span><span class="sxs-lookup"><span data-stu-id="96841-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="96841-106">Existem várias formas tooconsume Olá REST API e acesso Olá serviço web.</span><span class="sxs-lookup"><span data-stu-id="96841-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="96841-107">Por exemplo, pode escrever uma aplicação em c#, R, ou código gerado quando implementou o serviço web de Olá de exemplo do Python com Olá (disponível no Olá [Portal de serviços Web do Machine Learning](https://services.azureml.net/quickstart) ou no dashboard de serviço web Olá no O Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="96841-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="96841-108">Ou pode utilizar o livro do Microsoft Excel exemplo Olá criado por si em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="96841-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="96841-109">Mas Olá tooaccess de forma mais rápida e mais fácil é o serviço web através de modelos de aplicação de Web de Olá disponíveis no Olá [Azure Marketplace de aplicação Web](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="96841-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="96841-110">Olá modelos de aplicação Web do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="96841-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="96841-111">modelos de aplicação de web de Olá disponíveis no Azure Marketplace de Olá podem criar uma aplicação web personalizada que sabe o seu serviço web dados de entrada e resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="96841-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="96841-112">Tudo o que precisa toodo é a fornecer serviço web de tooyour acesso Olá web app e os dados e modelo Olá Olá rest.</span><span class="sxs-lookup"><span data-stu-id="96841-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="96841-113">Estão disponíveis dois modelos:</span><span class="sxs-lookup"><span data-stu-id="96841-113">Two templates are available:</span></span>

* [<span data-ttu-id="96841-114">Modelo de aplicação do Azure ML resposta-pedido serviço Web</span><span class="sxs-lookup"><span data-stu-id="96841-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="96841-115">Modelo de aplicação de Web de serviço de execução de lote do Azure ML</span><span class="sxs-lookup"><span data-stu-id="96841-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="96841-116">Cada modelo cria uma aplicação de ASP.NET de exemplo, através de Olá URI de API e a chave para o seu serviço web e implementa-o como um tooAzure de web site.</span><span class="sxs-lookup"><span data-stu-id="96841-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="96841-117">modelo de serviço de resposta-pedido (RRS) Olá cria uma aplicação web que permite-lhe toosend uma única linha de dados toohello web service tooget um resultado único.</span><span class="sxs-lookup"><span data-stu-id="96841-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="96841-118">modelo de serviço de execução de lote (BES) Olá cria uma aplicação web que permite-lhe toosend número de linhas de dados tooget vários resultados.</span><span class="sxs-lookup"><span data-stu-id="96841-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="96841-119">Sem codificação é necessária toouse estes modelos.</span><span class="sxs-lookup"><span data-stu-id="96841-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="96841-120">Forneça apenas o Olá chave de API e o URI e modelo Olá baseia-se a aplicação Olá por si.</span><span class="sxs-lookup"><span data-stu-id="96841-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="96841-121">chave de API de Olá tooget e URI de pedido para um serviço web:</span><span class="sxs-lookup"><span data-stu-id="96841-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="96841-122">No Olá [Portal de serviços Web](https://services.azureml.net/quickstart), para um novo serviço web, clique em **serviços Web** na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="96841-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="96841-123">Ou de um clique de serviço web clássico **serviços Web clássicos**.</span><span class="sxs-lookup"><span data-stu-id="96841-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="96841-124">Clique em Olá web serviço tooaccess.</span><span class="sxs-lookup"><span data-stu-id="96841-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="96841-125">Para um serviço web clássico, clique em ponto final de Olá pretende tooaccess.</span><span class="sxs-lookup"><span data-stu-id="96841-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="96841-126">Clique em **Consume** na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="96841-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="96841-127">Olá cópia **primário** ou **chave secundária** e guardá-lo.</span><span class="sxs-lookup"><span data-stu-id="96841-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="96841-128">Se estiver a criar um modelo de serviço de resposta-pedido (RRS), copiar Olá **pedido-resposta** URI e guardá-lo.</span><span class="sxs-lookup"><span data-stu-id="96841-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="96841-129">Se estiver a criar um modelo de serviço de execução de lote (BES), copiar Olá **pedidos de Batch** URI e guardá-lo.</span><span class="sxs-lookup"><span data-stu-id="96841-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="96841-130">Como toouse Olá modelo de serviço de resposta-pedido (RRS)</span><span class="sxs-lookup"><span data-stu-id="96841-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="96841-131">Siga estes passos toouse Olá RRS web modelo de aplicação, conforme mostrado no Olá diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="96841-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Modelo do processo toouse RRS web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="96841-133">Aceda toohello [portal do Azure](https://portal.azure.com), **início de sessão**, clique em **novo**, procure e selecione **do Azure ML resposta-pedido Web do App Service**, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="96841-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="96841-134">Dê um nome exclusivo da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="96841-134">Give your web app a unique name.</span></span> <span data-ttu-id="96841-135">URL de Olá da aplicação web de Olá será este nome seguido `.azurewebsites.net.` por exemplo,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="96841-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="96841-136">Selecione Olá subscrição do Azure e serviços em que o seu serviço web está em execução.</span><span class="sxs-lookup"><span data-stu-id="96841-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="96841-137">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="96841-137">Click **Create**.</span></span>
     
     ![Criar aplicação Web][image5]

4. <span data-ttu-id="96841-139">Quando o Azure foi concluída a implementação de aplicação web de Olá, clique em Olá **URL** no Olá página de definições de aplicação web no Azure, ou introduza o URL de Olá num web browser.</span><span class="sxs-lookup"><span data-stu-id="96841-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="96841-140">Por exemplo, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="96841-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="96841-141">Quando Olá execuções de primeiro de aplicação de web que irá pedir-lhe Olá **API Post URL** e **chave de API**.</span><span class="sxs-lookup"><span data-stu-id="96841-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="96841-142">Introduza os valores de Olá guardou anteriormente (**URI pedido** e **chave de API**, respetivamente).</span><span class="sxs-lookup"><span data-stu-id="96841-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="96841-143">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="96841-143">Click **Submit**.</span></span>
     
     ![Introduza o Post URI e chave de API][image6]

6. <span data-ttu-id="96841-145">Olá apresenta de aplicação web respetivo **configuração de aplicação Web** página com definições de serviço web de Olá atuais.</span><span class="sxs-lookup"><span data-stu-id="96841-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="96841-146">Aqui pode efetuar alterações definições toohello utilizadas pela aplicação de web de Olá.</span><span class="sxs-lookup"><span data-stu-id="96841-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="96841-147">Alterar as definições de Olá aqui apenas altera-los para esta aplicação web.</span><span class="sxs-lookup"><span data-stu-id="96841-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="96841-148">Não altera as definições predefinidas da Olá do seu serviço web.</span><span class="sxs-lookup"><span data-stu-id="96841-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="96841-149">Por exemplo, se alterar Olá **Descrição** aqui não altera descrição Olá apresentada no dashboard de serviço web Olá no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="96841-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="96841-150">Quando tiver terminado, clique em **guardar alterações**e, em seguida, clique em **aceda tooHome página**.</span><span class="sxs-lookup"><span data-stu-id="96841-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="96841-151">Página inicial, que pode introduzir valores de serviço web do toosend tooyour de Olá.</span><span class="sxs-lookup"><span data-stu-id="96841-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="96841-152">Clique em **submeter** quando tiver terminado e Olá resultado será devolvido.</span><span class="sxs-lookup"><span data-stu-id="96841-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="96841-153">Se quiser tooreturn toohello **configuração** página, visite toohello `setting.aspx` página da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="96841-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="96841-154">Por exemplo: `http://carprediction.azurewebsites.net/setting.aspx.` será chave de API de Olá tooenter pedido novamente - é necessário que tooaccess Olá página e atualizar as definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="96841-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="96841-155">Pode parar, reiniciar ou eliminar a aplicação web de Olá no Olá portal do Azure como qualquer outra aplicação web.</span><span class="sxs-lookup"><span data-stu-id="96841-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="96841-156">Enquanto estiver em execução pode procurar o endereço da web raiz toohello e introduza novos valores.</span><span class="sxs-lookup"><span data-stu-id="96841-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="96841-157">Como toouse Olá modelo de serviço de execução de lote (BES)</span><span class="sxs-lookup"><span data-stu-id="96841-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="96841-158">Pode utilizar Olá BES modelo de aplicação web no Olá mesma forma como o modelo de RRS Olá, exceto essa aplicação web Olá criado permitirá toosubmit várias linhas de dados e de receber vários resultados.</span><span class="sxs-lookup"><span data-stu-id="96841-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="96841-159">os valores de entrada Olá para um serviço de web de execução do batch podem provenientes de armazenamento do Azure ou um ficheiro local; resultados de Olá são armazenados no contentor de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="96841-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="96841-160">Por isso, irá precisa de um toohold do contentor de armazenamento do Azure Olá resultados devolvidos pela aplicação de web de Olá, e terá tooget os dados de entrada pronto.</span><span class="sxs-lookup"><span data-stu-id="96841-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Processar toouse BES modelo web][image2]

1. <span data-ttu-id="96841-162">Siga Olá mesmo Olá toocreate do procedimento BES web app para o modelo RRS Olá, exceto aceda demasiado[modelo de aplicação ao Web do serviço de execução do Azure ML Batch](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Olá modelo BES no Azure Marketplace e clique em **Criar aplicação da Web** .</span><span class="sxs-lookup"><span data-stu-id="96841-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="96841-163">toospecify onde pretende que os resultados de Olá armazenados, introduza as informações do contentor de destino Olá na home page do Olá web app.</span><span class="sxs-lookup"><span data-stu-id="96841-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="96841-164">Também pode especificar onde a aplicação web de Olá pode obter Olá os valores de entrada, a um ficheiro local ou um contentor de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="96841-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="96841-165">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="96841-165">Click **Submit**.</span></span>
   
    ![Informações de armazenamento][image7]

<span data-ttu-id="96841-167">aplicação web de Olá apresentará uma página com o estado da tarefa.</span><span class="sxs-lookup"><span data-stu-id="96841-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="96841-168">Quando concluir a tarefa de Olá irá ser indicado localização Olá dos resultados de Olá no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="96841-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="96841-169">Tem também a opção de Olá de transferência de ficheiros locais do Olá resultados tooa.</span><span class="sxs-lookup"><span data-stu-id="96841-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="96841-170">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="96841-170">For more information</span></span>
<span data-ttu-id="96841-171">toolearn mais informações sobre...</span><span class="sxs-lookup"><span data-stu-id="96841-171">toolearn more about...</span></span>

* <span data-ttu-id="96841-172">criar uma experimentação de aprendizagem com Machine Learning Studio, consulte [criar a sua primeira experimentação no Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="96841-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="96841-173">como ver toodeploy sua aprendizagem experimentação como um serviço web, [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="96841-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="96841-174">outras formas tooaccess seu serviço web, consulte [como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="96841-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
