## <a name="create-a-device-identity"></a>Criar uma identidade de dispositivo

Esta secção, irá utilizar Olá [portal do Azure] [ lnk-azure-portal] toocreate uma identidade de dispositivo no registo de identidade Olá no seu IoT hub. Um dispositivo não é possível ligar tooIoT hub exceto se tiver uma entrada no registo de identidade Olá. Para obter mais informações, consulte a secção "Registo de identidade" Olá Olá [guia para programadores do IoT Hub][lnk-devguide-identity]. Olá **Explorador de dispositivo** no Olá portal ajuda-o a gerar um ID de dispositivo exclusivo e uma chave que o seu dispositivo pode utilizar tooidentify próprio quando estabelece ligação tooIoT Hub. Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.

1. Certifique-se de que tem sessão iniciada toohello [portal do Azure][lnk-azure-portal].

1. No Jumpbar Olá, clique em **todos os recursos** e localizar o recurso do hub IoT.

    ![Navegue tooyour Iot hub][img-find-iothub]

1. Quando o recurso do hub IoT é aberto, clique em Olá **Explorador de dispositivo** ferramenta e, em seguida, clique em **adicionar** na parte superior do Olá. Forneça o nome de Olá para o novo dispositivo, tal como **myDeviceId**e clique em **guardar**.

    ![Criar a identidade de dispositivo no portal][img-create-device]

   Esta ação cria uma nova identidade de dispositivo do seu hub IoT.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. No Olá **Explorador de dispositivo**da lista de dispositivos, clique em dispositivo Olá recém-criado e tome nota dos Olá **cadeia de ligação---chave primária**. 

    ![Cadeia de ligação do dispositivo][img-connection-string]

> [!NOTE]
> Olá registo de identidade do IoT Hub apenas armazena dispositivo identidades tooenable acesso seguro toohello do IoT hub. Armazena toouse de IDs e chaves de dispositivo como credenciais de segurança e um sinalizador ativado/desativado que pode utilizar toodisable acesso de um dispositivo individual. Se a sua aplicação tiver toostore outros metadados específicos do dispositivo, deverá utilizar um armazenamento específico da aplicação. Para obter mais informações, veja o [IoT Hub developer guide (Guia do programador do Hub IoT)][lnk-devguide-identity].

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

