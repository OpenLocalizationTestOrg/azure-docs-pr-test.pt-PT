---
title: aaaConnect um dispositivo utilizando C no mbed | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurada solução de monitorização remota, utilizando uma aplicação de escrita no C executadas em dispositivos mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="35472-103">Ligar o seu toohello de dispositivo (mbed) de solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="35472-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="35472-104">Descrição geral do cenário</span><span class="sxs-lookup"><span data-stu-id="35472-104">Scenario overview</span></span>
<span data-ttu-id="35472-105">Neste cenário, vai criar um dispositivo que envia Olá seguir monitorização remota do telemetria toohello [solução pré-configurada][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="35472-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="35472-106">Temperatura externa</span><span class="sxs-lookup"><span data-stu-id="35472-106">External temperature</span></span>
* <span data-ttu-id="35472-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="35472-107">Internal temperature</span></span>
* <span data-ttu-id="35472-108">Humidade</span><span class="sxs-lookup"><span data-stu-id="35472-108">Humidity</span></span>

<span data-ttu-id="35472-109">Para uma simplicidade código Olá no dispositivo Olá gera valores de exemplo, mas Aconselhamo-tooextend Olá exemplo por ligar sensores real tooyour dispositivo e envia a telemetria real.</span><span class="sxs-lookup"><span data-stu-id="35472-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="35472-110">Olá é dispositivo também toomethods toorespond capaz de invocado a partir do dashboard de solução Olá e valores de propriedade definidos no dashboard de solução Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="35472-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="35472-111">toocomplete neste tutorial, precisa de uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35472-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="35472-112">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="35472-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="35472-113">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="35472-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="35472-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="35472-114">Before you start</span></span>
<span data-ttu-id="35472-115">Antes de escrever qualquer código para o seu dispositivo, terá de aprovisionar a sua solução pré-configurada de monitorização remota e aprovisionar um novo dispositivo personalizado nessa solução.</span><span class="sxs-lookup"><span data-stu-id="35472-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="35472-116">Aprovisionar a solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="35472-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="35472-117">dispositivo de Olá criar neste tutorial envia a instância de tooan de dados do Olá [monitorização remota] [ lnk-remote-monitoring] solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="35472-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="35472-118">Se não tiver sido já aprovisionada Olá solução pré-configurada na sua conta do Azure de monitorização remota, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="35472-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="35472-119">No Olá <https://www.azureiotsuite.com/> página, clique em  **+**  toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="35472-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="35472-120">Clique em **selecione** no Olá **monitorização remota** painel toocreate sua solução.</span><span class="sxs-lookup"><span data-stu-id="35472-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="35472-121">No Olá **criar solução de monitorização remota** página, introduza um **nome da solução** à sua escolha, selecione Olá **região** pretende toodeploy para e selecione Olá do Azure subscrição toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="35472-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="35472-122">Em seguida, clique em **Criar solução**.</span><span class="sxs-lookup"><span data-stu-id="35472-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="35472-123">Aguarde pela conclusão do processo de aprovisionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="35472-124">soluções de Olá pré-configuradas utilizam facturável serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="35472-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="35472-125">Certifique-se de tooremove Olá solução pré-configurada da sua subscrição quando tiver terminado com o mesmo tooavoid quaisquer custos desnecessários.</span><span class="sxs-lookup"><span data-stu-id="35472-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="35472-126">Pode remover por completo uma solução pré-configurada da sua subscrição, visitando Olá <https://www.azureiotsuite.com/> página.</span><span class="sxs-lookup"><span data-stu-id="35472-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="35472-127">Quando terminar, Olá processo para Olá solução de monitorização remota de aprovisionamento, clique em **iniciar** dashboard da solução Olá tooopen no seu browser.</span><span class="sxs-lookup"><span data-stu-id="35472-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Dashboard de soluções][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="35472-129">Aprovisionar o seu dispositivo no Olá solução de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="35472-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="35472-130">Se já tiver aprovisionado um dispositivo na sua solução, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="35472-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="35472-131">Precisa de credenciais de dispositivo tooknow Olá quando cria a aplicação de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="35472-132">Para uma solução de toohello pré-configurada tooconnect do dispositivo, tem de identificar próprio tooIoT Hub utilizando as credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="35472-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="35472-133">Pode obter credenciais de dispositivo Olá a partir do dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="35472-134">Incluir as credenciais de dispositivo Olá na sua aplicação de cliente mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="35472-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="35472-135">uma solução de monitorização remota do dispositivo tooyour tooadd, Olá concluir os seguintes passos no dashboard de solução Olá:</span><span class="sxs-lookup"><span data-stu-id="35472-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="35472-136">No Olá esquerda canto inferior do dashboard de Olá, clique em **adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="35472-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Adicionar um dispositivo][1]
2. <span data-ttu-id="35472-138">No Olá **dispositivo personalizado** painel, clique em **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="35472-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Adicionar um dispositivo personalizado][2]
3. <span data-ttu-id="35472-140">Escolha **Definir o meu próprio ID do Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="35472-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="35472-141">Introduza um ID de dispositivo como **mydevice**, clique em **verifique ID** tooverify esse nome não está já em utilização e, em seguida, clique em **criar** dispositivo de Olá tooprovision.</span><span class="sxs-lookup"><span data-stu-id="35472-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Adicionar ID do dispositivo][3]
4. <span data-ttu-id="35472-143">Se um dispositivo de Olá nota credenciais (ID de dispositivo, o nome de anfitrião do IoT Hub e a chave de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="35472-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="35472-144">A aplicação cliente tem toohello de tooconnect estes valores de solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="35472-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="35472-145">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="35472-145">Then click **Done**.</span></span>
   
    ![Ver as credenciais do dispositivo][4]
5. <span data-ttu-id="35472-147">Selecione o seu dispositivo na lista de dispositivos de Olá no dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="35472-148">Em seguida, no Olá **detalhes do dispositivo** painel, clique em **ativar dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="35472-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="35472-149">Estado de Olá do seu dispositivo está agora **executar**.</span><span class="sxs-lookup"><span data-stu-id="35472-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="35472-150">solução de monitorização remota Olá pode agora receber telemetria a partir do dispositivo e invocar métodos num dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="35472-151">Compilar e executar a solução de exemplo de Olá C</span><span class="sxs-lookup"><span data-stu-id="35472-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="35472-152">Olá instruções que se seguem descrevem Olá os passos para ligar um [preparados mbed K64F-FRDM Freescale] [ lnk-mbed-home] dispositivo toohello solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="35472-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="35472-153">Ligar a rede de tooyour Olá mbed dispositivo e a máquina de ambiente de trabalho</span><span class="sxs-lookup"><span data-stu-id="35472-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="35472-154">Ligar a rede tooyour Olá mbed dispositivo com um cabo de Ethernet.</span><span class="sxs-lookup"><span data-stu-id="35472-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="35472-155">Este passo é necessário porque a aplicação de exemplo de Olá requer acesso à internet.</span><span class="sxs-lookup"><span data-stu-id="35472-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="35472-156">Consulte [introdução mbed] [ lnk-mbed-getstarted] tooconnect o mbed dispositivo tooyour ambiente de trabalho PC.</span><span class="sxs-lookup"><span data-stu-id="35472-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="35472-157">Se o seu PC de secretária com o Windows, consulte o artigo [PC configuração] [ lnk-mbed-pcconnect] tooyour mbed dispositivo do tooconfigure porta série acesso.</span><span class="sxs-lookup"><span data-stu-id="35472-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="35472-158">Criar um projeto de mbed e importar o código de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="35472-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="35472-159">Siga estes passos tooadd algumas projeto de mbed de tooan de código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="35472-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="35472-160">Importar projeto de arranque de monitorização remota de Olá e, em seguida, altere Olá de toouse Olá projeto protocolo MQTT em vez de Olá protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="35472-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="35472-161">Atualmente, terá de toouse Olá MQTT protocolo toouse Olá funcionalidades gestão de dispositivos do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="35472-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="35472-162">No seu browser, aceda toohello mbed.org [site programador](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="35472-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="35472-163">Se ainda não inscrito, verá uma opção toocreate uma conta (é gratuito).</span><span class="sxs-lookup"><span data-stu-id="35472-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="35472-164">Caso contrário, inicie sessão com as credenciais da conta.</span><span class="sxs-lookup"><span data-stu-id="35472-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="35472-165">Em seguida, clique em **compilador** no canto direito superior da página Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="35472-166">Esta ação coloca toohello *área de trabalho* interface.</span><span class="sxs-lookup"><span data-stu-id="35472-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="35472-167">Certifique-se a plataforma de hardware de Olá estiver a utilizar é apresentado no canto direito superior da janela de Olá hello, ou clique em ícone Olá Olá canto direito tooselect sua plataforma de hardware.</span><span class="sxs-lookup"><span data-stu-id="35472-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="35472-168">Clique em **importação** no menu principal Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="35472-169">Em seguida, clique em **clique aqui tooimport a partir do URL**.</span><span class="sxs-lookup"><span data-stu-id="35472-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Área de trabalho de toombed de importação de início][6]

1. <span data-ttu-id="35472-171">Na janela de pop-up Olá, introduza a ligação de Olá para Olá exemplo código https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, em seguida, clique em **importação**.</span><span class="sxs-lookup"><span data-stu-id="35472-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importar a área de trabalho de toombed de código de exemplo][7]

1. <span data-ttu-id="35472-173">Pode ver na janela de compilador Olá mbed que também importar este projeto importa vários bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="35472-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="35472-174">Algumas são fornecidas e mantidas pela equipa do Azure IoT Olá ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), enquanto outros estão disponíveis no catálogo de bibliotecas de mbed Olá de bibliotecas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="35472-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Projeto de mbed de vista][8]

1. <span data-ttu-id="35472-176">No Olá **área de trabalho do programa**, contexto Olá **iothub\_amqp\_transporte** biblioteca, clique em **eliminar**e, em seguida, clique em **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="35472-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="35472-177">No Olá **área de trabalho do programa**, contexto Olá **azure\_amqp\_c** biblioteca, clique em **eliminar**e, em seguida, clique em **OK**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="35472-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="35472-178">Contexto Olá **remote_monitoring** projeto no Olá **área de trabalho do programa**, selecione **importação biblioteca**, em seguida, selecione **de URL**.</span><span class="sxs-lookup"><span data-stu-id="35472-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Iniciar a área de trabalho de toombed de importação de biblioteca][6]

1. <span data-ttu-id="35472-180">Na janela de pop-up Olá, introduza a ligação de Olá para Olá MQTT transporte biblioteca https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transporte /, em seguida, clique em **importação**.</span><span class="sxs-lookup"><span data-stu-id="35472-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importar a área de trabalho biblioteca toombed][12]

1. <span data-ttu-id="35472-182">Olá repetida passo tooadd Olá MQTT biblioteca anterior do https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="35472-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="35472-183">A área de trabalho aspeto agora Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="35472-183">Your workspace now looks like hello following:</span></span>

    ![Área de trabalho do Vista mbed][13]

1. <span data-ttu-id="35472-185">Abra Olá remoto\_monitoring\remote_monitoring.c ficheiro e substituir Olá existente `#include` instruções com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="35472-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="35472-186">Eliminar Olá todos os restantes código Olá remoto\_monitoring\remote\_monitoring.c ficheiro.</span><span class="sxs-lookup"><span data-stu-id="35472-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="35472-187">Compilar e executar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="35472-187">Build and run hello sample</span></span>

<span data-ttu-id="35472-188">Adicionar Olá do código tooinvoke **remoto\_monitorização\_executar** funcionar e, em seguida, criar e executar a aplicação de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="35472-189">Adicionar um **principal** função com o seguinte código no fim de Olá do Olá remoto\_Olá do monitoring.c ficheiro tooinvoke **remoto\_monitorização\_executar** função:</span><span class="sxs-lookup"><span data-stu-id="35472-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="35472-190">Clique em **compilar** programa de Olá toobuild.</span><span class="sxs-lookup"><span data-stu-id="35472-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="35472-191">Em segurança pode ignorar quaisquer avisos, mas se a compilação de Olá gerar erros, corrija-os antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="35472-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="35472-192">Se a compilação de Olá for bem-sucedida, o Web site de compilador do Olá mbed gera um ficheiro. bin com o nome de Olá do seu projeto e transfere-tooyour de computador local.</span><span class="sxs-lookup"><span data-stu-id="35472-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="35472-193">Dispositivo de cópia Olá. bin ficheiro toohello.</span><span class="sxs-lookup"><span data-stu-id="35472-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="35472-194">Guardar o dispositivo de toohello Olá. bin ficheiro faz com que Olá dispositivo toorestart e executar programa Olá contido num ficheiro. bin de Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="35472-195">Pode reiniciar manualmente o programa de Olá em qualquer altura, premindo o botão de reposição de Olá no dispositivo de mbed Olá.</span><span class="sxs-lookup"><span data-stu-id="35472-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="35472-196">Liga dispositivo toohello a utilizar uma aplicação de cliente SSH, como o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="35472-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="35472-197">Pode determinar a porta série Olá que utiliza o seu dispositivo, verificando o Gestor de dispositivos do Windows.</span><span class="sxs-lookup"><span data-stu-id="35472-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="35472-198">No PuTTY, clique em Olá **série** tipo de ligação.</span><span class="sxs-lookup"><span data-stu-id="35472-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="35472-199">dispositivo Olá liga-se normalmente na transmissão 9600, por isso, introduza 9600 no Olá **velocidade** caixa.</span><span class="sxs-lookup"><span data-stu-id="35472-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="35472-200">Em seguida, clique em **abra**.</span><span class="sxs-lookup"><span data-stu-id="35472-200">Then click **Open**.</span></span>

1. <span data-ttu-id="35472-201">programa de Olá começa a ser executada.</span><span class="sxs-lookup"><span data-stu-id="35472-201">hello program starts executing.</span></span> <span data-ttu-id="35472-202">Poderá ter quadro de Olá tooreset (prima CTRL + Break ou no botão de reposição do painel de Olá prima) se o programa de Olá não for iniciado automaticamente quando liga.</span><span class="sxs-lookup"><span data-stu-id="35472-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
