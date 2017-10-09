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
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatizar tarefas de gestão em Azure Virtual Machines com Olá extensão de agente do SQL Server (clássica)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Clássico](../classic/sql-server-agent-extension.md)
> 
>
 
Olá extensão do agente do SQL Server IaaS (SQLIaaSAgent) é executado em tarefas de administração de tooautomate de máquinas virtuais do Azure. Este tópico fornece uma descrição geral dos serviços de Olá suportados pela extensão de Olá, bem como as instruções para instalação, estado e remoção.

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. versão do Gestor de recursos de Olá tooview deste artigo, consulte [extensão de agente do SQL Server para o SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Serviços suportados
Olá extensão de agente do SQL Server IaaS suporta Olá seguintes tarefas de administração:

| Funcionalidade de administração | Descrição |
| --- | --- |
| **Cópia de segurança automatizada do SQL** |Automatiza Olá agendamento de cópias de segurança para todas as bases de dados para a instância de predefinida Olá do SQL Server no Olá VM. Para obter mais informações, consulte [cópia de segurança automatizada do SQL Server em Virtual Machines do Azure (clássica)](../classic/sql-automated-backup.md). |
| **Aplicação de patches automatizada do SQL** |Configura uma janela de manutenção durante as atualizações que coloque tooyour VM pode demorar, pelo que pode evitar atualizações durante períodos máximos para a carga de trabalho. Para obter mais informações, consulte [aplicação para o SQL Server em Virtual Machines do Azure (clássica) de patches automatizada](../classic/sql-automated-patching.md). |
| **Integração do Cofre de Chaves do Azure** |Permite tooautomatically instalar e configurar o Cofre de chaves do Azure na sua VM do SQL Server. Para obter mais informações, consulte [configurar integração do Azure chave de cofre para SQL Server em VMs do Azure (clássica)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Pré-requisitos
Requisitos toouse Olá extensão de agente do SQL Server IaaS na sua VM:

### <a name="operating-system"></a>Sistema operativo:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Versões do SQL Server:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>O Azure PowerShell:
[Transferir e configurar os comandos de Azure PowerShell mais recentes Olá](/powershell/azure/overview).

Inicie o Windows PowerShell e ligue-tooyour subscrição do Azure com Olá **Add-AzureAccount** comando.

    Add-AzureAccount

Se tiver várias subscrições, utilize **Select-AzureSubscription** subscrição de Olá tooselect que contém o seu destino VMS clássicas.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

Neste momento, pode obter uma lista de máquinas de virtuais clássico Olá e os respetivos nomes de serviço associado com Olá **Get-AzureVM** comando.

    Get-AzureVM

## <a name="installation"></a>Instalação
Para VMs clássicas, tem de utilizar o PowerShell tooinstall Olá extensão de agente do SQL Server IaaS e configurar os respetivos serviços associados. Olá utilize **conjunto AzureVMSqlServerExtension** extensão de Olá de tooinstall de cmdlet do PowerShell. Por exemplo, Olá comando a seguir instala a extensão de Olá numa VM do Windows Server (clássica) e de nomes, "SQLIaaSExtension".

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Se atualizar a versão mais recente do toohello do Olá extensão de agente do SQL Server IaaS, tem de reiniciar a máquina virtual após a atualização da extensão de Olá.

> [!NOTE]
> As máquinas virtuais clássicas não têm uma opção tooinstall e configurar Olá extensão de agente do SQL Server IaaS através do portal Olá.
> 
> 

## <a name="status"></a>Estado
Tooverify unidirecional que a extensão de Olá é instalada é o estado do agente de Olá tooview na Olá Portal do Azure. Selecione uma máquina virtual listada no painel da máquina virtual de Olá e, em seguida, clique em **extensões**. Deverá ver Olá **SQLIaaSAgent** extensões listada.

![Extensão de IaaS agente do SQL Server no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Também pode utilizar Olá **Get-AzureVMSqlServerExtension** cmdlet do Powershell do Azure.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Remoção
No Portal do Azure Olá, pode desinstalar a extensão de Olá clicando reticências Olá no Olá **extensões** painel das propriedades da máquina virtual. Em seguida, clique em **desinstalação**.

![Desinstalar Olá extensão de agente do SQL Server IaaS no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Também pode utilizar Olá **remover AzureVMSqlServerExtension** cmdlet do Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Passos Seguintes
Começar a utilizar um dos serviços de Olá suportados pela extensão de Olá. Para obter mais detalhes, consulte os tópicos de Olá referenciados no Olá [serviços suportados pelo](#supported-services) secção deste artigo.

Para obter mais informações sobre a execução do SQL Server em Azure Virtual Machines, consulte [SQL Server em Virtual Machines do Azure descrição-geral](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

