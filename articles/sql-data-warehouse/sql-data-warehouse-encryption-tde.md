---
title: "aaaTransparent encriptação de dados no SQL Data Warehouse (Portal) | Microsoft Docs"
description: "Encriptação de dados transparente (TDE) no SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="33a41-103">Começar com transparente dados encriptação (TDE) no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="33a41-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33a41-104">Descrição geral de segurança</span><span class="sxs-lookup"><span data-stu-id="33a41-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="33a41-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="33a41-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="33a41-106">Encriptação (Portal)</span><span class="sxs-lookup"><span data-stu-id="33a41-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="33a41-107">Encriptação (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="33a41-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="33a41-108">Permssions necessária</span><span class="sxs-lookup"><span data-stu-id="33a41-108">Required Permssions</span></span>
<span data-ttu-id="33a41-109">tooenable encriptação de dados transparente (TDE), tem de ser um administrador ou membro da função de dbmanager Olá.</span><span class="sxs-lookup"><span data-stu-id="33a41-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="33a41-110">Ativar a encriptação</span><span class="sxs-lookup"><span data-stu-id="33a41-110">Enabling Encryption</span></span>
<span data-ttu-id="33a41-111">tooenable TDE para um SQL Data Warehouse, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="33a41-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="33a41-112">Base de dados de Olá aberta no Olá [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="33a41-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="33a41-113">No painel da base de dados de Olá, clique em Olá **definições** botão</span><span class="sxs-lookup"><span data-stu-id="33a41-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="33a41-114">Selecione Olá **encriptação transparente de dados** opção![][1]</span><span class="sxs-lookup"><span data-stu-id="33a41-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="33a41-115">Selecione Olá **no** definição![][2]</span><span class="sxs-lookup"><span data-stu-id="33a41-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="33a41-116">Selecione **guardar**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="33a41-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="33a41-117">A desativação da encriptação</span><span class="sxs-lookup"><span data-stu-id="33a41-117">Disabling Encryption</span></span>
<span data-ttu-id="33a41-118">toodisable TDE para um SQL Data Warehouse, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="33a41-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="33a41-119">Base de dados de Olá aberta no Olá [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="33a41-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="33a41-120">No painel da base de dados de Olá, clique em Olá **definições** botão</span><span class="sxs-lookup"><span data-stu-id="33a41-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="33a41-121">Selecione Olá **encriptação transparente de dados** opção![][1]</span><span class="sxs-lookup"><span data-stu-id="33a41-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="33a41-122">Selecione Olá **desativar** definição![][4]</span><span class="sxs-lookup"><span data-stu-id="33a41-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="33a41-123">Selecione **guardar**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="33a41-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="33a41-124">Encriptação DMVs</span><span class="sxs-lookup"><span data-stu-id="33a41-124">Encryption DMVs</span></span>
<span data-ttu-id="33a41-125">Encriptação pode ser confirmada com Olá DMVs os seguintes:</span><span class="sxs-lookup"><span data-stu-id="33a41-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="33a41-126">[Databases]</span><span class="sxs-lookup"><span data-stu-id="33a41-126">[sys.databases]</span></span>
* <span data-ttu-id="33a41-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="33a41-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[Databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
