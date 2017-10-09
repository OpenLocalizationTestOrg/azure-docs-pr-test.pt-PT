> [!div class="op_single_selector"]
> * [<span data-ttu-id="f67fe-101">Linux</span><span class="sxs-lookup"><span data-stu-id="f67fe-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="f67fe-102">Windows</span><span class="sxs-lookup"><span data-stu-id="f67fe-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="f67fe-103">Este artigo fornece instruções detalhadas da Olá [código de exemplo Olá mundo] [ lnk-helloworld-sample] tooillustrate Olá fundamentais os componentes de Olá [Azure IoT Edge] [ lnk-iot-edge] arquitetura.</span><span class="sxs-lookup"><span data-stu-id="f67fe-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="f67fe-104">Olá exemplo utiliza Olá Azure IoT Edge toobuild um gateway simples que regista um ficheiro de tooa de mensagem "Olá mundo" cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="f67fe-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="f67fe-105">Estas instruções abrangem:</span><span class="sxs-lookup"><span data-stu-id="f67fe-105">This walkthrough covers:</span></span>

* <span data-ttu-id="f67fe-106">**Olá, mundo exemplo de arquitetura**: descreve como [conceitos de arquitetura do Azure IoT Edge] [ lnk-edge-concepts] aplicar toohello exemplo de Olá mundo e como Olá componentes se encaixam.</span><span class="sxs-lookup"><span data-stu-id="f67fe-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="f67fe-107">**Como toobuild Olá exemplo**: exemplo de Olá Olá passos toobuild necessária.</span><span class="sxs-lookup"><span data-stu-id="f67fe-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="f67fe-108">**Como toorun Olá exemplo**: exemplo de Olá Olá passos toorun necessária.</span><span class="sxs-lookup"><span data-stu-id="f67fe-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="f67fe-109">**Resultado típico**: um exemplo de Olá saída tooexpect quando executar o exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f67fe-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="f67fe-110">**Fragmentos de código**: uma coleção de tooshow de fragmentos de código como o exemplo de Olá mundo Olá implementa componentes de gateway de IoT Edge da chave.</span><span class="sxs-lookup"><span data-stu-id="f67fe-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="f67fe-111">Arquitetura do exemplo Olá Mundo</span><span class="sxs-lookup"><span data-stu-id="f67fe-111">Hello World sample architecture</span></span>
<span data-ttu-id="f67fe-112">exemplo de Olá mundo Olá ilustra os conceitos de Olá descritos na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="f67fe-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="f67fe-113">exemplo de Olá mundo Olá implementa um gateway de IoT limite que tem um pipeline composto por dois módulos de limite de IoT:</span><span class="sxs-lookup"><span data-stu-id="f67fe-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="f67fe-114">Olá *Olá mundo* módulo cria uma mensagem a cada cinco segundos e passa-toohello módulo de registo.</span><span class="sxs-lookup"><span data-stu-id="f67fe-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="f67fe-115">Olá *registador* mensagens hello do módulo escritas recebe tooa ficheiro.</span><span class="sxs-lookup"><span data-stu-id="f67fe-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Arquitetura do exemplo “Hello World” criada com o Azure IoT Edge][4]

<span data-ttu-id="f67fe-117">Conforme descrito na secção anterior Olá, Olá mundo Olá módulo não passa mensagens diretamente módulo de registo toohello cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="f67fe-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="f67fe-118">Em vez disso, publica um mediador de toohello mensagem cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="f67fe-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="f67fe-119">módulo de registo Olá recebe a mensagem de saudação do Mediador de Olá e age após, escrever Olá conteúdo de Olá mensagem tooa ficheiro.</span><span class="sxs-lookup"><span data-stu-id="f67fe-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="f67fe-120">módulo de registo Olá consome apenas mensagens do Mediador de Olá, nunca publica Mediador de toohello novas mensagens.</span><span class="sxs-lookup"><span data-stu-id="f67fe-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Como mediador Olá encaminha mensagens entre os módulos no limite de IoT do Azure][5]

<span data-ttu-id="f67fe-122">Olá figura acima mostra Olá arquitetura de exemplo de Olá mundo Olá e caminhos relativos Olá toohello ficheiros de origem que implementam partes diferentes de exemplo de Olá no Olá [repositório][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="f67fe-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="f67fe-123">Explorar o código de Olá ou utilize fragmentos de código Olá abaixo como guia.</span><span class="sxs-lookup"><span data-stu-id="f67fe-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md