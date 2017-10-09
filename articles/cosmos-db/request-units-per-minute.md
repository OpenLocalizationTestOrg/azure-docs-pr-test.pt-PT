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
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="f3525-103">Unidades de pedido por minuto do BD Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="f3525-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="f3525-104">BD do Azure do Cosmos é concebida toohelp alcançar um desempenho previsível, rápido e dimensionamento de forma totalmente integrada, juntamente com o crescimento da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="f3525-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="f3525-105">Pode aprovisionar débito num contentor Cosmos DB em ambos, por segundo e em granularidades por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="f3525-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="f3525-106">Olá débito aprovisionado por minuto granularidade é utilizado toomanage picos inesperados na carga de trabalho Olá ocorrer granularidade por segundo.</span><span class="sxs-lookup"><span data-stu-id="f3525-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="f3525-107">Este artigo fornece uma descrição geral sobre como funciona o Olá aprovisionamento da unidade de pedido de mensagens em fila por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="f3525-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="f3525-108">objetivo de Olá em consideração com o aprovisionamento de RU/m é tooprovide um desempenho previsível em torno imprevisíveis necessidades (especialmente se precisar de análise toorun por cima de dados operacionais) e spiky cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f3525-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="f3525-109">Queremos toohave que os nossos clientes consumam mais débito de Olá aprovisionam para dimensionamento rapidamente com tranquilidade.</span><span class="sxs-lookup"><span data-stu-id="f3525-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="f3525-110">Depois de ler este artigo, irá ser Olá tooanswer capaz de seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="f3525-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="f3525-111">Como funciona uma unidade de pedido de mensagens em fila por minuto?</span><span class="sxs-lookup"><span data-stu-id="f3525-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="f3525-112">O que é a diferença de Olá entre a unidade de pedido de mensagens em fila por minuto e unidade de pedido de mensagens em fila por segundo?</span><span class="sxs-lookup"><span data-stu-id="f3525-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="f3525-113">Como tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="f3525-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="f3525-114">Sob a qual o cenário deverá devo considerar aprovisionamento unidade de pedido de mensagens em fila por minuto?</span><span class="sxs-lookup"><span data-stu-id="f3525-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="f3525-115">Como toouse Olá métricas portal toooptimize meu custo e desempenho?</span><span class="sxs-lookup"><span data-stu-id="f3525-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="f3525-116">Definir o tipo de pedido pode consumir seu orçamento RU/m?</span><span class="sxs-lookup"><span data-stu-id="f3525-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="f3525-117">Aprovisionamento de unidades de pedido por minuto (RU/milhão)</span><span class="sxs-lookup"><span data-stu-id="f3525-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="f3525-118">Quando aprovisionar Azure Cosmos DB granularidade Olá segundo (RU/s), obtenha garantia Olá que o pedido for bem sucedida, a latência baixa se o débito não excedeu a capacidade de Olá aprovisionada dentro desse segundo.</span><span class="sxs-lookup"><span data-stu-id="f3525-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="f3525-119">Com RU/m, granularidade Olá está minuto Olá com a garantia de Olá que o pedido seja bem-sucedido dentro desse minuto.</span><span class="sxs-lookup"><span data-stu-id="f3525-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="f3525-120">Em comparação com sistemas de toobursting, iremos Certifique-se de que o desempenho Olá obtiver é previsível e pode planear no mesmo.</span><span class="sxs-lookup"><span data-stu-id="f3525-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="f3525-121">forma Olá por minuto aprovisionamento funciona é simple:</span><span class="sxs-lookup"><span data-stu-id="f3525-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="f3525-122">RU/m é faturada de hora a hora e na adição tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="f3525-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="f3525-123">Para obter mais detalhes, aceda a base de dados do Azure Cosmos [página de preços](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="f3525-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="f3525-124">RU/m pode ser ativado ao nível da coleção.</span><span class="sxs-lookup"><span data-stu-id="f3525-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="f3525-125">Que pode ser feito através de Olá SDKs (Node.js, Java ou .net) ou através do portal Olá (também incluir cargas de trabalho do MongoDB API)</span><span class="sxs-lookup"><span data-stu-id="f3525-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="f3525-126">Quando RU/m estiver ativada, para cada 100 RU/s aprovisionada, também obter 1.000 RU/m aprovisionado (rácio Olá é 10 x)</span><span class="sxs-lookup"><span data-stu-id="f3525-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="f3525-127">No segundo indicado, uma unidade de pedido consome o aprovisionamento de RU/m apenas se excedeu a por segundo aprovisionamento dentro desse segundo</span><span class="sxs-lookup"><span data-stu-id="f3525-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="f3525-128">Uma vez Olá terminar o período de 60-segundo (UTC), é refilled Olá por minuto de aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="f3525-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="f3525-129">RU/m pode ser ativada apenas para coleções com um máximo de aprovisionamento de 5000 RU/s por partição.</span><span class="sxs-lookup"><span data-stu-id="f3525-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="f3525-130">Se aumentar as suas necessidades de débito e ter um nível elevado de aprovisionamento por partição, irá receber uma mensagem de aviso</span><span class="sxs-lookup"><span data-stu-id="f3525-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="f3525-131">Abaixo está um exemplo concreto, em que um cliente pode aprovisionar 10kRU/s com 100kRU/m, guardar 73% custo em relação a aprovisionamento para o horário de pico (na 50kRU/seg) através de um período de 90 segundo numa coleção que tenha 10 000 RU/s e 100 000 de RU/s aprovisionada:</span><span class="sxs-lookup"><span data-stu-id="f3525-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="f3525-132">segundo 1ª: atribuição de RU/m Olá está definida em 100 000</span><span class="sxs-lookup"><span data-stu-id="f3525-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="f3525-133">segundo 3rd: durante esse Olá segundo consumo de unidade de pedido era 11,010 RUs, 1,010 RUs acima Olá RU/s de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="f3525-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="f3525-134">Por conseguinte, 1,010 RUs são deducted do orçamento de RU/m Olá.</span><span class="sxs-lookup"><span data-stu-id="f3525-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="f3525-135">98,990 RUs estão disponíveis para Olá seguintes segundos 57 na atribuição de RU/m Olá</span><span class="sxs-lookup"><span data-stu-id="f3525-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="f3525-136">segundo 29th: durante esse segundo, Ocorreu um grande pico de pedidos (> x 4 ou superior aprovisionamento por segundo) e o consumo de Olá de unidade de pedido foi 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="f3525-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="f3525-137">36,920 RUs são deducted do orçamento RU/m Olá removida da 92,323 RUs (28th segundo) too55, 403 RUs (29th segundo)</span><span class="sxs-lookup"><span data-stu-id="f3525-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="f3525-138">segundo 61st: RU/m orçamento está definido novamente too100, 000 RUs.</span><span class="sxs-lookup"><span data-stu-id="f3525-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Gráfico que mostra o consumo de Olá e aprovisionamento de base de dados do Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="f3525-140">Especificar a capacidade de unidade de pedido com RU/m</span><span class="sxs-lookup"><span data-stu-id="f3525-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="f3525-141">Ao criar uma coleção de BD do Cosmos do Azure, especifique o número de Olá de unidades de pedido por segundo (RU por segundo) que pretende reservado para a coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="f3525-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="f3525-142">Também pode decidir se pretende tooadd RU por minuto.</span><span class="sxs-lookup"><span data-stu-id="f3525-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="f3525-143">Isto pode ser feito Olá Portal ou Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="f3525-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="f3525-144">Através do Portal de Olá</span><span class="sxs-lookup"><span data-stu-id="f3525-144">Through hello Portal</span></span>

<span data-ttu-id="f3525-145">Ativar ou desativar RU por minuto simplesmente necessita de um clique quando o aprovisionamento de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="f3525-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Captura de ecrã com como tooset RU/m no Olá portal do Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="f3525-147">Através de Olá SDK</span><span class="sxs-lookup"><span data-stu-id="f3525-147">Through hello SDK</span></span>
<span data-ttu-id="f3525-148">Em primeiro lugar, isto é importante toonote que RU/m só está disponível para Olá SDKs os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f3525-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="f3525-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="f3525-149">.Net 1.14.0</span></span>
* <span data-ttu-id="f3525-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="f3525-150">Java 1.11.0</span></span>
* <span data-ttu-id="f3525-151">NODE.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="f3525-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="f3525-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="f3525-152">Python 2.2.0</span></span>

<span data-ttu-id="f3525-153">Eis um fragmento de código para criar uma coleção com 3,000 unidades de pedido por unidades de pedido segundo e 30 000 por minuto utilizando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="f3525-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

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

<span data-ttu-id="f3525-154">Eis um fragmento de código para alterar o débito de Olá de uma coleção too5, 000 unidades de pedido por segundo sem aprovisionamento RU por minuto utilizando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="f3525-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

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

## <a name="good-fit-scenarios"></a><span data-ttu-id="f3525-155">Boa caber cenários</span><span class="sxs-lookup"><span data-stu-id="f3525-155">Good fit scenarios</span></span>

<span data-ttu-id="f3525-156">Nesta secção, iremos fornecer uma descrição geral dos cenários que são uma boa opção para ativar as unidades de pedido por minuto.</span><span class="sxs-lookup"><span data-stu-id="f3525-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="f3525-157">**Ambiente de desenvolvimento/teste:** boa opção.</span><span class="sxs-lookup"><span data-stu-id="f3525-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="f3525-158">Durante a fase de desenvolvimento de Olá, se estiver a testar a aplicação com diferentes cargas de trabalho, RU/m pode fornecer flexibilidade Olá nesta fase.</span><span class="sxs-lookup"><span data-stu-id="f3525-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="f3525-159">Ao hello [emulador](local-emulator.md) é tootest uma ótima ferramenta gratuita do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3525-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="f3525-160">No entanto se quiser toostart num ambiente de nuvem, terá uma enorme flexibilidade com RU/m para as suas necessidades de desempenho adhoc.</span><span class="sxs-lookup"><span data-stu-id="f3525-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="f3525-161">Será demora mais tempo a desenvolver, menos worrying sobre as necessidades de desempenho em primeiro lugar.</span><span class="sxs-lookup"><span data-stu-id="f3525-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="f3525-162">É recomendável a partir de aprovisionamento Olá mínimo RU/s e ative RU/m.</span><span class="sxs-lookup"><span data-stu-id="f3525-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="f3525-163">**Tem de granularidade imprevisível, spiky, minuto:** boa caber – reduções: 25 75%.</span><span class="sxs-lookup"><span data-stu-id="f3525-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="f3525-164">Podemos ter visto grande melhoramento de RU/m e a maioria dos cenários de produção são para esse grupo.</span><span class="sxs-lookup"><span data-stu-id="f3525-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="f3525-165">Se tiver uma carga de trabalho de IoT que tenha o pico de pedidos algumas vezes num minuto, se tiver as consultas em execução quando o sistema faz mass inserir Olá mesmo tempo, precisa de capacidade extra para handeling spiky precisa.</span><span class="sxs-lookup"><span data-stu-id="f3525-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="f3525-166">Recomendamos a otimizar as suas necessidades de recursos aplicando a nossa abordagem de passo abaixo.</span><span class="sxs-lookup"><span data-stu-id="f3525-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Gráfico que mostra o consumo de pedido na granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="f3525-168">*Figura - benchmark de consumo do RU*</span><span class="sxs-lookup"><span data-stu-id="f3525-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="f3525-169">**Tranquilidade:** boa caber – reduções: 10-20%.</span><span class="sxs-lookup"><span data-stu-id="f3525-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="f3525-170">Por vezes, pretende apenas tranquilidade toohave e não se preocupe sobre potenciais picos e limitação.</span><span class="sxs-lookup"><span data-stu-id="f3525-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="f3525-171">Esta funcionalidade é o direito de Olá uma por si.</span><span class="sxs-lookup"><span data-stu-id="f3525-171">This feature is hello right one for you.</span></span> <span data-ttu-id="f3525-172">Nesse caso, recomendamos que ative a RU/m e ligeiramente inferior a por segundo de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="f3525-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="f3525-173">Neste caso é diferente do Olá acima, que não irá tentar toooptimize forma agressiva o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="f3525-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="f3525-174">Esta é a mais de uma mente "Limitação de Zero" estão em.</span><span class="sxs-lookup"><span data-stu-id="f3525-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="f3525-175">Operações críticas com necessidades adhoc:, por vezes, recomendamos que tooonly permitem operações críticas acesso RU/m budget para atribuição de Olá não obter consumir pelo ad hoc ou menos importantes operações.</span><span class="sxs-lookup"><span data-stu-id="f3525-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="f3525-176">Que pode ser facilmente definidas na secção de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="f3525-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="f3525-177">Utilizar Olá métricas portal toooptimize custo e desempenho</span><span class="sxs-lookup"><span data-stu-id="f3525-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="f3525-178">**Próximas semanas Olá, iremos irá desenvolver mais conteúdo Olá à volta de monitorização RUs consumo minuto toooptimize que tem do débito.**</span><span class="sxs-lookup"><span data-stu-id="f3525-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="f3525-179">Através de métricas de portal Olá, pode ver a quantidade de segundos de RU regulares consumir versus RU minutos.</span><span class="sxs-lookup"><span data-stu-id="f3525-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="f3525-180">Estas métricas de monitorização deve ajudar a otimizar o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="f3525-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="f3525-181">Recomendamos uma abordagem de passo a passo sobre como toouse RU/m tooyour partido.</span><span class="sxs-lookup"><span data-stu-id="f3525-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="f3525-182">Para cada passo, deve ter uma descrição geral do consumo de Olá RU que representa um ciclo completo da sua carga de trabalho (poderia ser horas, dias, ou até mesmo semanas) e obter conhecimentos aprofundados na utilização de Olá do que for aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="f3525-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="f3525-183">princípio Olá atrás esta abordagem é toomake o aprovisionamento de débito como fechar como tooa possíveis aprovisionamento ponto que corresponda aos critérios de desempenho abaixo.</span><span class="sxs-lookup"><span data-stu-id="f3525-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Gráfico que mostra o consumo de pedido na granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="f3525-185">toounderstand Olá ideal aprovisionamento ponto para a carga de trabalho, terá de toounderstand:</span><span class="sxs-lookup"><span data-stu-id="f3525-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="f3525-186">Padrões de consumo: nenhum, os picos de constante ou pouco frequentes?</span><span class="sxs-lookup"><span data-stu-id="f3525-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="f3525-187">Breve (média de x 2), médio ou grande (> 10 x média) picos?</span><span class="sxs-lookup"><span data-stu-id="f3525-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="f3525-188">Percentagem de pedidos otimizados: fazer sentir-se confortáveis ao se tiver um bit da limitação?</span><span class="sxs-lookup"><span data-stu-id="f3525-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="f3525-189">Se assim for, pelo que?</span><span class="sxs-lookup"><span data-stu-id="f3525-189">If so, by how much?</span></span> 

<span data-ttu-id="f3525-190">Depois de identificar quais são os objetivos, será capaz de tooget próximo toohello ideal de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="f3525-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="f3525-191">tooassist, queremos tooprovide uma orientação geral sobre como toooptimize o aprovisionamento com base no consumo RU/m.</span><span class="sxs-lookup"><span data-stu-id="f3525-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="f3525-192">Esta orientação não se aplica tooall tipo de cargas de trabalho, mas é com base em dados de conhecimento do Olá pré-visualização privada.</span><span class="sxs-lookup"><span data-stu-id="f3525-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="f3525-193">Vamos poderá alterar essas linhas de base como podemos Saiba mais:</span><span class="sxs-lookup"><span data-stu-id="f3525-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="f3525-194">RU/m % utilização</span><span class="sxs-lookup"><span data-stu-id="f3525-194">RU/m % utilization</span></span>|<span data-ttu-id="f3525-195">Nível de utilização de RU/m</span><span class="sxs-lookup"><span data-stu-id="f3525-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="f3525-196">Ações recomendadas para aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="f3525-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="f3525-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="f3525-197">0-1%</span></span>|<span data-ttu-id="f3525-198">Em utilização</span><span class="sxs-lookup"><span data-stu-id="f3525-198">Under utilization</span></span>|<span data-ttu-id="f3525-199">Reduzir tooconsume RU/s mais RU/m</span><span class="sxs-lookup"><span data-stu-id="f3525-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="f3525-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="f3525-200">1-10%</span></span>|<span data-ttu-id="f3525-201">Utilização de bom estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="f3525-201">Healthy use</span></span>|<span data-ttu-id="f3525-202">Manter hello mesmo aprovisionamento nível</span><span class="sxs-lookup"><span data-stu-id="f3525-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="f3525-203">Superior a 10%</span><span class="sxs-lookup"><span data-stu-id="f3525-203">Above 10%</span></span>|<span data-ttu-id="f3525-204">Ao longo de utilização</span><span class="sxs-lookup"><span data-stu-id="f3525-204">Over utilization</span></span>|<span data-ttu-id="f3525-205">Aumentar RU/s toorely menos RU/m</span><span class="sxs-lookup"><span data-stu-id="f3525-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="f3525-206">Selecione as operações de podem consumir orçamento de RU/m Olá</span><span class="sxs-lookup"><span data-stu-id="f3525-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="f3525-207">Ao nível do pedido, pode também Ativar/desativar pedido do RU/m orçamento tooserve Olá independentemente do tipo de operação.</span><span class="sxs-lookup"><span data-stu-id="f3525-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="f3525-208">Se regular orçamento RUs/seg aprovisionado é consumido e pedido Olá não pode consumir orçamento de RU/m Olá, este pedido será limitado.</span><span class="sxs-lookup"><span data-stu-id="f3525-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="f3525-209">Por predefinição, quaisquer pedidos servidos pelo RU/m orçamento se orçamento de débito RU/m está ativado.</span><span class="sxs-lookup"><span data-stu-id="f3525-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="f3525-210">Eis um fragmento de código para desativar o orçamento RU/m Olá DocumentDB API a utilizar para as operações CRUD e consulta.</span><span class="sxs-lookup"><span data-stu-id="f3525-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f3525-211">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f3525-211">Next steps</span></span>

<span data-ttu-id="f3525-212">Neste artigo, vamos já descrito funciona como criação de partições do BD Azure Cosmos, como pode criar coleções particionadas e como pode escolher uma chave de partição para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="f3525-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="f3525-213">Efetue o dimensionamento e desempenho de teste com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3525-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="f3525-214">Consulte [desempenho e dimensionamento de teste com base de dados do Azure Cosmos](performance-testing.md) para um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f3525-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="f3525-215">Introdução à programação com Olá [SDKs](documentdb-sdk-dotnet.md) ou Olá [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f3525-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="f3525-216">Saiba mais sobre [débito aprovisionado](request-units.md) do BD Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="f3525-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

