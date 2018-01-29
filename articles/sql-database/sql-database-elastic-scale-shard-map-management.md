---
title: Aumentar horizontalmente uma base de dados SQL do Azure | Microsoft Docs
description: "Como utilizar o ShardMapManager, a biblioteca de clientes de base de dados elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: ddove
ms.openlocfilehash: fe4c8b7b2a9d199c85faf11fcd35382d586fc009
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/08/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a>Aumentar horizontalmente bases de dados com o Gestor de mapa de partições horizontais
Para ampliar facilmente as bases de dados SQL Azure, utilize um Gestor de mapa de partições horizontais. O Gestor de mapa de partições horizontais é uma base de dados especial que mantém as informações de mapeamento global sobre todas as partições horizontais (bases de dados) de um conjunto de partições horizontais. Os metadados permite que uma aplicação ligar à base de dados correto com base no valor da **chave de fragmentação**. Além disso, todas as partições horizontais no conjunto contém maps que monitorizam os dados de partições horizontais local (conhecido como **shardlets**). 

![Gestão de mapa de partições horizontais](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Compreender como estes mapeamentos são construídos é essencial para gestão de mapa de partições horizontais. Isto é feito utilizando a classe de ShardMapManager ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)), foi encontrada no [biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md) para gerir os mapas de partições horizontais.  

## <a name="shard-maps-and-shard-mappings"></a>Mapas de partições horizontais e mapeamentos de partições horizontais
Para cada partição horizontal, tem de selecionar o tipo de mapa de partições horizontais criar. A opção depende a arquitetura de base de dados: 

1. Inquilino único por base de dados  
2. Vários inquilinos por base de dados (dois tipos):
   1. Mapeamento de lista
   2. Mapeamento de intervalo

Para um modelo de inquilino único, crie um **mapeamento de lista** mapa de partições horizontais. O modelo de inquilino único atribui uma base de dados por inquilino. Este é um modelo eficiente para programadores de SaaS que simplifica a gestão.

![Mapeamento de lista][1]

O modelo de multi-inquilino atribui vários inquilinos para uma base de dados (e pode distribuir grupos de inquilinos através de várias bases de dados). Utilize este modelo quando espera cada inquilino ter necessidades de dados pequeno. Neste modelo, atribuir um intervalo de inquilinos para uma base de dados utilizando **mapeamento de intervalo**. 

![Mapeamento de intervalo][2]

Ou pode implementar um modelo de base de dados do multi-inquilino utilizando um *mapeamento de lista* atribuir vários inquilinos para uma base de dados. Por exemplo, DB1 é utilizado para armazenar informações sobre o inquilino ID 1 e 5 e DB2 armazena os dados para o inquilino 7 e de inquilino 10. 

![Vários inquilinos na base de dados único][3] 

### <a name="supported-types-for-sharding-keys"></a>Tipos suportados para as chaves de fragmentação
Dimensionamento elástico suporta os seguintes tipos como chaves de fragmentação:

| .NET | Java |
| --- | --- |
| número inteiro |número inteiro |
| longa |longa |
| GUID |UUID |
| Byte]  |Byte] |
| DateTime | carimbo de data/hora |
| TimeSpan | Duração|
| Datetimeoffset |offsetdatetime |

### <a name="list-and-range-shard-maps"></a>Lista e o intervalo de mapas de partições horizontais
ID de partição horizontal maps podem ser construídos com **valores de chave de listas de fragmentação individuais**, ou podem ser construídos com **valores de chave de intervalos de fragmentação**. 

### <a name="list-shard-maps"></a>Mapas de partições horizontais de lista
**Shards** conter **shardlets** e o mapeamento do shardlets para shards é mantido por um mapa de partições horizontais. A **mapa de partições horizontais lista** é uma associação entre os valores de chave individuais que identificam o shardlets e as bases de dados que servem de partições horizontais.  **Lista de mapeamentos** são diferentes e explícita chave valores podem ser mapeados para a mesma base de dados. Por exemplo, a chave 1 mapeia para a base de dados A e B. da base de dados de referência de valores de chave 3 e 6

| Chave | Localização de partições horizontais |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Intervalo de partição horizontal maps
Num **mapa de partições horizontais intervalo**, o intervalo de chaves é descrito por um par **[valor baixo, valor elevado)** onde o *valor baixo* é a chave mínimo dentro do intervalo e o *valor elevado* é o primeiro valor superior ao intervalo. 

Por exemplo, **[0, 100)** inclui todos os números inteiros igual ou maior do que 0 e menor que 100. Tenha em atenção que vários intervalos podem apontar para a mesma base de dados e são suportados intervalos não contíguo (por exemplo, [100,200) e [400,600) ambos ponto c de base de dados no exemplo seguinte.)

| Chave | Localização de partições horizontais |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

Cada uma das tabelas mostradas acima é um exemplo concetual de um **ShardMap** objeto. Cada linha é um exemplo de um indivíduo simplificado **PointMapping** (para o mapa de partições horizontais lista) ou **RangeMapping** (para o mapa de partições horizontais de intervalo) objeto.

## <a name="shard-map-manager"></a>Gestor de mapa de partições horizontais
Na biblioteca de cliente, o Gestor de mapa de partições horizontais é uma coleção de mapas de partições horizontais. Os dados geridos por um **ShardMapManager** instância é mantida em três locais: 

1. **Mapa de partições horizontais global (GSM)**: Especifique uma base de dados para servir o repositório para todos os respetivos mapas de partições horizontais e mapeamentos. Tabelas especiais e procedimentos armazenados são criados automaticamente para gerir as informações. Isto é normalmente uma base de dados pequena e ligeiramente acedido e não deve ser utilizado para outras necessidades da aplicação. As tabelas são de um esquema especial com o nome **__ShardManagement**. 
2. **Mapa de partições horizontais local (LSM)**: cada base de dados que especificar para ser um ID de partição horizontal é modificada para conter várias tabelas pequenas e procedimentos armazenados especiais que contenham e gerir informações de mapa de partições horizontais específicas para essa partições horizontais. Esta informação é redundante com as informações do GSM e permite que a aplicação validar a informação de mapa de partições horizontais em cache sem colocar qualquer carga no GSM; a aplicação utiliza o LSM para determinar se um mapeamento em cache ainda é válido. As tabelas correspondente LSM em cada partições horizontais se encontrem no esquema **__ShardManagement**.
3. **Cache da aplicação**: cada instância de aplicação ao aceder a um **ShardMapManager** objeto mantém uma cache na memória local do respetivos mapeamentos. Armazena as informações de encaminhamento que recentemente foram obtidas. 

## <a name="constructing-a-shardmapmanager"></a>Construir uma ShardMapManager
A **ShardMapManager** objecto é construído através de uma fábrica ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory)) padrão. O **ShardMapManagerFactory.GetSqlShardMapManager** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.getsqlshardmapmanager), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager)) método aceita as credenciais (incluindo o nome do servidor e o nome de base de dados que contém o GSM) do formato de um **ConnectionString** e devolve uma instância de um **ShardMapManager**.  

**Tenha em atenção:** o **ShardMapManager** deve ser instanciado apenas uma vez por domínio de aplicação, dentro do código de inicialização de uma aplicação. Criação de instâncias adicionais de ShardMapManager no mesmo domínio de aplicação resulta num aumento de memória e a utilização de CPU da aplicação. A **ShardMapManager** pode conter qualquer número de mapas de partições horizontais. Enquanto um mapa de partições horizontais única pode ser suficiente para muitas aplicações, há horas quando são utilizados os diferentes conjuntos de bases de dados para outro esquema ou para fins de exclusivos; Nesses casos, várias partições horizontais maps poderão ser preferível. 

Neste código, uma aplicação tenta abrir um existente **ShardMapManager** com o TryGetSqlShardMapManager ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.trygetsqlshardmapmanager), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)) método.  Se os objetos que representa um Global **ShardMapManager** (GSM) não ainda existe na base de dados, a biblioteca de cliente cria-los existe utilizando o CreateSqlShardMapManager ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.createsqlshardmapmanager), [.NET ](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager)) método.

```Java
// Try to get a reference to the Shard Map Manager in the shardMapManager database.
// If it doesn't already exist, then create it.
ShardMapManager shardMapManager = null;
boolean shardMapManagerExists = ShardMapManagerFactory.tryGetSqlShardMapManager(shardMapManagerConnectionString,ShardMapManagerLoadPolicy.Lazy, refShardMapManager);
shardMapManager = refShardMapManager.argValue;

if (shardMapManagerExists) {
    ConsoleUtils.writeInfo("Shard Map %s already exists", shardMapManager);
}
else {
    // The Shard Map Manager does not exist, so create it
    shardMapManager = ShardMapManagerFactory.createSqlShardMapManager(shardMapManagerConnectionString);
    ConsoleUtils.writeInfo("Created Shard Map %s", shardMapManager);
}
```

```csharp
// Try to get a reference to the Shard Map Manager via the Shard Map Manager database.  
// If it doesn't already exist, then create it. 
ShardMapManager shardMapManager; 
bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

if (shardMapManagerExists) 
{ 
    Console.WriteLine("Shard Map Manager already exists");
} 
else
{
    // Create the Shard Map Manager. 
    ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
    Console.WriteLine("Created SqlShardMapManager"); 

    shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

// The connectionString contains server name, database name, and admin credentials for privileges on both the GSM and the shards themselves.
} 
```

Para a versão do .NET, pode utilizar o PowerShell para criar um novo Gestor de mapa de partições horizontais. Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Obter um RangeShardMap ou ListShardMap
Depois de criar um ID de partição horizontal manager mapa, pode obter o RangeShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807318.aspx)) ou ListShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807370.aspx)) utilizando o TryGetRangeShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetrangeshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)), o TryGetListShardMap ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetlistshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)), ou o GetShardMap ([ Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.getshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)) método.

```Java
// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
static <T> RangeShardMap<T> createOrGetRangeShardMap(ShardMapManager shardMapManager,
            String shardMapName,
            ShardKeyType keyType) {
    // Try to get a reference to the Shard Map.
    ReferenceObjectHelper<RangeShardMap<T>> refRangeShardMap = new ReferenceObjectHelper<>(null);
    boolean isGetSuccess = shardMapManager.tryGetRangeShardMap(shardMapName, keyType, refRangeShardMap);
    RangeShardMap<T> shardMap = refRangeShardMap.argValue;

    if (isGetSuccess && shardMap != null) {
        ConsoleUtils.writeInfo("Shard Map %1$s already exists", shardMap.getName());
    }
    else {
        // The Shard Map does not exist, so create it
        try {
            shardMap = shardMapManager.createRangeShardMap(shardMapName, keyType);
        }
        catch (Exception e) {
            e.printStackTrace();
        }
        ConsoleUtils.writeInfo("Created Shard Map %1$s", shardMap.getName());
    }

    return shardMap;
}
```

```csharp
// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
{
    // Try to get a reference to the Shard Map.
    RangeShardMap<T> shardMap;
    bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

    if (shardMapExists)
    {
        ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
    }
    else
    {
        // The Shard Map does not exist, so create it
        shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
        ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
    }

    return shardMap;
} 
```

### <a name="shard-map-administration-credentials"></a>Credenciais de administração de mapa de partições horizontais
As aplicações que administram e manipular mapas de partições horizontais são diferentes das que utilizam os maps de partições horizontais para ligações de rota. 

Para administrar o maps de partições horizontais (adicionar ou alterar shards, partições horizontais maps, os mapeamentos de partições horizontais, etc.) tem de instanciar o **ShardMapManager** utilizando **leitura/escritam de credenciais com privilégios em ambas as GSM base de dados e em cada base de dados que funciona como um ID de partição horizontal**. As credenciais têm de permitir para escritas relativamente a tabelas no GSM e LSM como informações de mapa de partições horizontais são introduzidas ou tiver sido alteradas, bem como para a criação de tabelas LSM numa nova shards.  

Consulte [credenciais utilizadas para aceder a biblioteca de clientes de base de dados elástica](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Apenas os metadados afetados
Métodos utilizados para preencher ou alterar o **ShardMapManager** dados não alterar os dados de utilizador armazenados no shards próprios. Por exemplo, os métodos, tais como **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. afetam apenas os metadados de mapa de partições horizontais. Não remova, adicionar ou alterar os dados de utilizador contidos nos shards. Em vez disso, estes métodos são concebidos para serem utilizados em conjunto com as operações separados que executar para criar ou remover bases de dados real, ou se mover linhas de um ID de partição horizontal para outro reequilibrar num ambiente em partição horizontal.  (O **divisão intercalação** ferramenta incluída com ferramentas de base de dados elástica faz com que a utilização destas APIs juntamente com a da orquestração movimento de dados entre shards.) Consulte [dimensionamento utilizando a ferramenta de intercalação de divisão de base de dados elástica](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="data-dependent-routing"></a>Encaminhamento dependente de dados
O Gestor de mapa de partições horizontais é utilizado em aplicações que necessitam de ligações de base de dados para efetuar as operações de dados específicos de aplicação. Essas ligações tem de estar associadas com a base de dados correto. Isto é conhecido como **dados dependentes encaminhamento**. Para estas aplicações, instanciar um objeto de Gestor de mapa de partições horizontais de fábrica utilizando as credenciais que têm acesso só de leitura na base de dados GSM. Pedidos individuais para ligações posteriores fornecem as credenciais necessárias para ligar à base de dados adequada partições horizontais.

Tenha em atenção que estas aplicações (utilizando **ShardMapManager** aberta com as credenciais só de leitura) não é possível efetuar alterações ao maps ou mapeamentos. Para essas necessidades, crie administrativas específicas aplicações ou scripts do PowerShell que fornecem credenciais de privilégio mais elevado, conforme debatido anteriormente. Consulte [credenciais utilizadas para aceder a biblioteca de clientes de base de dados elástica](sql-database-elastic-scale-manage-credentials.md).

Para obter mais informações, consulte [dados dependentes encaminhamento](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Modificar um mapa de partições horizontais
É possível alterar um mapa de partições horizontais formas diferentes. Todos os seguintes métodos de modificar os metadados que descrevem os shards e os respetivos mapeamentos, mas não modificar fisicamente dados dentro de shards nem possam criar ou eliminar as bases de dados reais.  Algumas das operações no mapa de partições horizontais descrito abaixo poderão ter de ser coordenada com ações administrativas que mover fisicamente dados ou que adicionar e remover bases de dados que servem como shards.

Estes métodos funcionam em conjunto como os blocos modulares disponíveis para modificar a distribuição geral dos dados no seu ambiente de base de dados em partição horizontal.  

* Para adicionar ou remover shards: utilizar **CreateShard** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map.createshard), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)) e **DeleteShard** ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map.deleteshard), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)) da Shardmap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)) classe. 
  
    O servidor e base de dados que representa as partições horizontais de destino tem de existir para estas operações executar. Estes métodos não tem qualquer impacto nas bases de dados, apenas nos metadados no mapa de partições horizontais.
* Para criar ou remover pontos ou intervalos que estão mapeados para as shards: utilizar **CreateRangeMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.createrangemapping), [.NET](https://msdn.microsoft.com/library/azure/dn841993.aspx)), **DeleteMapping** ( [Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.deletemapping), [.NET](https://msdn.microsoft.com/library/azure/dn824200.aspx)) da RangeShardMapping ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807318.aspx)) classe, e **CreatePointMapping**  ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map.createpointmapping), [.NET](https://msdn.microsoft.com/library/azure/dn807218.aspx)) da ListShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn842123.aspx)) classe.
  
    Muitos pontos diferentes ou intervalos de podem ser mapeados para as partições horizontais mesmo. Estes métodos afetam apenas metadados - não afetam todos os dados que podem já estar presentes no shards. Se precisam de dados a serem removidos da base de dados para que seja consistente com **DeleteMapping** operações, execute essas operações em separado, mas em conjunto com a utilização destes métodos.  
* Para dividir intervalos existentes em dois ou intercalar um intervalos adjacentes: utilizar **SplitMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.splitmapping), [.NET](https://msdn.microsoft.com/library/azure/dn824205.aspx)) e **MergeMappings** ( [Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.mergemappings), [.NET](https://msdn.microsoft.com/library/azure/dn824201.aspx)).  
  
    Tenha em atenção que divide e operações de intercalação **não altere as partições horizontais ao qual os valores de chaves estão mapeados**. Uma divisão de quebras de um intervalo existente em duas partes, mas deixa ambos como mapeado para o ID de partição horizontal mesmo. Uma intercalação opera em dois intervalos adjacentes que já estão mapeados para o mesmo ID de partição horizontal, União-los para um único intervalo.  O movimento dos pontos ou intervalos próprios entre shards tem de ser coordenado utilizando **UpdateMapping** em conjunto com o movimento de dados.  Pode utilizar o **divisão/intercalação** service, ou seja, parte das ferramentas de base de dados elástica para coordenar as alterações de mapa de ID de partição horizontal com o movimento de dados, quando é necessário o movimento. 
* Para voltar a mapear (ou mover) pontos individuais ou intervalos de shards diferentes: utilizar **UpdateMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.updatemapping), [.NET](https://msdn.microsoft.com/library/azure/dn824207.aspx)).  
  
    Uma vez que os dados poderão ter de ser movidos de um ID de partição horizontal para outro para estar consistente com **UpdateMapping** operações, tem de efetuar essa movimento separadamente, mas em conjunto com a utilização destes métodos.
* Para tirar mapeamentos online e offline: utilizar **MarkMappingOffline** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.markmappingoffline), [.NET](https://msdn.microsoft.com/library/azure/dn824202.aspx)) e **MarkMappingOnline** ([ Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.markmappingonline), [.NET](https://msdn.microsoft.com/library/azure/dn807225.aspx)) para controlar o estado online de um mapeamento. 
  
    Determinadas operações nos mapeamentos de partições horizontais só são permitidas quando um mapeamento está no estado "offline", incluindo **UpdateMapping** e **DeleteMapping**. Quando um mapeamento estiver offline, um pedido de dados dependentes com base numa chave incluída nesse mapeamento devolve um erro. Além disso, quando um intervalo primeiro seja colocado offline, são automaticamente eliminadas todas as ligações para o ID de partição horizontal afetado para evitar resultados inconsistentes ou incompletos para consultas direcionados contra intervalos a ser alterados. 

Mapeamentos são imutáveis no .net.  Todos os métodos acima alterar mapeamentos invalidar também quaisquer referências aos mesmos no seu código. Para facilitar a sequências de operações que alteram o estado de um mapeamento de efetuar, todos os métodos que alterar um mapeamento de devolvem uma referência de mapeamento novo, para que operações podem ser ligadas. Por exemplo, para eliminar um mapeamento no sm shardmap que contém a chave de 25 existente, pode executar o seguinte: 

```
    sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));
```

## <a name="adding-a-shard"></a>A adição de um ID de partição horizontal
As aplicações, muitas vezes, tem de adicionar novas shards para processar os dados que são esperados dos novas chaves ou intervalos de chaves, para um mapa de partições horizontais que já existe. Por exemplo, uma aplicação em partição horizontal por ID de inquilino poderá ter de aprovisionar um ID de partição horizontal novo para um novo inquilino ou mensal em partição horizontal de dados poderá ter um ID de partição horizontal novo aprovisionado antes do início de cada mês de novo. 

Se o novo intervalo de valores de chave já não faz parte de um mapeamento existente e não movimento de dados é necessário, é simple adicionar o ID de partição horizontal novo e associar a nova chave ou um intervalo a esse ID de partição horizontal. Para obter mais informações sobre como adicionar novos shards, consulte [adição de um ID de partição horizontal novo](sql-database-elastic-scale-add-a-shard.md).

Cenários que necessitam de movimento de dados, no entanto, a ferramenta de intercalação de divisão é necessário para orquestrar o movimento de dados entre shards em combinação com as atualizações de mapa de partições horizontais necessário. Para obter mais informações sobre como utilizar a ferramenta de intercalação de divisão, consulte [descrição geral da divisão de intercalação](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
