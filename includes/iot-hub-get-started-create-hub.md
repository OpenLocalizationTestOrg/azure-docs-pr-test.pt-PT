## <a name="create-an-iot-hub"></a>Criar um hub IoT
Crie um IoT hub para sua tooconnect de aplicação do dispositivo simulado para. Olá passos seguintes mostram como toocomplete esta tarefa pelo utilizando Olá portal do Azure.

1. Inicie sessão no toohello [portal do Azure][lnk-portal].
1. No Jumpbar Olá, clique em **novo** > **Internet das coisas** > **IoT Hub**.
   
    ![Barra de atalhos do portal do Azure][1]
1. No Olá **IoT hub** painel, escolha Olá configuração para o seu IoT hub.
   
    ![Painel do hub IoT][2]
   
   1. No Olá **nome** box, introduza um nome para o seu IoT hub. Se hello **nome** é válido e estiver disponível, irá aparecer uma marca de verificação verde no Olá **nome** caixa.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Selecione um [escalão de preços e dimensionamento][lnk-pricing]. Este tutorial não requer um escalão específico. Para este tutorial, utilize o escalão F1 gratuito de Olá.
   1. Em **Grupo de recursos**, crie um grupo de recursos ou selecione um existente. Para obter mais informações, consulte [utilizar recursos grupos toomanage os recursos do Azure][lnk-resource-groups].
   1. No **localização**, selecione Olá localização toohost seu IoT hub. Para este tutorial, escolha a localização mais próxima.
1. Quando tiver escolhido as opções de configuração do hub IoT, clique em **Criar**.  Pode demorar alguns minutos para Azure toocreate seu IoT hub. Estado de Olá toocheck, pode monitorizar o progresso de Olá Olá Startboard ou no painel de notificações de Olá.
   
    ![Estado do novo hub IoT][3]
1. Quando o hub IoT de Olá foi criado com êxito, clique no mosaico novo Olá para o seu hub IoT no painel de Olá Olá tooopen portal do Azure para o IoT hub novo Olá. Tome nota do Olá **Hostname**e, em seguida, clique em **políticas de acesso partilhado**.
   
    ![Novo painel do hub IoT][4]
1. No Olá **políticas de acesso partilhado** painel, clique em Olá **iothubowner** política e, em seguida, copie e tome nota da cadeia de ligação do IoT Hub de Olá Olá **iothubowner** painel. Para obter mais informações, consulte [controlo de acesso] [ lnk-access-control] no Olá "Guia para programadores do IoT Hub."
   
    ![Painel das políticas de acesso partilhado][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
