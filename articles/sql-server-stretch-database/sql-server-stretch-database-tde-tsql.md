---
title: "aaaEnable encriptação transparente de dados para Stretch TSQL de base de dados - Azure | Microsoft Docs"
description: "Ativar a encriptação de dados transparente (TDE) para o SQL Server Stretch Database no TSQL do Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Ativar a encriptação de dados transparente (TDE) para a Stretch Database no Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Encriptação de dados transparente (TDE) ajuda a proteger contra ameaças de Olá de atividade maliciosa através de encriptação em tempo real e a desencriptação da base de dados de Olá, cópias de segurança associadas e os ficheiros de registo de transações Inativos sem necessidade de alterações toohello aplicação.

TDE encripta armazenamento Olá de uma base de dados completo com uma chave de encriptação da base de dados de Olá chamado de chave simétrica. chave de encriptação de base de dados de Olá está protegido por um certificado de servidor incorporada. certificado de servidor incorporada Olá é exclusivo para cada servidor do Azure. Microsoft roda automaticamente estes certificados, pelo menos, todos os 90 dias. Para obter uma descrição geral de TDE, consulte [encriptação de dados transparente (TDE)].

## <a name="enabling-encryption"></a>Ativar a encriptação
tooenable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:

1. Ligar toohello *mestre* base de dados no Olá servidor do Azure alojamento Olá base de dados utilizando um início de sessão que é um administrador ou membro de Olá **dbmanager** função na base de dados mestra Olá
2. Execute Olá seguinte declaração tooencrypt Olá da base de dados.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>A desativação da encriptação
toodisable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:

1. Ligar toohello *mestre* da base de dados utilizando um início de sessão que é um administrador ou membro de Olá **dbmanager** função na base de dados mestra Olá
2. Execute Olá seguinte declaração tooencrypt Olá da base de dados.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Verificar a encriptação
Estado de encriptação tooverify para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:

1. Ligar toohello *mestre* ou base de dados de instância utilizando um início de sessão que é um administrador ou membro de Olá **dbmanager** função na base de dados mestra Olá
2. Execute Olá seguinte declaração tooencrypt Olá da base de dados.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Um resultado de ```1``` indica uma base de dados encriptado, ```0``` indica uma base de dados não encriptados.

<!--Anchors-->
[encriptação de dados transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
