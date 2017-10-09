---
title: "aaaUse os contadores de desempenho do diagnóstico do Azure | Microsoft Docs"
description: "Utilize os contadores de desempenho cloud services do Azure ou a máquina virtual toofind constrangimentos e otimizar o desempenho."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Criar e utilizar os contadores de desempenho na aplicação do Azure
Este artigo descreve os benefícios de Olá do e como contadores de desempenho do tooput na sua aplicação do Azure. Pode utilizá-los toocollect dados, localizar congestionamentos e otimizar o desempenho do sistema e de aplicações.

Contadores de desempenho disponíveis para o Windows Server, IIS e ASP.NET também podem ser recolhidos e utilizado o estado de funcionamento do toodetermine Olá das suas funções da web do Azure, as funções de trabalho e máquinas virtuais. Também pode criar e utilizar os contadores de desempenho personalizados.  

Pode examinar os dados de contador de desempenho

1. Diretamente no anfitrião da aplicação Olá com a ferramenta de Monitor de desempenho de Olá acedida através de ambiente de trabalho remoto
2. Utilizar o System Center Operations Manager Olá pacote de gestão do Azure
3. Com outras ferramentas de monitorização que acedem ao hello dados de diagnóstico transferidos tooAzure armazenamento. Consulte [loja e ver os dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obter mais informações.  

Para obter mais informações sobre como monitorizar o desempenho de Olá da sua aplicação no Olá [portal do Azure](http://portal.azure.com/), consulte [como tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Para obter orientações aprofundadas adicionais sobre como criar um registo e rastreio estratégia e utilizando os diagnósticos e outros problemas de tootroubleshoot técnicas e otimizar aplicações do Azure, consulte [resolução de problemas de melhores práticas para desenvolvimento do Azure Aplicações](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Ativar a monitorização do contador de desempenho
Contadores de desempenho não estão ativados por predefinição. A aplicação ou uma tarefa de arranque tem de modificar o diagnóstico de predefinição Olá contadores de desempenho de específica de Olá de tooinclude de configuração de agente que pretende toomonitor para cada instância de função.

### <a name="performance-counters-available-for-microsoft-azure"></a>Contadores de desempenho disponíveis para o Microsoft Azure
O Azure oferece um subconjunto dos contadores de desempenho de Olá disponíveis para Windows Server, IIS e Olá pilha do ASP.NET. Olá tabela seguinte lista algumas Olá contadores de desempenho do especial interesse para aplicações do Azure.

| Categoria do contador: Objeto (instância) | Nome do contador | Referência |
| --- | --- | --- |
| Exceções de CLR de .NET (*Global*) |# Exceções iniciadas / seg |Contadores de desempenho de exceção |
| Memória CLR de .NET (*Global*) |% De tempo na GC |Contadores de desempenho de memória |
| ASP.NET |Reinício da aplicação |Contadores de desempenho para o ASP.NET |
| ASP.NET |Tempo de execução do pedido |Contadores de desempenho para o ASP.NET |
| ASP.NET |Pedidos desligados |Contadores de desempenho para o ASP.NET |
| ASP.NET |Reinício do processo de trabalho |Contadores de desempenho para o ASP.NET |
| Aplicações do ASP.NET (**Total**) |Total de pedidos |Contadores de desempenho para o ASP.NET |
| Aplicações do ASP.NET (**Total**) |Pedidos/seg |Contadores de desempenho para o ASP.NET |
| ASP.NET v 4.0.30319 |Tempo de execução do pedido |Contadores de desempenho para o ASP.NET |
| ASP.NET v 4.0.30319 |Tempo de espera do pedido |Contadores de desempenho para o ASP.NET |
| ASP.NET v 4.0.30319 |Pedidos atuais |Contadores de desempenho para o ASP.NET |
| ASP.NET v 4.0.30319 |Pedidos colocados em fila |Contadores de desempenho para o ASP.NET |
| ASP.NET v 4.0.30319 |Pedidos rejeitados |Contadores de desempenho para o ASP.NET |
| Memória |MBytes disponíveis |Contadores de desempenho de memória |
| Memória |Bytes consolidadas |Contadores de desempenho de memória |
| Processor(_Total) |% Tempo do processador |Contadores de desempenho para o ASP.NET |
| TCPv4 |Falhas de ligação |Objeto TCP |
| TCPv4 |Ligações estabelecidas |Objeto TCP |
| TCPv4 |Reposição de ligações |Objeto TCP |
| TCPv4 |Segmentos enviados/seg |Objeto TCP |
| Interface(*) de rede |Bytes recebidos/seg |Objeto de Interface de rede |
| Interface(*) de rede |Bytes enviados/seg |Objeto de Interface de rede |
| Interface de rede (_2 de adaptador de rede de barramento de Máquina Virtual da Microsoft) |Bytes recebidos/seg |Objeto de Interface de rede |
| Interface de rede (_2 de adaptador de rede de barramento de Máquina Virtual da Microsoft) |Bytes enviados/seg |Objeto de Interface de rede |
| Interface de rede (_2 de adaptador de rede de barramento de Máquina Virtual da Microsoft) |Bytes totais/seg |Objeto de Interface de rede |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Criar e adicionar a aplicação de tooyour de contadores de desempenho personalizado
O Azure tem suporte toocreate e modificar os contadores de desempenho personalizado para funções da web e funções de trabalho. contadores de Olá podem ser utilizado comportamento tootrack e monitor e específicas da aplicação. Pode criar e eliminar categorias de contador de desempenho personalizados e os especificadores de uma tarefa de arranque, a função da web ou a função de trabalho com permissões elevadas.

> [!NOTE]
> Código que faz alterações toocustom contadores de desempenho tem de ter elevados toorun de permissões. Se Olá código numa função da web ou função de trabalho, a função de Olá tem de incluir tag Olá <Runtime executionContext="elevated" /> nos Olá servicedefinition. Csdef de ficheiros para Olá função tooinitialize corretamente.
>
>

Pode enviar desempenho personalizado contador tooAzure o armazenamento de dados com o agente de diagnóstico de Olá.

dados de contador de desempenho padrão de Olá são gerados pelo Olá que processa do Azure. Dados de contador de desempenho personalizado tem de ser criados pela sua aplicação de função web ou função de trabalho. Consulte [tipos de contador de desempenho](https://msdn.microsoft.com/library/z573042h.aspx) para obter informações sobre tipos de Olá de dados que podem ser armazenados nos contadores de desempenho personalizados. Consulte [PerformanceCounters exemplo](http://code.msdn.microsoft.com/azure/) para obter um exemplo que cria e define os dados do contador de desempenho personalizados numa função da web.

## <a name="store-and-view-performance-counter-data"></a>Arquivo e a vista de dados do contador de desempenho
Azure coloca em cache os dados de contador de desempenho com outras informações de diagnóstico. Estes dados estão disponíveis para monitorização remota durante a execução da instância de função Olá utilizando as ferramentas de tooview de acesso de ambiente de trabalho remoto, tais como o Monitor de desempenho. toopersist Olá fora da instância de função Olá, agente de diagnóstico de Olá tem transferência de dados de armazenamento de tooAzure Olá dados. limite de tamanho de Olá de dados do contador de desempenho de Olá em cache pode ser configurado no agente de diagnóstico hello, ou pode ser configurado toobe parte de um limite partilhado para Olá todos os dados de diagnóstico. Para obter mais informações sobre como definir o tamanho da memória intermédia de Olá, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Consulte [loja e ver os dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para uma descrição geral de como configurar Olá diagnóstico agente tootransfer dados tooa conta do storage.

Cada instância do contador de desempenho configurados é registada uma taxa de amostragem especificado e são transferidos dados Olá amostragem toohello de conta do storage por um pedido de transferência agendada ou um pedido de transferência a pedido. Transferências automáticas podem ser agendadas no máximo, uma vez por minuto. Dados de contador de desempenho transferidos pelo agente de diagnóstico de Olá são armazenados numa tabela, WADPerformanceCountersTable, na conta do storage Olá. Esta tabela pode ser acedida e consultar com métodos de armazenamento do Azure standard API. Consulte [exemplo do Microsoft Azure PerformanceCounters](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obter um exemplo de consulta e apresentar dados de contador de desempenho da tabela de WADPerformanceCountersTable Olá.

> [!NOTE]
> Consoante a frequência de transferência de agente de diagnóstico Olá e a latência de fila, hello mais recentes dados de contador de desempenho na conta do storage Olá poderá vários minutos desatualizada.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Ativar os contadores de desempenho com o ficheiro de configuração de diagnóstico
Utilize Olá seguir o procedimento tooenable os contadores de desempenho da aplicação do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Esta secção assume que importou o monitor de diagnóstico de Olá na sua aplicação e adicionados Olá diagnóstico configuração ficheiro tooyour solução do Visual Studio (diagnostics.wadcfg no SDK 2.4 e abaixo ou diagnostics.wadcfgx no SDK 2.5 e acima). Consulte os passos 1 e 2 no [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services-dotnet-diagnostics.md)) para obter mais informações.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Passo 1: Recolher e armazenar dados de contadores de desempenho
Depois de ter adicionado Olá diagnóstico ficheiro tooyour solução do Visual Studio, pode configurar o armazenamento de dados do contador de desempenho e a recolha de Olá numa aplicação do Azure. Isto é feito ao adicionar ficheiros de diagnóstico de toohello de contadores de desempenho. Dados de diagnóstico, incluindo os contadores de desempenho, primeiro são recolhidos na instância de Olá. dados de Olá, em seguida, toohello persistente WADPerformanceCountersTable tabela no Olá serviço tabela do Azure, pelo que irá também precisar toospecify Olá conta de armazenamento na sua aplicação. Se estiver a testar a aplicação localmente no Olá emulador de computação, pode também armazenar dados de diagnóstico localmente no Olá emulador do Storage. Antes de o armazenar dados de diagnóstico, primeiro tem de ir toohello [portal do Azure](http://portal.azure.com/) e crie uma conta de armazenamento clássico. Uma melhor prática é toolocate na sua conta do storage Olá geolocalização mesma que a aplicação do Azure. Ao manter Olá conta de armazenamento e de aplicações do Azure estão em Olá mesma geolocalização, evitar pagar os custos de largura de banda externa e reduzir a latência.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Adicionar ficheiros de diagnóstico de toohello de contadores de desempenho
Existem muitos contadores, que pode utilizar. Olá exemplo seguinte mostra vários contadores de desempenho que são recomendados para web e a monitorização da função de trabalho.

Abrir o ficheiro de diagnóstico Olá (diagnostics.wadcfg no SDK 2.4 e abaixo ou diagnostics.wadcfgx no SDK 2.5 e acima) e adicione Olá toohello DiagnosticMonitorConfiguration elemento a seguir:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

Olá bufferQuotaInMB atributo, o que especifica a quantidade máxima de Olá de armazenamento do sistema de ficheiros que está disponível para o tipo de coleção de dados Olá (os registos do Azure, registos de IIS, etc.). Olá predefinição é 0. Quando for atingida a quota de Olá, os dados mais antigos Olá são eliminados como sendo adicionados dados novos. soma de Olá de todas as propriedades de bufferQuotaInMB Olá tem de ser superior ao valor do atributo de OverallQuotaInMB Olá Olá. Para ver um debate mais detalhado de determinar a quantidade de armazenamento será necessária para a coleção de Olá dos dados de diagnóstico, consulte Olá secção de configuração WAD de [resolução de problemas de melhores práticas para desenvolver aplicações do Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

atributo de scheduledTransferPeriod Olá, o que especifica o intervalo de Olá entre agendada transferências de dados, arredondado toohello mais próximo minuto. No Olá seguir exemplos, está definido tooPT30M (30 minutos). Definição Olá transferência tooa período pequeno valor, tal como 1 minuto, negativamente irá afetar o desempenho da aplicação na produção, mas pode ser útil para ver o diagnóstico trabalhar rapidamente quando estiver a testar. período de transferência agendada de Olá deve ser suficientemente pequena tooensure que dados de diagnóstico não são substituídos na instância de Olá, mas suficientemente grande para que não irá afetar desempenho Olá da sua aplicação.

atributo de counterSpecifier Olá Especifica toocollect de contador de desempenho de Olá. atributo de sampleRate Olá Especifica taxa Olá no qual o contador de desempenho de Olá deve ser objeto de amostragem, neste caso, 30 segundos.

Depois de adicionar contadores de desempenho de Olá que pretende que o toocollect, guarde o ficheiro de diagnóstico de toohello de alterações. Em seguida, terá de conta de armazenamento de Olá toospecify dados de diagnóstico de Olá serão transferidos para o.

### <a name="specify-hello-storage-account"></a>Especifique a conta de armazenamento Olá
toopersist conta sua tooyour de informações de diagnóstico do armazenamento do Azure, tem de especificar uma cadeia de ligação no ficheiro de configuração (serviceconfiguration. Cscfg) do serviço.

Para o Azure SDK 2.5, Olá conta de armazenamento pode ser especificado no ficheiro de diagnostics.wadcfgx Olá.

> [!NOTE]
> Estas instruções aplicam-se apenas tooAzure SDK 2.4 e abaixo. Para o Azure SDK 2.5, Olá conta de armazenamento pode ser especificado no ficheiro de diagnostics.wadcfgx Olá.
>
>

cadeias de ligação de Olá tooset:

1. Abra o ficheiro de Serviceconfiguration Olá utilizando o seu editor de texto favorito e a cadeia de ligação de Olá de conjunto para o armazenamento. Olá *AccountName* e *AccountKey* valores encontram Olá portal do Azure no dashboard de conta de armazenamento de Olá, sob as chaves de acesso.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Guarde o ficheiro do Olá Serviceconfiguration.
3. Abrir o ficheiro de ServiceConfiguration.Local.cscfg Olá e certifique-se de que UseDevelopmentStorage está definida tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Agora que o conjunto de cadeias de ligação de Olá, a aplicação será mantido conta de armazenamento do diagnostics dados tooyour quando a aplicação for implementada.
4. Guardar e criar o projeto e, em seguida, implementar a sua aplicação.

## <a name="step-2-optional-create-custom-performance-counters"></a>Passo 2: Os contadores de desempenho personalizados (opcional) criar
Além disso toohello predefinidas contadores de desempenho, pode adicionar que o seus próprios desempenho personalizado contadores toomonitor funções de web ou de trabalho. Contadores de desempenho personalizado podem estar utilizado tootrack e monitor específico da aplicação o comportamento e pode ser criados ou eliminados numa tarefa de arranque, a função da web ou a função de trabalho com permissões elevadas.

agente de diagnóstico do Azure Olá atualiza Olá desempenho contador configuração a partir do ficheiro de .wadcfg Olá um minuto após a iniciar.  Se criar os contadores de desempenho personalizado no Olá método OnStart e as tarefas de arranque demorar mais do que um minuto tooexecute, os contadores de desempenho personalizados serão não ter sido criados quando o agente de diagnóstico do Azure Olá tenta tooload-los.  Neste cenário, verá que o Azure Diagnostics captura corretamente todos os dados de diagnóstico, exceto os contadores de desempenho personalizados.  tooresolve este problema, crie Olá contadores de desempenho numa tarefa de arranque ou mover algumas das suas tarefas de arranque trabalham toohello OnStart método depois de criar Olá contadores de desempenho.

Execute os seguintes passos toocreate de desempenho personalizado simple contador com o nome "\MyCustomCounterCategory\MyButton1Counter" de Olá:

1. Abrir Olá serviço de ficheiro de definição (. CSDEF) para a sua aplicação.
2. Adicione Olá Runtime elemento toohello WebRole ou WorkerRole elemento tooallow execução com privilégios elevados:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Guarde o ficheiro de Olá.
4. Abrir o ficheiro de diagnóstico Olá (diagnostics.wadcfg no SDK 2.4 e abaixo ou diagnostics.wadcfgx no SDK 2.5 e acima) e adicione Olá seguir toohello DiagnosticMonitorConfiguration

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Guarde o ficheiro de Olá.
6. Crie categoria de contador de desempenho personalizados Olá no método de OnStart Olá da sua função, antes de invocar base. OnStart. Olá c# exemplo seguinte cria uma categoria personalizada, se já existir:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Atualize contadores Olá dentro da sua aplicação. Olá seguinte o exemplo de atualizações de um contador de desempenho personalizados Button1_Click eventos:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Guarde o ficheiro de Olá.  

Dados do contador de desempenho personalizados agora serão recolhidos pelo monitor de diagnóstico do Azure Olá.

## <a name="step-3-query-performance-counter-data"></a>Passo 3: Dados de contador de desempenho de consulta
Depois da aplicação é implementada e em execução, monitor de diagnóstico de Olá começará a recolher contadores de desempenho e a persistência desse tooAzure o armazenamento de dados. Utilize ferramentas como o Explorador de servidores no Visual Studio, [Explorador de armazenamento do Azure](http://azurestorageexplorer.codeplex.com/), ou [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) por Cerebrata dados Olá de contadores de desempenho de Olá tooview Tabela WADPerformanceCountersTable. Pode também programaticamente consultar Olá tabela serviço a utilizar [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Olá c# exemplo seguinte mostra uma consulta básica relativamente à tabela de WADPerformanceCountersTable Olá e guarda Olá diagnóstico dados tooa um ficheiro CSV. Depois dos contadores de desempenho de Olá são guardados tooa um ficheiro CSV, pode utilizar Olá graphing capacidades no Microsoft Excel ou alguns outros dados de ferramenta toovisualize Olá. Ser tooadd se um tooMicrosoft.WindowsAzure.Storage.dll de referência, que está incluído no Olá Azure SDK para .NET Outubro 2012 e posterior. a assemblagem de Olá é instalado toohello % programa Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version num\ref\ diretório.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

As entidades mapeiam tooC # objetos utilizando uma classe personalizada derivada de **TableEntity**. Olá código seguinte define uma classe de entidade que representa um contador de desempenho Olá **WADPerformanceCountersTable** tabela.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Passos Seguintes
[Vista de artigos adicionais no diagnóstico do Azure](../azure-diagnostics.md)
