---
title: "aaaManage VMs através da automatização do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automatização do Azure pode ser utilizado toomanage máquinas virtuais do Azure à escala."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="b86f9-103">Gerir Máquinas Virtuais do Azure utilizando a Automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="b86f9-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="b86f9-104">Este guia apresenta-lhe como pode ser utilizado e do serviço de automatização do Azure toohello toosimplify gerir as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="b86f9-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b86f9-105">O que é a Automatização do Azure?</span><span class="sxs-lookup"><span data-stu-id="b86f9-105">What is Azure Automation?</span></span>
<span data-ttu-id="b86f9-106">[A automatização do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar a gestão de nuvem através de automatização de processos.</span><span class="sxs-lookup"><span data-stu-id="b86f9-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b86f9-107">Ao utilizar a automatização do Azure, as tarefas de longa execução, manuais, propensas ao erro e frequentemente repetidas podem ser automatizada tooincrease fiabilidade, eficiência e tempo ao valor para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="b86f9-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="b86f9-108">A automatização do Azure fornece um motor de execução do fluxo de trabalho altamente fiáveis e altamente disponível que ajusta às suas necessidades de toomeet à medida que aumenta a sua organização.</span><span class="sxs-lookup"><span data-stu-id="b86f9-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b86f9-109">Na automatização do Azure, os processos podem ser arrancou manualmente, por sistemas de terceiros ou em intervalos agendados para que as tarefas acontecer exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="b86f9-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b86f9-110">Pode reduzir a sobrecarga operacional e libertar IT e a equipa de DevOps toofocus no trabalho que adiciona o valor de negócio, executando a nuvem tarefas de gestão automaticamente com a automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="b86f9-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="b86f9-111">Como pode que o automatização do Azure ajuda a gerir máquinas virtuais do Azure?</span><span class="sxs-lookup"><span data-stu-id="b86f9-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="b86f9-112">Máquinas virtuais podem ser geridas na automatização do Azure utilizando [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="b86f9-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="b86f9-113">A automatização do Azure inclui cmdlets do Azure PowerShell Olá, pelo que pode efetuar todas as tarefas de gestão de máquina virtual no âmbito do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="b86f9-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="b86f9-114">Também pode ser emparelhado Olá cmdlets na automatização do Azure com cmdlets de Olá para outros serviços do Azure, as tarefas complexas tooautomate através de serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="b86f9-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b86f9-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b86f9-115">Next steps</span></span>
<span data-ttu-id="b86f9-116">Agora que aprendeu as noções básicas de Olá da automatização do Azure e como pode ser utilizado toomanage máquinas virtuais do Azure, saiba mais:</span><span class="sxs-lookup"><span data-stu-id="b86f9-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="b86f9-117">Descrição geral da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="b86f9-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="b86f9-118">O meu primeiro runbook</span><span class="sxs-lookup"><span data-stu-id="b86f9-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b86f9-119">Mapa de aprendizagem de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="b86f9-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

