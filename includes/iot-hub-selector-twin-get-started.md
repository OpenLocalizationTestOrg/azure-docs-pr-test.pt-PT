> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca577-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca577-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="ca577-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="ca577-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="ca577-103">C#</span><span class="sxs-lookup"><span data-stu-id="ca577-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="ca577-104">Java</span><span class="sxs-lookup"><span data-stu-id="ca577-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="ca577-105">Os dispositivos duplos são documentos JSON que armazenam informações de estado dos dispositivos (metadados, configurações e condições).</span><span class="sxs-lookup"><span data-stu-id="ca577-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="ca577-106">IoT Hub mantém um dispositivo duplo para cada dispositivo que liga tooit.</span><span class="sxs-lookup"><span data-stu-id="ca577-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="ca577-107">Utilize dispositivos duplos para:</span><span class="sxs-lookup"><span data-stu-id="ca577-107">Use device twins to:</span></span>

* <span data-ttu-id="ca577-108">Armazenar metadados do dispositivo da sua solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="ca577-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="ca577-109">Comunicarão as informações de estado atual, tais como condições (por exemplo, Olá conectividade método utilizado) e capacidades disponíveis da sua aplicação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca577-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="ca577-110">Sincronize o estado de Olá de execução longa os fluxos de trabalho (tais como atualizações de firmware e de configuração) entre uma aplicação de dispositivo e uma aplicação de back-end.</span><span class="sxs-lookup"><span data-stu-id="ca577-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="ca577-111">Consulta os metadados do dispositivo, a configuração ou o estado.</span><span class="sxs-lookup"><span data-stu-id="ca577-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="ca577-112">Dispositivos duplos foram concebidos para a sincronização de e para consultar as configurações de dispositivo e condições.</span><span class="sxs-lookup"><span data-stu-id="ca577-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="ca577-113">Mais informations no quando toouse dispositivos duplos podem ser encontrados na [compreender dispositivos duplos][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="ca577-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="ca577-114">Dispositivos duplos são armazenados num IoT hub e contenham:</span><span class="sxs-lookup"><span data-stu-id="ca577-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="ca577-115">*etiquetas*, os metadados do dispositivo acessível apenas a Olá solução de back-end;</span><span class="sxs-lookup"><span data-stu-id="ca577-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="ca577-116">*pretender propriedades*, objetos JSON modificável pela solução de Olá back-end e observable pela aplicação de dispositivo Olá; e</span><span class="sxs-lookup"><span data-stu-id="ca577-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="ca577-117">*comunicado propriedades*, objetos JSON modificável pela aplicação de dispositivo Olá e ser lido pelo Olá solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="ca577-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="ca577-118">As etiquetas e propriedades não podem conter matrizes, mas podem ser aninhados em objetos.</span><span class="sxs-lookup"><span data-stu-id="ca577-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="ca577-119">Além disso, Olá solução de back-end pode consultar dispositivos duplos com base em todos os Olá acima dados.</span><span class="sxs-lookup"><span data-stu-id="ca577-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="ca577-120">Consulte demasiado[compreender dispositivos duplos] [ lnk-twins] para obter mais informações sobre dispositivos duplos e toohello [idioma de consulta do IoT Hub] [ lnk-query] referência para consultas.</span><span class="sxs-lookup"><span data-stu-id="ca577-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="ca577-121">Neste momento, os dispositivos duplos são acessíveis apenas a partir de dispositivos que ligam tooIoT Hub através do protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="ca577-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="ca577-122">Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como toouse de aplicação de dispositivo existente do tooconvert MQTT.</span><span class="sxs-lookup"><span data-stu-id="ca577-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="ca577-123">Este tutorial mostrar-lhe como:</span><span class="sxs-lookup"><span data-stu-id="ca577-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ca577-124">Criar uma aplicação de back-end que adiciona *etiquetas* tooa dispositivo duplo e uma aplicação de dispositivo simulado que comunica a conectividade de canal como um *comunicadas propriedade* no dispositivo duplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca577-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="ca577-125">Consultar os dispositivos da sua aplicação de back-end utilizando filtros em etiquetas Olá e as propriedades que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca577-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md