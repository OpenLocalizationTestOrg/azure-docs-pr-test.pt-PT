---
title: "as credenciais de aaaManaging na biblioteca de clientes de base de dados elástica Olá | Microsoft Docs"
description: "Como tooset Olá nível adequado de credenciais, administrador tooread só, para aplicações de base de dados elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>As credenciais utilizadas biblioteca de clientes do tooaccess Olá base de dados elástica
Olá [biblioteca de clientes de base de dados elástica](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) utiliza três tipos diferentes de Olá de tooaccess credenciais [Gestor de mapa de partições horizontais](sql-database-elastic-scale-shard-map-management.md). Consoante a necessidade de Olá, utilize credencial de Olá com o nível mais baixo de Olá de possíveis de acesso.

* **Credenciais de gestão**: para criar ou manipular um Gestor de mapa de partições horizontais. (Consulte Olá [glossário](sql-database-elastic-scale-glossary.md).) 
* **Aceder às credenciais**: tooaccess um ID de partição horizontal existente mapear informações do Gestor de tooobtain sobre shards.
* **As credenciais de ligação**: tooconnect tooshards. 

Consulte também [gerir bases de dados e inícios de sessão SQL Database do Azure](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Sobre as credenciais de gestão
Credenciais de gestão são utilizado toocreate um [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) objeto para as aplicações que manipular mapas de partições horizontais. (Por exemplo, consulte [adição de uma partição horizontal com as ferramentas de base de dados elástica](sql-database-elastic-scale-add-a-shard.md) e [dados dependentes encaminhamento](sql-database-elastic-scale-data-dependent-routing.md)) utilizador Olá da biblioteca de clientes do dimensionamento elástico Olá cria os utilizadores do SQL Server de Olá e inícios de sessão do SQL Server e certifica-se de cada uma é concedidos permissões de leitura/escrita Olá no ID de partição horizontal global Olá mapeiam a base de dados e todas as partições horizontais bases de dados bem. Estas credenciais são mapa de partições horizontais global de Olá toomaintain utilizado e mapas de partições horizontais local Olá quando forem efetuadas alterações toohello partições horizontais mapa. Por exemplo, utilize Olá gestão credenciais toocreate Olá partições horizontais mapa objecto do Gestor de (utilizando [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

variável de Olá **smmAdminConnectionString** é uma cadeia de ligação que contém as credenciais de gestão de Olá. Olá ID de utilizador e palavra-passe fornece a base de dados de leitura/escrita acesso tooboth partições horizontais mapa e shards individuais. cadeia de ligação de gestão de Olá também inclui Olá servidor nome e a base de dados nome tooidentify Olá partições horizontais global mapa da base de dados. Eis uma cadeia de ligação típico para essa finalidade:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Não utilize valores no formulário de Olá de "username@server" — em vez disso, basta utilizar o valor de "nomedeutilizador" Olá.  Isto acontece porque as credenciais tem de trabalhar contra Olá a base de dados de Gestor de mapa do ID de partição horizontal e shards individuais, o que poderão estar em servidores diferentes.

## <a name="access-credentials"></a>Credenciais de acesso
Quando criar um ID de partição horizontal mapa manager numa aplicação que não administrar partições horizontais maps, utilize as credenciais que têm permissões só de leitura no mapa de partições horizontais global Olá. Olá informações obtidas a partir de mapa de partições horizontais global Olá estas credenciais são utilizadas para [encaminhamento de dados dependentes](sql-database-elastic-scale-data-dependent-routing.md) e toopopulate Olá ID de partição horizontal cache no cliente Olá do mapa. Olá credenciais são fornecidas através de Olá mesmo chamar padrão demasiado**GetSqlShardMapManager** conforme mostrado acima: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Tenha em atenção a utilização de Olá de Olá **smmReadOnlyConnectionString** tooreflect Olá utilização credenciais diferentes para este acesso em nome de **não admin** utilizadores: estas credenciais não devem fornecer escrita permissões no mapa de partições horizontais global Olá. 

## <a name="connection-credentials"></a>Credenciais de ligação
Credenciais adicionais necessários ao utilizar Olá [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) método tooaccess uma partição horizontal associado com uma chave de fragmentação. Estas credenciais têm tooprovide permissões para acesso só de leitura toohello partições horizontais local mapa as tabelas que reside no ID de partição horizontal Olá. Esta é a validação da ligação tooperform necessários para o encaminhamento de dados dependentes no ID de partição horizontal Olá. Este fragmento de código permite o acesso de dados no contexto de Olá de dados dependentes encaminhamento: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

Neste exemplo, **smmUserConnectionString** contém a cadeia de ligação de Olá para Olá credenciais de utilizador. Para a BD SQL do Azure, é uma cadeia de ligação típicos para as credenciais de utilizador: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Tal como acontece com as credenciais de administrador Olá, não os valores no formulário de Olá de "username@server". Em alternativa, utilize "nomedeutilizador" apenas.  Note também que cadeia de ligação de Olá não contém um nome de servidor e um nome de base de dados. Isto acontece porque Olá **OpenConnectionForKey** chamada irá encaminhar automaticamente Olá ligação toohello partições horizontais com base na chave de Olá correto. Por conseguinte, nome de base de dados de Olá e nome do servidor não são fornecidos. 

## <a name="see-also"></a>Consultar também
[Gerir bases de dados e inícios de sessão na Base de Dados SQL do Azure](sql-database-manage-logins.md)

[Securing your SQL Database (Proteger a sua Base de Dados SQL)](sql-database-security-overview.md)

[Introdução às tarefas de base de dados elástica](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

