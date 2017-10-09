---
title: aaaCreate SQL Data Warehouse com o PowerShell | Microsoft Docs
description: Criar SQL Data Warehouse com o PowerShell
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="86d64-103">Criar SQL Data Warehouse com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="86d64-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86d64-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="86d64-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="86d64-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="86d64-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="86d64-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86d64-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="86d64-107">Este artigo mostra como toocreate um SQL Server do armazém de dados com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86d64-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86d64-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86d64-108">Prerequisites</span></span>
<span data-ttu-id="86d64-109">tooget iniciada, é necessário:</span><span class="sxs-lookup"><span data-stu-id="86d64-109">tooget started, you need:</span></span>

* <span data-ttu-id="86d64-110">**Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do MSDN Azure] [ MSDN Azure Credits] toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="86d64-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="86d64-111">**O servidor SQL do Azure**: consulte [criar uma base de dados SQL do Azure no Portal do Azure de Olá] [ Create an Azure SQL database in hello Azure Portal] ou [criar uma base de dados SQL do Azure com o PowerShell] [ Create an Azure SQL database with PowerShell] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="86d64-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="86d64-112">**Grupo de recursos**: Utilize Olá mesmo recurso do grupo do Azure SQL Server ou consulte [como um grupo de recursos de toocreate](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="86d64-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="86d64-113">**PowerShell, versão 1.0.3 ou superior**: pode verificar a sua versão, executando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="86d64-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="86d64-114">versão mais recente Olá pode ser instalado na [instalador de plataforma Web Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="86d64-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="86d64-115">Para obter mais informações sobre como instalar a versão mais recente Olá, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="86d64-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="86d64-116">A criação de um SQL Data Warehouse poderá resultar num novo serviço sujeito a faturação.</span><span class="sxs-lookup"><span data-stu-id="86d64-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="86d64-117">Consulte [SQL Data Warehouse pricing (Preços do SQL Data Warehouse)][SQL Data Warehouse pricing], para mais detalhes sobre preços.</span><span class="sxs-lookup"><span data-stu-id="86d64-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="86d64-118">Criar um SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="86d64-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="86d64-119">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86d64-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="86d64-120">Execute este tooAzure toologin de cmdlet do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86d64-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="86d64-121">Selecione a subscrição de Olá toouse que pretende para a sua sessão atual.</span><span class="sxs-lookup"><span data-stu-id="86d64-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="86d64-122">Crie a base de dados.</span><span class="sxs-lookup"><span data-stu-id="86d64-122">Create database.</span></span> <span data-ttu-id="86d64-123">Este exemplo cria uma base de dados com o nome "mynewsqldw", com o objetivo de nível de serviço "DW400", servidor de toohello com o nome "sqldwserver1", que está no grupo de recursos de Olá com o nome "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="86d64-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="86d64-124">Os parâmetros necessários são:</span><span class="sxs-lookup"><span data-stu-id="86d64-124">Required Parameters are:</span></span>

* <span data-ttu-id="86d64-125">**RequestedServiceObjectiveName**: quantidade de Olá de [DWU] [ DWU] que está a pedir.</span><span class="sxs-lookup"><span data-stu-id="86d64-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="86d64-126">Os valores suportados são DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 e DW6000.</span><span class="sxs-lookup"><span data-stu-id="86d64-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="86d64-127">**DatabaseName**: nome Olá Olá SQL Data Warehouse que está a criar.</span><span class="sxs-lookup"><span data-stu-id="86d64-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="86d64-128">**ServerName**: nome de hello do servidor de Olá que está a utilizar para a criação (tem de ser V12).</span><span class="sxs-lookup"><span data-stu-id="86d64-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="86d64-129">**ResourceGroupName**: o grupo de recursos que está a utilizar.</span><span class="sxs-lookup"><span data-stu-id="86d64-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="86d64-130">os grupos de recursos disponíveis toofind na sua subscrição, utilize Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="86d64-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="86d64-131">**Edição**: tem de ser "DataWarehouse" toocreate um SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="86d64-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="86d64-132">Os parâmetros opcionais são:</span><span class="sxs-lookup"><span data-stu-id="86d64-132">Optional Parameters are:</span></span>

* <span data-ttu-id="86d64-133">**CollationName**: Olá agrupamento com o predefinido se não for especificado é SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="86d64-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="86d64-134">Não é possível alterar o agrupamento numa base de dados.</span><span class="sxs-lookup"><span data-stu-id="86d64-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="86d64-135">**MaxSizeBytes**: Olá predefinido o tamanho máximo de uma base de dados é de 10 GB.</span><span class="sxs-lookup"><span data-stu-id="86d64-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="86d64-136">Para obter mais detalhes sobre as opções de parâmetro de Olá, consulte [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] e [criar base de dados (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="86d64-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="86d64-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="86d64-137">Next steps</span></span>
<span data-ttu-id="86d64-138">Após terminar o SQL Data Warehouse aprovisionamento poderá pretender tootry [carregar dados de exemplo] [ loading sample data] ou verificar como demasiado[desenvolver] [ develop] , [carregar][load], ou [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="86d64-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="86d64-139">Se estiver interessado em obter mais informações sobre como toomanage SQL Data Warehouse através de programação, consulte nosso artigo sobre como toouse [cmdlets do PowerShell e REST APIs][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="86d64-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
