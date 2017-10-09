---
title: aaaAzure perguntas mais frequentes sobre (FAQ) do Service Bus | Microsoft Docs
description: Responde a algumas perguntas mais frequentes sobre o Service Bus do Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Perguntas Frequentes do Service Bus
Este artigo responde a algumas perguntas mais frequentes sobre o Microsoft Azure Service Bus. Também pode visitar Olá [perguntas frequentes do suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para gerais informações de preços e suporte do Azure.

## <a name="general-questions-about-azure-service-bus"></a>Perguntas gerais sobre o Service Bus do Azure
### <a name="what-is-azure-service-bus"></a>O que é o Service Bus do Azure?
[Service Bus do Azure](service-bus-messaging-overview.md) é uma plataforma de nuvem de mensagens assíncronas que permite-lhe dados toosend entre sistemas desassociados. A Microsoft disponibiliza esta funcionalidade, como um serviço, o que significa que não é necessário toohost algum do seu próprio hardware na ordem toouse-lo.

### <a name="what-is-a-service-bus-namespace"></a>O que é um espaço de nomes do Service Bus?
A [espaço de nomes](service-bus-create-namespace-portal.md) fornece um contentor de âmbito de endereçamento de recursos do Service Bus na sua aplicação. Criar um é necessário toouse Service Bus e deixará de ser um Olá passos primeiro na introdução.

### <a name="what-is-an-azure-service-bus-queue"></a>O que é uma fila do Service Bus do Azure?
A [fila do Service Bus](service-bus-queues-topics-subscriptions.md) é uma entidade em que as mensagens são guardadas. As filas são particularmente úteis quando tem várias aplicações ou de várias partes de uma aplicação distribuída que necessitam de toocommunicate entre si. fila de Olá é semelhantes Centro de distribuição tooa vários produtos (mensagens) são recebidos e, em seguida, enviados a partir dessa localização.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Quais são os tópicos de Service Bus do Azure e as subscrições?
Um tópico pode ser visualizado como uma fila e ao utilizar várias subscrições, torna-se um modelo de serviço de mensagens mais rico; essencialmente, uma ferramenta de comunicação de um-para-muitos. Este modelo de publicação (ou *pub/sub*) ativa uma aplicação que envia um tópico de tooa mensagem com várias subscrições toohave essa mensagem recebida por várias aplicações.

### <a name="what-is-a-partitioned-entity"></a>O que é uma entidade particionada?
Uma fila convencional ou um tópico é processado por um mediador de mensagens única e armazenado num arquivo de mensagens. A [particionada fila ou um tópico](service-bus-partitioning.md) é processada por vários mediadores de mensagens e armazenada em vários arquivos de mensagens. Isto significa que Olá débito global de uma fila particionada ou um tópico já não é limitada pelo desempenho Olá de um mediador de mensagens única ou um arquivo de mensagens. Além disso, uma falha temporária de um arquivo de mensagens não compor uma fila particionada ou um tópico indisponível.

Tenha em atenção que ordenação não é certificar-se ao utilizar a criação de partições de entidades. O evento de Olá que uma partição não está disponível, ainda pode enviar e receber mensagens hello outras partições.

## <a name="best-practices"></a>Melhores práticas
### <a name="what-are-some-azure-service-bus-best-practices"></a>Quais são algumas melhores práticas de Service Bus do Azure?
* [Melhores práticas para melhorias de desempenho utilizando o Service Bus] [ Best practices for performance improvements using Service Bus] – este artigo descreve como toooptimize desempenho ao trocar mensagens.

### <a name="what-should-i-know-before-creating-entities"></a>O que posso saber antes de criar entidades?
Olá seguintes propriedades de uma fila e um tópico é imutável. Execute isto em consideração quando aprovisionar as entidades que este não pode ser modificado, sem criar uma nova entidade de substituição.

* Tamanho
* Criação de partições
* Sessões
* Deteção de duplicados
* Entidade rápida

## <a name="pricing"></a>Preços
Esta secção responde a algumas perguntas mais frequentes sobre a estrutura de preço Olá Service Bus.

Olá [Service Bus preços e faturação](service-bus-pricing-billing.md) artigo explica medidores de faturação Olá no Service Bus e para obter informações sobre as opções de preços do Service Bus, consulte [detalhes de preços do Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).

Também pode visitar Olá [perguntas frequentes do suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para o Azure geral obter informações sobre preços. 

### <a name="how-do-you-charge-for-service-bus"></a>Como é cobram do Service Bus?
Para obter informações completas sobre preços do Service Bus, consulte [detalhes de preços do Service Bus][Pricing overview]. Além disso toohello preços indicado, são-lhe cobrados para transferências de dados associados de saída fora do Centro de dados de Olá na qual a aplicação está aprovisionada.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>Que a utilização do Service Bus é transferência do requerente toodata? O que não é?
Foi fornecida qualquer transferência de dados dentro de uma determinada região do Azure, sem encargos, bem como qualquer transferência de dados de entrada. Transferência de dados fora de uma região é encargos de tooegress assunto que podem ser encontrados [aqui](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Barramento de serviço cobram para armazenamento?
Não, o barramento de serviço não cobram para armazenamento. No entanto, não há uma quota restritiva Olá quantidade máxima de dados que podem ser persistidas por fila/tópico. Consulte as FAQ seguinte de Olá.

## <a name="quotas"></a>Quotas

Para obter uma lista de Service Bus limites e quotas, consulte Olá [descrição geral de quotas do Service Bus][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>A Service Bus tem quaisquer quotas de utilização?
Por predefinição, para qualquer nuvem serviço Microsoft define uma quota de utilização mensal agregado que é calculado em todas as subscrições de um cliente. Porque compreendemos que poderá ser necessário mais do que estes limites, contacte o serviço de cliente em qualquer altura para que iremos possa compreender as suas necessidades e ajustar estes limites adequadamente. Para o Service Bus, a quota de utilização de agregação de Olá é mensagens de mil milhões de 5 por mês.

Enquanto que reservar Olá direita toodisable uma conta de cliente que foi excedido o respetivas quotas de utilização num determinado mês, iremos fornecer notificação por correio electrónico e fazer várias tentativas toocontact um cliente antes de efetuar qualquer ação. Os clientes exceder destas quotas ainda será responsáveis por encargos excedem quotas Olá.

Tal como acontece com outros serviços no Azure, o Service Bus impõe um conjunto de tooensure quotas específico que não há justa utilização de recursos. Pode encontrar mais detalhes sobre estas quotas no Olá [descrição geral de quotas do Service Bus][Quotas overview].

## <a name="troubleshooting"></a>Resolução de problemas
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Quais são algumas das exceções Olá geradas pelas APIs de barramento de serviço do Azure e respetivas ações sugeridas?
Para obter uma lista de possíveis exceções de Service Bus, consulte [descrição geral de exceções][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>O que é uma assinatura de acesso partilhado e os idiomas suportam a geração de uma assinatura?
Assinaturas de acesso partilhado são um mecanismo de autenticação com base no SHA-256 hashes segurados ou URI. Para obter informações sobre como toogenerate as seus próprios assinaturas no nó, PHP, Java e C\#, consulte Olá [assinaturas de acesso partilhado] [ Shared Access Signatures] artigo.

## <a name="subscription-and-namespace-management"></a>Gestão de subscrição e o espaço de nomes
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Como posso migrar tooanother um espaço de nomes subscrição do Azure?

Pode mover um espaço de nomes de uma subscrição do Azure tooanother, utilizando qualquer um dos Olá [portal do Azure](https://portal.azure.com) ou comandos do PowerShell. Na operação de Olá tooexecute de ordem, Olá espaço de nomes já deve estar ativo. utilizador Olá executar comandos Olá tem de ser um administrador em ambos os origem Olá e subscrições de destino.

#### <a name="portal"></a>Portal

Olá toouse subscrição de tooanother espaços de nomes do Service Bus toomigrate portal do Azure, siga as instruções de Olá [aqui](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Olá sequência de comandos do PowerShell seguinte move um espaço de nomes de uma subscrição do Azure tooanother. tooexecute desta operação, Olá espaço de nomes já tem de estar ativo e utilizador Olá executar comandos do PowerShell Olá tem de ser um administrador em ambas as subscrições de origem e destino Olá.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre o Service Bus, consulte Olá os seguintes tópicos.

* [Introdução ao Azure Premium do Service Bus (blogue)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introdução do Azure Premium do Service Bus (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Descrição geral do Service Bus](service-bus-messaging-overview.md)
* [Descrição geral da arquitetura do Service Bus do Azure](service-bus-fundamentals-hybrid-solutions.md)
* [Introdução às filas do Service Bus](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
