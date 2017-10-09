> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Introdução

No [começar a utilizar dispositivos duplos do IoT Hub][lnk-twin-tutorial], aprendeu como tooset metadados do dispositivo da sua solução de back-end utilizando *etiquetas*, relatório de condições do dispositivo a partir de uma aplicação de dispositivo utilizar *comunicadas propriedades*e consultar esta informação utilizando uma linguagem como o SQL Server.

Neste tutorial, ficará a saber como toouse Olá Olá dispositivo duplo *pretendido propriedades* juntamente com *comunicadas propriedades*, tooremotely configurar aplicações de dispositivos. Mais especificamente, este tutorial mostra como um dispositivo duplo comunicadas e propriedades pretendidas ative uma configuração de vários passo de uma aplicação de dispositivo e fornecem Olá visibilidade toohello solução de back-end do Estado de Olá desta operação em todos os dispositivos. Pode encontrar mais informações sobre a função de Olá das configurações de dispositivo no [descrição geral da gestão de dispositivos do IoT hub][lnk-dm-overview].

Um nível elevado, a utilização de dispositivos duplos permite Olá solução de back-end toospecify Olá configuração pretendida para dispositivos Olá gerido, em vez de enviar comandos específicos. Isto coloca o dispositivo de Olá responsável pela configuração Olá melhor forma tooupdate respetiva configuração (muito importante nos cenários de IoT onde condições de dispositivo específico afetam Olá capacidade tooimmediately realizar comandos específicos), ao reporting continuamente toohello solução de back-end estado atual do Olá e potenciais condições de erro do processo de atualização de Olá. Este padrão é instrumental toohello gestão de grandes conjuntos de dispositivos, como permite Olá solução de back-end toohave visibilidade total do Estado de Olá do processo de configuração de Olá em todos os dispositivos.

> [!NOTE]
> Em cenários em que os dispositivos são controlados de forma interativa mais (ative uma ventoinha a partir de uma aplicação controlados pelo utilizador), considere a utilização de [direcionar métodos][lnk-methods].
> 
> 

Neste tutorial, Olá solução de back-end alterações a configuração de telemetria de Olá de um dispositivo de destino e, como consequência disso, a aplicação de dispositivo Olá segue um processo com vários passos de tooapply uma configuração de atualizações de (por exemplo, exigir um reinício de módulo de software, o qual este Tutorial simula com um atraso simple).

Olá solução de back-end armazena a configuração de Olá nas propriedades de pretendido do Olá dispositivo duplo na Olá seguinte forma:

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
> Uma vez que as configurações podem ser objetos complexos, normalmente, são atribuídas os ids exclusivos (hashes ou [GUIDs][lnk-guid]) toosimplify os respetivos comparações.
> 
> 

Olá aplicação de dispositivo relatórios de configuração atual espelhamento propriedade Olá pretendido **telemetryConfig** no Olá comunicadas propriedades:

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

Tenha em atenção a como comunicado Olá **telemetryConfig** tem uma propriedade adicional **estado**, utilizar o estado de Olá tooreport do processo de atualização de configuração de Olá.

Quando é recebida uma nova configuração pretendida, aplicações de dispositivo Olá relatórios uma configuração pendente alterando as informações de Olá:

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

Em seguida, em algum momento posterior, Olá aplicação de dispositivo irão comunicar êxito Olá ou falha desta operação atualizando Olá acima propriedade.
Tenha em atenção a como Olá solução de back-end é capaz de, em qualquer altura, o estado de Olá tooquery do processo de configuração de Olá em todos os dispositivos de Olá.

Este tutorial mostrar-lhe como:

* Criar uma aplicação de dispositivo simulado que recebe atualizações de configuração de Olá solução de back-end e relatórios de várias atualizações como *comunicadas propriedades* na configuração de Olá o processo de atualização.
* Crie uma aplicação de back-end que Olá de atualizações de configuração pretendida de um dispositivo e, em seguida, consultas Olá o processo de atualização de configuração.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
