---
title: 'Azure CosmosDB: Pedir unidades por minuto (RU/m) | Microsoft Docs'
description: "Saiba como o custo de tooreduce através da utilização de pedido unidades por minuto."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Unidades de pedido por minuto do BD Azure Cosmos

BD do Azure do Cosmos é concebida toohelp alcançar um desempenho previsível, rápido e dimensionamento de forma totalmente integrada, juntamente com o crescimento da sua aplicação. Pode aprovisionar débito num contentor Cosmos DB em ambos, por segundo e em granularidades por minuto (RU/m). Olá débito aprovisionado por minuto granularidade é utilizado toomanage picos inesperados na carga de trabalho Olá ocorrer granularidade por segundo. 

Este artigo fornece uma descrição geral sobre como funciona o Olá aprovisionamento da unidade de pedido de mensagens em fila por minuto (RU/m). objetivo de Olá em consideração com o aprovisionamento de RU/m é tooprovide um desempenho previsível em torno imprevisíveis necessidades (especialmente se precisar de análise toorun por cima de dados operacionais) e spiky cargas de trabalho. Queremos toohave que os nossos clientes consumam mais débito de Olá aprovisionam para dimensionamento rapidamente com tranquilidade.

Depois de ler este artigo, irá ser Olá tooanswer capaz de seguintes perguntas:

* Como funciona uma unidade de pedido de mensagens em fila por minuto?
* O que é a diferença de Olá entre a unidade de pedido de mensagens em fila por minuto e unidade de pedido de mensagens em fila por segundo?
* Como tooprovision RU/m?
* Sob a qual o cenário deverá devo considerar aprovisionamento unidade de pedido de mensagens em fila por minuto?
* Como toouse Olá métricas portal toooptimize meu custo e desempenho?
* Definir o tipo de pedido pode consumir seu orçamento RU/m?

## <a name="provisioning-request-units-per-minute-rum"></a>Aprovisionamento de unidades de pedido por minuto (RU/milhão)

Quando aprovisionar Azure Cosmos DB granularidade Olá segundo (RU/s), obtenha garantia Olá que o pedido for bem sucedida, a latência baixa se o débito não excedeu a capacidade de Olá aprovisionada dentro desse segundo. Com RU/m, granularidade Olá está minuto Olá com a garantia de Olá que o pedido seja bem-sucedido dentro desse minuto. Em comparação com sistemas de toobursting, iremos Certifique-se de que o desempenho Olá obtiver é previsível e pode planear no mesmo.

forma Olá por minuto aprovisionamento funciona é simple:

* RU/m é faturada de hora a hora e na adição tooRU/s. Para obter mais detalhes, aceda a base de dados do Azure Cosmos [página de preços](https://aka.ms/acdbpricing).
* RU/m pode ser ativado ao nível da coleção. Que pode ser feito através de Olá SDKs (Node.js, Java ou .net) ou através do portal Olá (também incluir cargas de trabalho do MongoDB API)
* Quando RU/m estiver ativada, para cada 100 RU/s aprovisionada, também obter 1.000 RU/m aprovisionado (rácio Olá é 10 x)
* No segundo indicado, uma unidade de pedido consome o aprovisionamento de RU/m apenas se excedeu a por segundo aprovisionamento dentro desse segundo
* Uma vez Olá terminar o período de 60-segundo (UTC), é refilled Olá por minuto de aprovisionamento
* RU/m pode ser ativada apenas para coleções com um máximo de aprovisionamento de 5000 RU/s por partição. Se aumentar as suas necessidades de débito e ter um nível elevado de aprovisionamento por partição, irá receber uma mensagem de aviso

Abaixo está um exemplo concreto, em que um cliente pode aprovisionar 10kRU/s com 100kRU/m, guardar 73% custo em relação a aprovisionamento para o horário de pico (na 50kRU/seg) através de um período de 90 segundo numa coleção que tenha 10 000 RU/s e 100 000 de RU/s aprovisionada:

* segundo 1ª: atribuição de RU/m Olá está definida em 100 000
* segundo 3rd: durante esse Olá segundo consumo de unidade de pedido era 11,010 RUs, 1,010 RUs acima Olá RU/s de aprovisionamento. Por conseguinte, 1,010 RUs são deducted do orçamento de RU/m Olá. 98,990 RUs estão disponíveis para Olá seguintes segundos 57 na atribuição de RU/m Olá
* segundo 29th: durante esse segundo, Ocorreu um grande pico de pedidos (> x 4 ou superior aprovisionamento por segundo) e o consumo de Olá de unidade de pedido foi 46,920 RUs. 36,920 RUs são deducted do orçamento RU/m Olá removida da 92,323 RUs (28th segundo) too55, 403 RUs (29th segundo)
* segundo 61st: RU/m orçamento está definido novamente too100, 000 RUs.
 
![Gráfico que mostra o consumo de Olá e aprovisionamento de base de dados do Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Especificar a capacidade de unidade de pedido com RU/m

Ao criar uma coleção de BD do Cosmos do Azure, especifique o número de Olá de unidades de pedido por segundo (RU por segundo) que pretende reservado para a coleção de Olá. Também pode decidir se pretende tooadd RU por minuto. Isto pode ser feito Olá Portal ou Olá SDK. 

### <a name="through-hello-portal"></a>Através do Portal de Olá

Ativar ou desativar RU por minuto simplesmente necessita de um clique quando o aprovisionamento de uma coleção. 

 ![Captura de ecrã com como tooset RU/m no Olá portal do Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Através de Olá SDK
Em primeiro lugar, isto é importante toonote que RU/m só está disponível para Olá SDKs os seguintes:

* .NET 1.14.0
* Java 1.11.0
* NODE.js 1.12.0
* Python 2.2.0

Eis um fragmento de código para criar uma coleção com 3,000 unidades de pedido por unidades de pedido segundo e 30 000 por minuto utilizando Olá .NET SDK:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Eis um fragmento de código para alterar o débito de Olá de uma coleção too5, 000 unidades de pedido por segundo sem aprovisionamento RU por minuto utilizando Olá .NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Boa caber cenários

Nesta secção, iremos fornecer uma descrição geral dos cenários que são uma boa opção para ativar as unidades de pedido por minuto.

**Ambiente de desenvolvimento/teste:** boa opção. Durante a fase de desenvolvimento de Olá, se estiver a testar a aplicação com diferentes cargas de trabalho, RU/m pode fornecer flexibilidade Olá nesta fase. Ao hello [emulador](local-emulator.md) é tootest uma ótima ferramenta gratuita do Azure Cosmos DB. No entanto se quiser toostart num ambiente de nuvem, terá uma enorme flexibilidade com RU/m para as suas necessidades de desempenho adhoc. Será demora mais tempo a desenvolver, menos worrying sobre as necessidades de desempenho em primeiro lugar. É recomendável a partir de aprovisionamento Olá mínimo RU/s e ative RU/m.

**Tem de granularidade imprevisível, spiky, minuto:** boa caber – reduções: 25 75%. Podemos ter visto grande melhoramento de RU/m e a maioria dos cenários de produção são para esse grupo. Se tiver uma carga de trabalho de IoT que tenha o pico de pedidos algumas vezes num minuto, se tiver as consultas em execução quando o sistema faz mass inserir Olá mesmo tempo, precisa de capacidade extra para handeling spiky precisa. Recomendamos a otimizar as suas necessidades de recursos aplicando a nossa abordagem de passo abaixo.

 ![Gráfico que mostra o consumo de pedido na granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Figura - benchmark de consumo do RU*

**Tranquilidade:** boa caber – reduções: 10-20%. Por vezes, pretende apenas tranquilidade toohave e não se preocupe sobre potenciais picos e limitação. Esta funcionalidade é o direito de Olá uma por si. Nesse caso, recomendamos que ative a RU/m e ligeiramente inferior a por segundo de aprovisionamento. Neste caso é diferente do Olá acima, que não irá tentar toooptimize forma agressiva o aprovisionamento. Esta é a mais de uma mente "Limitação de Zero" estão em.

Operações críticas com necessidades adhoc:, por vezes, recomendamos que tooonly permitem operações críticas acesso RU/m budget para atribuição de Olá não obter consumir pelo ad hoc ou menos importantes operações. Que pode ser facilmente definidas na secção de Olá abaixo.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Utilizar Olá métricas portal toooptimize custo e desempenho

**Próximas semanas Olá, iremos irá desenvolver mais conteúdo Olá à volta de monitorização RUs consumo minuto toooptimize que tem do débito.**

Através de métricas de portal Olá, pode ver a quantidade de segundos de RU regulares consumir versus RU minutos. Estas métricas de monitorização deve ajudar a otimizar o aprovisionamento. 

Recomendamos uma abordagem de passo a passo sobre como toouse RU/m tooyour partido. Para cada passo, deve ter uma descrição geral do consumo de Olá RU que representa um ciclo completo da sua carga de trabalho (poderia ser horas, dias, ou até mesmo semanas) e obter conhecimentos aprofundados na utilização de Olá do que for aprovisionado.

princípio Olá atrás esta abordagem é toomake o aprovisionamento de débito como fechar como tooa possíveis aprovisionamento ponto que corresponda aos critérios de desempenho abaixo. 

![Gráfico que mostra o consumo de pedido na granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand Olá ideal aprovisionamento ponto para a carga de trabalho, terá de toounderstand:

* Padrões de consumo: nenhum, os picos de constante ou pouco frequentes? Breve (média de x 2), médio ou grande (> 10 x média) picos?
* Percentagem de pedidos otimizados: fazer sentir-se confortáveis ao se tiver um bit da limitação? Se assim for, pelo que? 

Depois de identificar quais são os objetivos, será capaz de tooget próximo toohello ideal de aprovisionamento.

tooassist, queremos tooprovide uma orientação geral sobre como toooptimize o aprovisionamento com base no consumo RU/m. Esta orientação não se aplica tooall tipo de cargas de trabalho, mas é com base em dados de conhecimento do Olá pré-visualização privada. Vamos poderá alterar essas linhas de base como podemos Saiba mais:

|RU/m % utilização|Nível de utilização de RU/m|Ações recomendadas para aprovisionamento|
|---|---|---|
|0-1%|Em utilização|Reduzir tooconsume RU/s mais RU/m|
|1-10%|Utilização de bom estado de funcionamento|Manter hello mesmo aprovisionamento nível|
|Superior a 10%|Ao longo de utilização|Aumentar RU/s toorely menos RU/m|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Selecione as operações de podem consumir orçamento de RU/m Olá

Ao nível do pedido, pode também Ativar/desativar pedido do RU/m orçamento tooserve Olá independentemente do tipo de operação. Se regular orçamento RUs/seg aprovisionado é consumido e pedido Olá não pode consumir orçamento de RU/m Olá, este pedido será limitado. Por predefinição, quaisquer pedidos servidos pelo RU/m orçamento se orçamento de débito RU/m está ativado. 

Eis um fragmento de código para desativar o orçamento RU/m Olá DocumentDB API a utilizar para as operações CRUD e consulta.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Passos seguintes

Neste artigo, vamos já descrito funciona como criação de partições do BD Azure Cosmos, como pode criar coleções particionadas e como pode escolher uma chave de partição para a sua aplicação.

* Efetue o dimensionamento e desempenho de teste com base de dados do Azure Cosmos. Consulte [desempenho e dimensionamento de teste com base de dados do Azure Cosmos](performance-testing.md) para um exemplo.
* Introdução à programação com Olá [SDKs](documentdb-sdk-dotnet.md) ou Olá [REST API](/rest/api/documentdb/).
* Saiba mais sobre [débito aprovisionado](request-units.md) do BD Azure Cosmos 

