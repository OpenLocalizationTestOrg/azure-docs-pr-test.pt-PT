---
title: "aaaManage bases de dados do SQL do Azure através da automatização do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automatização do Azure pode ser utilizados toomanage bases de dados de SQL do Azure à escala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="dde76-103">Gerir bases de dados do SQL do Azure através da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="dde76-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="dde76-104">Este guia irá apresentar toohello serviço de automatização do Azure e como pode ser utilizado toosimplify gestão das bases de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="dde76-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="dde76-105">O que é a Automatização do Azure?</span><span class="sxs-lookup"><span data-stu-id="dde76-105">What is Azure Automation?</span></span>
<span data-ttu-id="dde76-106">[A automatização do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar a gestão de nuvem através de automatização de processos.</span><span class="sxs-lookup"><span data-stu-id="dde76-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="dde76-107">Tarefas de longa execução, manuais, propensas ao erro e frequentemente repetidas através da automatização do Azure, podem ser automatizada tooincrease fiabilidade, eficiência e toovalue de tempo para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="dde76-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="dde76-108">A automatização do Azure fornece um motor de execução do fluxo de trabalho altamente fiáveis e elevada disponibilidade que ajusta às suas necessidades de toomeet à medida que aumenta a sua organização.</span><span class="sxs-lookup"><span data-stu-id="dde76-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="dde76-109">Na automatização do Azure, os processos podem ser arrancou manualmente, por sistemas de terceiros 3rd ou em intervalos agendados para que as tarefas acontecer exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="dde76-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="dde76-110">Reduzir a sobrecarga operacional e libertar IT / toofocus de pessoal de DevOps no trabalho que adiciona o valor de negócio, movendo a sua toobe de tarefas de gestão de nuvem são executadas automaticamente pela automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="dde76-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="dde76-111">Como pode que o automatização do Azure ajuda a gerir bases de dados SQL do Azure?</span><span class="sxs-lookup"><span data-stu-id="dde76-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="dde76-112">Base de dados SQL do Azure podem ser gerido na automatização do Azure utilizando Olá [cmdlets do PowerShell de base de dados do SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) que estão disponíveis no Olá [ferramentas do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dde76-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="dde76-113">A automatização do Azure tem estes cmdlets PowerShell de base de dados SQL do Azure disponíveis Box Olá, para que possam executar todas as tarefas de gestão de BD do SQL no âmbito do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="dde76-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="dde76-114">Também pode ser emparelhado estes cmdlets na automatização do Azure com cmdlets de Olá para outros serviços do Azure, as tarefas complexas tooautomate através de serviços do Azure e 3rd sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="dde76-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="dde76-115">A automatização do Azure também tem Olá capacidade toocommunicate com servidores SQL diretamente, ao emitir comandos SQL com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dde76-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="dde76-116">Olá [Galeria de runbooks de automatização do Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contém uma variedade de produto equipa e da Comunidade runbooks tooget iniciado a automatizar a gestão de bases de dados do Azure SQL, outros serviços do Azure e 3rd sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="dde76-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="dde76-117">Galeria runbooks incluem:</span><span class="sxs-lookup"><span data-stu-id="dde76-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="dde76-118">Executar consultas do SQL Server em relação a uma base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="dde76-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="dde76-119">Aumentar verticalmente (ou reduzir verticalmente) uma base de dados do SQL do Azure com base numa agenda</span><span class="sxs-lookup"><span data-stu-id="dde76-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="dde76-120">Truncar uma tabela SQL, se a sua base de dados se aproxima o tamanho máximo</span><span class="sxs-lookup"><span data-stu-id="dde76-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="dde76-121">Índice de tabelas numa base de dados SQL do Azure se estes são muito fragmentados</span><span class="sxs-lookup"><span data-stu-id="dde76-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="dde76-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dde76-122">Next steps</span></span>
<span data-ttu-id="dde76-123">Agora que aprendeu as noções básicas de Olá da automatização do Azure e como pode ser utilizado toomanage bases de dados de SQL do Azure, siga estas toolearn ligações mais sobre a automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="dde76-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="dde76-124">Descrição geral da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="dde76-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="dde76-125">O meu primeiro runbook</span><span class="sxs-lookup"><span data-stu-id="dde76-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="dde76-126">Mapa de aprendizagem de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="dde76-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="dde76-127">Automatização do Azure: O SQL Server Agent no Olá na nuvem</span><span class="sxs-lookup"><span data-stu-id="dde76-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

