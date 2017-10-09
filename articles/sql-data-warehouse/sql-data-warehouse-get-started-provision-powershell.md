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
# <a name="create-sql-data-warehouse-using-powershell"></a>Criar SQL Data Warehouse com o PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este artigo mostra como toocreate um SQL Server do armazém de dados com o PowerShell.

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciada, é necessário:

* **Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do MSDN Azure] [ MSDN Azure Credits] toocreate uma conta.
* **O servidor SQL do Azure**: consulte [criar uma base de dados SQL do Azure no Portal do Azure de Olá] [ Create an Azure SQL database in hello Azure Portal] ou [criar uma base de dados SQL do Azure com o PowerShell] [ Create an Azure SQL database with PowerShell] para obter mais detalhes.
* **Grupo de recursos**: Utilize Olá mesmo recurso do grupo do Azure SQL Server ou consulte [como um grupo de recursos de toocreate](../azure-resource-manager/resource-group-portal.md).
* **PowerShell, versão 1.0.3 ou superior**: pode verificar a sua versão, executando **Get-Module -ListAvailable -Name Azure**.  versão mais recente Olá pode ser instalado na [instalador de plataforma Web Microsoft][Microsoft Web Platform Installer].  Para obter mais informações sobre como instalar a versão mais recente Olá, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> A criação de um SQL Data Warehouse poderá resultar num novo serviço sujeito a faturação.  Consulte [SQL Data Warehouse pricing (Preços do SQL Data Warehouse)][SQL Data Warehouse pricing], para mais detalhes sobre preços.
>
>

## <a name="create-a-sql-data-warehouse"></a>Criar um SQL Data Warehouse
1. Abra o Windows PowerShell.
2. Execute este tooAzure toologin de cmdlet do Resource Manager.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Selecione a subscrição de Olá toouse que pretende para a sua sessão atual.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Crie a base de dados. Este exemplo cria uma base de dados com o nome "mynewsqldw", com o objetivo de nível de serviço "DW400", servidor de toohello com o nome "sqldwserver1", que está no grupo de recursos de Olá com o nome "mywesteuroperesgp1".

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Os parâmetros necessários são:

* **RequestedServiceObjectiveName**: quantidade de Olá de [DWU] [ DWU] que está a pedir.  Os valores suportados são DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 e DW6000.
* **DatabaseName**: nome Olá Olá SQL Data Warehouse que está a criar.
* **ServerName**: nome de hello do servidor de Olá que está a utilizar para a criação (tem de ser V12).
* **ResourceGroupName**: o grupo de recursos que está a utilizar.  os grupos de recursos disponíveis toofind na sua subscrição, utilize Get-AzureResource.
* **Edição**: tem de ser "DataWarehouse" toocreate um SQL Data Warehouse.

Os parâmetros opcionais são:

* **CollationName**: Olá agrupamento com o predefinido se não for especificado é SQL_Latin1_General_CP1_CI_AS.  Não é possível alterar o agrupamento numa base de dados.
* **MaxSizeBytes**: Olá predefinido o tamanho máximo de uma base de dados é de 10 GB.

Para obter mais detalhes sobre as opções de parâmetro de Olá, consulte [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] e [criar base de dados (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Passos seguintes
Após terminar o SQL Data Warehouse aprovisionamento poderá pretender tootry [carregar dados de exemplo] [ loading sample data] ou verificar como demasiado[desenvolver] [ develop] , [carregar][load], ou [migrar][migrate].

Se estiver interessado em obter mais informações sobre como toomanage SQL Data Warehouse através de programação, consulte nosso artigo sobre como toouse [cmdlets do PowerShell e REST APIs][PowerShell cmdlets and REST APIs].

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
