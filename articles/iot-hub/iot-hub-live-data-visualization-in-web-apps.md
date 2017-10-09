---
title: "visualização de dados de aaaReal tempo dos dados de sensores do seu hub IoT do Azure – Web Apps | Microsoft Docs"
description: "Utilize a funcionalidade de aplicações Web de Olá do App Service do Microsoft Azure toovisualize relativos à temperatura e humidade dados que são recolhidas a partir do sensor Olá e enviados tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualização de dados em tempo real, visualização de dados em direto, visualização de dados de sensor"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="6c64d-104">Visualizar dados de sensores em tempo real do seu hub IoT do Azure utilizando a funcionalidade de aplicações Web Olá do App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="6c64d-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Diagrama de ponto a ponto](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="6c64d-106">O que irá aprender</span><span class="sxs-lookup"><span data-stu-id="6c64d-106">What you learn</span></span>

<span data-ttu-id="6c64d-107">Neste tutorial, saiba como os dados de sensores em tempo real de toovisualize que o seu IoT hub recebe ao executar uma aplicação web que estão alojados numa aplicação web.</span><span class="sxs-lookup"><span data-stu-id="6c64d-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="6c64d-108">Se pretende que os tootry toovisualize Olá dados no seu IoT hub, utilizando o Power BI, consulte o artigo [dados de sensores em tempo real de toovisualize utilize Power BI do IoT Hub do Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6c64d-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6c64d-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="6c64d-109">What you do</span></span>

- <span data-ttu-id="6c64d-110">Crie uma aplicação web no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c64d-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="6c64d-111">Prepare o seu IoT hub para acesso a dados através da adição de um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="6c64d-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="6c64d-112">Configure dados de sensores do Olá web app tooread do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c64d-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="6c64d-113">Carregar um toobe de aplicações web alojada pelo Olá web app.</span><span class="sxs-lookup"><span data-stu-id="6c64d-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="6c64d-114">Abrir Olá web toosee em tempo real relativos à temperatura e humidade dados da aplicação a partir do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c64d-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6c64d-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="6c64d-115">What you need</span></span>

- <span data-ttu-id="6c64d-116">[Configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), que abrange Olá os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="6c64d-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="6c64d-117">Uma subscrição do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c64d-117">An active Azure subscription</span></span>
  - <span data-ttu-id="6c64d-118">Um Iot hub na sua subscrição</span><span class="sxs-lookup"><span data-stu-id="6c64d-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="6c64d-119">Uma aplicação cliente que envia o Iot hub tooyour mensagens</span><span class="sxs-lookup"><span data-stu-id="6c64d-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="6c64d-120">Transferir o Git</span><span class="sxs-lookup"><span data-stu-id="6c64d-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="6c64d-121">Criar uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="6c64d-121">Create a web app</span></span>

1. <span data-ttu-id="6c64d-122">No Olá [portal do Azure](https://ms.portal.azure.com/), clique em **novo** > **Web + móvel** > **aplicação Web**.</span><span class="sxs-lookup"><span data-stu-id="6c64d-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="6c64d-123">Introduza um nome de tarefa exclusivo, certifique-se de subscrição de Olá, especifique um grupo de recursos e uma localização, selecione **Pin toodashboard**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6c64d-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="6c64d-124">Recomendamos que selecione Olá mesma localização que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c64d-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="6c64d-125">Se o fizer, auxilia com velocidade de processamento e reduz o custo de Olá de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="6c64d-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Criar uma aplicação Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="6c64d-127">Configurar Olá web tooread os dados da aplicação do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="6c64d-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="6c64d-128">Abra a aplicação de web de Olá que apenas tiver sido aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="6c64d-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="6c64d-129">Clique em **definições da aplicação**e, em **as definições de aplicação**, adicionar Olá pares chave/valor a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c64d-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="6c64d-130">Chave</span><span class="sxs-lookup"><span data-stu-id="6c64d-130">Key</span></span>                                   | <span data-ttu-id="6c64d-131">Valor</span><span class="sxs-lookup"><span data-stu-id="6c64d-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="6c64d-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="6c64d-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="6c64d-133">Obtidos a partir do Explorador do iothub</span><span class="sxs-lookup"><span data-stu-id="6c64d-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="6c64d-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="6c64d-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="6c64d-135">nome de Olá do grupo de consumidores Olá que adicione tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="6c64d-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Adicionar a aplicação de web de tooyour definições com pares chave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="6c64d-137">Clique em **definições da aplicação**, em **definições gerais**, Olá alternar **Web sockets** opção e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c64d-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Ative a opção de sockets Olá Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="6c64d-139">Carregar um toobe de aplicações web alojada pelo Olá web app</span><span class="sxs-lookup"><span data-stu-id="6c64d-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="6c64d-140">No GitHub, fizemos disponível uma aplicação web que apresenta dados de sensores em tempo real a partir do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c64d-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="6c64d-141">Tudo o que precisa toodo é configurar toowork de aplicação web de Olá com um repositório de Git, transfira a aplicação web de Olá a partir do GitHub e, em seguida, carregue-o tooAzure para Olá web app toohost.</span><span class="sxs-lookup"><span data-stu-id="6c64d-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="6c64d-142">Na aplicação web de Olá, clique em **opções de implementação** > **Escolher origem** > **repositório de Git Local**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c64d-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurar o web app implementação toouse Olá repositório de Git local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="6c64d-144">Clique em **as credenciais de implementação**, criar um utilizador nome e palavra-passe toouse tooconnect toohello repositório de Git no Azure e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c64d-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="6c64d-145">Clique em **descrição geral**e anote o valor Olá **url de clone de Git**.</span><span class="sxs-lookup"><span data-stu-id="6c64d-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Obter o URL do clone de Git Olá da sua aplicação web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="6c64d-147">Abra uma janela de terminal no seu computador local ou um comando.</span><span class="sxs-lookup"><span data-stu-id="6c64d-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="6c64d-148">Transferir a aplicação web de Olá a partir do GitHub e carregá-la tooAzure para Olá web app toohost.</span><span class="sxs-lookup"><span data-stu-id="6c64d-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="6c64d-149">toodo por isso, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6c64d-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="6c64d-150">\<URL de clone de Git\> é Olá URL do repositório de Git Olá encontrado no Olá **descrição geral** página da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="6c64d-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="6c64d-151">Abrir Olá web toosee em tempo real relativos à temperatura e humidade dados da aplicação a partir do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="6c64d-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="6c64d-152">No Olá **descrição geral** página da sua aplicação web, clique em Olá URL tooopen Olá web app.</span><span class="sxs-lookup"><span data-stu-id="6c64d-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Obter URL Olá da sua aplicação web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="6c64d-154">Deverá ver a temperatura em tempo real Olá e os dados de humidade do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c64d-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Página da aplicação Web em tempo real temperatura e humidade a mostrar](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="6c64d-156">Certifique-se a aplicação de exemplo de Olá está em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6c64d-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="6c64d-157">Se não, obterá um gráfico em branco, pode consultar toohello tutoriais em [configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6c64d-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c64d-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6c64d-158">Next steps</span></span>
<span data-ttu-id="6c64d-159">Utilizou com êxito os dados de sensores em tempo real de toovisualize de aplicação web do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c64d-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="6c64d-160">Para um maneira toovisualize de dados do IoT Hub do Azure, consulte [dados de sensores em tempo real de toovisualize Power BI da utilização do seu IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6c64d-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
