---
title: "aaaXEvent código de memória intermédia de anel para a base de dados SQL | Microsoft Docs"
description: "Fornece um exemplo de código de Transact-SQL que foi criado, fácil e rápido pela utilização de destino de memória intermédia de anel Olá, na SQL Database do Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="37d90-103">Anel código de destino de memória intermédia de eventos expandidos na base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="37d90-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="37d90-104">Pretende um exemplo de código completo para Olá mais fácil forma rápida toocapture e relatório de informações para um evento expandido durante um teste.</span><span class="sxs-lookup"><span data-stu-id="37d90-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="37d90-105">Olá o destino mais fácil para os dados de evento expandido é Olá [destino de memória intermédia de anel](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="37d90-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="37d90-106">Este tópico apresenta um exemplo de código de Transact-SQL que:</span><span class="sxs-lookup"><span data-stu-id="37d90-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="37d90-107">Cria uma tabela com dados toodemonstrate com.</span><span class="sxs-lookup"><span data-stu-id="37d90-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="37d90-108">Cria uma sessão para um evento expandido existente, nomeadamente **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="37d90-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="37d90-109">Olá evento está limitado tooSQL instruções que contêm uma cadeia de atualização específica: **instrução LIKE '% ATUALIZAÇÃO tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="37d90-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="37d90-110">Escolhe o resultado de Olá toosend Olá eventos tooa de destino do tipo memória intermédia de anel, nomeadamente **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="37d90-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="37d90-111">Inicia a sessão do evento Olá.</span><span class="sxs-lookup"><span data-stu-id="37d90-111">Starts hello event session.</span></span>
4. <span data-ttu-id="37d90-112">Problemas de duas instruções de ATUALIZAÇÃO SQL simples.</span><span class="sxs-lookup"><span data-stu-id="37d90-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="37d90-113">Emite uma SQL SELECT instrução tooretrieve eventos saída de Olá memória intermédia de anel.</span><span class="sxs-lookup"><span data-stu-id="37d90-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="37d90-114">**sys.dm_xe_database_session_targets** e são associadas a outras vistas de gestão dinâmica (DMVs).</span><span class="sxs-lookup"><span data-stu-id="37d90-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="37d90-115">Interrompe a sessão do evento Olá.</span><span class="sxs-lookup"><span data-stu-id="37d90-115">Stops hello event session.</span></span>
7. <span data-ttu-id="37d90-116">Remoções Olá destino de memória intermédia de anel, toorelease respetivos recursos.</span><span class="sxs-lookup"><span data-stu-id="37d90-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="37d90-117">Ignora a sessão do evento Olá e a tabela de demonstração de Olá.</span><span class="sxs-lookup"><span data-stu-id="37d90-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37d90-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="37d90-118">Prerequisites</span></span>

* <span data-ttu-id="37d90-119">Uma conta e subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="37d90-119">An Azure account and subscription.</span></span> <span data-ttu-id="37d90-120">Pode inscrever-se para obter uma [versão de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37d90-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="37d90-121">Qualquer base de dados que pode criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="37d90-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="37d90-122">Opcionalmente, pode [criar um **AdventureWorksLT** base de dados de demonstração](sql-database-get-started.md) em minutos.</span><span class="sxs-lookup"><span data-stu-id="37d90-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="37d90-123">SQL Server Management Studio (ssms.exe), idealmente, a última versão atualização mensal.</span><span class="sxs-lookup"><span data-stu-id="37d90-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="37d90-124">Pode transferir Olá ssms.exe mais recente do:</span><span class="sxs-lookup"><span data-stu-id="37d90-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="37d90-125">Tópico intitulado [transferir SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="37d90-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="37d90-126">Transferência de toohello uma ligação direta.</span><span class="sxs-lookup"><span data-stu-id="37d90-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="37d90-127">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="37d90-127">Code sample</span></span>

<span data-ttu-id="37d90-128">Com muito pequenas modificação, hello seguinte exemplo de código de memória intermédia de anel pode ser executado na SQL Database do Azure ou Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="37d90-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="37d90-129">diferença de Olá é Olá presença nó Olá _database no nome de Olá de algumas vistas de gestão dinâmica (DMVs), utilizada na cláusula FROM de Olá no passo 5.</span><span class="sxs-lookup"><span data-stu-id="37d90-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="37d90-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="37d90-130">For example:</span></span>

* <span data-ttu-id="37d90-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="37d90-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="37d90-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="37d90-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="37d90-133">Conteúdo de memória intermédia de anel</span><span class="sxs-lookup"><span data-stu-id="37d90-133">Ring Buffer contents</span></span>

<span data-ttu-id="37d90-134">Utilizámos o ssms.exe toorun Olá código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="37d90-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="37d90-135">resultados de Olá tooview, iremos clicado célula Olá sob o cabeçalho da coluna Olá **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="37d90-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="37d90-136">Em seguida, no painel de resultados de Olá clica na célula Olá sob o cabeçalho da coluna Olá **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="37d90-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="37d90-137">Isto, clique em criar noutro separador do ficheiro no ssms.exe no qual Olá foi apresentado o conteúdo da célula de resultado Olá como XML.</span><span class="sxs-lookup"><span data-stu-id="37d90-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="37d90-138">saída de Olá é mostrada na Olá seguir bloco.</span><span class="sxs-lookup"><span data-stu-id="37d90-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="37d90-139">Procura longo, mas é apenas dois  **<event>**  elementos.</span><span class="sxs-lookup"><span data-stu-id="37d90-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="37d90-140">Libertar recursos retidos, a memória intermédia de anel</span><span class="sxs-lookup"><span data-stu-id="37d90-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="37d90-141">Quando tiver terminado com a memória intermédia de anel, pode removê-lo e respetivos recursos de emissão da versão um **ALTER** com Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="37d90-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="37d90-142">definição de Olá da sua sessão do evento é atualizada, mas não foi removida.</span><span class="sxs-lookup"><span data-stu-id="37d90-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="37d90-143">Mais tarde pode adicionar outra instância da sessão do evento Olá memória intermédia de anel tooyour:</span><span class="sxs-lookup"><span data-stu-id="37d90-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="37d90-144">Mais informações</span><span class="sxs-lookup"><span data-stu-id="37d90-144">More information</span></span>

<span data-ttu-id="37d90-145">tópico principal do Olá expandida eventos na base de dados do Azure SQL é:</span><span class="sxs-lookup"><span data-stu-id="37d90-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="37d90-146">[Expandido considerações de evento na base de dados do SQL Server](sql-database-xevent-db-diff-from-svr.md), que contrasta alguns aspetos dos eventos expandidos que diferem entre a base de dados do Azure SQL em comparação com o Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="37d90-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="37d90-147">Outros tópicos de exemplo de código para expandida eventos estão disponíveis em Olá seguintes ligações.</span><span class="sxs-lookup"><span data-stu-id="37d90-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="37d90-148">No entanto, tem de verificar regularmente qualquer toosee exemplo se exemplo Olá está direcionada para Microsoft SQL Server em comparação com a SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="37d90-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="37d90-149">Em seguida, pode decidir se a pequenas alterações são exemplo de Olá toorun necessários.</span><span class="sxs-lookup"><span data-stu-id="37d90-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="37d90-150">Exemplo de código para a SQL Database do Azure: [código de destino de ficheiro de eventos para expandida eventos na base de dados SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="37d90-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
