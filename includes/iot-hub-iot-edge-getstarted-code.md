## <a name="typical-output"></a><span data-ttu-id="b33ad-101">Resultado típico</span><span class="sxs-lookup"><span data-stu-id="b33ad-101">Typical output</span></span>

<span data-ttu-id="b33ad-102">Olá exemplo seguinte mostra saída Olá escrita toohello ficheiro de registo pelo exemplo de Olá mundo Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="b33ad-103">saída de Olá está formatada corretamente para melhorar a legibilidade:</span><span class="sxs-lookup"><span data-stu-id="b33ad-103">hello output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="b33ad-104">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="b33ad-104">Code snippets</span></span>

<span data-ttu-id="b33ad-105">Esta secção descreve algumas secções principais do código Olá Olá Olá\_exemplo mundo.</span><span class="sxs-lookup"><span data-stu-id="b33ad-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="b33ad-106">Criação do gateway de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b33ad-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="b33ad-107">Tem de implementar um *processo gateway*.</span><span class="sxs-lookup"><span data-stu-id="b33ad-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="b33ad-108">Este programa cria a infra-estrutura interna de Olá (Mediador de Olá), carrega os módulos de limite de IoT Olá e configura o processo de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="b33ad-109">Limite de IoT fornece Olá **Gateway\_criar\_de\_JSON** funcionar tooenable toobootstrap um gateway a partir de um ficheiro JSON.</span><span class="sxs-lookup"><span data-stu-id="b33ad-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="b33ad-110">Olá toouse **Gateway\_criar\_de\_JSON** funcionar, transmita-Olá caminho tooa ficheiro de JSON que especifica Olá tooload de módulos de limite de IoT.</span><span class="sxs-lookup"><span data-stu-id="b33ad-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="b33ad-111">Pode encontrar Olá código para o processo de gateway Olá no Olá *Olá mundo* exemplo no Olá [Main] [ lnk-main-c] ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b33ad-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="b33ad-112">Para melhorar a legibilidade, hello fragmento seguinte mostra uma versão abreviada do código de processo do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="b33ad-113">Este programa de exemplo cria um gateway e, em seguida, aguarda que Olá do Olá utilizador toopress **ENTER** antes de fechar o gateway de Olá da chave.</span><span class="sxs-lookup"><span data-stu-id="b33ad-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="b33ad-114">ficheiro de definições JSON de Olá contém uma lista de tooload de módulos de limite de IoT e ligações de Olá entre módulos Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="b33ad-115">Cada módulo IoT limite tem de especificar um:</span><span class="sxs-lookup"><span data-stu-id="b33ad-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="b33ad-116">**nome**: um nome exclusivo para o módulo Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="b33ad-117">**carregador**: um carregador de que sabe como Olá tooload pretendido módulo.</span><span class="sxs-lookup"><span data-stu-id="b33ad-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="b33ad-118">Carregadores são um ponto de extensão para carregar diferentes tipos de módulos.</span><span class="sxs-lookup"><span data-stu-id="b33ad-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="b33ad-119">Limite de IoT fornece carregadores para utilização com módulos escritos em nativo C, Node.js, Java e .NET.</span><span class="sxs-lookup"><span data-stu-id="b33ad-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="b33ad-120">exemplo de Olá mundo Olá utiliza apenas carregador de C nativo Olá porque todos os módulos de Olá neste exemplo são dinâmicas bibliotecas escritas no C. Para obter mais informações sobre como módulos de limite de IoT toouse escritos em idiomas diferentes, consulte Olá [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), ou [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) amostras.</span><span class="sxs-lookup"><span data-stu-id="b33ad-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="b33ad-121">**nome**: nome Olá carregador Olá utilizado o módulo de Olá tooload.</span><span class="sxs-lookup"><span data-stu-id="b33ad-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="b33ad-122">**EntryPoint**: biblioteca de toohello Olá caminho que contém o módulo Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="b33ad-123">No Linux, esta biblioteca é um ficheiro .so; no Windows, é um ficheiro .dll.</span><span class="sxs-lookup"><span data-stu-id="b33ad-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="b33ad-124">ponto de entrada Olá é o tipo de toohello específico de carregador a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="b33ad-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="b33ad-125">Olá ponto de entrada do Node.js carregador é um ficheiro. js.</span><span class="sxs-lookup"><span data-stu-id="b33ad-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="b33ad-126">Olá ponto de entrada do Java loader é um classpath e um nome de classe.</span><span class="sxs-lookup"><span data-stu-id="b33ad-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="b33ad-127">Olá ponto de entrada do carregador de .NET é um nome de assemblagem e um nome de classe.</span><span class="sxs-lookup"><span data-stu-id="b33ad-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="b33ad-128">**args**: necessita de qualquer módulo de Olá de informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="b33ad-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="b33ad-129">Olá, Olá seguinte código mostra Olá JSON utilizado toodeclare todos os módulos de limite de IoT para o exemplo de Olá mundo Olá no Linux.</span><span class="sxs-lookup"><span data-stu-id="b33ad-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="b33ad-130">Se um módulo requer argumentos depende da estrutura de Olá do módulo Olá.</span><span class="sxs-lookup"><span data-stu-id="b33ad-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="b33ad-131">Neste exemplo, o módulo de registo de Olá assume um argumento que seja Olá caminho toohello ficheiro e de saída Olá Olá\_módulo mundo tem sem argumentos.</span><span class="sxs-lookup"><span data-stu-id="b33ad-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="b33ad-132">ficheiro JSON Olá também contém ligações de Olá entre módulos Olá que são transmitidos toohello mediador.</span><span class="sxs-lookup"><span data-stu-id="b33ad-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="b33ad-133">As ligações têm duas propriedades:</span><span class="sxs-lookup"><span data-stu-id="b33ad-133">A link has two properties:</span></span>

* <span data-ttu-id="b33ad-134">**origem**: um nome de módulo de Olá `modules` secção, ou `\*`.</span><span class="sxs-lookup"><span data-stu-id="b33ad-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="b33ad-135">**sink**: um nome de módulo de Olá `modules` secção.</span><span class="sxs-lookup"><span data-stu-id="b33ad-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="b33ad-136">Cada ligação define uma rota e direção de mensagem.</span><span class="sxs-lookup"><span data-stu-id="b33ad-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="b33ad-137">Mensagens de Olá **origem** módulo são entregues toohello **sink** módulo.</span><span class="sxs-lookup"><span data-stu-id="b33ad-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="b33ad-138">Pode definir Olá **origem** módulo demasiado`\*`, que indica que Olá **sink** módulo recebe mensagens de qualquer módulo.</span><span class="sxs-lookup"><span data-stu-id="b33ad-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="b33ad-139">Olá código seguinte mostra Olá JSON utilizado tooconfigure ligações entre os módulos de Olá utilizados Olá Olá\_exemplo mundo no Linux.</span><span class="sxs-lookup"><span data-stu-id="b33ad-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="b33ad-140">Cada mensagem produzido pelo Olá `hello_world` módulo é consumido pelo Olá `logger` módulo.</span><span class="sxs-lookup"><span data-stu-id="b33ad-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="b33ad-141">Publicação de mensagens do módulo hello\_world</span><span class="sxs-lookup"><span data-stu-id="b33ad-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="b33ad-142">Pode encontrar código Olá utilizado pelo Olá Olá\_mensagens toopublish do módulo do mundo no Olá ['hello_world'] [ lnk-helloworld-c] ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b33ad-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="b33ad-143">Olá fragmento seguinte mostra uma versão modificada do código Olá com comentários adicionados e algum código removido para melhorar a legibilidade de processamento de erros:</span><span class="sxs-lookup"><span data-stu-id="b33ad-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="b33ad-144">Processamento de mensagens do módulo hello\_world</span><span class="sxs-lookup"><span data-stu-id="b33ad-144">Hello\_world module message processing</span></span>

<span data-ttu-id="b33ad-145">Olá Olá\_módulo mundo nunca processa mensagens que outros módulos de limite de IoT publicar toohello mediador.</span><span class="sxs-lookup"><span data-stu-id="b33ad-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="b33ad-146">Por conseguinte, Olá implementação de chamada de retorno de mensagem de Olá no Olá Olá\_módulo mundo é uma função sem operações.</span><span class="sxs-lookup"><span data-stu-id="b33ad-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="b33ad-147">Processamento e publicação de mensagens do módulo de registo</span><span class="sxs-lookup"><span data-stu-id="b33ad-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="b33ad-148">módulo de registo Olá recebe mensagens do Mediador de Olá e escreve-los tooa ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b33ad-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="b33ad-149">Nunca publica mensagens.</span><span class="sxs-lookup"><span data-stu-id="b33ad-149">It never publishes any messages.</span></span> <span data-ttu-id="b33ad-150">Por conseguinte, Olá do módulo de registo Olá nunca chama Olá **Broker_Publish** função.</span><span class="sxs-lookup"><span data-stu-id="b33ad-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="b33ad-151">Olá **Logger_Receive** funcionar em Olá [Logger] [ lnk-logger-c] ficheiro é o Mediador de Olá de chamada de retorno de Olá invoca o módulo de registo do toodeliver mensagens toohello.</span><span class="sxs-lookup"><span data-stu-id="b33ad-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="b33ad-152">Olá fragmento seguinte mostra uma versão modificada com comentários adicionados e algum código removido para melhorar a legibilidade de processamento de erros:</span><span class="sxs-lookup"><span data-stu-id="b33ad-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="b33ad-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b33ad-153">Next steps</span></span>

<span data-ttu-id="b33ad-154">Neste artigo, foi executado um gateway de IoT Edge simple que escreve o ficheiro de registo de tooa de mensagens.</span><span class="sxs-lookup"><span data-stu-id="b33ad-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="b33ad-155">toorun uma amostra que envia mensagens tooIoT Hub, consulte [contorno de IoT – enviar mensagens do dispositivo-nuvem com um dispositivo simulado com Linux] [ lnk-gateway-simulated-linux] ou [contorno de IoT – enviar mensagens dispositivo-nuvem com um dispositivo simulado com Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="b33ad-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md