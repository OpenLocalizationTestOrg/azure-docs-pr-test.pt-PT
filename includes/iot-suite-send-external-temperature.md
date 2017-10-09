## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="af4c0-101">Configurar o dispositivo simulado do Olá Node.js</span><span class="sxs-lookup"><span data-stu-id="af4c0-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="af4c0-102">No dashboard de monitorização remota de Olá, clique em **+ adicionar um dispositivo** e, em seguida, adicione um *personalizadas do dispositivo*.</span><span class="sxs-lookup"><span data-stu-id="af4c0-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="af4c0-103">Tome nota do Olá IoT Hub, nome de anfitrião, a id de dispositivo e a chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="af4c0-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="af4c0-104">Terá de-los mais tarde no tutorial quando preparar a aplicação de cliente de dispositivo do Olá remote_monitoring.js.</span><span class="sxs-lookup"><span data-stu-id="af4c0-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="af4c0-105">Certifique-se de que a versão Node.js 0.12 ou posterior está instalado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="af4c0-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="af4c0-106">Executar `node --version` numa linha de comandos ou numa versão shell toocheck Olá.</span><span class="sxs-lookup"><span data-stu-id="af4c0-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="af4c0-107">Para obter informações sobre como utilizar um tooinstall do Gestor de pacote Node.js no Linux, consulte [instalar Node.js através do Gestor de pacote][node-linux].</span><span class="sxs-lookup"><span data-stu-id="af4c0-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="af4c0-108">Quando instalou o Node.js, clonar a versão mais recente do Olá do Olá [azure-iot-sdk-nó] [ lnk-github-repo] máquina de desenvolvimento do repositório tooyour.</span><span class="sxs-lookup"><span data-stu-id="af4c0-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="af4c0-109">Utilize sempre Olá **mestre** ramo para a versão mais recente do Olá das bibliotecas de Olá e exemplos.</span><span class="sxs-lookup"><span data-stu-id="af4c0-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="af4c0-110">Na sua cópia local do Olá [azure-iot-sdk-nó] [ lnk-github-repo] repositório, Olá cópia seguintes dois ficheiros de Olá nó/dispositivo/samples tooan vazio pasta no computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="af4c0-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="af4c0-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="af4c0-111">packages.json</span></span>
   * <span data-ttu-id="af4c0-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="af4c0-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="af4c0-113">Abrir o ficheiro de remote_monitoring.js Olá e procure a seguinte definição de variável de Olá:</span><span class="sxs-lookup"><span data-stu-id="af4c0-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="af4c0-114">Substitua **[cadeia de ligação do dispositivo IoT Hub]** com a cadeia de ligação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="af4c0-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="af4c0-115">Utilize valores de Olá para o nome de anfitrião do IoT Hub, o id de dispositivo e a chave de dispositivo que tomou nota no passo 1.</span><span class="sxs-lookup"><span data-stu-id="af4c0-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="af4c0-116">Uma cadeia de ligação do dispositivo tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="af4c0-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="af4c0-117">Se o seu nome de anfitrião do IoT Hub é **contoso** e o id do dispositivo é **mydevice**, a cadeia de ligação aspeto Olá seguinte fragmento:</span><span class="sxs-lookup"><span data-stu-id="af4c0-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Guarde o ficheiro de Olá. <span data-ttu-id="af4c0-119">Executar Olá os seguintes comandos numa linha de comandos na pasta de Olá que contenha estes pacotes necessários ficheiros tooinstall Olá ou shell e execute a aplicação de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="af4c0-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="af4c0-120">Observar telemetria dinâmica em ação</span><span class="sxs-lookup"><span data-stu-id="af4c0-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="af4c0-121">dashboard de Olá mostra Olá temperatura e humidade a telemetria de dispositivos simulados existente de Olá:</span><span class="sxs-lookup"><span data-stu-id="af4c0-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![dashboard de predefinição Olá][image1]

<span data-ttu-id="af4c0-123">Se selecionar a dispositivo do Node.js de Olá simulado que executou na secção anterior Olá, consulte temperatura, a humidade e a telemetria de temperatura externa:</span><span class="sxs-lookup"><span data-stu-id="af4c0-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Adicionar temperatura externa toohello dashboard][image2]

<span data-ttu-id="af4c0-125">solução de monitorização remota Olá Deteta tipo de telemetria de temperatura externa adicionais Olá e adiciona-o gráfico de toohello no dashboard de Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="af4c0-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png