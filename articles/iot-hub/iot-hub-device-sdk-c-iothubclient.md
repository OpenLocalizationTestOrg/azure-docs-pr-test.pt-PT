---
title: dispositivos de IoT aaaAzure SDK para C - IoTHubClient | Microsoft Docs
description: "Como biblioteca de IoTHubClient Olá toouse em dispositivos de IoT do Azure SDK Olá C toocreate para aplicações de dispositivo que comunicam com um IoT hub."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>Dispositivos de IoT do Azure SDK para C – mais informações sobre IoTHubClient
Olá [primeiro artigo](iot-hub-device-sdk-c-intro.md) no Olá série introduzida **dispositivos de IoT do Azure SDK para C**. Esse artigo explicado que existem duas camadas de arquitetura no SDK. A base de Olá é Olá **IoTHubClient** biblioteca que gere diretamente a comunicação com o IoT Hub. Também é Olá **serializador** biblioteca baseia-se em cima do que tooprovide serviços de serialização. Neste artigo fornecemos detalhes adicionais sobre Olá **IoTHubClient** biblioteca.

artigo anterior Olá descrito como toouse Olá **IoTHubClient** biblioteca toosend eventos tooIoT Hub e receber mensagens. Este artigo expande essa debate por explicar como gerir precisamente toomore *quando* enviar e receber dados, introduzindo-toohello **APIs de nível inferior**. Também vamos explicar como tooattach propriedades tooevents (e provenientes de mensagens) utilizando a propriedade Olá processamento funcionalidades no Olá **IoTHubClient** biblioteca. Por último, iremos fornecer explicação adicional de diferentes formas toohandle mensagens recebidas a partir do IoT Hub.

Olá artigo é concluída ao que abrangem alguns tópicos diversas, incluindo informações sobre as credenciais de dispositivo e como toochange Olá comportamento de Olá **IoTHubClient** através de opções de configuração.

Utilizaremos Olá **IoTHubClient** SDK amostras tooexplain estes tópicos. Se quiser toofollow ao longo, consulte Olá **iothub\_cliente\_exemplo\_http** e **iothub\_cliente\_exemplo\_amqp** aplicações que estão incluídas no dispositivo IoT do Azure de Olá SDK para C. tudo descrito nas seguintes secções de Olá é demonstrado nestes exemplos.

Pode encontrar Olá [ **dispositivos de IoT do Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositório e vista de detalhes de Olá API no Olá [referência da API de C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Olá APIs de nível inferior
artigo anterior Olá descrito funcionamento básico Olá Olá **IotHubClient** dentro do contexto Olá Olá **iothub\_cliente\_exemplo\_amqp** aplicação. Por exemplo, explicado como tooinitialize Olá biblioteca a utilizar este código.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Também descrita como eventos de toosend utilizando este a chamada de funções.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

artigo de Olá também descrita como tooreceive mensagens ao registar a uma função de chamada de retorno.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

artigo de Olá também mostrou como toofree recursos com o código como o seguinte Olá.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

No entanto, existem complementar funções tooeach destas APIs:

* IoTHubClient\_odas\_CreateFromConnectionString
* IoTHubClient\_odas\_SendEventAsync
* IoTHubClient\_odas\_SetMessageCallback
* IoTHubClient\_odas\_destruir

Estas funções de todos os incluem "Odas" no nome da API Olá. Além disso, os parâmetros de Olá de cada uma destas funções são homólogos de não odas tootheir idênticos. No entanto, o comportamento de Olá destas funções é diferente de uma forma importante.

Quando chamar **IoTHubClient\_CreateFromConnectionString**, bibliotecas subjacente Olá criar um novo thread que é executado em segundo plano de Olá. Envia eventos para este thread e recebe mensagens do IoT Hub. Nenhum desse thread é criado quando trabalhar com Olá "Odas" APIs. a criação do thread de segundo plano Olá Olá é um programador de toohello conveniência. Não tem tooworry sobre explicitamente enviar eventos e receber mensagens do IoT Hub – ocorre automaticamente em segundo plano de Olá. Em contrapartida, Olá "Odas" APIs dão-lhe explícito controlo sobre a comunicação com o IoT Hub, se o ficheiro necessário.

toounderstand esta melhor, vamos ver um exemplo:

Quando chamar **IoTHubClient\_SendEventAsync**, que, na verdade, está a fazer é colocar o evento de Olá numa memória intermédia. Olá thread de segundo plano que criou quando chamar **IoTHubClient\_CreateFromConnectionString** continuamente monitoriza desta memória intermédia e envia quaisquer dados que contém tooIoT Hub. Isto acontece em segundo plano de Olá em Olá mesmo tempo que Olá thread principal está a efetuar outras tarefas.

Da mesma forma, quando efetua o registo uma função de chamada de retorno para mensagens utilizando **IoTHubClient\_SetMessageCallback**, está a que dá instruções em segundo plano do Olá SDK toohave Olá thread invocar a função de chamada de retorno de Olá quando uma mensagem é foi recebido, independentemente do thread principal Olá.

Olá "Odas" APIs não criar um thread de segundo plano. Em vez disso, uma nova API tem de ser chamado tooexplicitly enviar e receber dados a partir do IoT Hub. Isto é demonstrado no seguinte exemplo de Olá.

Olá **iothub\_cliente\_exemplo\_http** aplicação que está incluída no Olá SDK demonstra Olá APIs de nível inferior. Este exemplo, vamos enviar eventos tooIoT Hub com o código como o seguinte Olá:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Olá primeiro três linhas criar mensagem de saudação e a última linha de Olá envia eventos Olá. No entanto, tal como mencionado anteriormente, "Enviar" evento de Olá significa que os dados de Olá simplesmente são colocados numa memória intermédia. Nada é transmitido na rede de Olá quando chamamos **IoTHubClient\_odas\_SendEventAsync**. Na ordem tooactually entrada Olá dados tooIoT Hub, tem de chamar **IoTHubClient\_odas\_DoWork**, tal como neste exemplo:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Este código (de Olá **iothub\_cliente\_exemplo\_http** aplicação) repetidamente chama **IoTHubClient\_odas\_DoWork** . Sempre que **IoTHubClient\_odas\_DoWork** é chamado, envia alguns eventos de memória intermédia de Olá tooIoT Hub e obtém uma mensagem em fila a ser enviada toohello dispositivo. caso última Olá significa que se registado é uma função de chamada de retorno de mensagens, em seguida, a chamada de retorno Olá é invocada (partindo do princípio de todas as mensagens são colocadas em cópia de segurança). Iremos seria registou uma função de chamada de retorno com o código como o seguinte Olá:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Olá pelo motivo que **IoTHubClient\_odas\_DoWork** é frequentemente designado ciclo for-que sempre que é denominado, envia *algumas* colocado na memória intermédia eventos tooIoT Hub e obtém *Olá junto* mensagem colocada em fila para o dispositivo de Olá. Cada chamada não é garantida toosend todos os colocado na memória intermédia de eventos ou colocadas na fila de tooretrieve todas as mensagens. Se quiser toosend todos os eventos Olá memória intermédia e, em seguida, prosseguir no processamento adicional, pode substituir este ciclo com o código como o seguinte Olá:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Este código chama **IoTHubClient\_odas\_DoWork** até que todos os eventos na memória intermédia de Olá terem sido enviados tooIoT Hub. Tenha em conta de que isto também implica que todas as mensagens em fila foram recebidas. Parte da razão de Olá para esta situação é que a verificar mensagens "all" não é determinística como uma ação. O que acontece se é possível obter "tudo" de mensagens hello, mas, em seguida, outra é enviada toohello dispositivo imediatamente após? Uma melhor toodeal de forma com que está com um tempo limite programados e. Por exemplo, a função de chamada de retorno de mensagem de Olá repor um temporizador sempre que é invocado. Pode, em seguida, escrever o processamento de toocontinue lógica se, por exemplo, não foram recebidas mensagens no Olá pela última vez *X* segundos.

Quando está a terminar ingressing eventos e receber mensagens, ser toocall se Olá correspondente função tooclean recursos.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Basicamente houver apenas um conjunto de APIs toosend e receber dados com um thread de segundo plano e outro conjunto de APIs que Olá a mesma coisa sem thread de segundo plano Olá. Muitos os programadores podem preferir Olá não - odas APIs, mas hello APIs de nível inferior são úteis quando programador Olá quiser explícito controlo sobre as transmissões de rede. Por exemplo, alguns dispositivos recolhem os dados ao longo do tempo e eventos de entrada apenas em intervalos especificados (por exemplo, uma vez uma hora ou uma vez por dia). Olá conceder APIs de nível inferior Olá controlo tooexplicitly de capacidade quando enviar e receber dados a partir do IoT Hub. Outras pessoas simplesmente preferirão simplicidade Olá esse Olá que fornecem APIs de nível inferior. Tudo acontece no thread principal Olá em vez de algumas acontecer de trabalho em segundo plano de Olá.

Qualquer modelo que escolher, ser se toobe consistente em que as APIs de utilizar. Se iniciar chamando **IoTHubClient\_odas\_CreateFromConnectionString**, certifique-se de utilizar apenas Olá correspondente APIs de nível inferior de qualquer trabalho seguimento:

* IoTHubClient\_odas\_SendEventAsync
* IoTHubClient\_odas\_SetMessageCallback
* IoTHubClient\_odas\_destruir
* IoTHubClient\_odas\_DoWork

Olá oposta também se aplica. Se iniciar com **IoTHubClient\_CreateFromConnectionString**, em seguida, utilize Olá não - odas as APIs para qualquer processamento adicional.

Olá Azure IoT dispositivo SDK para C, consulte Olá **iothub\_cliente\_exemplo\_http** para obter um exemplo de Olá concluída inferior ao nível da aplicação APIs. Olá **iothub\_cliente\_exemplo\_amqp** pode ser referenciada a aplicação para obter um exemplo completo de Olá não - odas APIs.

## <a name="property-handling"></a>Processamento de propriedade
Até ao momento quando que já descrito envio de dados, vamos tiver sido referir-se toohello corpo de mensagem de saudação. Por exemplo, considere este código:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Neste exemplo envia uma mensagem tooIoT Hub com texto de Olá "Olá mundo". No entanto, o IoT Hub permite também mensagem do propriedades toobe tooeach anexado. As propriedades são pares nome/valor que podem ser anexado toohello mensagem. Por exemplo, vamos pode modificar Olá anterior código tooattach uma mensagem de toohello da propriedade:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Vamos começar por chamar **IoTHubMessage\_propriedades** e passou-o identificador de Olá da nossa mensagem. O que vamos voltar é um **mapa\_PROCESSAR** referência que permite-nos toostart adicionar propriedades. Olá esta última opção é conseguido ao chamar **mapa\_AddOrUpdate**, que aceita uma referência tooa mapa\_identificador, o nome da propriedade Olá e o valor da propriedade Olá. Com esta API adicionamos tantos propriedades como podemos como.

Quando o evento Olá é lida **Event Hubs**, recetor Olá pode enumerar Olá propriedades e obter os valores correspondentes. Por exemplo, no .NET seria fazê acedendo Olá [coleção de propriedades no objeto de EventData Olá](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

No exemplo anterior Olá, iremos está a expor o evento de tooan propriedades que podemos enviar tooIoT Hub. As propriedades também podem ser anexados toomessages recebido a partir do IoT Hub. Se quisermos tooretrieve propriedades de uma mensagem, podemos utilizar código como o seguinte Olá na nossa função de chamada de retorno de mensagem:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

Olá chamada demasiado**IoTHubMessage\_propriedades** devolve Olá **mapa\_PROCESSAR** referência. Vamos então, passe essa referência demasiado**mapa\_GetInternals** tooobtain uma matriz de tooan de referência de Olá. o nome/valor pares (bem como uma contagem das propriedades de Olá). Nesse momento é tão simples como de Olá propriedades tooget toohello valores que queremos a enumerar.

Não tem propriedades toouse na sua aplicação. No entanto, se precisar de tooset-las em eventos ou provenientes de mensagens, hello **IoTHubClient** biblioteca torna mais fácil.

## <a name="message-handling"></a>Processamento de mensagens
Conforme indicado anteriormente, quando chegam mensagens da Olá do IoT Hub **IoTHubClient** biblioteca responde invocando uma função de chamada de retorno registado. Não há um parâmetro de retorno desta função que deserves algumas explicação adicional. Eis um excerpt da função de chamada de retorno de Olá na Olá **iothub\_cliente\_exemplo\_http** aplicação de exemplo:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Tenha em atenção que é do tipo de retorno de Olá **IOTHUBMESSAGE\_disposição\_resultado** e neste caso específico, Devolvemos **IOTHUBMESSAGE\_ACEITES**. Existem outros valores que pode devolver a partir desta função alteração como Olá **IoTHubClient** biblioteca reage toohello chamada de retorno de mensagem. Seguem-se as opções de Olá.

* **IOTHUBMESSAGE\_ACEITES** – mensagem de saudação foi processada com êxito. Olá **IoTHubClient** biblioteca não será invocar a função de chamada de retorno de Olá com Olá mesma mensagem.
* **IOTHUBMESSAGE\_rejeitado** – mensagem de saudação não foi processada e não existe nenhum toodo desire Olá, por isso, no futuro. Olá **IoTHubClient** biblioteca não deve invocar a função de chamada de retorno de Olá com Olá mesma mensagem.
* **IOTHUBMESSAGE\_ABANDONED** – a mensagem de saudação não foi processada com êxito, mas Olá **IoTHubClient** biblioteca deve invocar a função de chamada de retorno de Olá com Olá mesma mensagem.

Para Olá primeiro dois códigos de retorno, hello **IoTHubClient** biblioteca envia um tooIoT de mensagem que indica que mensagem de saudação do Hub deve ser eliminado da fila de dispositivo Olá e não entregar novamente. efeito net Olá é Olá mesmo (mensagem de saudação é eliminada da fila de dispositivo Olá), mas se a mensagem de saudação foi aceite ou rejeitada ainda é registada.  Gravar este distinção é útil toosenders de mensagem de saudação quem pode oiça comentários e saber se um dispositivo tem aceite ou rejeitou uma mensagem específica.

No caso de último Olá é enviada uma mensagem também tooIoT Hub, mas indica que essa mensagem de saudação deve ser reenviada. Normalmente, irá abandonar uma mensagem se encontrar algum erro, mas pretende tootry tooprocess Olá mensagem novamente. Em contrapartida, uma mensagem a rejeitar é adequada quando ocorrer um erro irrecuperável (ou se, simplesmente, decidir que não pretende a mensagem de saudação tooprocess).

Em qualquer caso, tenha em atenção de códigos de retorno diferentes Olá, de modo a que pode elicit comportamento Olá pretendido no Olá **IoTHubClient** biblioteca.

## <a name="alternate-device-credentials"></a>Credenciais de dispositivo alternativo
Tal como explicado anteriormente, Olá primeiro thing toodo ao trabalhar com Olá **IoTHubClient** biblioteca é tooobtain um **IOTHUB\_cliente\_PROCESSAR** com uma chamada como Olá os seguintes:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Olá argumentos demasiado**IoTHubClient\_CreateFromConnectionString** são cadeia de ligação do dispositivo Olá e um parâmetro que indica o protocolo de Olá utilizamos toocommunicate com o IoT Hub. cadeia de ligação do dispositivo Olá tem um formato que aparece da seguinte forma:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Existem quatro tipos de informações nesta cadeia: nome do IoT Hub, sufixo do IoT Hub, ID de dispositivo e chave de acesso partilhado. Obter o nome de domínio completamente qualificado (FQDN) Olá de um hub IoT quando criar a instância do hub IoT no portal do Azure de Olá — Isto dá-lhe nome de hub IoT Olá (Olá primeira parte do Olá FQDN) e o sufixo de hub IoT de Olá (Olá rest de Olá FQDN). Obter o ID de dispositivo de Olá e chave de acesso partilhado Olá quando registar o seu dispositivo com o IoT Hub (conforme descrito em Olá [artigo anterior](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** dá-lhe biblioteca de Olá tooinitialize unidirecional. Se preferir, pode criar um novo **IOTHUB\_cliente\_PROCESSAR** utilizando estes parâmetros individuais em vez de cadeia de ligação do dispositivo Olá. Isto é conseguido com Olá seguinte código:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Isto concretiza Olá mesma coisa como **IoTHubClient\_CreateFromConnectionString**.

Pode parecer que pretende toouse óbvios **IoTHubClient\_CreateFromConnectionString** em vez deste método de inicialização mais verboso. Tenha em atenção, no entanto, que, quando registar um dispositivo no IoT Hub, obter é um ID de dispositivo e a chave do dispositivo (não uma cadeia de ligação). Olá *Explorador de dispositivo* ferramenta SDK introduzida no Olá [artigo anterior](iot-hub-device-sdk-c-intro.md) utiliza bibliotecas na Olá **SDK do serviço do Azure IoT** toocreate cadeia de ligação do dispositivo de Olá do ID de dispositivo de Olá, a chave do dispositivo e o nome de anfitrião do IoT Hub. Por isso, ao chamar **IoTHubClient\_odas\_criar** poderá ser preferível porque que lhe poupa passo Olá de gerar uma cadeia de ligação. Utilize qualquer método é conveniente.

## <a name="configuration-options"></a>Opções de configuração
Até ao momento tudo descrito sobre Olá de forma Olá **IoTHubClient** biblioteca funciona reflete o comportamento predefinido. No entanto, existem algumas opções que pode definir toochange como funciona a biblioteca de Olá. Isto é conseguido ao tirar partido Olá **IoTHubClient\_odas\_SetOption** API. Neste exemplo, considere:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Existem duas opções são frequentemente utilizadas:

* **SetBatching** (bool) – se **verdadeiro**, em seguida, os dados enviados tooIoT Hub é enviada em lotes. Se **falso**, em seguida, são enviadas mensagens individualmente. predefinição de Olá é **falso**. Tenha em atenção que Olá **SetBatching** opção aplica-se apenas toohello HTTP protocolo e não toohello MQTT ou AMQP protocolos.
* **Tempo limite** (int não assinado) – este valor é representado em milissegundos. Se a enviar um pedido de HTTP ou receber uma resposta demora mais tempo superior a esse tempo, em seguida, ligação Olá exceder o tempo limite.

Olá, opção de criação de batches é importante. Por predefinição, Olá eventos de ingresses biblioteca individualmente (um único evento é independentemente demasiado passa**IoTHubClient\_odas\_SendEventAsync**). Se estiver a opção de criação de batches de Olá **verdadeiro**, biblioteca Olá recolhe os eventos tantos possível da memória intermédia de Olá (cópia de segurança toohello tamanho da mensagem máximo que o IoT Hub aceitará).  Olá batch de evento é enviada tooIoT Hub numa única chamada HTTP (eventos individuais Olá estão incluídos para uma matriz JSON). Ativar a criação de batches normalmente resulta em ganhos de desempenho grande, uma vez que está a reduzir ida e volta de rede. Reduz significativamente largura de banda, uma vez que está a enviar um conjunto de cabeçalhos de HTTP com o batch um evento, em vez de um conjunto de cabeçalhos para cada evento individual. A menos que tenha um motivo específico toodo, caso contrário, normalmente, deverá tooenable a criação de batches.

## <a name="next-steps"></a>Passos seguintes
Este artigo descreve no comportamento de Olá de detalhe de Olá **IoTHubClient** biblioteca encontrada na Olá **dispositivos de IoT do Azure SDK para C**. Com esta informação, deve ter uma boa compreensão das funcionalidades de Olá dos Olá **IoTHubClient** biblioteca. Olá [artigo seguinte](iot-hub-device-sdk-c-serializer.md) fornece detalhes semelhantes em Olá **serializador** biblioteca.

toolearn mais informações sobre desenvolver para o IoT Hub, consulte Olá [SDKs IoT do Azure][lnk-sdks].

toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
