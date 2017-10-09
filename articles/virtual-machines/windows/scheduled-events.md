---
title: aaaScheduled eventos para VMs do Windows no Azure | Microsoft Docs
description: "Eventos agendados utilizando o serviço de Azure metadados Olá para nas suas máquinas virtuais do Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Serviço de metadados do Azure: Agendados eventos (pré-visualização) para VMs do Windows

> [!NOTE] 
> Pré-visualizações que são efetuados tooyou disponível numa condição de Olá concorda toohello termos de utilização. Para obter mais informações, consulte [Termos de Utilização Suplementares do Microsoft Azure para Pré-visualizações do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Eventos agendados é uma das Olá subservices em Olá Service de metadados do Azure. É responsável por analisar informações sobre eventos futuros (por exemplo, reiniciar o computador) para a aplicação possa preparar para os mesmos e limitar interrupção. Está disponível para todos os tipos de Máquina Virtual do Azure, incluindo PaaS e IaaS. Eventos agendados fornece as suas máquinas virtuais tempo tooperform preventivo tarefas efeito de Olá toominimize de um evento. 

Eventos agendados está disponível para Linux e VMs do Windows. Para obter informações sobre eventos agendada no Linux, consulte [eventos agendados para VMs com Linux](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Por que motivo agendada eventos?

Com eventos agendadas, que pode tomar passos toolimit Olá impacto plataforma intiated manutenção ou ações iniciadas pelo utilizador no seu serviço. 

Cargas de trabalho de várias instâncias, que utilizam o estado de toomaintain de técnicas de replicação, podem ser toooutages vulnerável a acontecer em múltiplas instâncias. Como falhas poderão resultar em tarefas dispendiosas (por exemplo, os índices reconstrução) ou mesmo uma perda de réplica. 

Em muitos outros casos, hello global disponibilidade do serviço pode ser melhorada através de uma sequência de encerramento correto, tais como concluir (ou cancelamento) transações em trânsito, reatribuição tarefas tooother VMs no cluster de Olá (ativação pós-falha manual) ou remover Olá Máquina virtual de um conjunto de Balanceador de carga de rede. 

Existem casos onde enviar notificações de administrador sobre um evento futuros ou registar um evento deste tipo ajudar a melhorar a possibilidade de assistência de Olá das aplicações alojadas na nuvem de Olá.

Casos de utilização do Azure metadados analisa agendada eventos do serviço no seguinte Olá:
-   Plataforma iniciou a manutenção (por exemplo, a implementação de SO do anfitrião)
-   Chamadas iniciada pelo utilizador (por exemplo, os reinícios de utilizador ou redeploys uma VM)


## <a name="hello-basics"></a>Noções básicas de Olá  

Serviço de metadados do Azure expõe informações sobre como executar máquinas virtuais com um ponto final de REST acessível a partir do Olá VM. informações de Olá estão disponíveis através de um IP não encaminhável, para que não está exposta fora Olá VM.

### <a name="scope"></a>Âmbito
Eventos agendados estão anexado tooall máquinas virtuais num serviço em nuvem ou tooall máquinas virtuais num conjunto de disponibilidade. Como resultado, deve verificar Olá `Resources` campo no Olá eventos tooidentify que as VMs que vão toobe afetado. 

### <a name="discovering-hello-endpoint"></a>Detetar ponto final de Olá
No caso de olá onde é criada uma Máquina Virtual numa rede Virtual (VNet), o serviço de metadados de Olá está disponível a partir de um IP estático não encaminhável, `169.254.169.254`.
Se Olá Máquina Virtual não está a ser criado dentro de uma rede Virtual, casos de predefinição Olá para serviços em nuvem e as VMs clássicas, lógica adicional é necessário toodiscover Olá endpoint toouse. Consulte toothis exemplo toolearn como demasiado[detetar ponto final de anfitrião Olá](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Controlo de versões 
Olá instância metadados do serviço é com a versão. As versões são obrigatórias e a versão atual do Olá `2017-03-01`.

> [!NOTE] 
> Pré-visualização as versões anteriores dos eventos agendadas suportados {mais recente} como Olá api-version. Este formato já não é suportado e será preterido no Olá futura.

### <a name="using-headers"></a>Utilizar cabeçalhos
Quando consultar Olá metadados do serviço, tem de fornecer o cabeçalho de Olá `Metadata: true` tooensure Olá pedido não foi inadvertidamente redirecionado o pedido.

### <a name="enabling-scheduled-events"></a>Ativar eventos agendados
Olá pela primeira vez, que efetue um pedido para eventos agendados, Azure implicitamente ativa Olá funcionalidade na sua máquina Virtual. Como resultado, deve esperar uma resposta atrasada na sua primeira chamada de cópia de segurança tootwo minutos.

### <a name="user-initiated-maintenance"></a>Manutenção iniciada pelo utilizador
Utilizador iniciou a manutenção de máquina virtual através do portal do Azure, Olá API, CLI, ou PowerShell resulta num evento agendado. Isto permite-lhe lógica de preparação de manutenção de Olá tootest na sua aplicação e permite aos seus tooprepare de aplicações para manutenção iniciada pelo utilizador.

Reinício de uma máquina virtual agendas de um evento com o tipo `Reboot`. Voltar a implementar uma máquina virtual agendas de um evento com o tipo `Redeploy`.

> [!NOTE] 
> Atualmente um máximo de 10 operações de manutenção iniciada pelo utilizador pode ser simultaneamente agendado. Este limite irá ser flexibilizada antes de disponibilidade geral eventos agendados.

> [!NOTE] 
> Atualmente manutenção iniciada pelo utilizador, resultando em eventos agendado não é configurável. Capacidade está a ser planeada para uma versão futura.

## <a name="using-hello-api"></a>Utilizar a API de Olá

### <a name="query-for-events"></a>Consulta de eventos
Pode consultar eventos agendada, simplesmente ao efetuar o seguinte Olá chamada:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Uma resposta contém uma matriz de eventos agendadas. Uma matriz vazia significa que não existem atualmente não há eventos agendados.
No caso de olá onde existem eventos agendados, resposta Olá contém uma matriz de eventos: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Propriedades do evento
|Propriedade  |  Descrição |
| - | - |
| EventId | Identificador exclusivo global para este evento. <br><br> Exemplo: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Impacto faz com que a este evento. <br><br> Valores: <br><ul><li> `Freeze`: Olá Máquina Virtual é agendada toopause para alguns segundos. Olá CPU está suspenso, mas não há nenhum impacto na memória, ficheiros abertos ou ligações de rede. <li>`Reboot`: Olá Máquina Virtual está agendada para reiniciar o computador (memória não persistentes é perdida). <li>`Redeploy`: Olá Máquina Virtual é um nó de tooanother toomove agendada (discos efémeras perdem). |
| ResourceType | Tipo de recurso que afeta este evento. <br><br> Valores: <ul><li>`VirtualMachine`|
| Recursos| Lista de recursos que tem impacto este evento. Isto é garantido toocontain máquinas no máximo uma [domínio de atualização](manage-availability.md), mas não pode conter todas as máquinas no Olá UD. <br><br> Exemplo: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Estado do evento | Estado deste evento. <br><br> Valores: <ul><li>`Scheduled`: Este evento é agendada toostart após a hora de Olá especificada no Olá `NotBefore` propriedade.<li>`Started`: Este evento foi iniciado.</ul> Não `Completed` ou estado semelhante nunca é fornecido; já não vai ser devolvido eventos hello aquando da conclusão do evento de Olá.
| NotBefore| Tempo após o qual este evento pode iniciar. <br><br> Exemplo: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Agendamento de eventos
Cada evento está agendado uma quantidade mínima de tempo em Olá futura com base no tipo de evento. Este tempo é refletido num evento `NotBefore` propriedade. 

|EventType  | Tenha em atenção mínima |
| - | - |
| Fixar| 15 minutos |
| Reiniciar | 15 minutos |
| Voltar a implementar | 10 minutos |

### <a name="starting-an-event"></a>A partir de um evento 

Depois de ter aprendidas de um evento futura e concluir a lógica de encerramento correto, pode aprovar eventos pendentes Olá efetuando uma `POST` chamar o serviço de metadados de toohello com Olá `EventId`. Isto indica tooAzure que pode a Encurte notificação mínimo Olá (quando possível). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Confirmar um evento permite Olá eventos tooproceed todas `Resources` no evento Olá, não apenas Olá a máquina virtual que reconhece eventos Olá. Pode, por conseguinte, optar por tooelect uma confirmação de Olá toocoordinate leader, que pode ser tão simple como máquina primeiro Olá Olá `Resources` campo.


## <a name="powershell-sample"></a>Exemplo do PowerShell 

Olá seguintes consultas de exemplo Olá metadados de serviço para os eventos agendados e aprova cada evento pendente.

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>C\# exemplo 

Olá exemplo seguinte é de um cliente simple que comunica com o serviço de metadados de Olá.

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

Eventos agendados podem ser representados Olá seguinte estruturas de dados a utilizar:

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

Olá seguintes consultas de exemplo Olá metadados de serviço para os eventos agendados e aprova cada evento pendente.

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a>Exemplo de Python 

Olá seguintes consultas de exemplo Olá metadados de serviço para os eventos agendados e aprova cada evento pendente.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Passos seguintes 

- Saiba mais sobre Olá APIs disponíveis no Olá [metadados de instância de serviço](instance-metadata-service.md).
- Saiba mais sobre [planeada manutenção de máquinas virtuais do Windows no Azure](planned-maintenance.md).

