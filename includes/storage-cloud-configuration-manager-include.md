<span data-ttu-id="3e4f5-101">Olá [biblioteca do Gestor de configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornece uma classe para analisar uma cadeia de ligação de um ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="3e4f5-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="3e4f5-102">Olá [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analisa as definições de configuração, independentemente se aplicações de cliente Olá está em execução no ambiente de trabalho de Olá, num dispositivo móvel, numa máquina virtual do Azure ou num serviço em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e4f5-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="3e4f5-103">tooreference Olá pacote CloudConfigurationManager, adicione o seguinte Olá `using` diretiva:</span><span class="sxs-lookup"><span data-stu-id="3e4f5-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="3e4f5-104">Eis um exemplo que mostra como tooretrieve uma cadeia de ligação de um ficheiro de configuração:</span><span class="sxs-lookup"><span data-stu-id="3e4f5-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="3e4f5-105">A utilização de Olá Gestor de configuração do Azure é opcional.</span><span class="sxs-lookup"><span data-stu-id="3e4f5-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="3e4f5-106">Também pode utilizar uma API, tal como hello do .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="3e4f5-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

