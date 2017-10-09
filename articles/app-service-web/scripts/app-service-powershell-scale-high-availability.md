---
title: "aaaAzure exemplo de Script do PowerShell - dimensionar uma aplicação web em todo o mundo com uma arquitetura de elevada disponibilidade | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - escala uma aplicação web em todo o mundo com uma arquitetura de elevada disponibilidade"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="ba9f2-103">Dimensionar uma aplicação web em todo o mundo com uma arquitetura de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ba9f2-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="ba9f2-104">Neste cenário, irá criar um grupo de recursos, dois planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos finais Gestor de tráfego.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="ba9f2-105">Após a conclusão do exercício de Olá terá um elevado disponível arquitetura que permite que fornece disponibilidade global da sua aplicação web com base na latência de rede mais baixa Olá.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="ba9f2-106">Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma ligação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ba9f2-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ba9f2-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ba9f2-108">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="ba9f2-108">Clean up deployment</span></span> 

<span data-ttu-id="ba9f2-109">Depois de executar o script de exemplo Olá, Olá os seguintes comandos pode ser utilizados tooremove grupo de recursos de Olá, web aplicação e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="ba9f2-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="ba9f2-110">Script explanation</span></span>

<span data-ttu-id="ba9f2-111">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-111">This script uses hello following commands.</span></span> <span data-ttu-id="ba9f2-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ba9f2-113">Comando</span><span class="sxs-lookup"><span data-stu-id="ba9f2-113">Command</span></span> | <span data-ttu-id="ba9f2-114">Notas</span><span class="sxs-lookup"><span data-stu-id="ba9f2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba9f2-115">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ba9f2-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ba9f2-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba9f2-117">Novo AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="ba9f2-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="ba9f2-118">Cria um perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="ba9f2-119">Novo AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ba9f2-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="ba9f2-120">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ba9f2-121">Novo AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ba9f2-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="ba9f2-122">Cria uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-122">Creates a web app.</span></span> |
| [<span data-ttu-id="ba9f2-123">Novo AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="ba9f2-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="ba9f2-124">Cria um ponto final num perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="ba9f2-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba9f2-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ba9f2-125">Next steps</span></span>

<span data-ttu-id="ba9f2-126">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba9f2-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ba9f2-127">Exemplos do Azure Powershell adicionais para Web Apps do Azure App Service podem ser encontrados na Olá [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ba9f2-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
