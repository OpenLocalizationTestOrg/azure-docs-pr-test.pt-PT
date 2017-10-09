---
title: aaaDesign sua primeira SQL database do Azure - c# | Microsoft Docs
description: Saiba mais toodesign a sua primeira base de dados SQL do Azure e ligar tooit com um programa c# ADO.NET a utilizar.
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="7e190-103">Estruturar uma base de dados SQL do Azure e estabelecer ligação com C & #x; e ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7e190-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="7e190-104">Base de dados SQL do Azure é um relacional da base de dados como um serviço (DBaaS) no Olá Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="7e190-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="7e190-105">Neste tutorial, saiba como toouse Olá portal do Azure e ADO.NET com o Visual Studio para:</span><span class="sxs-lookup"><span data-stu-id="7e190-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7e190-106">Criar uma base de dados no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7e190-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="7e190-107">Configurar uma regra de firewall ao nível do servidor no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7e190-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="7e190-108">Ligar a base de dados toohello com ADO.NET e o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e190-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="7e190-109">Criar tabelas com ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7e190-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="7e190-110">Inserir, atualizar e eliminar os dados com ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7e190-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="7e190-111">Consultar dados ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7e190-111">Query data ADO.NET</span></span>

<span data-ttu-id="7e190-112">Se não tiver uma subscrição do Azure, [criar uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="7e190-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e190-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7e190-113">Prerequisites</span></span>

<span data-ttu-id="7e190-114">Uma instalação do [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7e190-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="7e190-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7e190-115">Next steps</span></span>

<span data-ttu-id="7e190-116">Neste tutorial, aprendeu a tarefas de base de dados básicas, tais como criar uma base de dados e tabelas, carregar e consultar dados e restaurar Olá da base de dados tooa anterior no tempo.</span><span class="sxs-lookup"><span data-stu-id="7e190-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="7e190-117">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="7e190-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7e190-118">Criar uma base de dados</span><span class="sxs-lookup"><span data-stu-id="7e190-118">Create a database</span></span>
> * <span data-ttu-id="7e190-119">Configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="7e190-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="7e190-120">Ligar a base de dados de toohello com [Visual Studio e c#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="7e190-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="7e190-121">Criar tabelas</span><span class="sxs-lookup"><span data-stu-id="7e190-121">Create tables</span></span>
> * <span data-ttu-id="7e190-122">Inserir, atualizar e eliminar dados</span><span class="sxs-lookup"><span data-stu-id="7e190-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="7e190-123">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="7e190-123">Query data</span></span>

<span data-ttu-id="7e190-124">Produzir toohello seguinte toolearn tutorial sobre como migrar os dados.</span><span class="sxs-lookup"><span data-stu-id="7e190-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="7e190-125">Migrar o tooAzure de base de dados do SQL Server da base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="7e190-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

