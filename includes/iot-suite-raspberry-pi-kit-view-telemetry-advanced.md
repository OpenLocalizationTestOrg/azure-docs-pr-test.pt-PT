## <a name="view-hello-telemetry"></a>Telemetria de visualizações de Olá

Olá Raspberry Pi agora está a enviar solução de monitorização remota telemetria toohello. Pode ver a telemetria de Olá no dashboard da solução Olá. Também pode enviar mensagens tooyour Raspberry Pi a partir do dashboard de solução Olá.

- Navegue toohello dashboard da solução.
- Selecione o seu dispositivo no Olá **dispositivo tooView** pendente.
- a telemetria de Olá de Olá Raspberry Pi apresenta no dashboard de Olá.

![Apresentar a telemetria de Olá Raspberry Pi][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Iniciar a atualização de firmware Olá

processo de atualização de firmware Olá transfere e instala uma versão atualizada da aplicação de cliente de dispositivo Olá em Olá Raspberry Pi. Para obter mais informações sobre o processo de atualização de firmware Olá, consulte a descrição de Olá padrão de atualização de firmware Olá no [descrição geral da gestão de dispositivos do IoT hub][lnk-update-pattern].

Iniciar o processo de atualização de firmware Olá ao invocar um método no dispositivo Olá. Este método é assíncrono e devolve assim que o processo de atualização de Olá começa. Olá dispositivo utiliza comunicadas solução do propriedades toonotify Olá sobre progresso Olá da atualização de Olá.

Invocar métodos no seu Raspberry Pi a partir do dashboard de solução Olá. Quando Olá Raspberry Pi ligado pela primeira vez toohello solução de monitorização remota, envia informações sobre métodos de Olá suporta. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
