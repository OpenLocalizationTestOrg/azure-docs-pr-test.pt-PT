## <a name="create-an-iot-hub"></a>Criar um hub IoT

1. No Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **Internet das coisas** > **IoT Hub**.

   ![Criar um hub IoT no Olá portal do Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. No Olá **IoT hub** painel, introduza Olá seguintes informações para o seu IoT hub:

     **Nome**: introduza o nome de Olá do seu IoT hub. Se o nome de Olá introduzido é válido, aparece uma marca de verificação verde.

     **Escalão de preço e escala**: Olá selecione **F1 - livre** camada. Esta opção é suficiente para esta demonstração. Para obter mais informações, consulte Olá [escalão de preço e escala](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Grupo de recursos**: criar um IoT hub do recurso grupo toohost Olá ou utilize uma já existente. Para obter mais informações, consulte [toomanage de grupos de recursos de utilização, os recursos do Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Localização**: selecione hello mais próximo tooyou de localização onde o hub IoT de Olá é criado.

     **PIN toodashboard**: selecione esta opção para o IoT hub tooyour facilitar o acesso a partir do dashboard de Olá.

   ![Introduza informações toocreate seu IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Clique em **Criar**. IoT hub poderá demorar alguns minutos toocreate. Pode ver o progresso na Olá **notificações** painel.

   ![Ver as notificações de progresso do hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Depois de criado o seu IoT hub, clique na mesma no dashboard de Olá. Tome nota do Olá **Hostname**e, em seguida, clique em **políticas de acesso partilhado**.

   ![Obter nome do anfitrião Olá do seu IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. No Olá **políticas de acesso partilhado** painel, clique em Olá **iothubowner** política e, em seguida, copiar e tome nota do Olá **cadeia de ligação** do seu IoT hub. Para obter mais informações, consulte [tooIoT de acesso de controlo Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
Não precisará da cadeia de ligação iothubowner para este tutorial de configuração. No entanto, poderá ser necessário, para algumas das tutoriais Olá sobre os diferentes cenários de IoT depois de concluir esta configuração.

   ![Obter a cadeia de ligação do hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Registar um dispositivo no Olá IoT hub para o dispositivo

1. No Olá [portal do Azure](https://portal.azure.com/), abra o seu IoT hub.

2. Clique em **Device Explorer**.
3. No painel do Explorador de dispositivo Olá, clique em **adicionar** tooadd um dispositivo tooyour do IoT hub. Em seguida, Olá seguintes:

   **ID de dispositivo**: introduza o ID de Olá do novo dispositivo de Olá. Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.

   **Tipo de Autenticação**: selecione **Chave Simétrica**.

   **Gerar Chaves Automaticamente**: selecione esta caixa de verificação.

   **Ligar dispositivo tooIoT Hub**: clique em **ativar**.

   ![Adicionar um dispositivo no Olá Explorador de dispositivo do seu IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Clique em **Guardar**.
5. Depois de criar dispositivo Olá, abra o dispositivo de Olá no Olá **Explorador de dispositivo** painel.
6. Tome nota da chave primária de Olá Olá da cadeia de ligação.

   ![Obter a cadeia de ligação do dispositivo Olá](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
