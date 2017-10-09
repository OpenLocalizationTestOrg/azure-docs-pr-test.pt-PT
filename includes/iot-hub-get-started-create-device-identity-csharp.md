## <a name="create-a-device-identity"></a>Criar uma identidade de dispositivo
Nesta secção, crie uma aplicação de consola .NET que cria uma identidade de dispositivo no registo de identidade Olá no seu IoT hub. Um dispositivo não é possível ligar tooIoT hub exceto se tiver uma entrada no registo de identidade Olá. Para obter mais informações, consulte a secção "Registo de identidade" Olá Olá [guia para programadores do IoT Hub][lnk-devguide-identity]. Quando executar esta aplicação de consola, gera um ID de dispositivo exclusivo e chave que o seu dispositivo pode utilizar tooidentify próprio quando envia dispositivo para nuvem mensagens tooIoT Hub. Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.

1. No Visual Studio, adicione uma solução do Visual c# Windows ambiente de trabalho clássico projeto tooa novo utilizando Olá **aplicação de consola (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior. Projeto de Olá nome **CreateDeviceIdentity** e nome Olá solução **IoTHubGetStarted**.
   
    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][10]
2. No Explorador de soluções, faça duplo clique Olá **CreateDeviceIdentity** projeto e, em seguida, clique em **gerir pacotes NuGet**.
3. No Olá **Gestor de pacotes NuGet** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** do pacote e aceite os termos de Olá de utilização. Este procedimento transfere, instala e adiciona uma referência toohello [SDK do serviço do Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e as respetivas dependências.
   
    ![Janela Gestor de Pacote NuGet][11]
4. Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Adicionar Olá seguintes campos toohello **programa** classe. Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub hub Olá que criou na secção anterior Olá.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Adicionar Olá seguinte método toohello **programa** classe:
   
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
   
    Este método cria uma identidade de dispositivo com o ID **myFirstDevice**. (Se o ID desse dispositivo já existe no registo de identidade Olá, Olá código apenas obtém informações do dispositivo existente Olá.) aplicação Olá, em seguida, apresenta a chave primária de Olá para essa identidade. Utilize esta chave no Olá simulado dispositivo aplicação tooconnect tooyour IoT hub.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Por fim, adicione Olá seguintes linhas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Executar esta aplicação e tome nota da chave do dispositivo Olá.
   
    ![Chave do dispositivo gerada pela aplicação Olá][12]

> [!NOTE]
> Olá registo de identidade do IoT Hub apenas armazena dispositivo identidades tooenable acesso seguro toohello do IoT hub. Armazena toouse de IDs e chaves de dispositivo como credenciais de segurança e um sinalizador ativado/desativado que pode utilizar toodisable acesso de um dispositivo individual. Se a sua aplicação tiver toostore outros metadados específicos do dispositivo, deverá utilizar um armazenamento específico da aplicação. Para obter mais informações, veja o [IoT Hub developer guide (Guia do programador do Hub IoT)][lnk-devguide-identity].
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
