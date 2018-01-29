---
title: "Transmissão em fluxo de dados de diagnóstico do Azure no caminho de acesso frequente utilizar Event Hubs | Microsoft Docs"
description: "Configurar diagnósticos do Azure com o Event Hubs ponto a ponto, incluindo documentação de orientação para cenários comuns."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: ca0dd96389a605ed8bf34af81eb4d75bef581338
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a>Transmissão em fluxo de dados de diagnóstico do Azure no caminho de acesso frequente ao utilizar os Hubs de eventos
Diagnóstico do Azure fornece opções flexíveis para recolher métricas e registos de máquinas de virtuais de serviços de nuvem (VMs) e transferir os resultados para o Storage do Azure. A partir de um período de tempo de Março de 2016 (SDK 2.9), pode enviar diagnósticos para origens de dados personalizados e transferir os dados de caminho frequente em segundos, utilizando [Event Hubs do Azure](https://azure.microsoft.com/services/event-hubs/).

Os tipos de dados suportados incluem:

* Eventos de Rastreio de Eventos para o Windows (ETW)
* Contadores de desempenho
* Registos de eventos do Windows
* Registos de aplicações
* Registos de infraestrutura de diagnóstico do Azure

Este artigo mostra como configurar o diagnóstico do Azure com os Event Hubs de extremidade a extremidade. Também é fornecida orientação para os seguintes cenários comuns:

* Como personalizar os registos e as métricas que obterem enviadas para os Event Hubs
* Como alterar as configurações de cada ambiente
* Como ver dados de fluxo de Event Hubs
* Como resolver problemas de ligação  

## <a name="prerequisites"></a>Pré-requisitos
Dados de receieving de Hubs de eventos de diagnóstico do Azure são suportados em serviços em nuvem, VMs, conjuntos de dimensionamento de Máquina Virtual e recursos de infraestrutura de serviço a partir do Azure SDK 2.9 e as ferramentas correspondente do Azure para Visual Studio.

* Extensão de diagnóstico do Azure 1.6 ([Azure SDK para .NET 2.9 ou posterior](https://azure.microsoft.com/downloads/) destina-se isto por predefinição)
* [Visual Studio 2013 ou posterior](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* As configurações existentes de diagnóstico do Azure numa aplicação, utilizando um *.wadcfgx* de ficheiros e um dos seguintes métodos:
  * Visual Studio: [configurar diagnósticos para máquinas virtuais e serviços em nuvem do Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [ative os diagnósticos nos serviços de nuvem do Azure com o PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Espaço de nomes do Hubs de eventos aprovisionado pelo artigo [introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a>Ligar o diagnóstico do Azure ao receptor de Event Hubs
Por predefinição, diagnósticos do Azure sempre envia os registos e as métricas para uma conta de armazenamento do Azure. Uma aplicação também pode enviar dados para Event Hubs, adicionando um novo **Sinks** secção sob o **PublicConfig** / **WadCfg** elemento do *. wadcfgx* ficheiro. No Visual Studio, o *.wadcfgx* ficheiro é armazenado no seguinte caminho: **projeto de serviço em nuvem** > **funções** > **( RoleName)** > **diagnostics.wadcfgx** ficheiro.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

Neste exemplo, o URL de hub de eventos está definido para o espaço de nomes completamente qualificado do hub de eventos: espaço de nomes de Event Hubs + "/" + o nome do hub de eventos.  

O hub de eventos URL é apresentado no [portal do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) no dashboard do Event Hubs.  

O **Sink** nome pode ser definido para qualquer cadeia de caracteres válida, desde que será utilizado o mesmo valor consistentemente em todo o ficheiro de configuração.

> [!NOTE]
> Poderão existir sinks adicionais, tais como *applicationInsights* configurada nesta secção. Diagnóstico do Azure permite uma ou mais sinks ser definida se cada sink também está declarado no **PrivateConfig** secção.  
>
>

O sink de Event Hubs tem também de ser declarado e definido no **PrivateConfig** secção o *.wadcfgx* ficheiro de configuração.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

O `SharedAccessKeyName` tem de corresponder ao valor de uma chave de assinatura de acesso partilhado (SAS) e a política que foi definida no **Event Hubs** espaço de nomes. Navegue para o dashboard de Event Hubs no [portal do Azure](https://portal.azure.com), clique em de **configurar** separador e configurar uma política com o nome (por exemplo, "SendRule") que tenha *enviar* permissões. O **StorageAccount** também está declarado no **PrivateConfig**. Não é necessário para alterar os valores aqui se estiverem a funcionar. Neste exemplo, vamos deixar os valores vazio, que é um início de sessão que um recurso a jusante irá definir os valores. Por exemplo, o *Serviceconfiguration* ficheiro de configuração do ambiente define os nomes de ambiente adequadas e as chaves.  

> [!WARNING]
> A chave de SAS de Hubs de eventos é armazenada em texto simples no *.wadcfgx* ficheiro. Muitas vezes, esta chave é verificada para controlo de código fonte ou está disponível como um recurso no servidor de compilação, pelo que deve protegê-lo conforme apropriado. Recomendamos que utilize uma chave SAS aqui com *enviar apenas* permissões para que um utilizador mal intencionado pode escrever o hub de eventos, mas não escutar ao mesmo ou geri-lo.
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a>Configurar o diagnóstico do Azure para enviar os registos e as métricas para os Event Hubs
Tal como abordado anteriormente, todos os dados de diagnóstico personalizadas e predefinidas, ou seja, métricas e registos, serão automaticamente enviados para armazenamento do Azure dos intervalos configurados. Com os Event Hubs e qualquer sink adicional, pode especificar qualquer nó de folha ou raiz da hierarquia sejam enviados para o hub de eventos. Isto inclui eventos ETW, contadores de desempenho, os registos de eventos do Windows e os registos de aplicações.   

É importante considerar o número de pontos de dados, na verdade, deve ser transferido para os Event Hubs. Normalmente, os programadores transferem dados de caminho de acesso frequente de baixa latência que tem de ser consumidos e interpretados rapidamente. Sistemas que monitorizar alertas ou regras de dimensionamento automático são exemplos. Um programador pode também configurar um arquivo de análise alternativo ou procure loja – por exemplo, o Azure Stream Analytics, Elasticsearch, um sistema de monitorização personalizada ou um sistema de monitorização favorito de outras.

Seguem-se algumas configurações de exemplo.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

No exemplo acima, o sink é aplicado ao principal **PerformanceCounters** nó da hierarquia, o que significa que todos os subordinados **PerformanceCounters** serão enviadas para os Event Hubs.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

O exemplo anterior, o sink é aplicado aos apenas três contadores: **colocados em fila de pedidos**, **pedidos rejeitados**, e **% tempo do processador**.  

O exemplo seguinte mostra como um programador pode limitar a quantidade de dados enviados das métricas críticas que são utilizadas para o estado de funcionamento deste serviço.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

Neste exemplo, o sink é aplicado aos registos e está filtrado apenas para o rastreio de nível de erro.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Implementar e atualizar a configuração de aplicação e diagnóstico de serviços Cloud
O Visual Studio fornece o caminho mais fácil para implementar a aplicação e a configuração de receptores de Event Hubs. Para ver e editar o ficheiro, abra o *.wadcfgx* ficheiro no Visual Studio, editá-lo e guardá-lo. O caminho é **projeto de serviço em nuvem** > **funções** > **(RoleName)** > **diagnostics.wadcfgx**.  

Neste momento, todos os de implementação e implementação de atualização de ações no Visual Studio, Visual Studio Team System e todos os comandos ou scripts que se baseiam em MSBuild e utilize o **/t: publicar** destino incluem o *.wadcfgx* no processo de empacotamento. Além disso, as implementações e atualizações de implementar o ficheiro para o Azure, utilizando a extensão de agente de diagnóstico do Azure adequada as suas VMs.

Depois de implementar a aplicação e a configuração de diagnósticos do Azure, irá ver atividade no dashboard do hub de eventos de imediato. Isto indica que está pronto para avançar para visualizar os dados de acesso frequente-path na ferramenta de cliente ou análise de serviço de escuta à sua escolha.  

Na figura seguinte, o dashboard de Event Hubs mostra em bom estado de envio de dados de diagnóstico para o hub de eventos iniciar após algum tempo a 23: 00. Que é quando a aplicação foi implementada com um atualizado *.wadcfgx* ficheiros e o sink estava corretamente configurada.

![][0]  

> [!NOTE]
> Quando efetuar atualizações para o ficheiro de configuração de diagnósticos do Azure (.wadcfgx), recomenda-se que push as atualizações para a aplicação completa, bem como a configuração utilizando a publicação do Visual Studio ou um script do Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Vista-path dados
Tal como abordado anteriormente, existem muitas casos de utilização para escutar e processamento de dados de Event Hubs.

Uma abordagem simple consiste em criar uma aplicação de consola pequeno teste para escutar o hub de eventos e imprimir o fluxo de saída. Pode colocar o código seguinte, o que é explicado mais detalhadamente na [introdução ao Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), numa aplicação de consola.  

Tenha em atenção que a aplicação de consola tem de incluir o [pacote NuGet de anfitrião do processador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Não se esqueça de substituir os valores parênteses angulares no **Main** função com os valores para os seus recursos.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Resolver problemas relacionados com os Event Hubs sinks
* O hub de eventos não apresentam a atividade de eventos de entrada ou saída conforme esperado.

    Certifique-se de que o seu hub de eventos é aprovisionado com êxito. Todas as informações de ligação no **PrivateConfig** secção *.wadcfgx* tem de coincidir com os valores do seu recurso visto no portal. Certifique-se de que tem uma política SAS definida ("SendRule" no exemplo) no portal e que *enviar* permissão é concedida.  
* Após uma atualização, o hub de eventos já não mostra atividade de eventos de entrada ou de saída.

    Em primeiro lugar, certifique-se de que as informações do event hub e a configuração estão correta, conforme explicado anteriormente. Por vezes, o **PrivateConfig** é reposto na atualização da implementação. A correção recomendada é efetuar todas as alterações ao *.wadcfgx* no projeto e, em seguida, push uma atualização da aplicação concluída. Se não for possível, certifique-se de que a atualização de diagnóstico pushes um concluída **PrivateConfig** que inclua a chave SAS.  
* Tentativa das sugestões e o hub de eventos ainda não está a funcionar.

    Tente procura na tabela de armazenamento do Azure que contém erros e registos para diagnósticos do Azure próprio: **WADDiagnosticInfrastructureLogsTable**. Uma opção é utilizar uma ferramenta como [Explorador de armazenamento do Azure](http://www.storageexplorer.com) para ligar a esta conta de armazenamento, visualizar esta tabela e adicionar uma consulta para TimeStamp nas últimas 24 horas. Pode utilizar a ferramenta para exportar um ficheiro. csv e abri-lo numa aplicação, tais como o Microsoft Excel. Excel torna mais fácil procurar cadeias de cartão de chamar, tais como **EventHubs**, para ver o erro é comunicado.  

## <a name="next-steps"></a>Passos seguintes
• [Saber mais sobre os Event Hubs](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Apêndice: Concluir o exemplo de ficheiro (.wadcfgx) de configuração de diagnósticos do Azure
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

O complementares *Serviceconfiguration* para este exemplo assemelha ao seguinte.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Definições de Json com base equivalentes para máquinas virtuais é o seguinte:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Passos seguintes
Pode saber mais sobre os Hubs de Eventos ao aceder às seguintes ligações:

* [Descrição geral dos Hubs de Eventos](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](../event-hubs/event-hubs-create.md)
* [FAQ dos Hubs de Eventos](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
