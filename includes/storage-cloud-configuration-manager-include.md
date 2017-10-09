Olá [biblioteca do Gestor de configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornece uma classe para analisar uma cadeia de ligação de um ficheiro de configuração. Olá [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analisa as definições de configuração, independentemente se aplicações de cliente Olá está em execução no ambiente de trabalho de Olá, num dispositivo móvel, numa máquina virtual do Azure ou num serviço em nuvem do Azure.

tooreference Olá pacote CloudConfigurationManager, adicione o seguinte Olá `using` diretiva:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Eis um exemplo que mostra como tooretrieve uma cadeia de ligação de um ficheiro de configuração:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

A utilização de Olá Gestor de configuração do Azure é opcional. Também pode utilizar uma API, tal como hello do .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.

