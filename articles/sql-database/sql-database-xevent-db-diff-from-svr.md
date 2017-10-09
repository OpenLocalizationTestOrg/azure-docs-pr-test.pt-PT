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
# <a name="extended-events-in-sql-database"></a>Eventos expandidos na base de dados SQL
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Este tópico explica como implementação de Olá de eventos expandidos na SQL Database do Azure é ligeiramente diferente tooextended em comparação com eventos no Microsoft SQL Server.

- SQL Database V12 adquiridos funcionalidade de eventos expandidos Olá no Olá segunda metade do calendário 2015.
- SQL Server tenha tido eventos expandidos desde 2008.
- conjunto de funcionalidades de Olá de eventos expandidos na base de dados do SQL Server é um subconjunto robusto de funcionalidades de Olá no SQL Server.

*XEvents* é uma alcunha informal que por vezes, é utilizada para 'eventos expandidos' em blogues e outras localizações informal.

Informações adicionais sobre eventos expandidas, para a SQL Database do Azure e o Microsoft SQL Server, estão disponíveis em:

- [Início rápido: Eventos expandidos no SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Eventos expandidos](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Pré-requisitos

Este tópico assume que já tiver algum conhecimento de:

- [Serviço de base de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/).
- [Expandido eventos](http://msdn.microsoft.com/library/bb630282.aspx) no Microsoft SQL Server.

- aplica-se em massa de Olá da nossa documentação sobre eventos expandidas tooboth do SQL Server e base de dados SQL.

Toohello exposição anterior seguintes itens de ação é útil quando escolher Olá ficheiro eventos como Olá [destino](#AzureXEventsTargets):

- [Serviço de armazenamento do Azure](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [Com o Azure PowerShell com o Storage do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço Storage do Azure.

## <a name="code-samples"></a>Exemplos de código

Tópicos relacionados fornecem dois exemplos de código:


- [Anel código de destino de memória intermédia de eventos expandidos na base de dados SQL](sql-database-xevent-code-ring-buffer.md)
    - Script de Transact-SQL simple curto.
    - Iremos destacar tópico de exemplo de código Olá que, quando tiver terminado com um destino de memória intermédia de anel, deve versão dos respetivos recursos, executando um largar alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrução. Mais tarde, pode adicionar outra instância da memória intermédia de anel por `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Código de destino de ficheiro de evento expandido eventos na base de dados do SQL Server](sql-database-xevent-code-event-file.md)
    - Fase 1 é PowerShell toocreate um contentor de armazenamento do Azure.
    - Fase 2 é Transact-SQL que utiliza o contentor de armazenamento do Azure Olá.

## <a name="transact-sql-differences"></a>Diferenças do Transact-SQL


- Quando executar Olá [eventos criar sessão](http://msdn.microsoft.com/library/bb677289.aspx) comando no SQL Server, utilize Olá **no servidor** cláusula. Mas na base de dados do SQL Server utilizar Olá **na base de dados** cláusula em vez disso.


- Olá **na base de dados** cláusula também se aplica toohello [eventos de falha de ALTER sessão](http://msdn.microsoft.com/library/bb630368.aspx) e [remover eventos da sessão](http://msdn.microsoft.com/library/bb630257.aspx) comandos Transact-SQL.


- Uma melhor prática é tooinclude opção da sessão do evento Olá de **STARTUP_STATE = ON** no seu **eventos criar sessão** ou **eventos de falha de ALTER sessão** instruções.
    - Olá **= ON** valor suporta um reinício automático após uma reconfiguração da base de dados lógica Olá devido a ativação pós-falha de tooa.

## <a name="new-catalog-views"></a>Novas vistas de catálogo

Olá eventos expandida funcionalidade é suportada por vários [vistas de catálogo](http://msdn.microsoft.com/library/ms174365.aspx). Vistas de catálogo conte *metadados ou com definições* de sessões de evento criados pelo utilizador na base de dados atual Olá. vistas de Olá não devolver informações sobre as instâncias de sessões de evento Active Directory.

| Nome de<br/>Vista de catálogo | Descrição |
|:--- |:--- |
| **sys.database_event_session_actions** |Devolve uma linha para cada ação em cada evento de uma sessão do evento. |
| **sys.database_event_session_events** |Devolve uma linha para cada evento na sessão do evento. |
| **sys.database_event_session_fields** |Devolve uma linha para cada personalizar coluna que foi explicitamente definida em eventos e destinos. |
| **sys.database_event_session_targets** |Devolve uma linha para cada destino de eventos de uma sessão do evento. |
| **sys.database_event_sessions** |Devolve uma linha para cada sessão de evento na base de dados do Olá base de dados SQL. |

No Microsoft SQL Server, vistas de catálogo semelhante têm nomes que incluem *.server\_*  em vez de *.database\_*. Olá padrão do nome é como **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>Novas vistas de gestão dinâmica [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)

Base de dados SQL do Azure tem [vistas de gestão dinâmica (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) que suportam eventos expandidos. DMVs conte *Active Directory* sessões de evento.

| Nome do DMV | Descrição |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Devolve informações sobre as ações de sessão do evento. |
| **sys.dm_xe_database_session_events** |Devolve informações sobre eventos da sessão. |
| **sys.dm_xe_database_session_object_columns** |Mostra os valores de configuração de Olá para objetos que estão vinculadas tooa sessão. |
| **sys.dm_xe_database_session_targets** |Devolve informações sobre os destinos de sessão. |
| **xe_database_sessions** |Devolve uma linha para cada sessão de evento que está confinada toohello base de dados atual. |

No Microsoft SQL Server, as vistas de catálogo semelhantes são denominadas sem Olá  *\_base de dados* nome de parte Olá, tais como:

- **sys.dm_xe_sessions**, em vez do nome<br/>**xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Tooboth comuns DMVs
Para eventos expandidos existem DMVs adicionais que são comuns tooboth SQL Database do Azure e o Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Encontrar eventos de expandida disponíveis Olá, ações e destinos

Pode executar um SQL simple **SELECIONE** tooobtain uma lista de eventos disponível Olá, ações e de destino.

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


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Destinos para as sessões de evento de base de dados SQL

Seguem-se destinos que podem capturar resultados a partir do seu sessões de evento na base de dados do SQL Server:

- [Destino de memória intermédia de anel](http://msdn.microsoft.com/library/ff878182.aspx) -brevemente contém dados de eventos na memória.
- [Destino de contador do evento](http://msdn.microsoft.com/library/ff878025.aspx) -contagens de todos os eventos que ocorrem durante uma sessão de eventos expandidos.
- [Destino do ficheiro de evento](http://msdn.microsoft.com/library/ff878115.aspx) -contentor de armazenamento do Azure de tooan de memórias intermédias concluída escritas.

Olá [rastreio de eventos para o Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API não está disponível para eventos expandidos na base de dados do SQL Server.

## <a name="restrictions"></a>Restrições

Existem algumas diferenças relacionadas com segurança befitting ambiente de nuvem Olá da base de dados do SQL Server:

- Eventos expandidos são founded no modelo de isolamento de inquilino único Olá. Uma sessão do evento na base de dados de um não é possível aceder a dados ou eventos de outra base de dados.
- Não é possível emitir uma **eventos criar sessão** instrução no contexto de Olá Olá **mestre** base de dados.

## <a name="permission-model"></a>Modelo de permissão

Tem de ter **controlo** permissão tooissue de base de dados de Olá um **eventos criar sessão** instrução. o proprietário da base de dados de Olá (dbo) tem **controlo** permissão.

### <a name="storage-container-authorizations"></a>Autorizações de contentor de armazenamento

token SAS de Olá gerar para o contentor de armazenamento do Azure tem de especificar **rwl** permissões Olá. Olá **rwl** valor fornece Olá as seguintes permissões:

- Leitura
- Escrita
- Lista

## <a name="performance-considerations"></a>Considerações de desempenho

Existem cenários onde utilização intensiva de eventos expandidos pode acumular ativa mais memória do que está em bom estado de Olá geral do sistema. Por conseguinte Olá sistema da base de dados do Azure SQL dinamicamente define e ajusta limites na quantidade de Olá de memória de Active Directory que pode ser acumulada por uma sessão do evento. Vários fatores tecnológica de cálculo dinâmica Olá.

Se receber uma mensagem de erro que indica que uma memória máxima tivesse sido imposta, algumas ações corretivas que pode tomar são:

- Execute menos sessões de evento em simultâneo.
- Através do seu **criar** e **ALTER** instruções para sessões de evento, reduzir a quantidade de Olá de memória que especificar no Olá **máximo\_memória** cláusula.

### <a name="network-latency"></a>Latência de rede

Olá **ficheiro eventos** destino pode ocorrer a latência de rede ou falhas ao tooAzure de dados persistentes blobs de armazenamento. Outros eventos na base de dados do SQL Server podem sofrer um atraso enquanto que terão de aguardar toocomplete de comunicação de rede Olá. Este atraso pode abrandar a sua carga de trabalho.

- toomitigate este desempenho risco, evite definir Olá **EVENT_RETENTION_MODE** opção demasiado**NO_EVENT_LOSS** nas definições de sessão do evento.

## <a name="related-links"></a>Ligações relacionadas

- [Utilizar o Azure PowerShell com o Storage do Azure](../storage/common/storage-powershell-guide-full.md).
- [Cmdlets de armazenamento do Azure](http://msdn.microsoft.com/library/dn806401.aspx)
- [Com o Azure PowerShell com o Storage do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço Storage do Azure.
- [Como toouse Blob storage do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CRIAR a sessão do evento (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Mensagens do blogue de Jonathan Kehayias sobre eventos expandidos no Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Olá, Azure *atualizações de serviço* página Web, narrowed pelo parâmetro tooAzure base de dados SQL:
    - [https://Azure.microsoft.com/Updates/?Service=SQL-Database](https://azure.microsoft.com/updates/?service=sql-database)


Outros tópicos de exemplo de código para expandida eventos estão disponíveis em Olá seguintes ligações. No entanto, tem de verificar regularmente qualquer toosee exemplo se exemplo Olá está direcionada para Microsoft SQL Server em comparação com a SQL Database do Azure. Em seguida, pode decidir se a pequenas alterações são exemplo de Olá toorun necessários.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
