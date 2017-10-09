---
title: aaaAzure Cosmos DB dimensionamento e o teste de desempenho | Microsoft Docs
description: Saiba como dimensionar tooperform e teste de desempenho com base de dados do Azure Cosmos
keywords: Teste de desempenho
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Desempenho e dimensionamento de teste com base de dados do Azure Cosmos
Desempenho e dimensionamento de teste é um passo chave no desenvolvimento de aplicações. Para muitas aplicações, o escalão de base de dados de Olá tem um impacto significativo Olá escalabilidade e desempenho global e está, por conseguinte, um componente crítico de desempenho de teste. [BD do Azure do Cosmos](https://azure.microsoft.com/services/cosmos-db/) é específico para a escala elástica e um desempenho previsível e, por conseguinte, uma excelente opção para aplicações que necessitam de uma camada de base de dados de elevado desempenho. 

Este artigo é uma referência para programadores implementar conjuntos de teste de desempenho para as respetivas cargas de trabalho de BD do Cosmos ou avaliar Cosmos DB para cenários de aplicações de elevado desempenho. Concentra-se principalmente nas teste isolado de desempenho da base de dados de Olá, mas também inclui as melhores práticas para aplicações de produção.

Depois de ler este artigo, irá ser Olá tooanswer capaz de seguintes perguntas:   

* Onde posso encontrar um exemplo de aplicação de cliente .NET para o teste de desempenho da base de dados do Cosmos? 
* Como alcançar níveis de débito elevado com Cosmos DB a minha aplicação de cliente?

tooget iniciado com o código,. Transfira o projeto de Olá de [amostra de testes de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> objetivo Olá esta aplicação é toodemonstrate melhores práticas para extrair um melhor desempenho fora do Cosmos DB com um pequeno número de computadores cliente. Este não foi efetuada uma capacidade de pico de Olá toodemonstrate do serviço de Olá, o que pode dimensionar ilimitada.
> 
> 

Se estiver à procura de opções de configuração do lado do cliente tooimprove desempenho de base de dados do Cosmos, consulte o artigo [sugestões de desempenho de base de dados do Azure Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Executar a aplicação de testes de desempenho de Olá
Olá tooget de forma mais rápida iniciado é toocompile e exemplos de .NET de execução Olá abaixo, conforme descrito nos passos Olá abaixo. Também pode rever o código de origem Olá e implementar aplicações de cliente própria de tooyour de configurações semelhantes.

**Passo 1:** projeto Olá de transferência do [amostra de testes de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), ou o repositório do GitHub bifurcação Olá.

**Passo 2:** modificar definições de Olá EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (opcional) no App. config.

> [!NOTE]
> Antes do aprovisionamento de coleções com débito elevado, consulte toohello [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/) os custos de Olá tooestimate por coleção. BD do Azure do Cosmos faturas armazenamento e débito independentemente numa base horária, pelo que pode reduzir os custos eliminando ou reduzir o débito de Olá das suas coleções de base de dados do Azure Cosmos depois de testar.
> 
> 

**Passo 3:** compilar e executar a aplicação de consola de Olá Olá linha de comandos. Deverá ver um resultado semelhante Olá seguinte:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Passo 4 (se necessário):** Olá débito comunicado (RU/s) da ferramenta de Olá deve ser Olá igual ou superior ao débito aprovisionado de Olá da coleção de Olá. Caso contrário, crescente Olá DegreeOfParallelism pequenos incrementos pode ajudá-lo a atingir o limite de Olá. Se plateaus débito Olá da sua aplicação de cliente, iniciar múltiplas instâncias da aplicação Olá no mesmo Olá ou diferentes máquinas irão ajudar a alcançar o limite de Olá aprovisionado em Olá instâncias diferentes. Se precisar de ajuda com este passo, escreva uma mensagem de e-mail tooaskcosmosdb@microsoft.com ou ficheiros de um pedido de suporte de Olá [Portal do Azure](https://portal.azure.com).

Assim que tiver de executar a aplicação Olá, pode experimentar diferentes [indexação políticas](indexing-policies.md) e [níveis de consistência](consistency-levels.md) toounderstand o impacto na débito e latência. Também pode rever o código de origem Olá e implementar aplicações de produção ou conjuntos de teste própria de tooyour configurações semelhantes.

## <a name="next-steps"></a>Passos seguintes
Neste artigo, vamos consultou como pode efetuar o desempenho e dimensionamento de teste com base de dados do Cosmos através de uma aplicação de consola .NET. Consulte toohello ligações abaixo para obter informações adicionais sobre como trabalhar com a base de dados do Azure Cosmos.

* [Exemplo de testes de desempenho de base de dados do Cosmos do Azure](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Tooimprove de opções de configuração do cliente desempenho de base de dados do Azure Cosmos](performance-tips.md)
* [Criação de partições do lado do servidor na base de dados do Azure Cosmos](partition-data.md)


