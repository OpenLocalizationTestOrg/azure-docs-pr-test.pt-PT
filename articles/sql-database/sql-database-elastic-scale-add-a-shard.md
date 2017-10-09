---
title: "aaaAdding um ID de partição horizontal com as ferramentas de base de dados elástica | Microsoft Docs"
description: "Como definir toouse APIs de dimensionamento flexível tooadd novo shards tooa partições horizontais."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Adicionar uma partição horizontal com as ferramentas de base de dados elástica
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd um para um novo intervalo ou chave de partição horizontal
As aplicações, muitas vezes, precisa de toosimply adicionam shards toohandle dados novos que são esperados dos novas chaves ou intervalos de chaves, para que já existe um mapa de partições horizontais. Por exemplo, uma aplicação em partição horizontal por ID de inquilino poderá ter tooprovision um ID de partição horizontal novo para um novo inquilino ou mensal em partição horizontal de dados poderá ter um ID de partição horizontal novo aprovisionado antes de iniciar Olá de cada mês de novo. 

Se o intervalo de nova Olá dos valores chave já não faz parte de um mapeamento existente, é muito simples tooadd Olá novo ID de partição horizontal e associar Olá nova chave ou um intervalo de toothat partições horizontais. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Exemplo: adicionar um ID de partição horizontal e respetivo mapa de partições horizontais existente do intervalo tooan
Este exemplo utiliza Olá [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) Olá [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) métodos e cria uma instância de Olá [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe. Exemplo de Olá abaixo, uma base de dados com o nome **sample_shard_2** e todos os objetos de esquema necessário dentro do mesmo tem sido criados toohold intervalo [300, 400).  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


Como alternativa, pode utilizar o Powershell toocreate um novo Gestor de mapa de partições horizontais. Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd um ID de partição horizontal para uma parte de um intervalo existente vazia
Em algumas circunstâncias, poderá ter já mapeado um intervalo tooa ID de partição horizontal e parcialmente preenchido este com dados, mas agora pretende dados futuros toobe tooa direcionados diferentes de partição horizontal. Por exemplo, a partições horizontais por dia intervalo e já tiver alocado dias 50 tooa ID de partição horizontal, mas no dia 24, pretende tooland dados futuras num ID de partição horizontal diferentes. base de dados elástica Olá [ferramenta de intercalação de divisão](sql-database-elastic-scale-overview-split-and-merge.md) podem efetuar esta operação, mas se o movimento de dados não é necessário (por exemplo, dados de intervalo de Olá de dias [25, 50), ou seja, dia 25 too50 inclusive exclusivo, ainda existe) pode efetuar Esta utilizando inteiramente Olá diretamente APIs de gestão de mapa de partições horizontais.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Exemplo: dividir um intervalo e atribuir Olá vazio parte tooa recentemente adicionado ID de partição horizontal
Uma base de dados com o nome "sample_shard_2" e todos os objetos de esquema necessário dentro do mesmo ter sido criado.  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**Importante**: utilizar esta técnica apenas se determinados que Olá intervalo para mapeamento de Olá atualizado está vazio.  métodos de Olá acima não verificar dados para o intervalo de Olá a ser movido, pelo que é melhor tooinclude verifica no seu código.  Se existirem linhas no intervalo de Olá a ser movido, distribuição de dados real de Olá não irá corresponder à mapa de partições horizontais atualizado Olá. Olá utilize [ferramenta de intercalação de divisão](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Olá operação em vez disso, nestes casos.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

