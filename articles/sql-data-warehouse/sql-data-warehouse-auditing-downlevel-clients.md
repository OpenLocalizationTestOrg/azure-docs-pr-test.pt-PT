---
title: "os clientes de nível inferior do armazém de dados aaaSQL suportem para auditoria de dados | Microsoft Docs"
description: "Saiba mais sobre o suporte de clientes de nível inferior do armazém de dados do SQL Server para auditoria de dados"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="cb8c3-103">Suportem de clientes de nível inferior do armazém de dados do SQL Server - para máscara de dados de auditoria e dinâmicos</span><span class="sxs-lookup"><span data-stu-id="cb8c3-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="cb8c3-104">[Auditoria](sql-data-warehouse-auditing-overview.md) funciona com os clientes de SQL que suportam redirecionamento de TDS.</span><span class="sxs-lookup"><span data-stu-id="cb8c3-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="cb8c3-105">Qualquer cliente que implementa TDS 7.4 também deve suportar redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="cb8c3-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="cb8c3-106">Exceções toothis incluem JDBC 4.0 no qual o recurso redirecionamento Olá não é totalmente suportado e Tedious do Node.JS em que o redirecionamento não foi implementado.</span><span class="sxs-lookup"><span data-stu-id="cb8c3-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="cb8c3-107">"Em clientes de", ou seja, que suportam TDS versão 7.3 e abaixo - Olá FQDN do servidor na cadeia de ligação de Olá deverá ser modificado:</span><span class="sxs-lookup"><span data-stu-id="cb8c3-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="cb8c3-108">Original FQDN do servidor na cadeia de ligação de Olá: <*nome do servidor*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb8c3-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="cb8c3-109">Modificação FQDN do servidor na cadeia de ligação de Olá: <*nome do servidor*> .database. **segura**. windows.net</span><span class="sxs-lookup"><span data-stu-id="cb8c3-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="cb8c3-110">Uma lista parcial de "Clientes de nível inferior" inclui:</span><span class="sxs-lookup"><span data-stu-id="cb8c3-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="cb8c3-111">O .NET 4.0 e abaixo</span><span class="sxs-lookup"><span data-stu-id="cb8c3-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="cb8c3-112">ODBC 10.0 e abaixo.</span><span class="sxs-lookup"><span data-stu-id="cb8c3-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="cb8c3-113">JDBC (enquanto JDBC suporta TDS 7.4, Olá funcionalidade de redirecionamento do TDS não é totalmente suportada)</span><span class="sxs-lookup"><span data-stu-id="cb8c3-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="cb8c3-114">Tedious (para Node.JS)</span><span class="sxs-lookup"><span data-stu-id="cb8c3-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="cb8c3-115">**Remark:** Olá acima modificação do FDQN de servidor pode ser úteis para além disso, para aplicar uma política de auditoria de nível de servidor de SQL, sem necessidade de uma configuração passo em cada base de dados (mitigação temporária).</span><span class="sxs-lookup"><span data-stu-id="cb8c3-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

