> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba8f5-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba8f5-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="ba8f5-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="ba8f5-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="ba8f5-103">C#</span><span class="sxs-lookup"><span data-stu-id="ba8f5-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="ba8f5-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="ba8f5-104">Introduction</span></span>

<span data-ttu-id="ba8f5-105">No [começar a utilizar dispositivos duplos do IoT Hub][lnk-twin-tutorial], aprendeu como tooset metadados do dispositivo da sua solução de back-end utilizando *etiquetas*, relatório de condições do dispositivo a partir de uma aplicação de dispositivo utilizar *comunicadas propriedades*e consultar esta informação utilizando uma linguagem como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="ba8f5-106">Neste tutorial, ficará a saber como toouse Olá Olá dispositivo duplo *pretendido propriedades* juntamente com *comunicadas propriedades*, tooremotely configurar aplicações de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="ba8f5-107">Mais especificamente, este tutorial mostra como um dispositivo duplo comunicadas e propriedades pretendidas ative uma configuração de vários passo de uma aplicação de dispositivo e fornecem Olá visibilidade toohello solução de back-end do Estado de Olá desta operação em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="ba8f5-108">Pode encontrar mais informações sobre a função de Olá das configurações de dispositivo no [descrição geral da gestão de dispositivos do IoT hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="ba8f5-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="ba8f5-109">Um nível elevado, a utilização de dispositivos duplos permite Olá solução de back-end toospecify Olá configuração pretendida para dispositivos Olá gerido, em vez de enviar comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="ba8f5-110">Isto coloca o dispositivo de Olá responsável pela configuração Olá melhor forma tooupdate respetiva configuração (muito importante nos cenários de IoT onde condições de dispositivo específico afetam Olá capacidade tooimmediately realizar comandos específicos), ao reporting continuamente toohello solução de back-end estado atual do Olá e potenciais condições de erro do processo de atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="ba8f5-111">Este padrão é instrumental toohello gestão de grandes conjuntos de dispositivos, como permite Olá solução de back-end toohave visibilidade total do Estado de Olá do processo de configuração de Olá em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8f5-112">Em cenários em que os dispositivos são controlados de forma interativa mais (ative uma ventoinha a partir de uma aplicação controlados pelo utilizador), considere a utilização de [direcionar métodos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ba8f5-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="ba8f5-113">Neste tutorial, Olá solução de back-end alterações a configuração de telemetria de Olá de um dispositivo de destino e, como consequência disso, a aplicação de dispositivo Olá segue um processo com vários passos de tooapply uma configuração de atualizações de (por exemplo, exigir um reinício de módulo de software, o qual este Tutorial simula com um atraso simple).</span><span class="sxs-lookup"><span data-stu-id="ba8f5-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="ba8f5-114">Olá solução de back-end armazena a configuração de Olá nas propriedades de pretendido do Olá dispositivo duplo na Olá seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ba8f5-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="ba8f5-115">Uma vez que as configurações podem ser objetos complexos, normalmente, são atribuídas os ids exclusivos (hashes ou [GUIDs][lnk-guid]) toosimplify os respetivos comparações.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="ba8f5-116">Olá aplicação de dispositivo relatórios de configuração atual espelhamento propriedade Olá pretendido **telemetryConfig** no Olá comunicadas propriedades:</span><span class="sxs-lookup"><span data-stu-id="ba8f5-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="ba8f5-117">Tenha em atenção a como comunicado Olá **telemetryConfig** tem uma propriedade adicional **estado**, utilizar o estado de Olá tooreport do processo de atualização de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="ba8f5-118">Quando é recebida uma nova configuração pretendida, aplicações de dispositivo Olá relatórios uma configuração pendente alterando as informações de Olá:</span><span class="sxs-lookup"><span data-stu-id="ba8f5-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="ba8f5-119">Em seguida, em algum momento posterior, Olá aplicação de dispositivo irão comunicar êxito Olá ou falha desta operação atualizando Olá acima propriedade.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="ba8f5-120">Tenha em atenção a como Olá solução de back-end é capaz de, em qualquer altura, o estado de Olá tooquery do processo de configuração de Olá em todos os dispositivos de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="ba8f5-121">Este tutorial mostrar-lhe como:</span><span class="sxs-lookup"><span data-stu-id="ba8f5-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ba8f5-122">Criar uma aplicação de dispositivo simulado que recebe atualizações de configuração de Olá solução de back-end e relatórios de várias atualizações como *comunicadas propriedades* na configuração de Olá o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="ba8f5-123">Crie uma aplicação de back-end que Olá de atualizações de configuração pretendida de um dispositivo e, em seguida, consultas Olá o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="ba8f5-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
