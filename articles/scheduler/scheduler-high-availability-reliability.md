---
title: aaaScheduler elevada disponibilidade e fiabilidade
description: Programador de elevada disponibilidade e fiabilidade
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Programador de elevada disponibilidade e fiabilidade
## <a name="azure-scheduler-high-availability"></a>O agendador do Azure de elevada disponibilidade
Como um núcleo de serviço de plataforma do Azure, o agendador do Azure está altamente disponível e as funcionalidades de implementação de serviço com redundância geográfica e o tarefa regionais georreplicação da replicação.

### <a name="geo-redundant-service-deployment"></a>Implementação de serviço com redundância geográfica
O agendador do Azure está disponível através de Olá IU em quase todas as região geográfica que está atualmente no Azure. a lista de regiões agendador do Azure está disponível no Olá está [listados aqui](https://azure.microsoft.com/regions/#services). Se um centro de dados numa região alojada é composto indisponível, são funcionalidades de ativação pós-falha de Olá do agendador do Azure que o serviço Olá esteja disponível a partir do Centro de dados de outro.

### <a name="geo-regional-job-replication"></a>Replicação de tarefa Georreplicação regionais
Não só é Olá agendador do Azure front-end disponível para pedidos de gestão, mas o seu próprio trabalho também é georreplicação. Quando houver uma falha na região de um, o agendador do Azure a ativação pós-falha e assegura que essa tarefa Olá é executada a partir de outro centro de dados na região geográfica emparelhado de Olá.

Por exemplo, se criou uma tarefa no Sul Central dos EUA, o agendador do Azure replica automaticamente essa tarefa no Norte Central-nos. Quando existe uma falha no Sul Central dos EUA, o agendador do Azure garante que essa tarefa Olá é executada a partir do Norte Central-nos. 

![][1]

Como resultado, o agendador do Azure garante que o seu mantém-se de dados dentro de Olá mesma região geográfica mais ampla em caso de uma falha do Azure. Como resultado, não precisa de duplicar a tarefa apenas tooadd elevada disponibilidade – agendador do Azure fornece automaticamente capacidades de elevada disponibilidade para os trabalhos.

## <a name="azure-scheduler-reliability"></a>Fiabilidade do agendador do Azure
O agendador do Azure garante que as suas próprias elevada disponibilidade e assume uma abordagem diferentes tarefas toouser criados. Por exemplo, a tarefa pode invocar um ponto final de HTTP que não está disponível. O agendador do Azure nonetheless tenta tooexecute a tarefa com êxito, pelo que lhe confere opções alternativo toodeal com falhas. O agendador do Azure efetua este procedimento de duas formas:

### <a name="configurable-retry-policy-via-retrypolicy"></a>Política Repita configurável através de "retryPolicy"
O agendador do Azure permite-lhe tooconfigure uma política de repetição. Por predefinição, se uma tarefa falhar, programador tenta tarefa Olá novamente quatro vezes mais, intervalos de 30 segundo. Poderá configurar novamente este repetição política toobe mais agressiva (por exemplo, dez vezes, em intervalos de 30 segundo) ou looser (por exemplo, duas vezes em intervalos diários.)

Como um exemplo de quando isto pode ajudar a, pode criar uma tarefa que é executada uma vez por semana e invoca um ponto final de HTTP. Se o ponto final de Olá HTTP está inativo para algumas horas, quando a tarefa é executada, não poderá toowait uma mais semana para Olá tarefa toorun novamente, uma vez que o mesmo Olá predefinido a política de repetição irá falhar. Nestes casos, poderá reconfigurar tooretry de política de repetição padrão Olá a cada três horas (por exemplo) em vez de cada 30 segundos.

toolearn como tooconfigure uma política de repetição, consulte demasiado[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Capacidade de ponto final alternativo através de "errorAction"
Se o ponto final de destino de Olá a tarefa do agendador do Azure permanece inacessível, agendador do Azure retrocede ponto final de processamento de erros alternativo toohello depois de seguir a política de repetição. Se estiver configurado um ponto de final alternativo do processamento de erros, o agendador do Azure invoca-lo. Com um ponto final alternativo, os seus próprios trabalhos são de elevada disponibilidade no enfrentam Olá da falha.

Por exemplo, no diagrama de Olá abaixo, o agendador do Azure segue a toohit de política de repetição um serviço web de Nova Iorque. Depois de Olá repete a falhar, verifica se há alternativa. Em seguida, passa diretamente e começa a efetuar pedidos toohello alternativa com Olá mesma política de repetição.

![][2]

Tenha em atenção que a mesma política de repetição de Olá aplica-se a ação original do tooboth Olá e ação de erro alternativo Olá. Tipo de ação de também toohave possíveis Olá alternativo ação de erro ser diferente do tipo de ação da ação Olá principal. Por exemplo, enquanto a ação principal Olá poderá ser invocar um ponto final de HTTP, ação de erro Olá em vez disso, pode ser uma fila de armazenamento, a fila de barramento de serviço ou a ação de tópico de barramento de serviço que suporta o registo de erros.

toolearn como tooconfigure um ponto final alternativo, consulte demasiado[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Veja Também
 [O que é o Scheduler?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Azure Scheduler](scheduler-concepts-terms.md)

 [Começar a utilizar o agendador no Olá portal do Azure](scheduler-get-started-portal.md)

 [Planos e faturação no Azure Scheduler](scheduler-plans-billing.md)

 [Como as agendas de toobuild complexas e periodicidade avançada com o agendador do Azure](scheduler-advanced-complexity.md)

 [Referência da API REST do Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Azure Scheduler](scheduler-powershell-reference.md)

 [Limites, predefinições e códigos de erro do Azure Scheduler](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Azure Scheduler](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
