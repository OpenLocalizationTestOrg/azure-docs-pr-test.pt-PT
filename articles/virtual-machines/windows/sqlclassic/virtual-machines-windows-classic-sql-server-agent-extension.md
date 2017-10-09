---
title: "tarefas de gestão aaaAutomate em VMs do SQL Server (clássica) | Microsoft Docs"
description: "Este tópico descreve como toomanage Olá extensão de agente do SQL Server, que automatiza as tarefas de administração do SQL Server específicas. Estes incluem a cópia de segurança automatizada, a aplicação de patches automatizada e integração do Cofre de chaves do Azure. Este tópico utiliza o modo de implementação clássica Olá."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="b9550-105">Automatizar tarefas de gestão em Azure Virtual Machines com Olá extensão de agente do SQL Server (clássica)</span><span class="sxs-lookup"><span data-stu-id="b9550-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9550-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b9550-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="b9550-107">Clássico</span><span class="sxs-lookup"><span data-stu-id="b9550-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="b9550-108">Olá extensão do agente do SQL Server IaaS (SQLIaaSAgent) é executado em tarefas de administração de tooautomate de máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9550-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="b9550-109">Este tópico fornece uma descrição geral dos serviços de Olá suportados pela extensão de Olá, bem como as instruções para instalação, estado e remoção.</span><span class="sxs-lookup"><span data-stu-id="b9550-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b9550-110">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b9550-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b9550-111">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="b9550-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b9550-112">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9550-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b9550-113">versão do Gestor de recursos de Olá tooview deste artigo, consulte [extensão de agente do SQL Server para o SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b9550-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="b9550-114">Serviços suportados</span><span class="sxs-lookup"><span data-stu-id="b9550-114">Supported services</span></span>
<span data-ttu-id="b9550-115">Olá extensão de agente do SQL Server IaaS suporta Olá seguintes tarefas de administração:</span><span class="sxs-lookup"><span data-stu-id="b9550-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="b9550-116">Funcionalidade de administração</span><span class="sxs-lookup"><span data-stu-id="b9550-116">Administration feature</span></span> | <span data-ttu-id="b9550-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9550-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9550-118">**Cópia de segurança automatizada do SQL**</span><span class="sxs-lookup"><span data-stu-id="b9550-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="b9550-119">Automatiza Olá agendamento de cópias de segurança para todas as bases de dados para a instância de predefinida Olá do SQL Server no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b9550-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="b9550-120">Para obter mais informações, consulte [cópia de segurança automatizada do SQL Server em Virtual Machines do Azure (clássica)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b9550-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="b9550-121">**Aplicação de patches automatizada do SQL**</span><span class="sxs-lookup"><span data-stu-id="b9550-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="b9550-122">Configura uma janela de manutenção durante as atualizações que coloque tooyour VM pode demorar, pelo que pode evitar atualizações durante períodos máximos para a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b9550-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="b9550-123">Para obter mais informações, consulte [aplicação para o SQL Server em Virtual Machines do Azure (clássica) de patches automatizada](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="b9550-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="b9550-124">**Integração do Cofre de Chaves do Azure**</span><span class="sxs-lookup"><span data-stu-id="b9550-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="b9550-125">Permite tooautomatically instalar e configurar o Cofre de chaves do Azure na sua VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b9550-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="b9550-126">Para obter mais informações, consulte [configurar integração do Azure chave de cofre para SQL Server em VMs do Azure (clássica)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="b9550-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="b9550-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9550-127">Prerequisites</span></span>
<span data-ttu-id="b9550-128">Requisitos toouse Olá extensão de agente do SQL Server IaaS na sua VM:</span><span class="sxs-lookup"><span data-stu-id="b9550-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="b9550-129">Sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="b9550-129">Operating System:</span></span>
* <span data-ttu-id="b9550-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b9550-130">Windows Server 2012</span></span>
* <span data-ttu-id="b9550-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b9550-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="b9550-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b9550-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="b9550-133">Versões do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="b9550-133">SQL Server versions:</span></span>
* <span data-ttu-id="b9550-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="b9550-134">SQL Server 2012</span></span>
* <span data-ttu-id="b9550-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="b9550-135">SQL Server 2014</span></span>
* <span data-ttu-id="b9550-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="b9550-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="b9550-137">O Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b9550-137">Azure PowerShell:</span></span>
<span data-ttu-id="b9550-138">[Transferir e configurar os comandos de Azure PowerShell mais recentes Olá](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9550-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="b9550-139">Inicie o Windows PowerShell e ligue-tooyour subscrição do Azure com Olá **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="b9550-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="b9550-140">Se tiver várias subscrições, utilize **Select-AzureSubscription** subscrição de Olá tooselect que contém o seu destino VMS clássicas.</span><span class="sxs-lookup"><span data-stu-id="b9550-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="b9550-141">Neste momento, pode obter uma lista de máquinas de virtuais clássico Olá e os respetivos nomes de serviço associado com Olá **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="b9550-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="b9550-142">Instalação</span><span class="sxs-lookup"><span data-stu-id="b9550-142">Installation</span></span>
<span data-ttu-id="b9550-143">Para VMs clássicas, tem de utilizar o PowerShell tooinstall Olá extensão de agente do SQL Server IaaS e configurar os respetivos serviços associados.</span><span class="sxs-lookup"><span data-stu-id="b9550-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="b9550-144">Olá utilize **conjunto AzureVMSqlServerExtension** extensão de Olá de tooinstall de cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9550-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="b9550-145">Por exemplo, Olá comando a seguir instala a extensão de Olá numa VM do Windows Server (clássica) e de nomes, "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="b9550-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="b9550-146">Se atualizar a versão mais recente do toohello do Olá extensão de agente do SQL Server IaaS, tem de reiniciar a máquina virtual após a atualização da extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9550-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="b9550-147">As máquinas virtuais clássicas não têm uma opção tooinstall e configurar Olá extensão de agente do SQL Server IaaS através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="b9550-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="b9550-148">Estado</span><span class="sxs-lookup"><span data-stu-id="b9550-148">Status</span></span>
<span data-ttu-id="b9550-149">Tooverify unidirecional que a extensão de Olá é instalada é o estado do agente de Olá tooview na Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9550-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="b9550-150">Selecione uma máquina virtual listada no painel da máquina virtual de Olá e, em seguida, clique em **extensões**.</span><span class="sxs-lookup"><span data-stu-id="b9550-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="b9550-151">Deverá ver Olá **SQLIaaSAgent** extensões listada.</span><span class="sxs-lookup"><span data-stu-id="b9550-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Extensão de IaaS agente do SQL Server no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="b9550-153">Também pode utilizar Olá **Get-AzureVMSqlServerExtension** cmdlet do Powershell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9550-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="b9550-154">Remoção</span><span class="sxs-lookup"><span data-stu-id="b9550-154">Removal</span></span>
<span data-ttu-id="b9550-155">No Portal do Azure Olá, pode desinstalar a extensão de Olá clicando reticências Olá no Olá **extensões** painel das propriedades da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b9550-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="b9550-156">Em seguida, clique em **desinstalação**.</span><span class="sxs-lookup"><span data-stu-id="b9550-156">Then click **Uninstall**.</span></span>

![Desinstalar Olá extensão de agente do SQL Server IaaS no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="b9550-158">Também pode utilizar Olá **remover AzureVMSqlServerExtension** cmdlet do Powershell.</span><span class="sxs-lookup"><span data-stu-id="b9550-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="b9550-159">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="b9550-159">Next Steps</span></span>
<span data-ttu-id="b9550-160">Começar a utilizar um dos serviços de Olá suportados pela extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9550-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="b9550-161">Para obter mais detalhes, consulte os tópicos de Olá referenciados no Olá [serviços suportados pelo](#supported-services) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="b9550-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="b9550-162">Para obter mais informações sobre a execução do SQL Server em Azure Virtual Machines, consulte [SQL Server em Virtual Machines do Azure descrição-geral](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9550-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

