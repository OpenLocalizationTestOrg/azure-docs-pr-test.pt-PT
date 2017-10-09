## <a name="create-a-device-identity"></a><span data-ttu-id="e46b3-101">Criar uma identidade de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e46b3-101">Create a device identity</span></span>
<span data-ttu-id="e46b3-102">Nesta secção, crie uma aplicação de consola .NET que cria uma identidade de dispositivo no registo de identidade Olá no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e46b3-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="e46b3-103">Um dispositivo não é possível ligar tooIoT hub exceto se tiver uma entrada no registo de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="e46b3-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="e46b3-104">Para obter mais informações, consulte a secção "Registo de identidade" Olá Olá [guia para programadores do IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="e46b3-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="e46b3-105">Quando executar esta aplicação de consola, gera um ID de dispositivo exclusivo e chave que o seu dispositivo pode utilizar tooidentify próprio quando envia dispositivo para nuvem mensagens tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e46b3-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="e46b3-106">Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e46b3-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="e46b3-107">No Visual Studio, adicione uma solução do Visual c# Windows ambiente de trabalho clássico projeto tooa novo utilizando Olá **aplicação de consola (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="e46b3-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="e46b3-108">Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e46b3-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="e46b3-109">Projeto de Olá nome **CreateDeviceIdentity** e nome Olá solução **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="e46b3-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][10]
2. <span data-ttu-id="e46b3-111">No Explorador de soluções, faça duplo clique Olá **CreateDeviceIdentity** projeto e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e46b3-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="e46b3-112">No Olá **Gestor de pacotes NuGet** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** do pacote e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="e46b3-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="e46b3-113">Este procedimento transfere, instala e adiciona uma referência toohello [SDK do serviço do Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="e46b3-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela Gestor de Pacote NuGet][11]
4. <span data-ttu-id="e46b3-115">Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="e46b3-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="e46b3-116">Adicionar Olá seguintes campos toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="e46b3-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="e46b3-117">Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub hub Olá que criou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="e46b3-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="e46b3-118">Adicionar Olá seguinte método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="e46b3-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="e46b3-119">Este método cria uma identidade de dispositivo com o ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="e46b3-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="e46b3-120">(Se o ID desse dispositivo já existe no registo de identidade Olá, Olá código apenas obtém informações do dispositivo existente Olá.) aplicação Olá, em seguida, apresenta a chave primária de Olá para essa identidade.</span><span class="sxs-lookup"><span data-stu-id="e46b3-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="e46b3-121">Utilize esta chave no Olá simulado dispositivo aplicação tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e46b3-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="e46b3-122">Por fim, adicione Olá seguintes linhas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="e46b3-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="e46b3-123">Executar esta aplicação e tome nota da chave do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="e46b3-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Chave do dispositivo gerada pela aplicação Olá][12]

> [!NOTE]
> <span data-ttu-id="e46b3-125">Olá registo de identidade do IoT Hub apenas armazena dispositivo identidades tooenable acesso seguro toohello do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e46b3-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="e46b3-126">Armazena toouse de IDs e chaves de dispositivo como credenciais de segurança e um sinalizador ativado/desativado que pode utilizar toodisable acesso de um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="e46b3-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="e46b3-127">Se a sua aplicação tiver toostore outros metadados específicos do dispositivo, deverá utilizar um armazenamento específico da aplicação.</span><span class="sxs-lookup"><span data-stu-id="e46b3-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="e46b3-128">Para obter mais informações, veja o [IoT Hub developer guide (Guia do programador do Hub IoT)][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="e46b3-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
