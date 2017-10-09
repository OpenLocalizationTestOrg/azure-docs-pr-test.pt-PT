---
title: "aaaManage Cofre de chaves do Azure através da automatização do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automatização do Azure pode ser utilizado toomanage Cofre de chaves do Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="435e5-103">Gerir o Cofre de chaves do Azure através da automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="435e5-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="435e5-104">Este guia irá apresentar toohello serviço de automatização do Azure e como pode ser utilizado toosimplify gestão das suas chaves e segredos no Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="435e5-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="435e5-105">O que é a Automatização do Azure?</span><span class="sxs-lookup"><span data-stu-id="435e5-105">What is Azure Automation?</span></span>
<span data-ttu-id="435e5-106">[A automatização do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar a gestão de nuvem através de automatização de processos e a configuração de estado pretendido.</span><span class="sxs-lookup"><span data-stu-id="435e5-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="435e5-107">Através da automatização do Azure, as tarefas manuais, repetidas, execução longa e propensas ao erro podem ser automatizada tooincrease fiabilidade, eficiência e toovalue de tempo para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="435e5-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="435e5-108">A automatização do Azure fornece um motor de execução do fluxo de trabalho altamente fiável, de elevada disponibilidade que dimensiona toomeet às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="435e5-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="435e5-109">Na automatização do Azure, os processos podem ser arrancou manualmente, por sistemas de terceiros 3rd ou em intervalos agendados para que as tarefas acontecer exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="435e5-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="435e5-110">Reduzir a sobrecarga operacional e libertar IT e DevOps pessoal toofocus no trabalho que adiciona o valor de negócio, movendo a sua toobe de tarefas de gestão de nuvem são executadas automaticamente pela automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="435e5-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="435e5-111">Como pode que o automatização do Azure ajuda a gerir o Cofre de chaves do Azure?</span><span class="sxs-lookup"><span data-stu-id="435e5-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="435e5-112">O Cofre de chaves que podem ser gerido na automatização do Azure utilizando Olá [cmdlets do Cofre de chaves AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e [cmdlets do Cofre de chaves do Azure clássico](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="435e5-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="435e5-113">Olá módulo do Azure para gerir o Cofre de chaves clássico está disponível automaticamente na automatização do Azure e pode importar Olá [AzureRM KeyVault módulo](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) na automatização do Azure, para que possam executar muitas da gestão de Cofre de chaves tarefas no âmbito do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="435e5-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="435e5-114">Também pode ser emparelhado estes cmdlets na automatização do Azure com cmdlets de Olá para outros serviços do Azure, as tarefas complexas tooautomate através de serviços do Azure e 3rd sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="435e5-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="435e5-115">Com os cmdlets do Cofre de chaves do Azure Olá pode efetuar estas tarefas das restantes:</span><span class="sxs-lookup"><span data-stu-id="435e5-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="435e5-116">Criar e configurar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="435e5-116">Create and configure a key vault</span></span>
* <span data-ttu-id="435e5-117">Criar ou importar uma chave</span><span class="sxs-lookup"><span data-stu-id="435e5-117">Create or import a key</span></span>
* <span data-ttu-id="435e5-118">Criar ou atualizar um segredo</span><span class="sxs-lookup"><span data-stu-id="435e5-118">Create or update a secret</span></span>
* <span data-ttu-id="435e5-119">Atualizar os atributos de uma chave</span><span class="sxs-lookup"><span data-stu-id="435e5-119">Update attributes of a key</span></span>
* <span data-ttu-id="435e5-120">Obter uma chave ou segredo</span><span class="sxs-lookup"><span data-stu-id="435e5-120">Get a key or secret</span></span>
* <span data-ttu-id="435e5-121">Eliminar uma chave ou segredo</span><span class="sxs-lookup"><span data-stu-id="435e5-121">Delete a key or secret</span></span>

<span data-ttu-id="435e5-122">Seguem-se alguns exemplos de utilização do PowerShell toomanage Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="435e5-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="435e5-123">Cofre de chaves do Azure - passo a passo</span><span class="sxs-lookup"><span data-stu-id="435e5-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="435e5-124">Definir e configurar um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="435e5-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="435e5-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="435e5-125">Next steps</span></span>
<span data-ttu-id="435e5-126">Agora que aprendeu as noções básicas de Olá da automatização do Azure e como pode ser utilizado toomanage Cofre de chaves do Azure, siga estas toolearn ligações mais sobre a automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="435e5-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="435e5-127">Consulte Olá da automatização do Azure [introdução Tutorial iniciado](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="435e5-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="435e5-128">Consulte Olá [scripts do PowerShell do Cofre de chaves do Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="435e5-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

