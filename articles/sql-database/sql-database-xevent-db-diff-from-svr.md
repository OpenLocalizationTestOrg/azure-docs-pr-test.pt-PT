---
title: eventos de aaaExtended na base de dados SQL | Microsoft Docs
description: "Descreve eventos expandidos (XEvents) na SQL Database do Azure e como sessões de evento diferirem ligeiramente do sessões de evento no Microsoft SQL Server."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="47840-103">Eventos expandidos na base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="47840-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="47840-104">Este tópico explica como implementação de Olá de eventos expandidos na SQL Database do Azure é ligeiramente diferente tooextended em comparação com eventos no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47840-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="47840-105">SQL Database V12 adquiridos funcionalidade de eventos expandidos Olá no Olá segunda metade do calendário 2015.</span><span class="sxs-lookup"><span data-stu-id="47840-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="47840-106">SQL Server tenha tido eventos expandidos desde 2008.</span><span class="sxs-lookup"><span data-stu-id="47840-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="47840-107">conjunto de funcionalidades de Olá de eventos expandidos na base de dados do SQL Server é um subconjunto robusto de funcionalidades de Olá no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47840-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="47840-108">*XEvents* é uma alcunha informal que por vezes, é utilizada para 'eventos expandidos' em blogues e outras localizações informal.</span><span class="sxs-lookup"><span data-stu-id="47840-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="47840-109">Informações adicionais sobre eventos expandidas, para a SQL Database do Azure e o Microsoft SQL Server, estão disponíveis em:</span><span class="sxs-lookup"><span data-stu-id="47840-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="47840-110">Início rápido: Eventos expandidos no SQL Server</span><span class="sxs-lookup"><span data-stu-id="47840-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="47840-111">Eventos expandidos</span><span class="sxs-lookup"><span data-stu-id="47840-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="47840-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47840-112">Prerequisites</span></span>

<span data-ttu-id="47840-113">Este tópico assume que já tiver algum conhecimento de:</span><span class="sxs-lookup"><span data-stu-id="47840-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="47840-114">[Serviço de base de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="47840-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="47840-115">[Expandido eventos](http://msdn.microsoft.com/library/bb630282.aspx) no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47840-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="47840-116">aplica-se em massa de Olá da nossa documentação sobre eventos expandidas tooboth do SQL Server e base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="47840-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="47840-117">Toohello exposição anterior seguintes itens de ação é útil quando escolher Olá ficheiro eventos como Olá [destino](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="47840-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="47840-118">Serviço de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="47840-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="47840-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47840-119">PowerShell</span></span>
    - <span data-ttu-id="47840-120">[Com o Azure PowerShell com o Storage do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="47840-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="47840-121">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="47840-121">Code samples</span></span>

<span data-ttu-id="47840-122">Tópicos relacionados fornecem dois exemplos de código:</span><span class="sxs-lookup"><span data-stu-id="47840-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="47840-123">Anel código de destino de memória intermédia de eventos expandidos na base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="47840-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="47840-124">Script de Transact-SQL simple curto.</span><span class="sxs-lookup"><span data-stu-id="47840-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="47840-125">Iremos destacar tópico de exemplo de código Olá que, quando tiver terminado com um destino de memória intermédia de anel, deve versão dos respetivos recursos, executando um largar alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrução.</span><span class="sxs-lookup"><span data-stu-id="47840-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="47840-126">Mais tarde, pode adicionar outra instância da memória intermédia de anel por `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="47840-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="47840-127">Código de destino de ficheiro de evento expandido eventos na base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="47840-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="47840-128">Fase 1 é PowerShell toocreate um contentor de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47840-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="47840-129">Fase 2 é Transact-SQL que utiliza o contentor de armazenamento do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="47840-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="47840-130">Diferenças do Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="47840-130">Transact-SQL differences</span></span>


- <span data-ttu-id="47840-131">Quando executar Olá [eventos criar sessão](http://msdn.microsoft.com/library/bb677289.aspx) comando no SQL Server, utilize Olá **no servidor** cláusula.</span><span class="sxs-lookup"><span data-stu-id="47840-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="47840-132">Mas na base de dados do SQL Server utilizar Olá **na base de dados** cláusula em vez disso.</span><span class="sxs-lookup"><span data-stu-id="47840-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="47840-133">Olá **na base de dados** cláusula também se aplica toohello [eventos de falha de ALTER sessão](http://msdn.microsoft.com/library/bb630368.aspx) e [remover eventos da sessão](http://msdn.microsoft.com/library/bb630257.aspx) comandos Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="47840-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="47840-134">Uma melhor prática é tooinclude opção da sessão do evento Olá de **STARTUP_STATE = ON** no seu **eventos criar sessão** ou **eventos de falha de ALTER sessão** instruções.</span><span class="sxs-lookup"><span data-stu-id="47840-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="47840-135">Olá **= ON** valor suporta um reinício automático após uma reconfiguração da base de dados lógica Olá devido a ativação pós-falha de tooa.</span><span class="sxs-lookup"><span data-stu-id="47840-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="47840-136">Novas vistas de catálogo</span><span class="sxs-lookup"><span data-stu-id="47840-136">New catalog views</span></span>

<span data-ttu-id="47840-137">Olá eventos expandida funcionalidade é suportada por vários [vistas de catálogo](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="47840-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="47840-138">Vistas de catálogo conte *metadados ou com definições* de sessões de evento criados pelo utilizador na base de dados atual Olá.</span><span class="sxs-lookup"><span data-stu-id="47840-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="47840-139">vistas de Olá não devolver informações sobre as instâncias de sessões de evento Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47840-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="47840-140">Nome de</span><span class="sxs-lookup"><span data-stu-id="47840-140">Name of</span></span><br/><span data-ttu-id="47840-141">Vista de catálogo</span><span class="sxs-lookup"><span data-stu-id="47840-141">catalog view</span></span> | <span data-ttu-id="47840-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="47840-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="47840-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="47840-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="47840-144">Devolve uma linha para cada ação em cada evento de uma sessão do evento.</span><span class="sxs-lookup"><span data-stu-id="47840-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="47840-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="47840-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="47840-146">Devolve uma linha para cada evento na sessão do evento.</span><span class="sxs-lookup"><span data-stu-id="47840-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="47840-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="47840-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="47840-148">Devolve uma linha para cada personalizar coluna que foi explicitamente definida em eventos e destinos.</span><span class="sxs-lookup"><span data-stu-id="47840-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="47840-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="47840-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="47840-150">Devolve uma linha para cada destino de eventos de uma sessão do evento.</span><span class="sxs-lookup"><span data-stu-id="47840-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="47840-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="47840-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="47840-152">Devolve uma linha para cada sessão de evento na base de dados do Olá base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="47840-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="47840-153">No Microsoft SQL Server, vistas de catálogo semelhante têm nomes que incluem *.server\_*  em vez de *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="47840-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="47840-154">Olá padrão do nome é como **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="47840-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="47840-155">Novas vistas de gestão dinâmica [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="47840-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="47840-156">Base de dados SQL do Azure tem [vistas de gestão dinâmica (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) que suportam eventos expandidos.</span><span class="sxs-lookup"><span data-stu-id="47840-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="47840-157">DMVs conte *Active Directory* sessões de evento.</span><span class="sxs-lookup"><span data-stu-id="47840-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="47840-158">Nome do DMV</span><span class="sxs-lookup"><span data-stu-id="47840-158">Name of DMV</span></span> | <span data-ttu-id="47840-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="47840-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="47840-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="47840-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="47840-161">Devolve informações sobre as ações de sessão do evento.</span><span class="sxs-lookup"><span data-stu-id="47840-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="47840-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="47840-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="47840-163">Devolve informações sobre eventos da sessão.</span><span class="sxs-lookup"><span data-stu-id="47840-163">Returns information about session events.</span></span> |
| <span data-ttu-id="47840-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="47840-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="47840-165">Mostra os valores de configuração de Olá para objetos que estão vinculadas tooa sessão.</span><span class="sxs-lookup"><span data-stu-id="47840-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="47840-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="47840-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="47840-167">Devolve informações sobre os destinos de sessão.</span><span class="sxs-lookup"><span data-stu-id="47840-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="47840-168">**xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="47840-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="47840-169">Devolve uma linha para cada sessão de evento que está confinada toohello base de dados atual.</span><span class="sxs-lookup"><span data-stu-id="47840-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="47840-170">No Microsoft SQL Server, as vistas de catálogo semelhantes são denominadas sem Olá  *\_base de dados* nome de parte Olá, tais como:</span><span class="sxs-lookup"><span data-stu-id="47840-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="47840-171">**sys.dm_xe_sessions**, em vez do nome</span><span class="sxs-lookup"><span data-stu-id="47840-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="47840-172">**xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="47840-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="47840-173">Tooboth comuns DMVs</span><span class="sxs-lookup"><span data-stu-id="47840-173">DMVs common tooboth</span></span>
<span data-ttu-id="47840-174">Para eventos expandidos existem DMVs adicionais que são comuns tooboth SQL Database do Azure e o Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="47840-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="47840-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="47840-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="47840-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="47840-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="47840-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="47840-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="47840-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="47840-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="47840-179">Encontrar eventos de expandida disponíveis Olá, ações e destinos</span><span class="sxs-lookup"><span data-stu-id="47840-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="47840-180">Pode executar um SQL simple **SELECIONE** tooobtain uma lista de eventos disponível Olá, ações e de destino.</span><span class="sxs-lookup"><span data-stu-id="47840-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="47840-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="47840-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="47840-182">Destinos para as sessões de evento de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="47840-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="47840-183">Seguem-se destinos que podem capturar resultados a partir do seu sessões de evento na base de dados do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="47840-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="47840-184">[Destino de memória intermédia de anel](http://msdn.microsoft.com/library/ff878182.aspx) -brevemente contém dados de eventos na memória.</span><span class="sxs-lookup"><span data-stu-id="47840-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="47840-185">[Destino de contador do evento](http://msdn.microsoft.com/library/ff878025.aspx) -contagens de todos os eventos que ocorrem durante uma sessão de eventos expandidos.</span><span class="sxs-lookup"><span data-stu-id="47840-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="47840-186">[Destino do ficheiro de evento](http://msdn.microsoft.com/library/ff878115.aspx) -contentor de armazenamento do Azure de tooan de memórias intermédias concluída escritas.</span><span class="sxs-lookup"><span data-stu-id="47840-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="47840-187">Olá [rastreio de eventos para o Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API não está disponível para eventos expandidos na base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47840-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="47840-188">Restrições</span><span class="sxs-lookup"><span data-stu-id="47840-188">Restrictions</span></span>

<span data-ttu-id="47840-189">Existem algumas diferenças relacionadas com segurança befitting ambiente de nuvem Olá da base de dados do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="47840-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="47840-190">Eventos expandidos são founded no modelo de isolamento de inquilino único Olá.</span><span class="sxs-lookup"><span data-stu-id="47840-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="47840-191">Uma sessão do evento na base de dados de um não é possível aceder a dados ou eventos de outra base de dados.</span><span class="sxs-lookup"><span data-stu-id="47840-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="47840-192">Não é possível emitir uma **eventos criar sessão** instrução no contexto de Olá Olá **mestre** base de dados.</span><span class="sxs-lookup"><span data-stu-id="47840-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="47840-193">Modelo de permissão</span><span class="sxs-lookup"><span data-stu-id="47840-193">Permission model</span></span>

<span data-ttu-id="47840-194">Tem de ter **controlo** permissão tooissue de base de dados de Olá um **eventos criar sessão** instrução.</span><span class="sxs-lookup"><span data-stu-id="47840-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="47840-195">o proprietário da base de dados de Olá (dbo) tem **controlo** permissão.</span><span class="sxs-lookup"><span data-stu-id="47840-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="47840-196">Autorizações de contentor de armazenamento</span><span class="sxs-lookup"><span data-stu-id="47840-196">Storage container authorizations</span></span>

<span data-ttu-id="47840-197">token SAS de Olá gerar para o contentor de armazenamento do Azure tem de especificar **rwl** permissões Olá.</span><span class="sxs-lookup"><span data-stu-id="47840-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="47840-198">Olá **rwl** valor fornece Olá as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="47840-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="47840-199">Leitura</span><span class="sxs-lookup"><span data-stu-id="47840-199">Read</span></span>
- <span data-ttu-id="47840-200">Escrita</span><span class="sxs-lookup"><span data-stu-id="47840-200">Write</span></span>
- <span data-ttu-id="47840-201">Lista</span><span class="sxs-lookup"><span data-stu-id="47840-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="47840-202">Considerações de desempenho</span><span class="sxs-lookup"><span data-stu-id="47840-202">Performance considerations</span></span>

<span data-ttu-id="47840-203">Existem cenários onde utilização intensiva de eventos expandidos pode acumular ativa mais memória do que está em bom estado de Olá geral do sistema.</span><span class="sxs-lookup"><span data-stu-id="47840-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="47840-204">Por conseguinte Olá sistema da base de dados do Azure SQL dinamicamente define e ajusta limites na quantidade de Olá de memória de Active Directory que pode ser acumulada por uma sessão do evento.</span><span class="sxs-lookup"><span data-stu-id="47840-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="47840-205">Vários fatores tecnológica de cálculo dinâmica Olá.</span><span class="sxs-lookup"><span data-stu-id="47840-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="47840-206">Se receber uma mensagem de erro que indica que uma memória máxima tivesse sido imposta, algumas ações corretivas que pode tomar são:</span><span class="sxs-lookup"><span data-stu-id="47840-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="47840-207">Execute menos sessões de evento em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="47840-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="47840-208">Através do seu **criar** e **ALTER** instruções para sessões de evento, reduzir a quantidade de Olá de memória que especificar no Olá **máximo\_memória** cláusula.</span><span class="sxs-lookup"><span data-stu-id="47840-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="47840-209">Latência de rede</span><span class="sxs-lookup"><span data-stu-id="47840-209">Network latency</span></span>

<span data-ttu-id="47840-210">Olá **ficheiro eventos** destino pode ocorrer a latência de rede ou falhas ao tooAzure de dados persistentes blobs de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="47840-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="47840-211">Outros eventos na base de dados do SQL Server podem sofrer um atraso enquanto que terão de aguardar toocomplete de comunicação de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="47840-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="47840-212">Este atraso pode abrandar a sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47840-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="47840-213">toomitigate este desempenho risco, evite definir Olá **EVENT_RETENTION_MODE** opção demasiado**NO_EVENT_LOSS** nas definições de sessão do evento.</span><span class="sxs-lookup"><span data-stu-id="47840-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="47840-214">Ligações relacionadas</span><span class="sxs-lookup"><span data-stu-id="47840-214">Related links</span></span>

- <span data-ttu-id="47840-215">[Utilizar o Azure PowerShell com o Storage do Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="47840-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="47840-216">Cmdlets de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="47840-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="47840-217">[Com o Azure PowerShell com o Storage do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="47840-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="47840-218">Como toouse Blob storage do .NET</span><span class="sxs-lookup"><span data-stu-id="47840-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="47840-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="47840-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="47840-220">CRIAR a sessão do evento (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="47840-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="47840-221">Mensagens do blogue de Jonathan Kehayias sobre eventos expandidos no Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="47840-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="47840-222">Olá, Azure *atualizações de serviço* página Web, narrowed pelo parâmetro tooAzure base de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="47840-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="47840-223">https://Azure.microsoft.com/Updates/?Service=SQL-Database</span><span class="sxs-lookup"><span data-stu-id="47840-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="47840-224">Outros tópicos de exemplo de código para expandida eventos estão disponíveis em Olá seguintes ligações.</span><span class="sxs-lookup"><span data-stu-id="47840-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="47840-225">No entanto, tem de verificar regularmente qualquer toosee exemplo se exemplo Olá está direcionada para Microsoft SQL Server em comparação com a SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="47840-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="47840-226">Em seguida, pode decidir se a pequenas alterações são exemplo de Olá toorun necessários.</span><span class="sxs-lookup"><span data-stu-id="47840-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
