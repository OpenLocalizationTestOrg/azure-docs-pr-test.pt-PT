---
title: aaaPartitioning e dimensionamento horizontal do BD Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre como criação de partições funciona do BD Azure Cosmos, como a criação de partições de tooconfigure e chaves de partição e como toopick Olá direito de partição chave para a sua aplicação."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Como toopartition e escala do BD Azure Cosmos

[Base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) é um toohelp de serviço de base de dados distribuída, com vários modelo global que poderá alcançar previsível e rápido de desempenho e dimensionamento totalmente integrada, juntamente com a aplicação à medida que o que aumenta. Este artigo fornece uma descrição geral de como criação de partições funciona para todos os dados de Olá modelos do BD Azure Cosmos e descreve como pode configurar o dimensionamento do Azure Cosmos DB contentores tooeffectively as suas aplicações.

Divisão em partições e chaves de partição são também abordadas neste Azure vídeo com autoria de Scott Hanselman e o Azure Cosmos BD Principal de engenharia Manager, Shireesh Thota sexta-feira.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>A criação de partições no Azure Cosmos DB
BD do Cosmos do Azure, pode armazenar e consultar dados sem esquema com tempos de resposta de ordem de milissegundo em qualquer escala. BD do cosmos fornece contentores para armazenar dados denominado **nas coleções (documento), gráficos ou tabelas**. Contentores são recursos lógicos e podem abranger uma ou mais partições físicas ou servidores. número de Olá de partições é determinado pelo DB Cosmos com base no tamanho de armazenamento Olá e débito aprovisionado de Olá do contentor de Olá. Cada partição na base de dados do Cosmos tem uma quantidade fixa de armazenamento SSD de segurança associada e é replicada para elevada disponibilidade. Gestão de partição é totalmente gerida por base de dados do Azure Cosmos e não tem o código complexo toowrite ou gerir as partições. Contentores de BD do cosmos são ilimitados em termos de armazenamento e débito. 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

Criação de partições é a aplicação de tooyour transparente. BD do cosmos suporta rápidas leituras e escritas, consultas, lógica transacional, níveis de consistência e controlo de acesso detalhado através do recurso de contentor único tooa de métodos/APIs. serviço de Olá processa dados de distribuição em partições e encaminhamento consulta pedidos toohello direita partição. 

Como funciona a criação de partições? Cada item tem de ter uma chave de partição e uma chave de linha, identificar exclusivamente. A chave de partição atua como uma partição lógica para os seus dados e fornece Cosmos DB com um limite natural para distribuir dados em partições. No brief, eis como criação de partições funciona do BD Azure Cosmos:

* Aprovisionar um contentor de BD do Cosmos com `T` débito de pedidos/s
* Em segundo plano do Olá, as partições do Cosmos DB Aprovisiona necessário tooserve `T` pedidos/s. Se `T` é superior ao débito máximo de Olá por partição `t`, em seguida, a base de dados do Cosmos Aprovisiona `N`  =  `T/t` partições
* BD do cosmos atribui Olá chave espaço da partição hashes chaves uniformemente em Olá `N` partições. Por isso, cada partição (partição física) aloja valores de chave de partição de 1-N (partições lógicas)
* Quando uma partição física `p` atingir o limite de armazenamento, base de dados do Cosmos perfeitamente divide `p` em duas partições novo `p1` e `p2` e distribui valores correspondente tooroughly meio Olá chaves tooeach de Olá partições. Esta operação de divisão é aplicação tooyour invisível.
* Da mesma forma, quando aprovisionar débito superior `t*N` débito, base de dados do Cosmos divide uma ou mais das suas partições toosupport Olá um maior débito

semântica de Olá para as chaves de partição é semântica de Olá toomatch ligeiramente diferentes de cada API, conforme apresentado no Olá a tabela seguinte:

| API | Chave de partição | Chave de linha |
| --- | --- | --- |
| DocumentDB | caminho da chave de partição personalizado | fixo`id` | 
| MongoDB | chave de partição horizontal personalizado  | fixo`_id` | 
| Graph | propriedade de chave de partição personalizado | fixo`id` | 
| Tabela | fixo`PartitionKey` | fixo`RowKey` | 

BD do cosmos utiliza a criação de partições com base em hash. Quando escreve um item, Cosmos DB codifica o valor da chave de partição Olá e utilize Olá codificadas toodetermine de resultado que partição toostore Olá item. Olá, arquivos de cosmos DB todos os itens com Olá a mesma chave de partição na mesma partição física. Escolha de Olá de chave de partição Olá é uma decisão importante que têm toomake no momento da concepção. Tem de escolher um nome de propriedade que tenha uma vasta gama de valores e tem o mesmo padrões de acesso.

> [!NOTE]
> É uma melhor toohave de prática uma chave de partição com vários valores distintos (1000s 100s no mínimo).
>

Contentores do Cosmos BD do Azure podem ser criados como "fixed" ou "ilimitados." Os contentores de tamanho fixo têm um limite máximo de 10 GB e 10 000 de RU/s débito. Algumas APIs permitem toobe de chave de partição de Olá omitidas para contentores de tamanho fixo. toocreate um contentor como ilimitado, tem de especificar um débito mínimo de 2500 RU/s.

## <a name="partitioning-and-provisioned-throughput"></a>Débito aprovisionado e criação de partições
BD do cosmos foi concebido para um desempenho previsível. Quando cria um contentor, reservar débito em termos de  **[unidades de pedido](request-units.md) (RU) por segundo com um potencial suplemento para RU por minuto**. Cada pedido está atribuído um custo de unidade de pedido é proporcional toohello quantidade de recursos do sistema, como CPU, memória e consumidas pela operação de Olá e/s. Uma leitura de um documento de 1 KB com consistência de sessão consome uma unidade de pedido. Uma leitura é 1 RU independentemente do número de Olá de itens armazenados ou Olá número de pedidos simultâneos em execução num Olá mesmo tempo. Itens de maior necessitam de unidades de pedido superiores, dependendo do tamanho de Olá. Se souber o tamanho de Olá das entidades e Olá número de leituras toosupport é necessário para a sua aplicação, pode aprovisionar quantidade exata de Olá de débito necessário para a aplicação do leia necessidades. 

> [!NOTE]
> tooachieve Olá completa débito contentor Olá, tem de escolher uma chave de partição permite-lhe tooevenly distribuir pedidos entre alguns valores de chave de partição distintos.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Trabalhar com Olá APIs de BD do Cosmos do Azure
Pode utilizar Olá portal do Azure ou contentores de toocreate da CLI do Azure e dimensioná-los em qualquer altura. Esta secção mostra como contentores toocreate e especifique Olá débito e partição de definição da chave em cada um dos Olá suportado APIs.

### <a name="documentdb-api"></a>API do DocumentDB
Olá seguinte exemplo mostra como toocreate utilizando um contentor (coleção) Olá API do DocumentDB. Pode encontrar mais detalhes em [a criação de partições, com o DocumentDB API](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Pode ler um item (documento) utilizando Olá `GET` método no Olá REST API ou utilizando `ReadDocumentAsync` dos Olá SDKs.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>API do MongoDB
Com Olá MongoDB API, pode criar uma coleção em partição horizontal através da sua ferramenta favorita, controlador ou SDK. Neste exemplo, utilizamos Olá Shell do Mongo para a criação de coleção de Olá.

Na Shell do Mongo Olá:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Resultados:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>API de Tabela

Com Olá API de tabela, especificar débito Olá para tabelas na configuração de appSettings Olá para a sua aplicação:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Em seguida, crie uma tabela utilizando Olá Table storage do Azure SDK. chave de partição Olá implicitamente é criado como Olá `PartitionKey` valor. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Pode obter uma entidade única com Olá seguinte fragmento:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Consulte [desenvolver com Olá API de tabela](tutorial-develop-table-dotnet.md) para obter mais detalhes.

### <a name="graph-api"></a>Graph API

Com Olá Graph API, tem de utilizar Olá portal do Azure ou contentores de toocreate CLI. Em alternativa, uma vez que a BD do Azure Cosmos múltiplos modelo, pode utilizar um dos Olá toocreate outros modelos e dimensionar o contentor do gráfico.

Pode ler qualquer vértice ou limite a utilizar a chave de partição Olá e id na Gremlin. Por exemplo, para um gráfico com a região ("EUA") como chave de partição Olá e "Seattle" como chave de linha de Olá, pode encontrar um vértice utilizando Olá sintaxe:

```
g.V(['USA', 'Seattle'])
```

Mesmo com margens, pode referenciar um limite de utilização de chave de partição Olá e chave de linha.

```
g.E(['USA', 'I5'])
```

Consulte [suporte Gremlin para Cosmos DB](gremlin-support.md) para obter mais detalhes.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Estruturar para criação de partições
tooscale eficazmente com a base de dados do Azure Cosmos, terá de toopick uma chave de partição ao criar o contentor. Existem duas considerações-chave para escolher uma chave de partição:

* **Limite da consulta e transações**: à sua escolha de chave de partição deve balancear Olá necessidade tooenable Olá utilização transações contra Olá requisito toodistribute as entidades de várias tooensure de chaves de partição uma solução dimensionável. Em uma Alpine, pode configurar Olá mesma chave de partição para todos os seus itens, mas isto pode limitar a escalabilidade de Olá da sua solução. Em Olá outro Alpine, pode atribuir uma chave de partição exclusiva para cada item, o qual será altamente dimensionável, mas seria o impede de utilizar transações entre documentos através de acionadores e procedimentos armazenados. Uma chave de partição ideal é que lhe permite consultas eficiente toouse e que tem cardinalidade suficiente tooensure a sua solução é dimensionável. 
* **Nenhum congestionamentos de desempenho e armazenamento**: é importante toopick uma propriedade que permite que escreve toobe distribuído por vários valores distintos. Pedidos toohello mesma chave de partição não pode exceder o débito de Olá de uma única partição e são limitadas. Por isso, é importante toopick uma chave de partição não resulta numa "frequente oportunidades" na sua aplicação. Dado que todos os dados de Olá para uma chave de partição única têm de ser armazenada dentro de uma partição, recomenda-se também tooavoid as chaves de partição que têm elevados volumes de dados para Olá mesmo valor. 

Vamos ver alguns cenários no mundo real e chaves de partição para cada:
* Se estiver a implementar um back-end de perfil do utilizador, o ID de utilizador Olá é uma boa opção para a chave de partição.
* Se estiver a armazenar dados de IoT por exemplo, o estado do dispositivo, um ID de dispositivo é uma boa opção para a chave de partição.
* Se estiver a utilizar a base de dados do Azure Cosmos para registo de dados de séries de tempo, em seguida, Olá hostname ou ID de processo é uma boa opção para a chave de partição.
* Se tiver uma arquitetura de multi-inquilino, o ID do inquilino Olá é uma boa opção para a chave de partição.

Em alguns casos, como o IoT de utilização e perfis de utilizador, a chave de partição Olá poderá ser Olá mesmo como o seu id (chave do documento). Em outras pessoas como dados de séries de tempo de Olá, poderá ter uma chave de partição que é diferente do id de Olá.

### <a name="partitioning-and-loggingtime-series-data"></a>Data de criação de partições e de registo /-série de tempo da
Um dos Olá casos de utilização comuns de BD do Cosmos destina-se a telemetria e de registo. É importante toopick uma chave de partição, uma vez que poderá ser necessário tooread/escrita vasta volumes de dados. Escolha Olá depende da sua leitura e escrita taxas e tipos de consultas que esperar toorun. Eis algumas sugestões sobre como toochoose uma chave de partição.

* Se for o caso de utilização envolve uma taxa pequena do grava acumulado durante um longo período de tempo e necessidade tooquery por intervalos de carimbos e outros filtros, em seguida, utilizar um rollup de Olá timestamp, por exemplo, date como uma chave de partição é uma boa abordagem. Isto permite-lhe tooquery através de todos os dados de Olá de uma data a partir de uma única partição. 
* Se a carga de trabalho é escrita pesado, que é mais comum, deve utilizar uma chave de partição não é baseada em timestamp, para que Cosmos DB possam distribuir escritas uniformemente entre várias partições. Um nome de anfitrião, o ID do processo, o ID de atividade ou outra propriedade com cardinalidade elevada Eis uma boa opção. 
* Uma abordagem terceira é uma versão híbrida um onde tiver vários contentores, um de cada mês/dia e a chave de partição Olá é uma propriedade granular como o nome do anfitrião. Isto tem o benefício de Olá que pode definir débito diferentes com base na janela de tempo de Olá, por exemplo, contentor Olá para Olá mês atual está aprovisionado com um maior débito porque funciona leituras e escritas, enquanto que o menor de meses anteriores com débito desde servem apenas operações de leitura.

### <a name="partitioning-and-multi-tenancy"></a>Criação de partições e de vários inquilinos
Se estiver a implementar uma aplicação de multi-inquilino através da BD do Cosmos, existem dois padrões populares – chave de uma partição por inquilino e um contentor por inquilino. Seguem-se os profissionais de Olá e contras para cada:

* Uma chave de partição por inquilino: neste modelo, os inquilinos estão colocalizados dentro de um único contentor. Mas, consultas e inserções de itens dentro de um único inquilino podem executar uma única partição. Também pode implementar a lógica transacional em todos os itens dentro de um inquilino. Uma vez que vários inquilinos partilharem um contentor, pode guardar os custos de armazenamento e débito por agrupamento de recursos para os inquilinos dentro de um único contentor, em vez de aprovisionamento headroom adicional para cada inquilino. desvantagem Olá é que não dispõe de isolamento de desempenho por inquilino. Os aumentos de desempenho/débito aplicam toohello contentor inteiro vs direcionados aumenta para os inquilinos.
* Um contentor por inquilino: cada inquilino tem a suas próprias contentor. Neste modelo, pode reservar desempenho por inquilino. Com o BD do Cosmos novo aprovisionamento modelo de preços, este modelo é mais económico para aplicações de multi-inquilinos com alguns inquilinos.

Também pode utilizar uma abordagem de combinação/camadas de mensagens em fila que collocates inquilinos pequenos e migra maior contentor própria de tootheir inquilinos.

## <a name="next-steps"></a>Passos seguintes
Neste artigo, fornecemos-lhe uma descrição geral para uma descrição geral dos conceitos e procedimentos recomendados para a criação de partições com qualquer API de BD do Cosmos do Azure. 

* Saiba mais sobre [débito aprovisionado do BD Azure Cosmos](request-units.md)
* Saiba mais sobre [distribuição global do BD Azure Cosmos](distribute-data-globally.md)



