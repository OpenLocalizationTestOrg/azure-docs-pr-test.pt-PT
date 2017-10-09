## <a name="create-a-device-identity"></a>Criar uma identidade de dispositivo

Nesta secção, utilize uma ferramenta de Node.js chamada [iothub explorer] [ iot-hub-explorer] toocreate uma identidade de dispositivo para este tutorial. Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.

1. Execute o seguinte Olá no seu ambiente de linha de comandos:

    `npm install -g iothub-explorer@latest`

1. Em seguida, execute Olá hub de tooyour toologin de comando a seguir. Substitute `{iot hub connection string}` com Olá cadeia de ligação do IoT Hub que copiou anteriormente:

    `iothub-explorer login "{iot hub connection string}"`

1. Por fim, crie uma nova identidade de dispositivo chamada `myDeviceId` com comando Olá:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Tome nota da cadeia de ligação do dispositivo Olá do resultado de Olá. Esta cadeia de ligação do dispositivo é utilizada por Olá dispositivo aplicação tooconnect tooyour IoT Hub como um dispositivo.

![][img-identity]

Consulte demasiado[introdução ao IoT Hub] [ lnk-getstarted] tooprogrammatically criar as identidades de dispositivo.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
