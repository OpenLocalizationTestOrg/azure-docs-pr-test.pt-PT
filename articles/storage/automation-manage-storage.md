---
title: "aaaManage armazenamento do Azure com a automatização do Azure"
description: "Saiba mais sobre como Olá serviço de automatização do Azure pode ser utilizado toomanage Storage do Azure à escala."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 15e34128ffb0ba3315b5260442f628b5978c5197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="63706-103">Gerir o armazenamento do Azure através da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="63706-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="63706-104">Este guia irá apresentar toohello serviço de automatização do Azure e como pode ser utilizado toosimplify gestão da sua blobs, tabelas e filas do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="63706-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="63706-105">O que é a Automatização do Azure?</span><span class="sxs-lookup"><span data-stu-id="63706-105">What is Azure Automation?</span></span>
<span data-ttu-id="63706-106">[A automatização do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar a gestão de nuvem através de automatização de processos.</span><span class="sxs-lookup"><span data-stu-id="63706-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="63706-107">Utilizar a automatização do Azure, execução longa, manual, propensas ao erro e frequentemente repetidas tarefas podem ser automatizada tooincrease fiabilidade e a eficiência e reduzir o tempo toovalue para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="63706-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="63706-108">A automatização do Azure fornece um motor de execução do fluxo de trabalho altamente fiáveis e elevada disponibilidade que ajusta às suas necessidades de toomeet à medida que aumenta a sua organização.</span><span class="sxs-lookup"><span data-stu-id="63706-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="63706-109">Na automatização do Azure, os processos podem ser arrancou manualmente, por sistemas de terceiros 3rd ou em intervalos agendados para que as tarefas acontecer exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="63706-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="63706-110">Reduzir a sobrecarga operacional e libertar IT / toofocus de pessoal de DevOps no trabalho que adiciona o valor de negócio, movendo a sua toobe de tarefas de gestão de nuvem são executadas automaticamente pela automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="63706-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="63706-111">Como pode que o automatização do Azure ajuda a gerir o armazenamento do Azure?</span><span class="sxs-lookup"><span data-stu-id="63706-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="63706-112">Armazenamento do Azure pode ser gerido na automatização do Azure utilizando cmdlets do PowerShell Olá que estão disponíveis no [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="63706-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="63706-113">A automatização do Azure tem estes cmdlets PowerShell do armazenamento disponíveis Box Olá, para que possam executar todos os seus blob, tabela e tarefas de gestão de fila no âmbito do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="63706-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="63706-114">Também pode ser emparelhado estes cmdlets na automatização do Azure com cmdlets de Olá para outros serviços do Azure, as tarefas complexas tooautomate através de serviços do Azure e 3rd sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="63706-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="63706-115">Olá [Galeria de runbooks de automatização do Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contém uma variedade de produto equipa e da Comunidade runbooks tooget iniciado a automatizar a gestão de armazenamento do Azure, outros serviços do Azure e 3rd sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="63706-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="63706-116">Galeria runbooks incluem:</span><span class="sxs-lookup"><span data-stu-id="63706-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="63706-117">Remova os Blobs Storage do Azure são Certain dias antigo utilizando o serviço de automatização</span><span class="sxs-lookup"><span data-stu-id="63706-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="63706-118">Transferir um Blob Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="63706-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="63706-119">Todos os discos de cópia de segurança para uma única VM do Azure ou para todas as VMs num serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="63706-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="63706-120">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="63706-120">Next Steps</span></span>
<span data-ttu-id="63706-121">Agora que aprendeu as noções básicas de Olá da automatização do Azure e como pode ser utilizado toomanage blobs de armazenamento do Azure, tabelas e filas, siga estas toolearn ligações mais sobre a automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="63706-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="63706-122">Consulte o tutorial de automatização do Azure Olá [criar ou importar um runbook na automatização do Azure](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="63706-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

