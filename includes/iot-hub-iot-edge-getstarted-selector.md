> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Este artigo fornece instruções detalhadas da Olá [código de exemplo Olá mundo] [ lnk-helloworld-sample] tooillustrate Olá fundamentais os componentes de Olá [Azure IoT Edge] [ lnk-iot-edge] arquitetura. Olá exemplo utiliza Olá Azure IoT Edge toobuild um gateway simples que regista um ficheiro de tooa de mensagem "Olá mundo" cada cinco segundos.

Estas instruções abrangem:

* **Olá, mundo exemplo de arquitetura**: descreve como [conceitos de arquitetura do Azure IoT Edge] [ lnk-edge-concepts] aplicar toohello exemplo de Olá mundo e como Olá componentes se encaixam.
* **Como toobuild Olá exemplo**: exemplo de Olá Olá passos toobuild necessária.
* **Como toorun Olá exemplo**: exemplo de Olá Olá passos toorun necessária. 
* **Resultado típico**: um exemplo de Olá saída tooexpect quando executar o exemplo de Olá.
* **Fragmentos de código**: uma coleção de tooshow de fragmentos de código como o exemplo de Olá mundo Olá implementa componentes de gateway de IoT Edge da chave.


## <a name="hello-world-sample-architecture"></a>Arquitetura do exemplo Olá Mundo
exemplo de Olá mundo Olá ilustra os conceitos de Olá descritos na secção anterior Olá. exemplo de Olá mundo Olá implementa um gateway de IoT limite que tem um pipeline composto por dois módulos de limite de IoT:

* Olá *Olá mundo* módulo cria uma mensagem a cada cinco segundos e passa-toohello módulo de registo.
* Olá *registador* mensagens hello do módulo escritas recebe tooa ficheiro.

![Arquitetura do exemplo “Hello World” criada com o Azure IoT Edge][4]

Conforme descrito na secção anterior Olá, Olá mundo Olá módulo não passa mensagens diretamente módulo de registo toohello cada cinco segundos. Em vez disso, publica um mediador de toohello mensagem cada cinco segundos.

módulo de registo Olá recebe a mensagem de saudação do Mediador de Olá e age após, escrever Olá conteúdo de Olá mensagem tooa ficheiro.

módulo de registo Olá consome apenas mensagens do Mediador de Olá, nunca publica Mediador de toohello novas mensagens.

![Como mediador Olá encaminha mensagens entre os módulos no limite de IoT do Azure][5]

Olá figura acima mostra Olá arquitetura de exemplo de Olá mundo Olá e caminhos relativos Olá toohello ficheiros de origem que implementam partes diferentes de exemplo de Olá no Olá [repositório][lnk-iot-edge]. Explorar o código de Olá ou utilize fragmentos de código Olá abaixo como guia.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md