## <a name="create-a-device-identity"></a><span data-ttu-id="9986e-101">Criar uma identidade de dispositivo</span><span class="sxs-lookup"><span data-stu-id="9986e-101">Create a device identity</span></span>

<span data-ttu-id="9986e-102">Esta secção, irá utilizar Olá [portal do Azure] [ lnk-azure-portal] toocreate uma identidade de dispositivo no registo de identidade Olá no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9986e-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="9986e-103">Um dispositivo não é possível ligar tooIoT hub exceto se tiver uma entrada no registo de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="9986e-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="9986e-104">Para obter mais informações, consulte a secção "Registo de identidade" Olá Olá [guia para programadores do IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="9986e-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="9986e-105">Olá **Explorador de dispositivo** no Olá portal ajuda-o a gerar um ID de dispositivo exclusivo e uma chave que o seu dispositivo pode utilizar tooidentify próprio quando estabelece ligação tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9986e-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="9986e-106">Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9986e-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="9986e-107">Certifique-se de que tem sessão iniciada toohello [portal do Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9986e-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="9986e-108">No Jumpbar Olá, clique em **todos os recursos** e localizar o recurso do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9986e-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Navegue tooyour Iot hub][img-find-iothub]

1. <span data-ttu-id="9986e-110">Quando o recurso do hub IoT é aberto, clique em Olá **Explorador de dispositivo** ferramenta e, em seguida, clique em **adicionar** na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="9986e-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="9986e-111">Forneça o nome de Olá para o novo dispositivo, tal como **myDeviceId**e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="9986e-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Criar a identidade de dispositivo no portal][img-create-device]

   <span data-ttu-id="9986e-113">Esta ação cria uma nova identidade de dispositivo do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9986e-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="9986e-114">No Olá **Explorador de dispositivo**da lista de dispositivos, clique em dispositivo Olá recém-criado e tome nota dos Olá **cadeia de ligação---chave primária**.</span><span class="sxs-lookup"><span data-stu-id="9986e-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Cadeia de ligação do dispositivo][img-connection-string]

> [!NOTE]
> <span data-ttu-id="9986e-116">Olá registo de identidade do IoT Hub apenas armazena dispositivo identidades tooenable acesso seguro toohello do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9986e-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="9986e-117">Armazena toouse de IDs e chaves de dispositivo como credenciais de segurança e um sinalizador ativado/desativado que pode utilizar toodisable acesso de um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="9986e-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="9986e-118">Se a sua aplicação tiver toostore outros metadados específicos do dispositivo, deverá utilizar um armazenamento específico da aplicação.</span><span class="sxs-lookup"><span data-stu-id="9986e-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="9986e-119">Para obter mais informações, veja o [IoT Hub developer guide (Guia do programador do Hub IoT)][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="9986e-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

