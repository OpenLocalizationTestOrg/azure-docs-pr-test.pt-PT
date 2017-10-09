---
title: "bases de dados aaaQuery em partição horizontal SQL do Azure | Microsoft Docs"
description: "Execute consultas em shards com biblioteca de cliente de base de dados elástica Olá."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Consulta de várias partições horizontais
## <a name="overview"></a>Descrição geral
Com Olá [ferramentas de base de dados elástica](sql-database-elastic-scale-introduction.md), pode criar soluções de base de dados em partição horizontal. **Consulta de partições horizontais Multi** é utilizada para tarefas, tais como recolha/relatórios de dados que requerem a execução de uma consulta que é alongada entre várias partições horizontais. (Contraste isto demasiado[encaminhamento de dados dependentes](sql-database-elastic-scale-data-dependent-routing.md), que efetua todo trabalho um ID de partição horizontal único.) 

1. Obter um [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) utilizando Olá [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Olá [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou Olá [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método. Consulte [ **construir um ShardMapManager** ](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) e [ **obter um RangeShardMap ou ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Criar um  **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**  objeto.
3. Criar um  **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Conjunto Olá  **[propriedade CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa comando T-SQL.
5. Executar o comando de Olá ao chamar Olá  **[método ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Ver resultados de Olá utilizando Olá  **[MultiShardDataReader classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Exemplo
Olá seguinte código ilustra a utilização de Olá de partições horizontais multi consulta utilizando um determinado **ShardMap** denominado *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


Uma principal diferença é construção Olá de ligações de várias partições horizontais. Onde **SqlConnection** funciona numa base de dados único, hello **MultiShardConnection** demora um ***coleção de partições horizontais*** como entrada. Povoar a colecção de Olá de partições horizontais de um mapa de partições horizontais. consulta de Olá, em seguida, é executada numa coleção de Olá de partições horizontais utilizando **UNION ALL** semântica tooassemble um único resultado geral. Opcionalmente, pode ser adicionado toohello saída utilizando Olá nome Olá de partições horizontais olá onde linha Olá tem origem **ExecutionOptions** propriedade no comando. 

Tenha em atenção chamada Olá demasiado**myShardMap.GetShards()**. Este método obtém todas as partições horizontais do mapa de partições horizontais Olá e fornece uma forma fácil toorun uma consulta em todas as bases de dados relevantes. Olá coleção de partições horizontais para uma consulta de partições horizontais multi pode ser avançada mais efetuando uma LINQ consultar sobre recolha de Olá devolvida da chamada de Olá demasiado**myShardMap.GetShards()**. Em combinação com a política de resultados parciais Olá, a capacidade atual da Olá na consulta de partições horizontais multi foi concebida toowork bem para dezenas segurança toohundreds de partições horizontais.

Uma limitação com várias partições horizontais consulta está atualmente a falta de Olá de validação para shards e shardlets são consultadas. Enquanto o encaminhamento de dados dependentes verifica que um ID de partição horizontal especificado faz parte do mapa de partições horizontais Olá momento Olá da consulta, consultas de partições horizontais multi não executar esta verificação. Isto pode levar a consultas de partições horizontais o toomulti em execução em bases de dados que foram removidas do mapa de partições horizontais Olá.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Operações de divisão de intercalação e consultas de várias partições horizontais
Consultas de partições horizontais multi não verificar se shardlets na base de dados consultado Olá participam em operações de divisão de intercalação em curso. (Consulte [dimensionamento utilizando a ferramenta de Olá intercalação de divisão de base de dados elástica](sql-database-elastic-scale-overview-split-and-merge.md).) Esta funcionalidade pode originar tooinconsistencies onde as linhas de Olá mesmo shardlet Mostrar várias bases de dados no Olá mesma consulta de várias partições horizontais. Tenha em conta estas limitações e considere a ser drenado e em curso divisão intercalação operações e alterações toohello partições horizontais mapa ao efetuar consultas de várias partições horizontais.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Consultar também
**[SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**  classes e métodos.

Gerir shards utilizando Olá [biblioteca de clientes de base de dados elástica](sql-database-elastic-database-client-library.md). Inclui um espaço de nomes chamado [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) que fornece Olá capacidade tooquery shards vários utilizando uma única consulta e o resultado. Fornece uma abstração de consulta através de uma coleção de partições horizontais. Também fornece as políticas de execução alternativo, resultados parciais em particular, toodeal com falhas ao consultar através de várias partições horizontais.  

