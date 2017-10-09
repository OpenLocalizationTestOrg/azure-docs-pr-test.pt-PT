## <a name="configure-hello-nodejs-simulated-device"></a>Configurar o dispositivo simulado do Olá Node.js
1. No dashboard de monitorização remota de Olá, clique em **+ adicionar um dispositivo** e, em seguida, adicione um *personalizadas do dispositivo*. Tome nota do Olá IoT Hub, nome de anfitrião, a id de dispositivo e a chave do dispositivo. Terá de-los mais tarde no tutorial quando preparar a aplicação de cliente de dispositivo do Olá remote_monitoring.js.
2. Certifique-se de que a versão Node.js 0.12 ou posterior está instalado no computador de desenvolvimento. Executar `node --version` numa linha de comandos ou numa versão shell toocheck Olá. Para obter informações sobre como utilizar um tooinstall do Gestor de pacote Node.js no Linux, consulte [instalar Node.js através do Gestor de pacote][node-linux].
3. Quando instalou o Node.js, clonar a versão mais recente do Olá do Olá [azure-iot-sdk-nó] [ lnk-github-repo] máquina de desenvolvimento do repositório tooyour. Utilize sempre Olá **mestre** ramo para a versão mais recente do Olá das bibliotecas de Olá e exemplos.
4. Na sua cópia local do Olá [azure-iot-sdk-nó] [ lnk-github-repo] repositório, Olá cópia seguintes dois ficheiros de Olá nó/dispositivo/samples tooan vazio pasta no computador de desenvolvimento:
   
   * Packages.JSON
   * remote_monitoring.js
5. Abrir o ficheiro de remote_monitoring.js Olá e procure a seguinte definição de variável de Olá:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Substitua **[cadeia de ligação do dispositivo IoT Hub]** com a cadeia de ligação do dispositivo. Utilize valores de Olá para o nome de anfitrião do IoT Hub, o id de dispositivo e a chave de dispositivo que tomou nota no passo 1. Uma cadeia de ligação do dispositivo tem Olá seguinte formato:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Se o seu nome de anfitrião do IoT Hub é **contoso** e o id do dispositivo é **mydevice**, a cadeia de ligação aspeto Olá seguinte fragmento:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Guarde o ficheiro de Olá. Executar Olá os seguintes comandos numa linha de comandos na pasta de Olá que contenha estes pacotes necessários ficheiros tooinstall Olá ou shell e execute a aplicação de exemplo de Olá:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Observar telemetria dinâmica em ação
dashboard de Olá mostra Olá temperatura e humidade a telemetria de dispositivos simulados existente de Olá:

![dashboard de predefinição Olá][image1]

Se selecionar a dispositivo do Node.js de Olá simulado que executou na secção anterior Olá, consulte temperatura, a humidade e a telemetria de temperatura externa:

![Adicionar temperatura externa toohello dashboard][image2]

solução de monitorização remota Olá Deteta tipo de telemetria de temperatura externa adicionais Olá e adiciona-o gráfico de toohello no dashboard de Olá automaticamente.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png