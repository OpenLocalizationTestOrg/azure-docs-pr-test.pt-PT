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
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="82b45-103">Adicionar uma partição horizontal com as ferramentas de base de dados elástica</span><span class="sxs-lookup"><span data-stu-id="82b45-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="82b45-104">tooadd um para um novo intervalo ou chave de partição horizontal</span><span class="sxs-lookup"><span data-stu-id="82b45-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="82b45-105">As aplicações, muitas vezes, precisa de toosimply adicionam shards toohandle dados novos que são esperados dos novas chaves ou intervalos de chaves, para que já existe um mapa de partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="82b45-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="82b45-106">Por exemplo, uma aplicação em partição horizontal por ID de inquilino poderá ter tooprovision um ID de partição horizontal novo para um novo inquilino ou mensal em partição horizontal de dados poderá ter um ID de partição horizontal novo aprovisionado antes de iniciar Olá de cada mês de novo.</span><span class="sxs-lookup"><span data-stu-id="82b45-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="82b45-107">Se o intervalo de nova Olá dos valores chave já não faz parte de um mapeamento existente, é muito simples tooadd Olá novo ID de partição horizontal e associar Olá nova chave ou um intervalo de toothat partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="82b45-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="82b45-108">Exemplo: adicionar um ID de partição horizontal e respetivo mapa de partições horizontais existente do intervalo tooan</span><span class="sxs-lookup"><span data-stu-id="82b45-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="82b45-109">Este exemplo utiliza Olá [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) Olá [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) métodos e cria uma instância de Olá [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe.</span><span class="sxs-lookup"><span data-stu-id="82b45-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="82b45-110">Exemplo de Olá abaixo, uma base de dados com o nome **sample_shard_2** e todos os objetos de esquema necessário dentro do mesmo tem sido criados toohold intervalo [300, 400).</span><span class="sxs-lookup"><span data-stu-id="82b45-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

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


<span data-ttu-id="82b45-111">Como alternativa, pode utilizar o Powershell toocreate um novo Gestor de mapa de partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="82b45-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="82b45-112">Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="82b45-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="82b45-113">tooadd um ID de partição horizontal para uma parte de um intervalo existente vazia</span><span class="sxs-lookup"><span data-stu-id="82b45-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="82b45-114">Em algumas circunstâncias, poderá ter já mapeado um intervalo tooa ID de partição horizontal e parcialmente preenchido este com dados, mas agora pretende dados futuros toobe tooa direcionados diferentes de partição horizontal.</span><span class="sxs-lookup"><span data-stu-id="82b45-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="82b45-115">Por exemplo, a partições horizontais por dia intervalo e já tiver alocado dias 50 tooa ID de partição horizontal, mas no dia 24, pretende tooland dados futuras num ID de partição horizontal diferentes.</span><span class="sxs-lookup"><span data-stu-id="82b45-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="82b45-116">base de dados elástica Olá [ferramenta de intercalação de divisão](sql-database-elastic-scale-overview-split-and-merge.md) podem efetuar esta operação, mas se o movimento de dados não é necessário (por exemplo, dados de intervalo de Olá de dias [25, 50), ou seja, dia 25 too50 inclusive exclusivo, ainda existe) pode efetuar Esta utilizando inteiramente Olá diretamente APIs de gestão de mapa de partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="82b45-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="82b45-117">Exemplo: dividir um intervalo e atribuir Olá vazio parte tooa recentemente adicionado ID de partição horizontal</span><span class="sxs-lookup"><span data-stu-id="82b45-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="82b45-118">Uma base de dados com o nome "sample_shard_2" e todos os objetos de esquema necessário dentro do mesmo ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="82b45-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

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

<span data-ttu-id="82b45-119">**Importante**: utilizar esta técnica apenas se determinados que Olá intervalo para mapeamento de Olá atualizado está vazio.</span><span class="sxs-lookup"><span data-stu-id="82b45-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="82b45-120">métodos de Olá acima não verificar dados para o intervalo de Olá a ser movido, pelo que é melhor tooinclude verifica no seu código.</span><span class="sxs-lookup"><span data-stu-id="82b45-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="82b45-121">Se existirem linhas no intervalo de Olá a ser movido, distribuição de dados real de Olá não irá corresponder à mapa de partições horizontais atualizado Olá.</span><span class="sxs-lookup"><span data-stu-id="82b45-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="82b45-122">Olá utilize [ferramenta de intercalação de divisão](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Olá operação em vez disso, nestes casos.</span><span class="sxs-lookup"><span data-stu-id="82b45-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

