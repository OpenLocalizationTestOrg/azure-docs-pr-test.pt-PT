---
title: "aaaEnabling as métricas do storage no portal do Azure de Olá | Microsoft Docs"
description: "Como as métricas do storage tooenable para Olá serviços Blob, fila, tabela e ficheiro"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Ativar as métricas do Storage e visualizar dados de métricas
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Descrição geral
As métricas do Storage está ativada por predefinição quando cria uma nova conta de armazenamento. Pode configurar a monitorização utilizando o Olá [Portal clássico do Azure](https://manage.windowsazure.com), Windows PowerShell, ou através de programação através de um API de armazenamento.

Quando ativar as métricas do Storage, tem de escolher um período de retenção de dados de Olá: este período determina para armazenamento de Olá quanto serviço mantém métricas Olá e eventuais encargos lhe Olá espaço necessário toostore-los. Normalmente, deve utilizar um período de retenção mais curto minuto com base nas métricas que métricas horárias devido a Olá significativas extra o espaço necessário para as métricas de minutos. Deverá escolher um período de retenção de forma a que tem suficiente vez tooanalyze Olá que os dados e transferir quaisquer métricas desejar tookeep para fins de relatórios ou de análise offline. Lembre-se de que será também faturado para transferência de dados de métricas da sua conta de armazenamento.

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>Como as métricas do Storage tooenable utilizando Olá Portal clássico do Azure
No Olá [Portal clássico do Azure](https://manage.windowsazure.com), utilize a página de configuração de Olá para um toocontrol de conta de armazenamento as métricas do Storage. Para a monitorização, pode definir um nível e um período de retenção em dias para cada um dos blobs, tabelas e filas. Em cada caso, o nível de Olá é uma das seguintes Olá:

* Terminar a sessão — Não haver métricas são recolhidas.
* Mínimo — As métricas do Storage recolhe um conjunto básico de métricas, tais como entrada/saída, disponibilidade, latência e percentagens de êxito, o que são agregadas para serviços Blob, tabela e fila de Olá.
* Verboso — Recolhe as métricas do Storage, defina um completo de métricas que inclui Olá mesmas métricas para cada operação de API de armazenamento, além disso toohello nível de serviço métricas. Métricas verbosas ativar análise quanto mais próximo dos problemas que ocorrem durante as operações de aplicação.

Tenha em atenção que Olá Portal clássico do Azure não atualmente permitem-lhe tooconfigure métricas minuto na sua conta de armazenamento; tem de ativar as métricas minutos com o PowerShell ou através de programação.

## <a name="how-tooenable-storage-metrics-using-powershell"></a>Como as métricas do Storage tooenable através do PowerShell
Pode utilizar o PowerShell no seu computador local de tooconfigure as métricas do Storage na sua conta de armazenamento utilizando Olá Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Olá definições atuais e Olá cmdlet Conjunto AzureStorageServiceMetricsProperty toochange Olá definições atuais.

cmdlets de Olá que controlam as métricas do Storage utilizam Olá os seguintes parâmetros:

* Valores possíveis MetricsType são horas e minutos.
* Valores possíveis ServiceType são tabela, fila e Blob.
* Valores possíveis MetricsLevel são nenhum (tooOff equivalente no Olá Portal clássico do Azure), o serviço (tooMinimal equivalente no Olá Portal clássico do Azure) e ServiceAndApi (tooVerbose equivalente no Olá Portal clássico do Azure).

Por exemplo, hello seguinte comando muda num minuto métricas para o serviço de blob Olá na sua conta de armazenamento predefinido com um período de retenção de Olá definir toofive dias:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
Olá seguinte comando obtém Olá atuais por hora métricas e retenção de nível de dias para o serviço de blob Olá na sua conta do storage predefinida:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
Para obter informações sobre como tooconfigure Olá Azure PowerShell cmdlets toowork com a sua subscrição do Azure e como tooselect Olá armazenamento predefinido toouse de contas, consulte: [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Como tooenable as métricas do Storage através de programação
Olá c# fragmento a seguir mostra como tooenable métricas e registo de utilização de serviço Blob do Olá hello a biblioteca de clientes de armazenamento para .NET:

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Ver as métricas do Storage
Quando tiver configurado as métricas do Storage toomonitor a sua conta do storage, regista métricas Olá num conjunto de tabelas bem conhecidas na sua conta do storage. Pode utilizar a página de Monitor de Olá na sua conta de armazenamento no Olá as métricas no Portal clássico do Azure tooview Olá horárias à medida que ficam disponíveis num gráfico. Nesta página no Olá Portal clássico do Azure, pode:

* Selecione o tooplot métricas no gráfico de Olá (escolher Olá as métricas disponíveis dependerão se escolheu verboso ou mínima de monitorização para o serviço de Olá na página de configurar Olá).
* Selecione o intervalo de tempo de Olá apresentado no gráfico de Olá com base nas métricas Olá.
* Escolha toouse uma métrica de Olá tooplot escala absoluto ou relativo.
* Configurar toonotify de alertas de e-mail, quando uma métrica específica atinge um determinado valor.

Se pretender que as métricas de Olá toodownload para armazenamento de longa duração ou tooanalyze-los localmente, será necessário toouse uma ferramenta ou escrever alguns códigos tabelas de Olá tooread. Tem de transferir as métricas de minuto Olá para análise. tabelas de Olá não são apresentados se lista todas as tabelas de Olá na sua conta de armazenamento, mas pode aceder às mesmas diretamente pelo nome. Muitas ferramentas de navegação de armazenamento de terceiros estão cientes estas tabelas e permitem-lhe tooview-los diretamente (consulte a mensagem de blogue de Olá [exploradores de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) para obter uma lista das ferramentas disponíveis).

### <a name="hourly-metrics"></a>Métricas por hora
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Métricas de minutos
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Capacidade
* $MetricsCapacityBlob

Pode encontrar detalhes completos de esquemas Olá para estas tabelas em [armazenamento esquema da tabela de métricas de análise](https://msdn.microsoft.com/library/azure/hh343264.aspx). linhas de exemplo de Olá abaixo mostram apenas um subconjunto de colunas de Olá disponíveis, mas ilustram algumas funcionalidades importantes de forma Olá que as métricas do Storage guarda estas métricas:

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Disponibilidade | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |utilizador; Todos os |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |utilizador; QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |utilizador; QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |utilizador; UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

Dados de métricas minuto neste exemplo, a chave de partição Olá utiliza a hora de Olá na resolução minuto. chave de linha de Olá identifica o tipo de Olá de informações que são armazenadas na linha de Olá e isto é composto por duas partes de informações, o tipo de acesso de Olá e o tipo de pedido de Olá:

* tipo de acesso de Olá é utilizador ou sistema, onde o utilizador refere-se o serviço de armazenamento do tooall utilizador pedidos toohello e sistema refere-se toorequests graças à análise de armazenamento.
* tipo de pedido de Olá é tudo caso em que é uma linha de resumo, ou identifica Olá API específica, como QueryEntity ou UpdateEntity.

dados de exemplo de Olá acima mostra que todos os Olá regista para um único minuto (começando às 11:00), por isso, Olá número de pedidos de QueryEntities plus hello número de pedidos de QueryEntity mais o número de Olá de pedidos de UpdateEntity adicionados até tooseven, que é Olá total apresentado no linha de utilizador: All Olá. Da mesma forma, podem derivar Olá latência média de ponto a ponto 104.4286 na linha de utilizador: All Olá calculando ((143.8 * 5) + 3 + 9) / 7.

Deve considerar como configurar alertas no Olá Portal clássico do Azure na página de Monitor de Olá, para que as métricas do Storage pode automaticamente notificá-lo de quaisquer alterações importantes no comportamento de Olá dos seus serviços de armazenamento. Se utilizar um toodownload de ferramenta do Explorador de armazenamento estes dados de métricas num formato delimitado, pode utilizar os dados do Microsoft Excel tooanalyze Olá. Consulte a mensagem de blogue de Olá [exploradores de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) para obter uma lista das ferramentas do Explorador de armazenamento disponível.

## <a name="accessing-metrics-data-programmatically"></a>Aceder aos dados de métricas programaticamente
Olá listagem seguinte mostra c# código de exemplo que acede ao métricas de minuto Olá para um intervalo de minutos e apresenta os resultados de Olá numa janela de consola. Utiliza Olá biblioteca de armazenamento do Azure versão 4, que inclui Olá CloudAnalyticsClient classe que simplifica a tabelas de métricas de Olá ao aceder no armazenamento.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Cobra o que pode implicar ao ativar as métricas do storage?
Escreva as entidades da tabela de toocreate pedidos com base nas métricas são cobradas às operações de armazenamento do Azure Olá taxas padrão tooall aplicável.

Pedidos de leitura e eliminar por um toometrics de dados de cliente também são facturável às taxas padrão. Se tiver configurado uma política de retenção de dados, não lhe serem cobrados ao Storage do Azure elimina dados antigos de métricas. No entanto, se eliminar dados de análise, a sua conta é cobrada para operações de eliminação de Olá.

capacidade de Olá utilizada pelo tabelas de métricas de Olá também é facturável: pode utilizar Olá quantidade de Olá tooestimate utilizada para armazenar dados de métricas de capacidade de os seguintes:

* Se a cada hora um serviço utiliza a cada API em cada serviço, aproximadamente 148KB de dados é armazenado nas tabelas de transação Olá métricas a cada hora se tiver ativado o serviço e o nível da API resumo.
* Se a cada hora um serviço utiliza a cada API em cada serviço, aproximadamente 12KB de dados é armazenado nas tabelas de transação Olá métricas a cada hora se tiver ativado apenas nível de serviço resumo.
* Olá tabela de capacidade para os blobs tem duas linhas adicionadas por dia (fornecidos pelo utilizador foi optada ativamente por participar para os registos): Isto implica que cada tamanho de Olá dia desta tabela aumenta em segurança tooapproximately 300 bytes.

## <a name="next-steps"></a>Passos seguintes:
[Ativar a análise do armazenamento de registo e aceder aos dados de registo](https://msdn.microsoft.com/library/dn782840.aspx)
