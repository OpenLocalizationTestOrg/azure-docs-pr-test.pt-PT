---
title: as filas de armazenamento aaaAzure e filas do Service Bus - comparados e contrasted | Microsoft Docs
description: "Analisa as diferenças e semelhanças entre dois tipos de filas oferecidas pelo Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>As filas de armazenamento e de filas do Service Bus - comparados e contrasted
Este artigo analisa diferenças Olá e semelhanças entre tipos de Olá dois de filas oferecidas pelo Microsoft Azure hoje: as filas de armazenamento e de filas do Service Bus. Ao utilizar esta informação, pode comparar e contraste tecnologias respetivos Olá e ser capaz de toomake uma decisão informada mais sobre a solução que melhor satisfaz as suas necessidades.

## <a name="introduction"></a>Introdução
Azure suporta dois tipos de mecanismos de fila: **as filas de armazenamento** e **filas do Service Bus**.

**As filas de armazenamento**, que fazem parte do Olá [storage do Azure](https://azure.microsoft.com/services/storage/) infraestrutura, funcionalidade uma interface de acesso baseado em REST GET/PUT/observar simples, fornecendo fiável, persistente mensagens dentro e entre os serviços.

**Filas do Service Bus** fazem parte de um mais ampla [mensagens do Azure](https://azure.microsoft.com/services/service-bus/) infraestrutura que suporta a colocação em fila, bem como de publicação/subscrição e, mais avançadas padrões de integração. Para obter mais informações sobre as filas/tópicos/subscrições do Service Bus, consulte Olá [descrição geral do Service Bus](service-bus-messaging-overview.md).

Embora ambas as tecnologias de colocação existirem em simultâneo, as filas de armazenamento foram introduzidas em primeiro lugar, como um mecanismo de armazenamento dedicado fila desenvolvido com serviços de armazenamento do Azure. Filas do Service Bus assentes Olá mais ampla de "mensagens" infraestrutura concebida toointegrate aplicações ou componentes da aplicação que podem abranger vários protocolos de comunicação, contratos de dados, os domínios de confiança, e/ou ambientes de rede.

## <a name="technology-selection-considerations"></a>Considerações de seleção de tecnologia
As filas de armazenamento e de filas do Service Bus são implementações de mensagem de saudação colocação serviço atualmente disponibilizado no Microsoft Azure. Cada um tem um conjunto de funcionalidades ligeiramente diferentes, o que significa que pode escolher um ou Olá outros ou ambos, consoante as necessidades de Olá da sua solução específica ou um problema de negócio/técnica que são resolver.

Quando determinar que tecnologia colocação se adequa a finalidade Olá para uma determinada solução, aos programadores e arquitetos de soluções, devem considerar recomendações Olá abaixo. Para obter mais detalhes, consulte a secção seguinte Olá.

Como um arquiteto de solução/programador, **deve considerar a utilização de filas de armazenamento** quando:

* A aplicação tem de armazenar mais de 80 GB de mensagens numa fila, onde o mensagens hello têm uma duração mais curta mais de 7 dias.
* A aplicação pretende tootrack progresso para processar uma mensagem dentro de fila de Olá. Isto é útil se o trabalho Olá processar uma mensagem de falha. Uma função de trabalho subsequente, em seguida, pode utilizar essa toocontinue de informações de onde parou trabalho anterior Olá.
* Precisa de registos do lado do servidor de todas as transações Olá executadas contra as filas.

Como um arquiteto de solução/programador, **deve considerar a utilização de filas do Service Bus** quando:

* A solução tem de ser capaz de tooreceive mensagens sem ter de fila de Olá toopoll. Com o Service Bus, isto pode ser conseguido através de Olá utilizar protocolos baseados em TCP de Olá Service Bus suporta de operação de receção de utilização de Olá longa-consulta.
* A solução requer Olá fila tooprovide um garantida primeiro-na-primeiro-out (FIFO) ordenada de entrega.
* Pretende uma experiência simétrica no Azure e no Windows Server (nuvem privada). Para obter mais informações, consulte [barramento de serviço para o Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* A solução tem de ser capaz de toosupport a deteção duplicada automática.
* Pretende que as mensagens de tooprocess aplicação como fluxos de longa execução paralelas (mensagens estão associadas com uma transmissão em fluxo utilizando Olá [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propriedade na mensagem de saudação). Neste modelo, cada nó no Olá consumir aplicação compete para fluxos, como toomessages oposição ao. Quando um fluxo é determinado tooa consumir nó, nó de Olá pode examinar o estado de Olá Olá fluxo do Estado da aplicação através de transações.
* A solução requer comportamento transacional e atomicity ao enviar ou receber várias mensagens numa fila.
* Olá time-to-live (TTL) característica da carga de trabalho do Olá específicas da aplicação pode exceder o período de 7 dias Olá.
* A aplicação processa mensagens que podem exceder 64 KB, mas será provavelmente não abordagem Olá 256 KB limite.
* A lidar com um requisito tooprovide um toohello de modelo de acesso baseado em funções filas e outras direitos/permissões para os remetentes e os recetores.
* O tamanho da fila não irá aumentar com mais de 80 GB.
* Pretende toouse Olá AMQP 1.0 baseada em normas mensagens protocolo. Para mais informações sobre AMQP, consulte [descrição geral do Service Bus AMQP](service-bus-amqp-overview.md).
* Pode envision uma eventual a migração de ponto a ponto baseados em fila tooa mensagem exchange padrão de comunicação que permite uma integração perfeita de recetores adicionais (subscritores), cada um dos que recebe cópias independentes de alguns ou todos os as mensagens enviadas toohello fila. Olá última refere-se a capacidade de publicação/subscrição de toohello nativamente fornecida pelo Service Bus.
* A solução de mensagens tem de ser capaz de toosupport garantia de entrega de Olá "em-maioria-uma vez" sem necessidade de Olá para que os componentes de infraestrutura adicionais do toobuild Olá.
* Seria como toopublish capaz de toobe e consumir lotes de mensagens em fila.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Comparar as filas de armazenamento e de filas do Service Bus
tabelas Olá Olá seguintes secções fornecem um agrupamento lógico das funcionalidades de fila e permitem-lhe comparar, de forma rápida, capacidades de Olá disponíveis em filas de armazenamento e de filas do Service Bus.

## <a name="foundational-capabilities"></a>Capacidades fundamentais sobre
Esta secção compara algumas Olá capacidades fundamentais colocação fornecidas as filas de armazenamento e de filas do Service Bus.

| Critérios de comparação | Filas de armazenamento | Filas de Service Bus |
| --- | --- | --- |
| Ordenação garantia |**Não** <br/><br>Para obter mais informações, consulte a nota primeiro do Olá no Olá secção "Informações adicionais".</br> |**Sim - primeiro na primeira Out (FIFO)**<br/><br>(através da utilização de Olá de sessões de mensagens) |
| Garantia de entrega |**Em menos uma** |**Em menos uma**<br/><br/>**Em-maioria-uma vez** |
| Suporte de operação Atómica |**Não** |**Sim**<br/><br/> |
| Receber comportamento |**Bloquear o não**<br/><br/>(conclui imediatamente não se for encontrada nenhuma mensagem de novo) |**Bloquear com/sem tempo limite**<br/><br/>(oferece período de tempo de consulta ou Olá ["Técnica Comet"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Bloquear o não**<br/><br/>(através de Olá utilizar do .NET geridas API apenas) |
| API de estilo de push |**Não** |**Sim**<br/><br/>[OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) e **OnMessage** sessões .NET API. |
| Receber modo |**Observar & concessão** |**Observar & bloqueio**<br/><br/>**Receber e eliminar** |
| Modo de acesso exclusivo |**Com base em concessão** |**Com base em bloqueio** |
| Duração de concessão/bloqueio |**30 segundos (predefinição)**<br/><br/>**7 dias (máximo)** (pode renovar ou versão uma concessão de mensagem utilizando Olá [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 segundos (predefinição)**<br/><br/>Pode renovar um bloqueio de mensagem utilizando Olá [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| / Bloqueio de concessão precisão |**Nível de mensagem**<br/><br/>(cada mensagem pode ter um valor de tempo limite diferentes, que, em seguida, pode atualizar conforme necessário ao processar mensagem de saudação utilizando Olá [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Nível de fila**<br/><br/>(cada fila tem tooall de precisão aplicado um bloqueio da respetivas mensagens, mas podem renovar o bloqueio de Olá utilizando Olá [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Em lotes receber |**Sim**<br/><br/>(especifique explicitamente contagem de mensagens quando a obtenção de mensagens, cópia de segurança tooa máximo de 32 mensagens) |**Sim**<br/><br/>(implicitamente ativar uma propriedade de obtenção prévia ou através de Olá utilizem explicitamente de transações) |
| Em lote de envio |**Não** |**Sim**<br/><br/>(através da utilização de Olá de transações ou criação de batches do lado do cliente) |

### <a name="additional-information"></a>Informações adicionais
* Mensagens nas filas de armazenamento são normalmente primeiro no-first-escalamento, mas por vezes, podem estar fora de ordem; Por exemplo, quando duração do tempo limite de visibilidade de uma mensagem expira (por exemplo, como resultado de uma aplicação de cliente falhar durante o processamento). Quando o tempo limite de visibilidade de Olá expira, mensagem de saudação fica visível novamente na fila de Olá para outro trabalho toodequeue-lo. Nessa altura, mensagem de saudação recentemente visível pode ser colocada na fila de Olá (toobe removida novamente) depois de uma mensagem que foi originalmente colocados em fila depois.
* Olá garantida padrão de FIFO nas filas do Service Bus requer a utilização de Olá de sessões de mensagens. No Olá eventos Olá aplicação falhas ao processar uma mensagem recebida no Olá **observar & Bloquear** modo, Olá próxima vez que um recetor de fila aceita uma sessão de mensagens, será iniciada com a mensagem de falha de Olá após a respetiva período de (TTL) Time-to-live expira.
* As filas de armazenamento são cenários de colocação padrão o toosupport concebida, tais como desacoplamento tolerância a falhas e escalabilidade de tooincrease de componentes de aplicação, carregue nivelamento e a criação de fluxos de trabalho do processo.
* Filas do Service Bus suportam Olá *em menos uma* garantia de entrega. Além disso, Olá *em-maioria-uma vez* semântica pode ser suportado utilizando o estado da aplicação Olá sessão Estado toostore e utilizando transações tooatomically receber mensagens e atualizar o estado da sessão Olá.
* As filas de armazenamento fornecem um modelo de programação uniform e consistente através de filas, tabelas e os BLOBs – para os programadores e equipas de operações.
* Filas do Service Bus fornecem suporte para transações locais no contexto de Olá de uma fila única.
* Olá **receber e eliminar** modo suportado pelo Service Bus fornece Olá tooreduce capacidade de Olá mensagens contagem da operação (e o custo associado) in exchange for garantia de entrega lowered.
* As filas de armazenamento fornecem concessões com concessões de Olá Olá capacidade tooextend para mensagens. Isto permite trabalhadores Olá concessões curto toomaintain nas mensagens. Assim, se um trabalho falhar, mensagem de saudação pode rapidamente processada novamente por outro worker. Além disso, uma função de trabalho pode expandir a concessão Olá numa mensagem se necessita de tooprocess-tempo superior Olá atual da concessão.
* As filas de armazenamento oferecem um tempo limite de visibilidade que pode definir após Olá colocar ou dequeuing de uma mensagem. Além disso, pode atualizar uma mensagem com valores de concessão diferentes em tempo de execução e valores de atualização diferentes em mensagens na Olá mesma fila. Tempos limite de bloqueio do Service Bus são definidos nos metadados da fila de Olá; No entanto, podem renovar o bloqueio de Olá ao chamar Olá [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) método.
* tempo limite máximo de Olá para um bloquear a operação de receção de filas do Service Bus é de 24 dias. No entanto, os tempos limite baseado em REST tem um valor máximo de segundos 55.
* A criação de batches de lado do cliente fornecida pelo Service Bus permite um toobatch de cliente de fila várias mensagens para uma operação de envio único. Criação de batches só está disponível para operações de envio assíncrono.
* Funcionalidades, tais como o limite de 200 TB Olá de filas de armazenamento (mais quando virtualizar contas) e de filas ilimitadas torná-lo numa plataforma ideal para fornecedores de SaaS.
* As filas de armazenamento fornecem um flexível e performant delegado mecanismo de controlo de acesso.

## <a name="advanced-capabilities"></a>Capacidades avançadas
Esta secção compara as capacidades avançadas disponibilizadas pelas filas de armazenamento e de filas do Service Bus.

| Critérios de comparação | Filas de armazenamento | Filas de Service Bus |
| --- | --- | --- |
| Entrega agendada |**Sim** |**Sim** |
| Entregues inactivo automática |**Não** |**Sim** |
| Aumentar o valor time-to-live de fila |**Sim**<br/><br/>(através de atualização no local do tempo limite de visibilidade) |**Sim**<br/><br/>(fornecido através de uma função de API dedicada) |
| Poison suporte de mensagem |**Sim** |**Sim** |
| Atualização no local |**Sim** |**Sim** |
| Registo de transações do lado do servidor |**Sim** |**Não** |
| Métricas do Storage |**Sim**<br/><br/>**Minutos de métricas**: fornece métricas em tempo real para a API de disponibilidade, TPS, chamar contagens, contagens de erro e muito mais, todos em tempo real (agregados por minuto e comunicou dentro de alguns minutos a partir do que aconteceu apenas na produção. Para obter mais informações, consulte [sobre análise as métricas do Storage](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Sim**<br/><br/>(em massa consultas ao chamar [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Gestão de estado |**Não** |**Sim**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Auto-reencaminhamento de mensagens |**Não** |**Sim** |
| Remover a função de fila |**Sim** |**Não** |
| Grupos de mensagem |**Não** |**Sim**<br/><br/>(através da utilização de Olá de sessões de mensagens) |
| Estado da aplicação por grupo de mensagem |**Não** |**Sim** |
| Deteção de duplicados |**Não** |**Sim**<br/><br/>(configurável no lado de remetente Olá) |
| Navegação nos grupos de mensagem |**Não** |**Sim** |
| Obter as sessões de mensagens por ID |**Não** |**Sim** |

### <a name="additional-information"></a>Informações adicionais
* Ambas as tecnologias de colocação permitem toobe uma mensagem agendada para entrega posterior.
* Fila auto-reencaminhamento permite milhares de filas tooauto-reencaminhar os respetivos tooa único a fila de mensagens, de que aplicação recetora Olá consome a mensagem de saudação. Pode utilizar este mecanismo tooachieve segurança, o fluxo de controlo e armazenamento isolar entre cada fabricante de mensagem.
* As filas de armazenamento fornecem suporte para atualizar o conteúdo da mensagem. Pode utilizar esta funcionalidade para as informações de estado persistentes e atualizações incrementais progresso na mensagem de saudação para que possam ser processado de Olá último ponto de verificação conhecido, em vez de a partir do zero. Com as filas do Service Bus, pode ativar Olá cenário mesmo através da utilização de Olá de sessões de mensagens. Sessões permitem-lhe toosave e obter o estado de processamento de aplicação Olá (utilizando [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) e [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Inutilizado lettering](service-bus-dead-letter-queues.md), que é apenas suportado por filas do Service Bus, pode ser útil para isolar as mensagens que não não possível processar com êxito pela aplicação recetora Olá ou quando as mensagens não consegue contactar o seu destino devido tooan expirado propriedade de (TTL) Time-to-live. Olá valor de TTL, especifica quanto permanece de uma mensagem na fila de Olá. Com o Service Bus, mensagem de saudação será fila especial tooa movido chamada $DeadLetterQueue quando o período de TTL Olá expira.
* mensagens de "nocivas" toofind nas filas de armazenamento, quando dequeuing uma aplicação de Olá mensagem examina Olá  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  propriedade da mensagem de saudação. Se **DequeueCount** é maior do que um determinado limiar, aplicação Olá move fila do Olá mensagem tooan definido pela aplicação "entregues".
* As filas de armazenamento permitem-lhe tooobtain um registo detalhado de todas as transações de Olá executadas contra fila Olá, bem como agregados de métricas. Estas opções são úteis para depuração e compreender a forma como a aplicação utiliza as filas de armazenamento. Também são úteis para a aplicação otimização de desempenho e reduzir os custos de Olá de utilizar as filas.
* conceito Olá de "sessões de mensagens" suportado pelo Service Bus permite mensagens que pertencem tooa determinada toobe grupo lógico associado um determinado recetor, que por sua vez, cria uma afinidade de sessão como entre as mensagens e os respetivos recetores. Pode ativar esta avançada funcionalidade do Service Bus através da definição Olá [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propriedade de uma mensagem. Recetores, em seguida, podem escutar num ID de específica de sessão e receber mensagens que partilham Olá especificado identificador de sessão.
* Olá funcionalidade de deteção de duplicação suportada pelo filas do Service Bus automaticamente remove duplicado mensagens enviadas tooa fila ou um tópico, com base no valor Olá Olá [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriedade.

## <a name="capacity-and-quotas"></a>Capacidade e quotas
Esta secção compara as filas de armazenamento e de filas do Service Bus da perspetiva de Olá de [capacidade e quotas](service-bus-quotas.md) que podem ser aplicadas.

| Critérios de comparação | Filas de armazenamento | Filas de Service Bus |
| --- | --- | --- |
| Tamanho máximo da fila |**500 TB**<br/><br/>(tooa limitado [única capacidade das contas de armazenamento](../storage/common/storage-introduction.md#queue-storage)) |**1 GB de too80 GB**<br/><br/>(definido após a criação de uma fila e [ativar a criação de partições](service-bus-partitioning.md) – Consulte Olá secção "Informações adicionais") |
| Tamanho da mensagem máximo |**64 KB**<br/><br/>(48 KB quando utilizar **Base64** codificação)<br/><br/>Azure suporta mensagens grandes através da combinação de filas e blobs – ponto em que pode colocar em fila segurança too200GB para um único item. |**256 KB** ou **1 MB**<br/><br/>(incluindo o cabeçalho e corpo, tamanho do cabeçalho máximo: 64 KB).<br/><br/>Depende Olá [camada de serviço](service-bus-premium-messaging.md). |
| TTL da mensagem máximo |**7 dias** |**`TimeSpan.Max`** |
| Número máximo de filas |**Ilimitado** |**10,000**<br/><br/>(por espaço de nomes de serviço, pode ser aumentada) |
| Número máximo de clientes em simultâneo |**Ilimitado** |**Ilimitado**<br/><br/>(limite de ligações simultâneas 100 aplica-se apenas a comunicação de baseada no protocolo tooTCP) |

### <a name="additional-information"></a>Informações adicionais
* Barramento de serviço impõe limites de tamanho da fila. Olá tamanho máximo da fila é especificada durante a criação da fila de Olá e pode ter um valor entre 1 e 80 GB. Se for atingido o valor de tamanho de fila de Olá definido na criação da fila de Olá, mensagens de entrada adicionais serão rejeitadas e uma exceção será recebida pelo Olá chamar código. Para obter mais informações sobre as quotas no Service Bus, consulte [Quotas de barramento de serviço](service-bus-quotas.md).
* No Olá [escalão Standard](service-bus-premium-messaging.md), pode criar filas do Service Bus em tamanhos de 1, 2, 3, 4 ou 5 GB (a predefinição de Olá é 1 GB). Na camada do Olá Premium, pode criar filas se too80 GB de tamanho. No padrão camadas, com a criação de partições ativada (que é o predefinido de Olá), Service Bus cria 16 partições para cada GB que especificar. Como tal, se criar uma fila que é de 5 GB de tamanho, com 16 partições Olá tamanho máximo da fila fique (5 * 16) = 80 GB. Pode ver o tamanho máximo do Olá da sua fila particionada ou tópico observando a entrada no Olá [portal do Azure][Azure portal]. Na camada de Premium Olá, apenas 2 partições são criadas por fila.
* Com as filas de armazenamento, se hello conteúdo da mensagem de saudação não é segura de XML, em seguida, tem de ser **Base64** codificado. Se lhe **Base64**-codificar a mensagem de saudação, payload de utilizador Olá pode ser segurança too48 KB, em vez de 64 KB.
* Com as filas do Service Bus, cada mensagem armazenada numa fila é composta por duas partes: um cabeçalho e um corpo. tamanho total do Olá de mensagem de saudação não pode exceder a mensagem de saudação máximo tamanho suportado pela camada de serviço Olá.
* Quando os clientes comunicam com as filas do Service Bus através de Olá protocolo TCP, o número máximo de Olá de fila do Service Bus único tooa ligações simultâneas é too100 limitado. Este número é partilhado entre os remetentes e os recetores. Se esta quota é atingida, os pedidos subsequentes para ligações adicionais serão rejeitados e uma exceção será recebida pelo Olá chamar código. Este limite não é imposto nos clientes que se ligam filas toohello baseado em REST API a utilizar.
* Se necessitar de mais de 10 000 filas num único espaço de nomes de barramento de serviço, pode contactar a equipa de suporte do Azure Olá e pedir um aumento. tooscale se para além dos 10 000 filas com o Service Bus, também pode criar espaços de nomes adicionais utilizando Olá [portal do Azure][Azure portal].

## <a name="management-and-operations"></a>Gestão e operações
Esta secção compara as funcionalidades de gestão de Olá fornecidas as filas de armazenamento e de filas do Service Bus.

| Critérios de comparação | Filas de armazenamento | Filas do Service Bus |
| --- | --- | --- |
| Protocolo de gestão |**REST através de HTTP/HTTPS** |**REST através de HTTPS** |
| Protocolo de tempo de execução |**REST através de HTTP/HTTPS** |**REST através de HTTPS**<br/><br/>**AMQP 1.0 Standard (TCP com TLS)** |
| API .NET |**Sim**<br/><br/>(.NET armazenamento cliente API) |**Sim**<br/><br/>(Barramento de serviço de .NET API) |
| C++ nativas |**Sim** |**Sim** |
| API de Java |**Sim** |**Sim** |
| API DE PHP |**Sim** |**Sim** |
| API node.js |**Sim** |**Sim** |
| Suporte de metadados arbitrário |**Sim** |**Não** |
| Regras de nomenclatura de filas |**Cópia de segurança too63 carateres**<br/><br/>(Letras no nome da fila tem de estar em minúsculas.) |**Cópia de segurança too260 carateres**<br/><br/>(Nomes e caminhos de fila são sensível.) |
| Obter a função de comprimento da fila |**Sim**<br/><br/>(Aproximado valor se mensagens expirarem para além de Olá TTL sem ser eliminado.) |**Sim**<br/><br/>(Valor exato, no momento.) |
| Observar função |**Sim** |**Sim** |

### <a name="additional-information"></a>Informações adicionais
* As filas de armazenamento oferecem suporte para atributos arbitrários que podem ser aplicados toohello descrição de fila, no formato Olá pares nome/valor.
* Ambas as tecnologias de fila oferecem Olá capacidade toopeek uma mensagem sem ter toolock departamento de TI que pode ser útil quando implementar uma ferramenta de explorer/browser de fila.
* Olá .NET do Service Bus mediadas mensagens APIs tire partido full-duplex ligações TCP para um melhor desempenho quando comparadas tooREST através de HTTP e que suportam o protocolo padrão Olá AMQP 1.0.
* Os nomes de filas de armazenamento pode ter entre 3 e 63 carateres, pode conter letras minúsculas, números e hífenes. Para obter mais informações, consulte [nomenclatura de filas e metadados](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Nomes de filas do Service Bus podem ser segurança too260 carateres e ter regras de nomenclatura menos restritivas. Nomes de filas do Service Bus podem conter letras, números, períodos, hífenes e carateres de sublinhado.

## <a name="authentication-and-authorization"></a>Autenticação e autorização
Esta secção descreve Olá autenticação e autorização as funcionalidades suportadas pelas filas de armazenamento e de filas do Service Bus.

| Critérios de comparação | Filas de armazenamento | Filas de Service Bus |
| --- | --- | --- |
| Autenticação |**Chave simétrica** |**Chave simétrica** |
| Modelo de segurança |Acesso delegado através de SAS tokens. |SAS |
| Federação do fornecedor de identidade |**Não** |**Sim** |

### <a name="additional-information"></a>Informações adicionais
* Cada tooeither de pedido de Olá colocação tecnologias tem de ser autenticado. As filas públicas com acesso anónimo não são suportadas. Utilizar [SAS](service-bus-sas.md), pode resolver este cenário através da publicação de uma SAS só de escrita, SAS só de leitura ou mesmo uma SAS de acesso completo.
* Olá esquema de autenticação fornecidos pelo armazenamento de filas envolve a utilização de Olá de uma chave simétrica, que é uma base em hash Message Authentication Code (HMAC), calculada com o algoritmo de Olá SHA-256 e codificados como um **Base64** cadeia. Para obter mais informações sobre o protocolo respetivos Olá, consulte [autenticação para Olá dos serviços de armazenamento do Azure](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Filas do Service Bus suportam um modelo semelhante utilizando chaves simétricas. Para obter mais informações, consulte [autenticação de assinatura de acesso partilhado com o Service Bus](service-bus-sas.md).

## <a name="conclusion"></a>Conclusão
Por obter uma compreensão mais aprofundada de tecnologias de Olá dois, que irá ser capaz de toomake uma decisão informada mais no qual espera toouse de tecnologia e quando. Olá decisão no quando as filas de armazenamento toouse ou barramento de serviço e escalona as claramente depende de vários fatores. Estes fatores podem depender fortemente necessidades individuais de Olá da sua aplicação e respetiva arquitetura. Se a aplicação já utiliza Olá principais funcionalidades do Microsoft Azure, poderá preferir toochoose filas de armazenamento, especialmente se necessitar de comunicação básica e processamento de mensagens entre serviços necessidade partilhadas ou filas podem ser superiores a 80 GB de tamanho.

Porque as filas do Service Bus fornecem diversas funcionalidades avançadas, tais como sessões, as transações, deteção, automática de duplicar capacidades de mensagens não entregues e durável publicação/subscrição, podem ser uma opção preferencial se está a criar uma versão híbrida aplicação ou se a sua aplicação, caso contrário requer estas funcionalidades.

## <a name="next-steps"></a>Passos seguintes
Olá seguintes artigos fornece mais informações sobre como utilizar as filas de armazenamento ou filas do Service Bus e documentação de orientação.

* [Introdução às filas do Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Como tooUse Olá o serviço de fila de armazenamento](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Melhores práticas para melhorias de desempenho utilizando o Service Bus mensagens mediadas](service-bus-performance-improvements.md)
* [Introdução às filas e tópicos de Service Bus do Azure (blogue)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Olá tooService de guia para programadores Bus](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Utilizar Olá serviço de colocação no Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

