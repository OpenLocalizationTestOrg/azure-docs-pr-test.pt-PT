---
title: "aaaCreate vários modelos de uma experimentação | Microsoft Docs"
description: "Utilize o PowerShell toocreate vários modelos de Machine Learning e web pontos finais de serviço com Olá mesmo algoritmo mas formação diferentes conjuntos de dados."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="33ce5-103">Utilizar o PowerShell para criar muitos modelos do Machine Learning e pontos finais do serviço Web a partir de uma experimentação</span><span class="sxs-lookup"><span data-stu-id="33ce5-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="33ce5-104">Segue-se um problema de aprendizagem máquina comum: pretende toocreate muitos modelos que tenham Olá mesmo fluxo de trabalho de formação e utilize Olá mesmo algoritmo, mas tem conjuntos de dados de formação diferente como entrada.</span><span class="sxs-lookup"><span data-stu-id="33ce5-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="33ce5-105">Este artigo mostra como toodo isto à escala no Azure Machine Learning Studio utilizando apenas uma única experimentação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="33ce5-106">Por exemplo, vamos supor que é proprietário de uma bicicleta global rental franchise empresa.</span><span class="sxs-lookup"><span data-stu-id="33ce5-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="33ce5-107">Pretende toobuild uma regressão modelo toopredict Olá rental a pedido com base nos dados históricos.</span><span class="sxs-lookup"><span data-stu-id="33ce5-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="33ce5-108">Tiver 1.000 rental localizações em Olá mundo e ter recolhido um conjunto de dados para cada localização que inclui funcionalidades importantes, como data, hora, meteorologia e o tráfego que são específicas tooeach localização.</span><span class="sxs-lookup"><span data-stu-id="33ce5-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="33ce5-109">Foi possível preparar o seu modelo uma vez com uma versão intercalada de todos os conjuntos de dados de Olá em todas as localizações.</span><span class="sxs-lookup"><span data-stu-id="33ce5-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="33ce5-110">Mas porque cada um dos seus localizações tem um ambiente exclusivo, uma abordagem de melhor seria possível tootrain o modelo de regressão Olá conjunto de dados a utilizar em separado para cada localização.</span><span class="sxs-lookup"><span data-stu-id="33ce5-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="33ce5-111">Dessa forma, pode demorar cada modelo treinado para tamanhos de arquivo diferente conta Olá, volume, geografia, população, ambiente de tráfego de bicicleta amigável, *etc.*.</span><span class="sxs-lookup"><span data-stu-id="33ce5-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="33ce5-112">Que podem ser abordagem das melhores Olá, mas que não pretende experimentações de formação toocreate 1.000 no Azure Machine Learning com cada um, que representa uma localização única.</span><span class="sxs-lookup"><span data-stu-id="33ce5-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="33ce5-113">Para além de ser uma tarefa muito confuso, também é parece pretty ineficaz, uma vez que cada experimentação teria todas Olá componentes mesmos, exceto para o conjunto de dados de formação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33ce5-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="33ce5-114">Felizmente, iremos pode conseguir isto utilizando Olá [reparametrização API do Azure Machine Learning](machine-learning-retrain-models-programmatically.md) e automatizar tarefas de Olá com [PowerShell do Azure Machine Learning](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="33ce5-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="33ce5-115">toomake nosso exemplo são executadas mais rápido, iremos irá reduzir Olá número de localizações de too10 1000.</span><span class="sxs-lookup"><span data-stu-id="33ce5-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="33ce5-116">Mas hello mesmo princípios e procedimentos aplicam too1, 000 localizações.</span><span class="sxs-lookup"><span data-stu-id="33ce5-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="33ce5-117">Step-by-Olá única diferença é que se quiser tootrain de conjuntos de 1.000 dados provavelmente pretende toothink da execução Olá seguintes scripts do PowerShell em paralelo.</span><span class="sxs-lookup"><span data-stu-id="33ce5-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="33ce5-118">Como toodo ultrapassa o âmbito de Olá neste artigo, mas pode encontrar exemplos do PowerShell vários segmentos no Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="33ce5-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="33ce5-119">Configurar a experimentação de preparação de Olá</span><span class="sxs-lookup"><span data-stu-id="33ce5-119">Set up hello training experiment</span></span>
<span data-ttu-id="33ce5-120">Vamos toouse um exemplo [experimentação de preparação](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) que criámos já no Olá [galeria da Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="33ce5-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="33ce5-121">Abrir este experimentação na sua [Azure Machine Learning Studio](https://studio.azureml.net) área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="33ce5-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="33ce5-122">Na ordem toofollow juntamente com este exemplo, poderá ser útil toouse uma área de trabalho padrão em vez de uma área de trabalho gratuita.</span><span class="sxs-lookup"><span data-stu-id="33ce5-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="33ce5-123">Estamos irá criar um ponto final de cada cliente - para um total de pontos 10 finais - e que irão solicitar uma área de trabalho padrão, uma vez que a área de trabalho gratuita pontos finais de too3 limitado.</span><span class="sxs-lookup"><span data-stu-id="33ce5-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="33ce5-124">Se tiver apenas uma área de trabalho gratuita, basta modificar scripts Olá abaixo tooallow apenas 3 localizações.</span><span class="sxs-lookup"><span data-stu-id="33ce5-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="33ce5-125">Olá experimentação utiliza um **importar dados** o conjunto de dados do módulo tooimport Olá formação *customer001.csv* de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce5-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="33ce5-126">Vamos assumir que tem recolhidas conjuntos de dados de formação de todas as localizações de rental bicicleta e armazenou numa Olá mesma localização de armazenamento de Blobs com nomes de ficheiro de *rentalloc001.csv* demasiado*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="33ce5-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![Imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="33ce5-128">Tenha em atenção que um **saída de serviço Web** módulo foi adicionado toohello **preparar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="33ce5-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="33ce5-129">Quando esta fase experimental é implementado como um serviço web, o ponto final de Olá associada com essa saída irá devolver modelo treinado Olá no formato de Olá de um ficheiro de .ilearner.</span><span class="sxs-lookup"><span data-stu-id="33ce5-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="33ce5-130">Tenha também em atenção que configuramos um parâmetro de serviço web para o URL de Olá esse Olá **importar dados** módulo utiliza.</span><span class="sxs-lookup"><span data-stu-id="33ce5-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="33ce5-131">Isto permite-nos toouse Olá parâmetro toospecify formação individuais conjuntos de dados tootrain Olá modelo para cada localização.</span><span class="sxs-lookup"><span data-stu-id="33ce5-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="33ce5-132">Existem outras formas que pode ter efetuado esta ação, por exemplo, utilizando uma consulta SQL com um web service parâmetro tooget de dados de uma base de dados do SQL Azure, ou simplesmente um **entrada de serviço Web** serviço web do módulo toopass no toohello conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="33ce5-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![Imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="33ce5-134">Agora, vamos executar este experimentação de preparação utilizando um valor predefinido de Olá *rental001.csv* como Olá conjunto de dados de formação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="33ce5-135">Se visualizar resultado Olá Olá **Evaluate** módulo (clique saída Olá e selecione **visualizar**), pode ver obtemos um desempenho decent de *AUC* = 0.91.</span><span class="sxs-lookup"><span data-stu-id="33ce5-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="33ce5-136">Neste momento, estamos pronto toodeploy um serviço web fora deste experimentação de preparação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="33ce5-137">Implementar serviços web de classificação de cenários e estimativas de Olá</span><span class="sxs-lookup"><span data-stu-id="33ce5-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="33ce5-138">Olá toodeploy preparação do serviço web, clique em Olá **segurança serviço Web** no botão abaixo tela de experimentação Olá e selecione **implementar serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="33ce5-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="33ce5-139">Chamar este serviço web "" bicicleta Rental formação".</span><span class="sxs-lookup"><span data-stu-id="33ce5-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="33ce5-140">Agora que temos o serviço de web do toodeploy Olá classificação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="33ce5-141">toodo isto, iremos pode clicar em **segurança serviço Web** abaixo Olá tela e selecione **preditiva serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="33ce5-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="33ce5-142">Esta ação cria uma experimentação de classificação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="33ce5-143">Precisamos toomake alguns ajustes secundárias toomake, que funciona como um serviço web, tal como remover a coluna de etiqueta de Olá "cnt" da Olá dados de entrada e limitar o id de instância do Olá saída tooonly Olá e Olá correspondente prever valor.</span><span class="sxs-lookup"><span data-stu-id="33ce5-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="33ce5-144">toosave-se de que funcionam, pode simplesmente abrir Olá [experimentação preditiva](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) no Olá galeria que já foi preparada.</span><span class="sxs-lookup"><span data-stu-id="33ce5-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="33ce5-145">serviço web de Olá toodeploy, execute a experimentação preditiva Olá, em seguida, clique em Olá **implementar serviço Web** no botão abaixo tela Olá.</span><span class="sxs-lookup"><span data-stu-id="33ce5-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="33ce5-146">Olá nome da classificação de serviço web "Bicicleta Rental classificação" ".</span><span class="sxs-lookup"><span data-stu-id="33ce5-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="33ce5-147">Criar 10 pontos finais do serviço web idênticos com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="33ce5-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="33ce5-148">Este serviço web é fornecido com um ponto final predefinido.</span><span class="sxs-lookup"><span data-stu-id="33ce5-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="33ce5-149">Mas não estamos como interessados no ponto final predefinido de Olá, uma vez que não pode ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="33ce5-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="33ce5-150">É necessário toodo é toocreate 10 os pontos finais adicionais, um para cada localização.</span><span class="sxs-lookup"><span data-stu-id="33ce5-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="33ce5-151">Iremos irá efetuar este procedimento com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33ce5-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="33ce5-152">Em primeiro lugar, iremos configurar nosso ambiente de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="33ce5-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="33ce5-153">Em seguida, execute o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="33ce5-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="33ce5-154">Agora, criámos 10 pontos finais e contêm Olá mesmo modelo treinado preparado no *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="33ce5-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="33ce5-155">Pode visualizá-los no Olá Portal de gestão do Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce5-155">You can view them in hello Azure Management Portal.</span></span>

![Imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="33ce5-157">Atualizar Olá pontos finais toouse formação separado conjuntos de dados com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="33ce5-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="33ce5-158">Olá passo seguinte consiste em pontos finais de Olá tooupdate com os modelos que preparado exclusivamente nos dados individuais de cada cliente.</span><span class="sxs-lookup"><span data-stu-id="33ce5-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="33ce5-159">Mas, primeiro é preciso tooproduce estes modelos de Olá **bicicleta Rental formação** serviço web.</span><span class="sxs-lookup"><span data-stu-id="33ce5-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="33ce5-160">Passemos back toohello **bicicleta Rental formação** serviço web.</span><span class="sxs-lookup"><span data-stu-id="33ce5-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="33ce5-161">É necessário toocall seu ponto final de BES 10 vezes com 10 formação diferentes conjuntos de dados na ordem tooproduce 10 diferentes criação de modelos.</span><span class="sxs-lookup"><span data-stu-id="33ce5-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="33ce5-162">Utilizaremos Olá **InovkeAmlWebServiceBESEndpoint** toodo de cmdlet do PowerShell isto.</span><span class="sxs-lookup"><span data-stu-id="33ce5-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="33ce5-163">Também terá de tooprovide credenciais para a sua conta de armazenamento de BLOBs para `$configContent`, nomeadamente, em campos de Olá `AccountName`, `AccountKey` e `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="33ce5-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="33ce5-164">Olá `AccountName` pode ser um dos seus nomes de conta, visto na Olá **Portal de gestão clássico do Azure** (*armazenamento* separador).</span><span class="sxs-lookup"><span data-stu-id="33ce5-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="33ce5-165">Assim que clicar na conta de armazenamento, o `AccountKey` pode encontrar, premindo Olá **gerir chaves de acesso** botão na parte inferior de Olá e copiar Olá *chave de acesso primária*.</span><span class="sxs-lookup"><span data-stu-id="33ce5-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="33ce5-166">Olá `RelativeLocation` é o armazenamento de tooyour relativo de caminho olá onde um novo modelo será armazenado.</span><span class="sxs-lookup"><span data-stu-id="33ce5-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="33ce5-167">Por exemplo, caminho de Olá `hai/retrain/bike_rental/` no script de Olá abaixo pontos tooa contentor com o nome `hai`, e `/retrain/bike_rental/` estão subpastas.</span><span class="sxs-lookup"><span data-stu-id="33ce5-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="33ce5-168">Atualmente, não é possível criar subpastas através da IU do portal de Olá, mas existem [várias exploradores de armazenamento do Azure](../storage/common/storage-explorers.md) que permitem-lhe toodo por isso.</span><span class="sxs-lookup"><span data-stu-id="33ce5-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="33ce5-169">Recomenda-se que crie um novo contentor no seu Olá de toostore armazenamento novos modelos de formação (ficheiros .ilearner) da seguinte forma: a página de armazenamento, clique em Olá **adicionar** botão na parte inferior de Olá e dê-lhe nome `retrain`.</span><span class="sxs-lookup"><span data-stu-id="33ce5-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="33ce5-170">Em resumo, o script de toohello das alterações necessárias Olá abaixo pertençam demasiado`AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="33ce5-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="33ce5-171">Olá BES endpoint é Olá modo apenas suportado para esta operação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="33ce5-172">RRS não pode ser utilizada para produzir os modelos de formação.</span><span class="sxs-lookup"><span data-stu-id="33ce5-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="33ce5-173">Como pode ver acima, em vez de construir 10 diferentes BES tarefa json ficheiros de configuração, vamos criar uma cadeia de configuração de Olá em vez disso e dinamicamente feed-toohello *jobConfigString* parâmetro de Olá  **InvokeAmlWebServceBESEndpoint** cmdlet, porque não existe realmente não tookeep necessidade de uma cópia no disco.</span><span class="sxs-lookup"><span data-stu-id="33ce5-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="33ce5-174">Se tudo correr bem, ao fim de algum deve vir de 10 .ilearner os ficheiros, de *model001.ilearner* demasiado*model010.ilearner*, na sua conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce5-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="33ce5-175">Agora está tudo pronto tooupdate nosso 10 classificação web service pontos finais com estes modelos utilizando Olá **Patch AmlWebServiceEndpoint** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33ce5-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="33ce5-176">Lembre-se novamente, apenas pode corrigir pontos finais não predefinidas de Olá que programaticamente criámos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="33ce5-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="33ce5-177">Isto deve ser executada razoavelmente depressa.</span><span class="sxs-lookup"><span data-stu-id="33ce5-177">This should run fairly quickly.</span></span> <span data-ttu-id="33ce5-178">Quando termina a execução de Olá, iremos irá criada com êxito 10 web preditiva pontos finais de serviço, cada um possuindo um modelo preparado exclusivamente preparado no Olá conjunto de dados específico tooa rental localização, tudo a partir de uma experimentação de preparação único.</span><span class="sxs-lookup"><span data-stu-id="33ce5-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="33ce5-179">tooverify, pode tentar chamar estes pontos finais utilizando Olá **InvokeAmlWebServiceRRSEndpoint** cmdlet, fornecendo-las com Olá mesmo dados de entrada e deve esperar toosee resultados de predição diferentes, desde que os modelos do Olá preparado com conjuntos de formação diferentes.</span><span class="sxs-lookup"><span data-stu-id="33ce5-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="33ce5-180">Total de script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="33ce5-180">Full PowerShell script</span></span>
<span data-ttu-id="33ce5-181">Eis listagem Olá do código de origem completo Olá:</span><span class="sxs-lookup"><span data-stu-id="33ce5-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
