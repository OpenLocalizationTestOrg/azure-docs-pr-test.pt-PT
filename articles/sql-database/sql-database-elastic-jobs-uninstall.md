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
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="d7805-103">Desinstalar componentes de tarefas da base de dados elástica</span><span class="sxs-lookup"><span data-stu-id="d7805-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="d7805-104">**As tarefas de base de dados elásticas** componentes podem ser desinstalados através do Portal de Olá ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7805-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="d7805-105">Desinstalar componentes de tarefas de bases de dados elásticas com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d7805-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="d7805-106">Abra Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d7805-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d7805-107">Navegue toohello subscrição que contém **tarefas de bases de dados elásticas** componentes, nomeadamente Olá subscrição na base de dados elásticas foram instalados componentes de tarefas.</span><span class="sxs-lookup"><span data-stu-id="d7805-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="d7805-108">Clique em **procurar** e clique em **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d7805-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="d7805-109">Grupo de recursos de Olá selecione com o nome "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="d7805-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="d7805-110">Elimine grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7805-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="d7805-111">Desinstalar componentes de tarefas de bases de dados elásticas com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7805-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="d7805-112">Inicie uma janela de comandos do PowerShell do Microsoft Azure e navegue toohello ferramentas subdiretório sob a pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x Olá: tipo **cd ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="d7805-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="d7805-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > Ferramentas de cd</span><span class="sxs-lookup"><span data-stu-id="d7805-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="d7805-114">Execute script do PowerShell Olá.\UninstallElasticDatabaseJobs.ps1.</span><span class="sxs-lookup"><span data-stu-id="d7805-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="d7805-115">PS c:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > ficheiro de desbloqueio.\UninstallElasticDatabaseJobs.ps1 PS c\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="d7805-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="d7805-116">Ou simplesmente, executar Olá script a seguir, partindo do princípio de predefinição valores onde utilizado numa instalação dos componentes de Olá:</span><span class="sxs-lookup"><span data-stu-id="d7805-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d7805-117">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d7805-117">Next steps</span></span>
<span data-ttu-id="d7805-118">tarefas de bases de dados elásticas toore instalação, consulte [instalar o serviço de tarefas de bases de dados elásticas Olá](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="d7805-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="d7805-119">Para obter uma descrição geral das tarefas de bases de dados elásticas, consulte [descrição geral de tarefas de bases de dados elásticas](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7805-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


