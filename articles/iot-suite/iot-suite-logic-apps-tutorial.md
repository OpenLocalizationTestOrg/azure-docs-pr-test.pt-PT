---
title: aaaAzure IoT Suite e Logic Apps | Microsoft Docs
description: "Um tutorial sobre como toohook segurança Logic Apps tooAzure IoT Suite para o processo empresarial."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ad9fc-103">Tutorial: Ligar a solução de monitorização do Azure IoT Suite remota pré-configurada tooyour de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="ad9fc-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="ad9fc-104">Olá [Microsoft Azure IoT Suite] [ lnk-internetofthings] solução pré-configurada de monitorização remota é uma excelente forma tooget a trabalhar rapidamente com um conjunto de funcionalidades de ponto-a-ponto que exemplifies uma solução de IoT.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="ad9fc-105">Este tutorial orienta como tooadd aplicação lógica tooyour Microsoft Azure IoT Suite remoto solução pré-configurada de monitorização.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ad9fc-106">Estes passos demonstram como pode tirar ainda mais a sua solução de IoT ligando-o processo de negócios tooa.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="ad9fc-107">*Se pretender para instruções sobre como tooprovision uma monitorização remota solução pré-configurada, consulte o artigo [Tutorial: introdução às soluções pré-configuradas de IoT de Olá][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="ad9fc-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="ad9fc-108">Antes de começar este tutorial, deve:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="ad9fc-109">Aprovisionar Olá remoto solução pré-configurada de monitorização na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="ad9fc-110">Criar um tooenable de conta do SendGrid toosend uma mensagem de e-mail que aciona o processo de negócio.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="ad9fc-111">Pode inscrever-se para uma conta de avaliação gratuita em [SendGrid](https://sendgrid.com/) clicando **Experimente gratuitamente**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="ad9fc-112">Depois de ter registado para a sua conta de avaliação gratuita, terá de toocreate um [chave de API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) no SendGrid que concede permissões toosend correio.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="ad9fc-113">É necessário esta chave de API mais tarde no tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="ad9fc-114">toocomplete neste tutorial, terá de Visual Studio 2015 ou Visual Studio 2017 toomodify Olá as ações do Olá solução pré-configurada de back-end.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="ad9fc-115">Partindo do princípio de que já tenha sido já aprovisionada monitorização remota solução pré-configurada, navegue toohello o grupo de recursos para essa solução na Olá [portal do Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="ad9fc-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="ad9fc-116">grupo de recursos de Olá tem Olá mesmo nome como hello solução nome escolheu quando aprovisionou a sua solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ad9fc-117">No grupo de recursos de Olá, pode ver todas as Olá aprovisionado recursos do Azure para a sua solução exceto Olá aplicação Azure Active Directory que pode encontrar no Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="ad9fc-118">Olá seguinte captura de ecrã mostra um exemplo **grupo de recursos** solução pré-configurada do painel para uma monitorização remota:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="ad9fc-119">toobegin, configurar toouse de aplicação de lógica de Olá com Olá solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="ad9fc-120">Configurar Olá aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="ad9fc-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="ad9fc-121">Clique em **adicionar** , Olá parte superior do seu painel do grupo de recursos no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="ad9fc-122">Procurar **aplicação lógica**, selecione-o e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="ad9fc-123">Preencha Olá **nome** e utilize Olá mesmo **subscrição** e **grupo de recursos** que utilizou quando aprovisionou a sua solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ad9fc-124">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="ad9fc-125">Quando tiver concluído a sua implementação, pode ver Olá que aplicação lógica está listada como um recurso no seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="ad9fc-126">Clique em Painel aplicação lógica toonavigate toohello Olá aplicação lógica, selecione de Olá **aplicação lógica em branco** Olá do modelo tooopen **Designer de aplicações lógicas**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="ad9fc-127">Selecione **pedido**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-127">Select **Request**.</span></span> <span data-ttu-id="ad9fc-128">Esta ação Especifica que um pedido HTTP recebido com um JSON específico formatado atos de payload como um acionador.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="ad9fc-129">Cole o seguinte código para Olá esquema de JSON de corpo do pedido de Olá:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ad9fc-130">Pode copiar Olá URL para o post Olá HTTP depois de guardar a aplicação de lógica de Olá, mas primeiro tem de adicionar uma ação.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="ad9fc-131">Clique em **+ novo passo** sob o acionador manual.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="ad9fc-132">Em seguida, clique em **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="ad9fc-133">Procurar **SendGrid - enviar e-mail** e clique no mesmo.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="ad9fc-134">Introduza um nome para a ligação de Olá, tais como **SendGridConnection**, introduza Olá **chave de API do SendGrid** que criou quando configurar a conta do SendGrid e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="ad9fc-135">Adicionar endereços de e-mail tooboth própria Olá **de** e **para** campos.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="ad9fc-136">Adicionar **alerta de monitorização remota [DeviceId]** toohello **requerente** campo.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="ad9fc-137">No Olá **corpo da mensagem** campo, adicione **dispositivo [DeviceId] apresentou [measurementName] com o valor [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="ad9fc-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="ad9fc-138">Pode adicionar **[DeviceId]**, **[measurementName]**, e **[measuredValue]** clicando no Olá **pode inserir dados dos passos anteriores**secção.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="ad9fc-139">Clique em **guardar** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="ad9fc-140">Clique em Olá **pedido** Olá acionador e copie **Http Post toothis URL** valor.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="ad9fc-141">Este URL é necessário mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="ad9fc-142">As Logic Apps permitem-lhe toorun [vários tipos de ação] [ lnk-logic-apps-actions] incluindo ações no Office 365.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="ad9fc-143">Configurar Olá EventProcessor Web tarefa</span><span class="sxs-lookup"><span data-stu-id="ad9fc-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="ad9fc-144">Nesta secção, ligar a solução pré-configurada de toohello aplicação lógica que criou.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="ad9fc-145">toocomplete nesta tarefa, adicionar Olá URL tootrigger Olá aplicação lógica toohello ação que é acionado quando um valor de sensor dispositivo excede um limiar.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="ad9fc-146">Utilizar o git tooclone Olá mais recente versão de cliente Olá [azure-iot-remote-monitoring repositório do github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="ad9fc-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="ad9fc-147">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="ad9fc-148">No Visual Studio, abra Olá **RemoteMonitoring.sln** a partir de cópia de local de Olá do repositório de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="ad9fc-149">Abra Olá **ActionRepository.cs** ficheiro Olá **infraestrutura\\repositório** pasta.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="ad9fc-150">Olá atualização **actionIds** dicionário com Olá **Http Post toothis URL** que anotou da sua aplicação lógica da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="ad9fc-151">Guardar alterações de Olá na solução e sair do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="ad9fc-152">Implementar a partir da linha de comandos Olá</span><span class="sxs-lookup"><span data-stu-id="ad9fc-152">Deploy from hello command line</span></span>
<span data-ttu-id="ad9fc-153">Nesta secção, implementar a versão atualizada do Olá monitorização solução tooreplace Olá versão remoto atualmente em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="ad9fc-154">Os seguintes Olá [dev configuração] [ lnk-devsetup] instruções tooset configurar o ambiente para implementação.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="ad9fc-155">toodeploy localmente, siga Olá [implementação local] [ lnk-localdeploy] instruções.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="ad9fc-156">toodeploy toohello na nuvem e atualizar a implementação de nuvem existente, siga Olá [implementação na nuvem] [ lnk-clouddeploy] instruções.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="ad9fc-157">Utilize o nome de Olá da implementação original como nome da implementação Olá.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="ad9fc-158">Por exemplo, se a implementação original Olá foi chamada **demologicapp**, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="ad9fc-159">Quando Olá compilar o script é executado, não se esqueça de toouse Olá a mesma conta do Azure, subscrição, região e instância do Active Directory que utilizou quando aprovisionou a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="ad9fc-160">Ver a sua aplicação lógica em ação</span><span class="sxs-lookup"><span data-stu-id="ad9fc-160">See your Logic App in action</span></span>
<span data-ttu-id="ad9fc-161">Olá solução pré-configurada de monitorização remota tem duas regras configurar por predefinição, quando Aprovisiona uma solução.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="ad9fc-162">Ambas as regras são no Olá **SampleDevice001** dispositivo:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="ad9fc-163">Temperatura > 38.00</span><span class="sxs-lookup"><span data-stu-id="ad9fc-163">Temperature > 38.00</span></span>
* <span data-ttu-id="ad9fc-164">Humidade > 48.00</span><span class="sxs-lookup"><span data-stu-id="ad9fc-164">Humidity > 48.00</span></span>

<span data-ttu-id="ad9fc-165">regra de temperatura Olá aciona Olá **elevar alarme** ação e Olá regra humidade aciona Olá **SendMessage** ação.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="ad9fc-166">Partindo do princípio que utilizou Olá mesmo URL para ambos os Olá ações **ActionRepository** classe, os acionadores da aplicação lógica para a regra.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="ad9fc-167">Ambas as regras de utilizam SendGrid toosend toohello um e-mail **para** endereço com detalhes de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ad9fc-168">Olá aplicação lógica continua tootrigger sempre Olá limiar ser cumprido.</span><span class="sxs-lookup"><span data-stu-id="ad9fc-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="ad9fc-169">tooavoid desnecessários mensagens de correio eletrónico, pode desativar ou regras Olá na sua solução portal ou desativar Olá aplicação lógica em Olá [portal do Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="ad9fc-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="ad9fc-170">Além disso tooreceiving e-mails, também pode ver quando Olá lógica de aplicação é executada no portal de Olá:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="ad9fc-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ad9fc-171">Next steps</span></span>
<span data-ttu-id="ad9fc-172">Agora que utilizou um aplicação lógica tooconnect Olá pré-configurada solução tooa negócio processo, pode saber mais sobre as opções de Olá para personalizar as soluções pré-configuradas de Olá:</span><span class="sxs-lookup"><span data-stu-id="ad9fc-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="ad9fc-173">[Utilizar telemetria dinâmica com Olá solução pré-configurada de monitorização remota][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="ad9fc-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="ad9fc-174">[Metadados de informações do dispositivo Olá solução pré-configurada de monitorização remota][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="ad9fc-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
