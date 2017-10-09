## <a name="associate-an-azure-storage-account-tooiot-hub"></a>Associar um tooIoT de conta do Storage do Azure Hub

Porque a aplicação de dispositivo simulada Olá carrega um ficheiro tooa blob, tem de ter um [Storage do Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) conta associados tooIoT Hub. Quando associa uma conta de armazenamento do Azure com um hub IoT, iothub Olá gera um URI de SAS. Um dispositivo pode utilizar este carregamento de toosecurely URI de SAS um contentor de BLOBs de tooa do ficheiro. Olá serviço IoT Hub e Olá SDKs do dispositivo coordenam processos Olá que gera Olá URI de SAS e torna disponível tooa-tooupload dispositivo toouse um ficheiro.

Siga as instruções de Olá em [configurar ficheiro carrega utilizando o portal do Azure de Olá](../articles/iot-hub/iot-hub-configure-file-upload.md) tooassociate um tooyour IoT hub da conta de armazenamento do Azure. Certifique-se de que um contentor de blob está associado ao seu IoT hub e que as notificações de ficheiros estão ativadas.

![Ativar notificações de ficheiros no portal](media/iot-hub-associate-storage/enable-file-notifications.png)