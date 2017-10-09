---
title: "ferramenta de tarefas do aaaHow toouninstall base de dados elástica"
description: "Como toouninstall Olá a ferramenta de tarefas de bases de dados elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Desinstalar componentes de tarefas da base de dados elástica
**As tarefas de base de dados elásticas** componentes podem ser desinstalados através do Portal de Olá ou PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Desinstalar componentes de tarefas de bases de dados elásticas com Olá portal do Azure
1. Abra Olá [portal do Azure](https://portal.azure.com/).
2. Navegue toohello subscrição que contém **tarefas de bases de dados elásticas** componentes, nomeadamente Olá subscrição na base de dados elásticas foram instalados componentes de tarefas.
3. Clique em **procurar** e clique em **grupos de recursos**.
4. Grupo de recursos de Olá selecione com o nome "__ElasticDatabaseJob".
5. Elimine grupo de recursos de Olá.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Desinstalar componentes de tarefas de bases de dados elásticas com o PowerShell
1. Inicie uma janela de comandos do PowerShell do Microsoft Azure e navegue toohello ferramentas subdiretório sob a pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x Olá: tipo **cd ferramentas**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > Ferramentas de cd
2. Execute script do PowerShell Olá.\UninstallElasticDatabaseJobs.ps1.
   
     PS c:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > ficheiro de desbloqueio.\UninstallElasticDatabaseJobs.ps1 PS c\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1

Ou simplesmente, executar Olá script a seguir, partindo do princípio de predefinição valores onde utilizado numa instalação dos componentes de Olá:

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Passos seguintes
tarefas de bases de dados elásticas toore instalação, consulte [instalar o serviço de tarefas de bases de dados elásticas Olá](sql-database-elastic-jobs-service-installation.md)

Para obter uma descrição geral das tarefas de bases de dados elásticas, consulte [descrição geral de tarefas de bases de dados elásticas](sql-database-elastic-jobs-overview.md).

<!--Image references-->


