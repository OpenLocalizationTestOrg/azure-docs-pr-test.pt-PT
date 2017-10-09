---
title: "relatórios de estado de funcionamento de Service Fabric aaaAdd personalizados | Microsoft Docs"
description: "Descreve como entidades de estado de funcionamento do Service Fabric tooAzure os relatórios de estado personalizado toosend. Fornece recomendações para estruturar e implementar os relatórios de estado de funcionamento de qualidade."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Adicionar relatórios personalizados de estado de funcionamento do Service Fabric
Azure Service Fabric apresenta um [modelo de estado de funcionamento](service-fabric-health-introduction.md) concebido cluster mau estado de funcionamento tooflag e condições de aplicação no entidades específicas. utiliza o modelo de estado de funcionamento de Olá **Informadores de estado de funcionamento** (componentes de sistema e watchdogs). o objetivo de Olá é rápido e fácil de diagnóstico e de reparação. Os escritores de serviço tem de antemão toothink sobre estado de funcionamento. Deve ser comunicada qualquer condição que pode afetar o estado de funcionamento, especialmente se pode ajudar a problemas de sinalizador fechar toohello raiz. informações de estado de funcionamento de Olá podem poupar tempo e esforço na depuração e investigação. Olá utilidade é especialmente clara assim que o serviço de Olá está a funcionar à escala na nuvem de Olá (privada ou do Azure).

monitor de Informadores de Service Fabric Olá identificados condições de interesse. Estes relatórios sobre as condições com base na respetiva vista local. Olá [arquivo de estado de funcionamento](service-fabric-health-introduction.md#health-store) agrega dados de estado de funcionamento enviados por todos os Informadores toodetermine se entidades estão em bom estado de funcionamento global. modelo de Olá é toouse avançado, flexíveis e fáceis de toobe pretendido. qualidade de Olá dos relatórios de estado de funcionamento de Olá determina precisão Olá da vista de estado de funcionamento de Olá do cluster de Olá. Falsos positivos que mostram erradamente problemas mau estado de funcionamento podem afetar negativamente as atualizações ou outros serviços que utilizam dados de estado de funcionamento. Exemplos desses serviços são serviços de reparação e mecanismos de alertas. Por conseguinte, algumas profundamente é tooprovide necessários relatórios que capturam as condições de interesse no Olá melhor forma possível.

tem de toodesign e implementar estado de funcionamento de relatórios, watchdogs e sistema componentes:

* Definir a condição de Olá que estão interessados, forma Olá que é monitorizado e Olá afetam a funcionalidade de cluster ou aplicação Olá. Com base nestas informações, opte por utilizar Olá relatório propriedade e o estado de funcionamento do Estado de funcionamento.
* Determinar Olá [entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy) que aplica-se ao relatório Olá.
* Determinar onde Olá relatórios é efetuada, a partir do Olá watchdog do serviço ou uma interno ou externo.
* Defina um relatório de Olá tooidentify origem utilizada.
* Escolha uma estratégia de criação de relatórios, periodicamente ou em transições. Olá recomendado forma é periodicamente, necessita de código simples e menos propenso tooerrors.
* Determine o relatório de Olá quanto para condições de mau estado de funcionamento devem permanecer no arquivo de estado de funcionamento de Olá e como deve ser desmarcada-lo. Utilizando estas informações, decida Olá do tempo toolive e remover no expiração comportamento dos relatórios.

Conforme mencionado, Reporting Services podem ser efetuada a partir da:

* Olá monitorizados réplica de serviço do Service Fabric.
* Watchdogs internos implementados como um serviço do Service Fabric (por exemplo, um serviço sem monitorização de estado serviço Fabric que monitoriza condições e relatórios de problemas). watchdogs Olá podem ser implementado um todos os nós ou podem ser serviço toohello com monitorizados.
* Watchdogs internos serem executadas em nós de Service Fabric Olá, mas que estão *não* implementado como serviços do Service Fabric.
* Externa watchdogs esse recurso Olá de sonda de *fora* cluster do Service Fabric Olá (por exemplo, serviço de monitorização, como Gomez).

> [!NOTE]
> Box Olá, cluster Olá é preenchido com os relatórios de estado de funcionamento enviados pelos componentes do sistema de Olá. Leia mais em [utilizar o estado de funcionamento do sistema de relatórios para resolução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Olá relatórios de utilizador devem ser enviados [entidades de estado de funcionamento](service-fabric-health-introduction.md#health-entities-and-hierarchy) que já foram criadas pelo sistema Olá.
> 
> 

Uma vez hello estrutura de relatórios de estado de funcionamento está desmarcada, os relatórios de estado de funcionamento podem ser enviados facilmente. Pode utilizar [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport de estado de funcionamento se o cluster Olá não está [segura](service-fabric-cluster-security.md) ou se o cliente de fabric Olá tem privilégios de administrador. Relatórios podem ser feito Olá API por utilizando [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), através do PowerShell ou através de REST. Botões de configuração do batch relatórios para um melhor desempenho.

> [!NOTE]
> Estado de funcionamento do relatório é síncrono e representa funciona para validação de Olá apenas do lado do cliente de Olá. Olá facto Olá relatório é aceite pelo cliente do Estado de funcionamento de Olá ou Olá `Partition` ou `CodePackageActivationContext` objetos não significa que é aplicada no arquivo de Olá. É enviada de forma assíncrona e, possivelmente, em lotes com outros relatórios. Olá processamento no servidor de Olá ainda poderão falhar: número de sequência de Olá pode ser obsoleto, entidade Olá no qual Olá relatório tem de ser aplicado foi eliminado, etc.
> 
> 

## <a name="health-client"></a>Cliente do Estado de funcionamento
relatórios de estado de funcionamento de Olá são enviados toohello o arquivo de estado de funcionamento através de um cliente do Estado de funcionamento, que se encontrem dentro de cliente de fabric Olá. cliente do Estado de funcionamento de Olá pode ser configurado com Olá seguintes definições:

* **HealthReportSendInterval**: atraso Olá entre o relatório de Olá Olá hora está na altura de cliente e Olá do toohello adicionado é enviado toohello arquivo de estado de funcionamento. Relatórios de toobatch utilizadas numa única mensagem, em vez de enviar uma mensagem para cada relatório. a criação de batches de Olá melhora o desempenho. Predefinição: 30 segundos.
* **HealthReportRetrySendInterval**: intervalo de Olá no qual Olá cliente do Estado de funcionamento reenvia o estado de funcionamento acumulado relatórios toohello arquivo de estado de funcionamento. Predefinição: 30 segundos.
* **HealthOperationTimeout**: período de tempo limite de Olá de uma mensagem de relatório enviado toohello arquivo de estado de funcionamento. Se uma mensagem exceder o tempo limite, o cliente do Estado de funcionamento de Olá tentará novamente-lo até o arquivo de estado de funcionamento de Olá confirma que o relatório de Olá foi processado. Predefinição: dois minutos.

> [!NOTE]
> Quando Olá relatórios são em lotes, o cliente de fabric Olá deve ser mantido activa para, pelo menos, Olá tooensure HealthReportSendInterval que são enviadas. Se a mensagem de saudação for perdida ou arquivo de estado de funcionamento de Olá não é possível aplicar-lhes devido a erros de tootransient, o cliente de fabric Olá têm de ser mantido alive toogive mais do um tooretry hipótese.
> 
> 

colocação em memória intermédia Olá no cliente Olá demora exclusividade Olá Olá relatórios em consideração. Por exemplo, se um relatório incorreto específico está a comunicar 100 relatórios por segundo no Olá mesma propriedade de Olá mesma entidade, Olá relatórios são substituídos com a última versão de Olá. No máximo uma esses relatórios existe na fila de cliente Olá. Se a criação de batches é configurada, o número de Olá dos relatórios enviados toohello arquivo de estado de funcionamento é apenas uma por intervalo de envio. Este relatório é Olá último adicionado relatório, que reflete o estado mais recente do Olá da entidade de Olá.
Especifique parâmetros de configuração quando `FabricClient` é criado através da transmissão [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) com Olá pretendido valores para as entradas relacionadas com o estado de funcionamento.

Olá exemplo seguinte cria um cliente de recursos de infraestrutura e especifica que os relatórios de Olá devem ser enviados quando são adicionados. Em tempos limite e erros que podem ser repetidos, tentativas acontecer cada 40 segundos.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Recomendamos que mantenha Olá predefinido dos recursos de infraestrutura de definições de cliente, definiram `HealthReportSendInterval` too30 segundos. Esta definição garante o desempenho ideal toobatching devida. Para os relatórios críticos que devem ser enviados logo que possível, utilize `HealthReportSendOptions` com Immediate `true` no [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API. Relatórios de imediato ignorar Olá intervalo de criação de batches. Utilize este sinalizador com cuidado; Queremos tootake partido do cliente do Estado de funcionamento de Olá criação de batches sempre que possível. Enviar imediata também é útil quando está a fechar o cliente de fabric Olá (por exemplo, o processo de Olá determinou estado inválido e tem de tooshut baixo tooprevent lado efeitos). Assegura um envio de melhor esforço de Olá acumulado relatórios. Quando é adicionado um relatório com o sinalizador de imediato, o cliente do Estado de funcionamento de Olá lotes todos os relatórios de Olá acumulado desde o último envio.

É possível especificar parâmetros mesmos quando é criado um cluster de tooa de ligação através do PowerShell. Olá seguinte o exemplo é iniciado um cluster local de tooa de ligação:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Da mesma forma tooAPI, relatórios podem ser enviados utilizando `-Immediate` comutador toobe enviado imediatamente, independentemente de Olá `HealthReportSendInterval` valor.

Para REST, Olá relatórios são enviados gateway de Service Fabric toohello, que tem um cliente de recursos de infraestrutura interna. Por predefinição, este cliente está relatórios toosend configurado em lotes cada 30 segundos. Pode alterar o intervalo de lote Olá com a definição de configuração de cluster Olá `HttpGatewayHealthReportSendInterval` no `HttpGateway`. Conforme mencionado, uma melhor opção é toosend Olá relatórios com `Immediate` verdadeiro. 

> [!NOTE]
> tooensure não autorizado serviços não é possível comunicar o estado de funcionamento contra Olá as entidades de cluster Olá, configurar Olá tooaccept de pedidos de servidor apenas a partir de clientes protegidos. Olá `FabricClient` utilizada para os relatórios têm de ter com segurança ativada toobe toocommunicate consegue com cluster Olá (por exemplo, com o Kerberos ou autenticação de certificados). Leia mais sobre [cluster segurança](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Relatório de dentro de serviços de baixo privilégio
Se os serviços do Service Fabric não dispõe de cluster de toohello de acesso de administrador, pode comunicar o estado de funcionamento entidades do contexto atual do Olá através de `Partition` ou `CodePackageActivationContext`.

* Para os serviços sem monitorização de estado, utilize [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport na instância de serviço atual Olá.
* Para os serviços com monitorização de estado, utilize [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport na réplica atual.
* Utilize [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport na entidade de partição atual Olá.
* Utilize [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport na aplicação atual.
* Utilize [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport na aplicação atual Olá implementada no nó atual Olá.
* Utilize [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport num pacote de serviço para a aplicação Olá implementado no nó atual Olá.

> [!NOTE]
> Internamente, Olá `Partition` e Olá `CodePackageActivationContext` conter um cliente do Estado de funcionamento configurado com predefinições. Conforme explicado para Olá [cliente do Estado de funcionamento](service-fabric-report-health.md#health-client), relatórios são compilados em batch e enviados um temporizador. objetos de Olá devem ser mantida alive toohave um relatório de Olá toosend hipótese.
> 
> 

Pode especificar `HealthReportSendOptions` quando enviar relatórios através de `Partition` e `CodePackageActivationContext` APIs de estado de funcionamento. Se tiver relatórios críticos que devem ser enviados logo que possível, utilize `HealthReportSendOptions` com Immediate `true`. Relatórios de imediato ignorar Olá intervalo do cliente do Estado de funcionamento interno de Olá de criação de batches. Tal como mencionado anteriormente, utilize este sinalizador com cuidado; Queremos tootake partido do cliente do Estado de funcionamento de Olá criação de batches sempre que possível.

## <a name="design-health-reporting"></a>Relatórios de estado de funcionamento de design
Olá primeiro passo na geração de relatórios de alta qualidade está a identificar as condições de Olá que podem afetar o estado de funcionamento de Olá do serviço de Olá. Quaisquer condições que podem ajudar a problemas de sinalizador num cluster ou de serviço Olá quando inicia - ou mesmo melhor, antes de um problema ocorre – pode potencialmente guardar billions dos utilizados no compromisso. vantagens de Olá incluem menor tempo, menos noite horas despendem a investigar e reparar problemas e superior satisfação do cliente.

Depois de condições de Olá são identificadas, escritores watchdog tem toofigure saída Olá melhor forma toomonitor-los para equilibrar entre sobrecarga e utilidade. Por exemplo, considere um serviço que cálculos complexos que utilizam alguns ficheiros temporários numa partilha. Um watchdog do foi monitorizar Olá partilha tooensure ficará disponível espaço suficiente. Foi possível escutar a para notificações de alterações do ficheiro ou diretório. -Foi reportar um aviso se for atingido um limiar de compromisso e reportar um erro se a partilha de Olá está cheia. Num aviso, um sistema de reparação foi possível iniciar a limpeza mais antigos ficheiros numa partilha de Olá. Um erro, um sistema de reparação foi Olá serviço réplica tooanother move o nó para. Tenha em atenção a como Olá condição Estados são descritos em termos de estado de funcionamento: hello do Estado de Olá condição que pode ser considerados como estando em bom estado (ok) ou mau estado de funcionamento (aviso ou erro).

Depois de detalhes de monitorização de Olá estiver definidos, um escritor watchdog tem toofigure enviados como tooimplement Olá watchdog do. Se a condições de Olá podem ser determinadas a partir do serviço de Olá, Watchdog de Olá pode fazer parte do próprio serviço de Olá monitorizado. Por exemplo, código do serviço Olá pode verificar a utilização da partilha de Olá e, em seguida, comunicar sempre que este tenta toowrite um ficheiro. Olá vantagem esta abordagem é que o Reporting Services é simples. Deve ter cuidado tooprevent erros de watchdog de afetar a funcionalidade do serviço de Olá.

Relatórios a partir de serviço Olá monitorizado nem sempre é uma opção. Um Watchdog no âmbito do serviço de Olá pode não ser capaz de toodetect condições de Olá. Poderá não ter Olá lógica ou dados toomake Olá determinação. overhead de Olá de monitorização de condições de Olá pode ser elevado. condições de Olá também poderão não ser serviço tooa específico, mas em vez disso, afetar as interações entre os serviços. Outra opção é toohave watchdogs num cluster de Olá como processos separados. watchdogs Olá monitorizar condições Olá e o relatório, sem afetar os serviços de Olá principal de qualquer forma. Por exemplo, estes watchdogs ser implementados como serviços sem monitorização de estado no Olá mesma aplicação, implementada em todos os nós ou num Olá nós mesmos como serviço Olá.

Por vezes, um Watchdog em execução no cluster de Olá não é uma opção:. Se a condição Olá monitorizado é disponibilidade Olá ou funcionalidade do serviço de Olá, tal como os utilizadores veem-lo, é melhor watchdogs de Olá toohave no Olá mesmo colocar como clientes de utilizador Olá. Não existe, podem testar as operações de Olá no Olá mesmo modo, os utilizadores chamá-los. Por exemplo, pode ter um watchdog do que se encontra fora do cluster de Olá, emite pedidos de serviço toohello e verifica a latência de Olá e a correção do resultado de Olá. (Para um serviço de calculadora, por exemplo, 2 + 2 devolver 4 dentro de um período de tempo razoável?)

Depois de tem sido finalizados detalhes de watchdog Olá, deve decidir num ID de origem que identifica exclusivamente. Se vários watchdogs de Olá mesmo tipo são living no hello cluster, estes tem um relatório sobre entidades diferentes ou, se estes relatórios sobre Olá mesma entidade, o ID de origem diferente de utilização ou propriedade. Desta forma, os relatórios podem coexistir. propriedade de Olá do relatório de estado de funcionamento de Olá deve capturar condição Olá monitorizado. (Por exemplo de Olá acima, pode ser propriedade de Olá **ShareSize**.) Se vários relatórios aplicam toohello mesmo condição, hello propriedade deve conter algumas informações dinâmicas que lhe permite toocoexist de relatórios. Por exemplo, se precisam de múltiplas partilhas toobe monitorizado, o nome da propriedade Olá pode ser **ShareSize sharename**.

> [!NOTE]
> Efetue *não* utilizar informações de estado de tookeep de arquivo de estado de funcionamento de Olá. Apenas as informações relacionadas com o estado de funcionamento devem reportadas como estado de funcionamento, como esta avaliação do Estado de funcionamento de Olá impactos informações de uma entidade. arquivo de estado de funcionamento de Olá não foi concebido como um arquivo para fins gerais. Utiliza tooaggregate de lógica de avaliação do Estado de funcionamento todos os dados em estado de funcionamento de Olá. Estado de funcionamento de agregados de enviar informações relacionado com toohealth (como comunicar o estado com um Estado de funcionamento de OK) não tem impacto Olá, mas pode afetar negativamente desempenho Olá do arquivo de estado de funcionamento de Olá.
> 
> 

ponto de decisão seguinte Olá-se que tooreport de entidade. A maioria do tempo de Olá, condição Olá claramente idetifies Olá entidade. Escolha entidade Olá com melhores granularidade possíveis. Se uma condição afeta todas as réplicas numa partição, um relatório sobre partição Olá, não é possível no serviço de Olá. Existem onde mais profundamente for necessária, apesar de nos casos extremos. Se a condição de Olá afeta uma entidade, tal como uma réplica, mas Olá desire é toohave Olá condição sinalizada mais de duração Olá de vida de réplica, em seguida, deve ser declarada na partição de Olá. Caso contrário, quando é eliminada réplica Olá, arquivo de estado de funcionamento de Olá limpa todos os seus relatórios. Escritores Watchdog tem de pensar sobre durações Olá de entidade Olá e relatório Olá. Tem de ser encriptado quando um relatório deve ser limpa a partir de um arquivo (por exemplo, quando um erro comunicado numa entidade já não se aplica).

Vamos ver um exemplo que coloca em conjunto pontos Olá que posso descrito. Considere que uma aplicação de Service Fabric é composto por um serviço com monitorização de estado de persistente principal e secundários serviços sem monitorização de estado implementados em todos os nós (um tipo de serviço secundário para cada tipo de tarefa). mestre de Olá tem uma fila de processamento que contém toobe comandos executado por secundárias. bases de dados secundárias Olá executar pedidos de entrada Olá e enviar sinais de back-confirmação. Uma condição que foi monitorizada é o comprimento da fila de processamento mestre Olá Olá. Se o comprimento da fila principal de Olá atinge um limiar, é reportado um aviso. Aviso de Olá indica que bases de dados secundárias Olá não consegue processar a carga de Olá. Se a fila de Olá atinge o comprimento de máximo de Olá e comandos são ignorados, é reportado um erro, como Olá não é possível recuperar o serviço. Olá relatórios podem ser propriedade de Olá **QueueStatus**. Watchdog de Olá se encontrem dentro Olá serviço e é enviada periodicamente na réplica primária principal de Olá. tempo de Olá toolive é dois minutos e é enviada periodicamente a cada 30 segundos. Se Olá primário ficar inativo, relatório de Olá é automaticamente limpa da loja. Se a réplica do serviço de Olá está a funcionar, mas este é está bloqueada ou ter outros problemas, Olá relatório expira no arquivo de estado de funcionamento de Olá. Neste caso, a entidade de Olá é avaliada no erro.

Outra condição que pode ser monitorizada é o tempo de execução de tarefas. Olá mestre distribui as tarefes toohello secundárias com base no tipo de tarefa Olá. Dependendo da estrutura de Olá, mestre Olá foi consultar secundárias Olá para o estado da tarefa. Foi também Aguarde para bases de dados secundárias toosend confirmação back sinais quando estes terminado. No segundo caso Olá, deve ter cuidado situações toodetect em que as réplicas secundárias die ou mensagens sejam perdidas. Uma opção é para Olá mestre toosend um toohello de pedido de ping secundários, mesmo que envia o estado. Se não for recebido nenhuma Estado, o mestre de Olá considera-la uma falha e reschedules tarefas Olá. Este comportamento parte do pressuposto de que as tarefas de Olá idempotent.

condição de Olá monitorizado possa ser convertida como um aviso se a tarefa de Olá não é efetuada num determinado período de tempo (**t1**, por exemplo, 10 minutos). Se a tarefa de Olá não é concluída no tempo (**t2**, por exemplo, 20 minutos), pode ser convertida condição Olá monitorizado como erro. Este relatório pode ser feito de várias formas:

* réplica primária principal de Olá os relatórios no próprio periodicamente. Pode ter uma propriedade para todas as tarefas pendentes na fila de Olá. Se, pelo menos, uma tarefa demora mais, comunicar o estado Olá na propriedade Olá **PendingTasks** é um aviso ou erro, conforme apropriado. Se não existem tarefas pendentes ou todas as tarefas iniciou a execução, o estado do relatório de Olá é OK. tarefas de Olá sejam persistentes. Se Olá primário ficar inativo, primário Olá recentemente promovido pode continuar tooreport corretamente.
* Outro processo watchdog (na nuvem de Olá ou externa) verifica tarefas Olá (do fora, com base no resultado da tarefa Olá pretendido) toosee se estes estão concluídas. Se não Respeitamos a limiares Olá, é enviado um relatório de serviço principal Olá. Também é enviado um relatório de cada tarefa que inclui o identificador de tarefa Olá, como **PendingTask + taskId**. Relatórios devem ser enviados apenas em mau estado de funcionamento Estados. Definir tooa toolive tempo alguns minutos e marcar Olá relatórios toobe removido quando expirarem tooensure limpeza.
* Olá secundário que está a executar uma tarefa relatórios quando demora mais do que esperado toorun-lo. Esta comunica na instância do serviço Olá na propriedade Olá **PendingTasks**. relatório de Olá pinpoints instância de serviço de Olá tem problemas, mas não captura situação olá onde a instância de Olá dies. relatórios de Olá são, em seguida, limpa. Foi de relatório no serviço secundário Olá. Se Olá secundário concluir a tarefa de Olá, instância secundário Olá limpa relatório Olá do arquivo de Olá. relatório de Olá não captura situação olá onde mensagem de confirmação de saudação perde-se e tarefas de Olá não foi concluída do ponto de vista do mestre de Olá.

No entanto, os relatórios de Olá é efetuada em casos Olá descritos acima, Olá relatórios são capturados no estado de funcionamento da aplicação quando o estado de funcionamento é avaliado.

## <a name="report-periodically-vs-on-transition"></a>Relatório periodicamente vs em transição
Utilizando o modelo de relatório de funcionamento de Olá, watchdogs pode enviar relatórios periodicamente ou transições. Olá recomendada forma para watchdog do Reporting Services é periodicamente, porque o código de Olá tooerrors muito mais simples e menos propenso. watchdogs Olá devem esforçar-nos toobe tão simple como tooavoid possíveis erros que acionam relatórios incorretos. Incorreto *mau estado de funcionamento* relatórios afetam os cenários de com base no estado de funcionamento, incluindo atualizações e avaliações do Estado de funcionamento. Incorreto *bom* relatórios ocultar os problemas no cluster de Olá, que não for pretendida.

Para os relatórios periódica, Watchdog de Olá pode ser implementada com um temporizador. Uma chamada de retorno do temporizador, Watchdog de Olá pode verificar o estado de Olá e enviar um relatório com base no estado atual do Olá. Não há nenhum toosee necessidade, o relatório foi enviado anteriormente ou efetuar quaisquer otimizações em termos de mensagens. cliente do Estado de funcionamento de Olá tem toohelp lógica com um desempenho de criação de batches. Enquanto o cliente do Estado de funcionamento de Olá é mantida activa, internamente repete até que o relatório de Olá é confirmado ao arquivo de estado de funcionamento de Olá ou Watchdog de Olá gera um relatório mais recente com Olá mesma entidade, de propriedade e origem.

Transições de relatórios requer processamento tenha o cuidado de estado. Watchdog de Olá monitoriza algumas condições e os relatórios apenas quando as condições de Olá alterar. Olá upside desta abordagem é que são necessários menos relatórios. downside Olá está lógica Olá de Watchdog de Olá complexa. Watchdog de Olá tem de manter condições Olá ou relatórios Olá, para que possam ser inspecionado toodetermine alterações de estado. Na ativação pós-falha, deve ter cuidado com relatórios adicionado, mas ainda não enviou toohello arquivo de estado de funcionamento. número de sequência de Olá tem de ser alguma vez aumentar. Caso contrário, Olá relatórios são rejeitados como obsoletos. Em casos raros olá onde é tarifas de perda de dados, a sincronização pode ser necessária entre o estado de Olá do relatório de Olá e estado de Olá do arquivo de estado de funcionamento de Olá.

Elaboração de relatórios em transições faz sentido para elaboração de relatórios em si próprios, através de serviços `Partition` ou `CodePackageActivationContext`. Olá quando o objeto local (réplica ou de um pacote de serviço implementado / implementado aplicação) é removida, todos os respetivos relatórios são também removidos. Este limpeza automática relaxes Olá necessário para a sincronização entre o relatório e o arquivo de estado de funcionamento. Se o relatório de Olá destina-se a partição principal ou a aplicação principal, deve ter cuidado nos relatórios de obsoletos de tooavoid de ativação pós-falha no arquivo de estado de funcionamento de Olá. Lógica tem de ser adicionada Estado correto do toomaintain Olá e relatório Olá clara da loja quando já não é necessária.

## <a name="implement-health-reporting"></a>Implementar o relatório de estado de funcionamento
Assim hello detalhes de entidade e o relatório estiverem encriptados, enviar relatórios de estado de funcionamento pode ser feito através da API de Olá, PowerShell ou REST.

### <a name="api"></a>API
tooreport através de Olá API, terá de toocreate um tipo de entidade do toohello específico do Estado de funcionamento relatório pretendem tooreport no. Atribua o cliente de estado de funcionamento do Olá relatório tooa. Em alternativa, crie uma informações de estado de funcionamento e transmita-toocorrect reporting métodos em `Partition` ou `CodePackageActivationContext` tooreport entidades atual.

Olá exemplo seguinte mostra periódico de relatórios a partir de um Watchdog num cluster de Olá. Watchdog de Olá verifica se um recurso externo pode ser acedido a partir dentro de um nó. recurso de Olá é necessário um manifesto de serviço na aplicação Olá. Se o recurso de Olá não estiver disponível, hello outros serviços dentro da aplicação Olá podem continuará a funcionar corretamente. Por conseguinte, Olá relatório é enviado na entidade de pacote de serviço Olá implementado cada 30 segundos.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Enviar relatórios de estado de funcionamento com  **envio ServiceFabric*EntityType*HealthReport * *.

Olá exemplo seguinte mostra periódico de relatórios nos valores de CPU num nó. relatórios de Olá devem ser enviados a cada 30 segundos e têm um período de tempo toolive de dois minutos. Se expirarem, o relatório de Olá tem problemas, para que o nó Olá é avaliada em erro. Quando Olá CPU está acima de um limiar, o relatório de Olá tem um Estado de funcionamento de aviso. Quando Olá CPU permanece acima de um limiar mais de tempo de Olá configurado, é reportado como um erro. Caso contrário, o relatório de Olá envia um Estado de funcionamento de OK.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Olá exemplo seguinte relatórios um aviso transitório numa réplica. Este primeiro obtém o ID de partição Olá e Olá, em seguida, o ID de réplica para o serviço de Olá que é interessado no. Em seguida, envia um relatório na **PowershellWatcher** na propriedade Olá **ResourceDependency**. relatório de Olá é de interesse para apenas dois minutos e este é removido do arquivo de Olá automaticamente.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Envie relatórios de estado de funcionamento através de REST com pedidos POST, aceda a entidade de toohello pretendida e que tenham na descrição de relatório de estado de funcionamento do Olá corpo Olá. Por exemplo, consulte como toosend REST [relatórios de estado de funcionamento do cluster](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) ou [relatórios de estado de funcionamento do serviço](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Todas as entidades são suportadas.

## <a name="next-steps"></a>Passos seguintes
Com base nos dados de estado de funcionamento de Olá, escritores de serviço e os administradores de cluster/aplicação podem considerar informações de Olá tooconsume de formas. Por exemplo, pode definir alertas com base no graves problemas do Estado de funcionamento Estado toocatch antes de poderem provoke falhas de cópia de segurança. Os administradores podem também configurar problemas de toofix de sistemas de reparação automaticamente.

[Introdução tooService estado de funcionamento de recursos de infraestrutura monitorização](service-fabric-health-introduction.md)

[Ver relatórios de estado de funcionamento do Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Como tooreport e verificação de estado de funcionamento do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Utilizar relatórios de estado de funcionamento do sistema para resolução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Monitorizar e diagnosticar os serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização da aplicação de Service Fabric](service-fabric-application-upgrade.md)

