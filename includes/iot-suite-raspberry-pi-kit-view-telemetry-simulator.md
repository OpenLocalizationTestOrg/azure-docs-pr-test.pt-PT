## <a name="view-hello-telemetry"></a>Telemetria de visualizações de Olá

Olá Raspberry Pi agora está a enviar solução de monitorização remota telemetria toohello. Pode ver a telemetria de Olá no dashboard da solução Olá. Também pode enviar mensagens tooyour Raspberry Pi a partir do dashboard de solução Olá.

- Navegue toohello dashboard da solução.
- Selecione o seu dispositivo no Olá **dispositivo tooView** pendente.
- a telemetria de Olá de Olá Raspberry Pi apresenta no dashboard de Olá.

![Apresentar a telemetria de Olá Raspberry Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Atuar no dispositivo Olá

A partir do dashboard de solução Olá, pode invocar métodos no seu Raspberry Pi. Quando Olá Raspberry Pi se liga a solução de monitorização remota toohello, envia informações sobre métodos de Olá suporta.

- No dashboard de solução Olá, clique em **dispositivos** toovisit Olá **dispositivos** página. Selecione o seu Raspberry Pi na Olá **lista de dispositivos**. Em seguida, escolha **métodos**:

    ![Lista de dispositivos no dashboard][img-list-devices]

- No Olá **invocar método** página, escolha **LightBlink** no Olá **método** pendente.

- Escolha **InvokeMethod**. simulador de Olá imprima uma mensagem na consola de Olá no Olá Raspberry Pi. aplicação Olá Olá Raspberry Pi envia um dashboard de solução de back-toohello confirmação:

    ![Mostrar histórico de método][img-method-history]

- Pode mudar Olá LED e desativar a utilização Olá **ChangeLightStatus** método com um **LightStatusValue** definido demasiado**1** no ou **0** para desativado.

> [!WARNING]
> Se deixar Olá em execução na sua conta do Azure de solução de monitorização remota, é-lhe faturado por período de tempo de Olá que é executada. Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config]. Elimine a solução pré-configurada de Olá da sua conta do Azure quando tiver concluído a utilizá-la.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md