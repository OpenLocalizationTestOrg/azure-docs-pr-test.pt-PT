---
title: "aaaEnable encriptação transparente de dados para a Stretch Database - Azure | Microsoft Docs"
description: "Ativar a encriptação de dados transparente (TDE) para o SQL Server Stretch Database no Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="6f2f9-103">Ativar a encriptação de dados transparente (TDE) para a Stretch Database no Azure</span><span class="sxs-lookup"><span data-stu-id="6f2f9-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f2f9-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6f2f9-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="6f2f9-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="6f2f9-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="6f2f9-106">Encriptação de dados transparente (TDE) ajuda a proteger contra ameaças de Olá de atividade maliciosa através de encriptação em tempo real e a desencriptação da base de dados de Olá, cópias de segurança associadas e os ficheiros de registo de transações Inativos sem necessidade de alterações toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="6f2f9-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="6f2f9-107">TDE encripta armazenamento Olá de uma base de dados completo com uma chave de encriptação da base de dados de Olá chamado de chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="6f2f9-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="6f2f9-108">chave de encriptação de base de dados de Olá está protegido por um certificado de servidor incorporada.</span><span class="sxs-lookup"><span data-stu-id="6f2f9-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="6f2f9-109">certificado de servidor incorporada Olá é exclusivo para cada servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2f9-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="6f2f9-110">Microsoft roda automaticamente estes certificados, pelo menos, todos os 90 dias.</span><span class="sxs-lookup"><span data-stu-id="6f2f9-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="6f2f9-111">Para obter uma descrição geral de TDE, consulte [encriptação de dados transparente (TDE)].</span><span class="sxs-lookup"><span data-stu-id="6f2f9-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="6f2f9-112">Ativar a encriptação</span><span class="sxs-lookup"><span data-stu-id="6f2f9-112">Enabling Encryption</span></span>
<span data-ttu-id="6f2f9-113">tooenable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="6f2f9-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="6f2f9-114">Base de dados de Olá aberta no Olá [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6f2f9-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="6f2f9-115">No painel da base de dados de Olá, clique em Olá **definições** botão</span><span class="sxs-lookup"><span data-stu-id="6f2f9-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="6f2f9-116">Selecione Olá **encriptação transparente de dados** opção![][1]</span><span class="sxs-lookup"><span data-stu-id="6f2f9-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="6f2f9-117">Selecione Olá **no** definição e, em seguida, selecione **guardar**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="6f2f9-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="6f2f9-118">A desativação da encriptação</span><span class="sxs-lookup"><span data-stu-id="6f2f9-118">Disabling Encryption</span></span>
<span data-ttu-id="6f2f9-119">toodisable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="6f2f9-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="6f2f9-120">Base de dados de Olá aberta no Olá [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6f2f9-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="6f2f9-121">No painel da base de dados de Olá, clique em Olá **definições** botão</span><span class="sxs-lookup"><span data-stu-id="6f2f9-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="6f2f9-122">Selecione Olá **encriptação transparente de dados** opção</span><span class="sxs-lookup"><span data-stu-id="6f2f9-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="6f2f9-123">Selecione Olá **desativar** definição e, em seguida, selecione **guardar**</span><span class="sxs-lookup"><span data-stu-id="6f2f9-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[encriptação de dados transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
