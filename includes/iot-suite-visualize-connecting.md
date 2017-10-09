## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="b54c6-101">Ver telemetria do dispositivo no dashboard de Olá</span><span class="sxs-lookup"><span data-stu-id="b54c6-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="b54c6-102">dashboard de Olá no Olá ativa de solução tooview Olá telemetria tooIoT Hub de enviar os seus dispositivos de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="b54c6-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="b54c6-103">No seu browser, toohello retorno solução dashboard de monitorização remota, clique em **dispositivos** no Olá painel da esquerda toonavigate toohello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="b54c6-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="b54c6-104">No Olá **lista de dispositivos**, deverá ver que o estado de Olá do seu dispositivo é **executar**.</span><span class="sxs-lookup"><span data-stu-id="b54c6-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="b54c6-105">Se não estiver, clique em **ativar dispositivos** no Olá **detalhes do dispositivo** painel.</span><span class="sxs-lookup"><span data-stu-id="b54c6-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Ver o estado do dispositivo][18]
3. <span data-ttu-id="b54c6-107">Clique em **Dashboard** tooreturn toohello dashboard, selecione o seu dispositivo no Olá **dispositivo tooView** pendente tooview sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="b54c6-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="b54c6-108">Olá a telemetria de aplicação de exemplo de Olá é 50 unidades de temperatura interna, 55 unidades para a temperatura externa e 50 unidades para humidade.</span><span class="sxs-lookup"><span data-stu-id="b54c6-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Ver a telemetria do dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="b54c6-110">Invocar um método no seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="b54c6-110">Invoke a method on your device</span></span>
<span data-ttu-id="b54c6-111">dashboard de Olá na solução de monitorização remota Olá permite-lhe tooinvoke métodos nos seus dispositivos através do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b54c6-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="b54c6-112">Por exemplo, na solução de monitorização remota Olá pode invocar toosimulate um método reiniciar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b54c6-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="b54c6-113">No Olá solução dashboard de monitorização remota, clique em **dispositivos** no Olá painel da esquerda toonavigate toohello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="b54c6-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="b54c6-114">Clique em **ID de dispositivo** para o seu dispositivo no Olá **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="b54c6-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="b54c6-115">No Olá **detalhes do dispositivo** painel, clique em **métodos**.</span><span class="sxs-lookup"><span data-stu-id="b54c6-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Métodos do dispositivo][13]
4. <span data-ttu-id="b54c6-117">No Olá **método** pendente, selecione **InitiateFirmwareUpdate**e, em seguida, no **FWPACKAGEURI** introduzir um URL fictício.</span><span class="sxs-lookup"><span data-stu-id="b54c6-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="b54c6-118">Clique em **invocar método** toocall o método de Olá no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="b54c6-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Invocar um método de dispositivo][14]
   

5. <span data-ttu-id="b54c6-120">Verá uma mensagem na consola de Olá executar o seu código de dispositivo quando o dispositivo de Olá processa método Olá.</span><span class="sxs-lookup"><span data-stu-id="b54c6-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="b54c6-121">resultados de Olá do método Olá são adicionados toohello histórico no portal de solução Olá:</span><span class="sxs-lookup"><span data-stu-id="b54c6-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Ver o histórico do método][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="b54c6-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b54c6-123">Next steps</span></span>
<span data-ttu-id="b54c6-124">artigo de Olá [Customizing soluções pré-configuradas] [ lnk-customize] descreve algumas formas pode expandir este exemplo.</span><span class="sxs-lookup"><span data-stu-id="b54c6-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="b54c6-125">As extensões possíveis incluem a utilização de sensores reais e a implementação de comandos adicionais.</span><span class="sxs-lookup"><span data-stu-id="b54c6-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="b54c6-126">Pode saber mais sobre Olá [permissões no site azureiotsuite.com de Olá][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="b54c6-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
