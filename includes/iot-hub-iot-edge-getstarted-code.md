## <a name="typical-output"></a>Resultado típico

Olá exemplo seguinte mostra saída Olá escrita toohello ficheiro de registo pelo exemplo de Olá mundo Olá. saída de Olá está formatada corretamente para melhorar a legibilidade:

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

## <a name="code-snippets"></a>Fragmentos de código

Esta secção descreve algumas secções principais do código Olá Olá Olá\_exemplo mundo.

### <a name="iot-edge-gateway-creation"></a>Criação do gateway de IoT Edge

Tem de implementar um *processo gateway*. Este programa cria a infra-estrutura interna de Olá (Mediador de Olá), carrega os módulos de limite de IoT Olá e configura o processo de gateway Olá. Limite de IoT fornece Olá **Gateway\_criar\_de\_JSON** funcionar tooenable toobootstrap um gateway a partir de um ficheiro JSON. Olá toouse **Gateway\_criar\_de\_JSON** funcionar, transmita-Olá caminho tooa ficheiro de JSON que especifica Olá tooload de módulos de limite de IoT.

Pode encontrar Olá código para o processo de gateway Olá no Olá *Olá mundo* exemplo no Olá [Main] [ lnk-main-c] ficheiro. Para melhorar a legibilidade, hello fragmento seguinte mostra uma versão abreviada do código de processo do gateway Olá. Este programa de exemplo cria um gateway e, em seguida, aguarda que Olá do Olá utilizador toopress **ENTER** antes de fechar o gateway de Olá da chave.

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

ficheiro de definições JSON de Olá contém uma lista de tooload de módulos de limite de IoT e ligações de Olá entre módulos Olá. Cada módulo IoT limite tem de especificar um:

* **nome**: um nome exclusivo para o módulo Olá.
* **carregador**: um carregador de que sabe como Olá tooload pretendido módulo. Carregadores são um ponto de extensão para carregar diferentes tipos de módulos. Limite de IoT fornece carregadores para utilização com módulos escritos em nativo C, Node.js, Java e .NET. exemplo de Olá mundo Olá utiliza apenas carregador de C nativo Olá porque todos os módulos de Olá neste exemplo são dinâmicas bibliotecas escritas no C. Para obter mais informações sobre como módulos de limite de IoT toouse escritos em idiomas diferentes, consulte Olá [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), ou [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) amostras.
    * **nome**: nome Olá carregador Olá utilizado o módulo de Olá tooload.
    * **EntryPoint**: biblioteca de toohello Olá caminho que contém o módulo Olá. No Linux, esta biblioteca é um ficheiro .so; no Windows, é um ficheiro .dll. ponto de entrada Olá é o tipo de toohello específico de carregador a ser utilizado. Olá ponto de entrada do Node.js carregador é um ficheiro. js. Olá ponto de entrada do Java loader é um classpath e um nome de classe. Olá ponto de entrada do carregador de .NET é um nome de assemblagem e um nome de classe.

* **args**: necessita de qualquer módulo de Olá de informações de configuração.

Olá, Olá seguinte código mostra Olá JSON utilizado toodeclare todos os módulos de limite de IoT para o exemplo de Olá mundo Olá no Linux. Se um módulo requer argumentos depende da estrutura de Olá do módulo Olá. Neste exemplo, o módulo de registo de Olá assume um argumento que seja Olá caminho toohello ficheiro e de saída Olá Olá\_módulo mundo tem sem argumentos.

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

ficheiro JSON Olá também contém ligações de Olá entre módulos Olá que são transmitidos toohello mediador. As ligações têm duas propriedades:

* **origem**: um nome de módulo de Olá `modules` secção, ou `\*`.
* **sink**: um nome de módulo de Olá `modules` secção.

Cada ligação define uma rota e direção de mensagem. Mensagens de Olá **origem** módulo são entregues toohello **sink** módulo. Pode definir Olá **origem** módulo demasiado`\*`, que indica que Olá **sink** módulo recebe mensagens de qualquer módulo.

Olá código seguinte mostra Olá JSON utilizado tooconfigure ligações entre os módulos de Olá utilizados Olá Olá\_exemplo mundo no Linux. Cada mensagem produzido pelo Olá `hello_world` módulo é consumido pelo Olá `logger` módulo.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Publicação de mensagens do módulo hello\_world

Pode encontrar código Olá utilizado pelo Olá Olá\_mensagens toopublish do módulo do mundo no Olá ['hello_world'] [ lnk-helloworld-c] ficheiro. Olá fragmento seguinte mostra uma versão modificada do código Olá com comentários adicionados e algum código removido para melhorar a legibilidade de processamento de erros:

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

### <a name="helloworld-module-message-processing"></a>Processamento de mensagens do módulo hello\_world

Olá Olá\_módulo mundo nunca processa mensagens que outros módulos de limite de IoT publicar toohello mediador. Por conseguinte, Olá implementação de chamada de retorno de mensagem de Olá no Olá Olá\_módulo mundo é uma função sem operações.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Processamento e publicação de mensagens do módulo de registo

módulo de registo Olá recebe mensagens do Mediador de Olá e escreve-los tooa ficheiro. Nunca publica mensagens. Por conseguinte, Olá do módulo de registo Olá nunca chama Olá **Broker_Publish** função.

Olá **Logger_Receive** funcionar em Olá [Logger] [ lnk-logger-c] ficheiro é o Mediador de Olá de chamada de retorno de Olá invoca o módulo de registo do toodeliver mensagens toohello. Olá fragmento seguinte mostra uma versão modificada com comentários adicionados e algum código removido para melhorar a legibilidade de processamento de erros:

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

## <a name="next-steps"></a>Passos seguintes

Neste artigo, foi executado um gateway de IoT Edge simple que escreve o ficheiro de registo de tooa de mensagens. toorun uma amostra que envia mensagens tooIoT Hub, consulte [contorno de IoT – enviar mensagens do dispositivo-nuvem com um dispositivo simulado com Linux] [ lnk-gateway-simulated-linux] ou [contorno de IoT – enviar mensagens dispositivo-nuvem com um dispositivo simulado com Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md