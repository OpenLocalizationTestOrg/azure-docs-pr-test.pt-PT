## <a name="create-a-device-identity"></a><span data-ttu-id="9526a-101">Criar uma identidade de dispositivo</span><span class="sxs-lookup"><span data-stu-id="9526a-101">Create a device identity</span></span>

<span data-ttu-id="9526a-102">Nesta secção, utilize uma ferramenta de Node.js chamada [iothub explorer] [ iot-hub-explorer] toocreate uma identidade de dispositivo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9526a-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="9526a-103">Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9526a-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="9526a-104">Execute o seguinte Olá no seu ambiente de linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="9526a-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="9526a-105">Em seguida, execute Olá hub de tooyour toologin de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="9526a-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="9526a-106">Substitute `{iot hub connection string}` com Olá cadeia de ligação do IoT Hub que copiou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="9526a-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="9526a-107">Por fim, crie uma nova identidade de dispositivo chamada `myDeviceId` com comando Olá:</span><span class="sxs-lookup"><span data-stu-id="9526a-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="9526a-108">Tome nota da cadeia de ligação do dispositivo Olá do resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="9526a-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="9526a-109">Esta cadeia de ligação do dispositivo é utilizada por Olá dispositivo aplicação tooconnect tooyour IoT Hub como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9526a-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="9526a-110">Consulte demasiado[introdução ao IoT Hub] [ lnk-getstarted] tooprogrammatically criar as identidades de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9526a-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
