## <a name="view-device-telemetry-in-hello-dashboard"></a>Ver telemetria do dispositivo no dashboard de Olá
dashboard de Olá no Olá ativa de solução tooview Olá telemetria tooIoT Hub de enviar os seus dispositivos de monitorização remota.

1. No seu browser, toohello retorno solução dashboard de monitorização remota, clique em **dispositivos** no Olá painel da esquerda toonavigate toohello **lista de dispositivos**.
2. No Olá **lista de dispositivos**, deverá ver que o estado de Olá do seu dispositivo é **executar**. Se não estiver, clique em **ativar dispositivos** no Olá **detalhes do dispositivo** painel.
   
    ![Ver o estado do dispositivo][18]
3. Clique em **Dashboard** tooreturn toohello dashboard, selecione o seu dispositivo no Olá **dispositivo tooView** pendente tooview sua telemetria. Olá a telemetria de aplicação de exemplo de Olá é 50 unidades de temperatura interna, 55 unidades para a temperatura externa e 50 unidades para humidade.
   
    ![Ver a telemetria do dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Invocar um método no seu dispositivo
dashboard de Olá na solução de monitorização remota Olá permite-lhe tooinvoke métodos nos seus dispositivos através do IoT Hub. Por exemplo, na solução de monitorização remota Olá pode invocar toosimulate um método reiniciar um dispositivo.

1. No Olá solução dashboard de monitorização remota, clique em **dispositivos** no Olá painel da esquerda toonavigate toohello **lista de dispositivos**.
2. Clique em **ID de dispositivo** para o seu dispositivo no Olá **lista de dispositivos**.
3. No Olá **detalhes do dispositivo** painel, clique em **métodos**.
   
    ![Métodos do dispositivo][13]
4. No Olá **método** pendente, selecione **InitiateFirmwareUpdate**e, em seguida, no **FWPACKAGEURI** introduzir um URL fictício. Clique em **invocar método** toocall o método de Olá no dispositivo Olá.
   
    ![Invocar um método de dispositivo][14]
   

5. Verá uma mensagem na consola de Olá executar o seu código de dispositivo quando o dispositivo de Olá processa método Olá. resultados de Olá do método Olá são adicionados toohello histórico no portal de solução Olá:

    ![Ver o histórico do método][img-method-history]

## <a name="next-steps"></a>Passos seguintes
artigo de Olá [Customizing soluções pré-configuradas] [ lnk-customize] descreve algumas formas pode expandir este exemplo. As extensões possíveis incluem a utilização de sensores reais e a implementação de comandos adicionais.

Pode saber mais sobre Olá [permissões no site azureiotsuite.com de Olá][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
