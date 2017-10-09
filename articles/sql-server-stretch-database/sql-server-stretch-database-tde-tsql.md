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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="c1374-103">Ativar a encriptação de dados transparente (TDE) para a Stretch Database no Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="c1374-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1374-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c1374-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="c1374-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="c1374-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="c1374-106">Encriptação de dados transparente (TDE) ajuda a proteger contra ameaças de Olá de atividade maliciosa através de encriptação em tempo real e a desencriptação da base de dados de Olá, cópias de segurança associadas e os ficheiros de registo de transações Inativos sem necessidade de alterações toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="c1374-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="c1374-107">TDE encripta armazenamento Olá de uma base de dados completo com uma chave de encriptação da base de dados de Olá chamado de chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="c1374-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="c1374-108">chave de encriptação de base de dados de Olá está protegido por um certificado de servidor incorporada.</span><span class="sxs-lookup"><span data-stu-id="c1374-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="c1374-109">certificado de servidor incorporada Olá é exclusivo para cada servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1374-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="c1374-110">Microsoft roda automaticamente estes certificados, pelo menos, todos os 90 dias.</span><span class="sxs-lookup"><span data-stu-id="c1374-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="c1374-111">Para obter uma descrição geral de TDE, consulte [encriptação de dados transparente (TDE)].</span><span class="sxs-lookup"><span data-stu-id="c1374-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="c1374-112">Ativar a encriptação</span><span class="sxs-lookup"><span data-stu-id="c1374-112">Enabling Encryption</span></span>
<span data-ttu-id="c1374-113">tooenable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="c1374-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="c1374-114">Ligar toohello *mestre* base de dados no Olá servidor do Azure alojamento Olá base de dados utilizando um início de sessão que é um administrador ou membro de Olá **dbmanager** função na base de dados mestra Olá</span><span class="sxs-lookup"><span data-stu-id="c1374-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="c1374-115">Execute Olá seguinte declaração tooencrypt Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="c1374-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="c1374-116">A desativação da encriptação</span><span class="sxs-lookup"><span data-stu-id="c1374-116">Disabling Encryption</span></span>
<span data-ttu-id="c1374-117">toodisable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="c1374-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="c1374-118">Ligar toohello *mestre* da base de dados utilizando um início de sessão que é um administrador ou membro de Olá **dbmanager** função na base de dados mestra Olá</span><span class="sxs-lookup"><span data-stu-id="c1374-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="c1374-119">Execute Olá seguinte declaração tooencrypt Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="c1374-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="c1374-120">Verificar a encriptação</span><span class="sxs-lookup"><span data-stu-id="c1374-120">Verifying Encryption</span></span>
<span data-ttu-id="c1374-121">Estado de encriptação tooverify para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="c1374-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="c1374-122">Ligar toohello *mestre* ou base de dados de instância utilizando um início de sessão que é um administrador ou membro de Olá **dbmanager** função na base de dados mestra Olá</span><span class="sxs-lookup"><span data-stu-id="c1374-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="c1374-123">Execute Olá seguinte declaração tooencrypt Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="c1374-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="c1374-124">Um resultado de ```1``` indica uma base de dados encriptado, ```0``` indica uma base de dados não encriptados.</span><span class="sxs-lookup"><span data-stu-id="c1374-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[encriptação de dados transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
