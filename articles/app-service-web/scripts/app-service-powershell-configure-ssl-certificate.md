---
title: "aaaAzure exemplo de Script do PowerShell - vincular uma certificado SSL personalizada aplicação de web de tooa | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - enlace uma aplicação de web do tooa de certificado SSL personalizada"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="dec9e-103">Vincular uma certificado SSL personalizada aplicação de web de tooa</span><span class="sxs-lookup"><span data-stu-id="dec9e-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="dec9e-104">Este script de exemplo cria uma aplicação web no App Service com os respetivos recursos relacionados, em seguida, vincula o certificado SSL Olá um tooit de nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="dec9e-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="dec9e-105">Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dec9e-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="dec9e-106">Além disso, certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="dec9e-106">Also, ensure that:</span></span>

- <span data-ttu-id="dec9e-107">Foi criada uma ligação com o Azure utilizando Olá `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="dec9e-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="dec9e-108">Tem de página de configuração de DNS de acesso tooyour domínio da entidade de registo.</span><span class="sxs-lookup"><span data-stu-id="dec9e-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="dec9e-109">Tem um válido. Ficheiro PFX e a respetiva palavra-passe para Olá SSL de certificado pretende tooupload e vincular.</span><span class="sxs-lookup"><span data-stu-id="dec9e-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="dec9e-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="dec9e-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dec9e-111">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="dec9e-111">Clean up deployment</span></span> 

<span data-ttu-id="dec9e-112">Depois de executar o script de exemplo Olá, Olá os seguintes comandos pode ser utilizados tooremove grupo de recursos de Olá, web aplicação e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="dec9e-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="dec9e-113">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="dec9e-113">Script explanation</span></span>

<span data-ttu-id="dec9e-114">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="dec9e-114">This script uses hello following commands.</span></span> <span data-ttu-id="dec9e-115">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="dec9e-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dec9e-116">Comando</span><span class="sxs-lookup"><span data-stu-id="dec9e-116">Command</span></span> | <span data-ttu-id="dec9e-117">Notas</span><span class="sxs-lookup"><span data-stu-id="dec9e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dec9e-118">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dec9e-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dec9e-119">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="dec9e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dec9e-120">Novo AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="dec9e-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="dec9e-121">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="dec9e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="dec9e-122">Novo AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="dec9e-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="dec9e-123">Cria uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="dec9e-123">Creates a web app.</span></span> |
| [<span data-ttu-id="dec9e-124">Conjunto AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="dec9e-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="dec9e-125">Modifica uma toochange do plano de serviço de aplicações com o escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="dec9e-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="dec9e-126">Conjunto AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="dec9e-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="dec9e-127">Modifica a configuração de uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="dec9e-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="dec9e-128">Novo AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="dec9e-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="dec9e-129">Cria um enlace de certificado SSL para uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="dec9e-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dec9e-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dec9e-130">Next steps</span></span>

<span data-ttu-id="dec9e-131">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dec9e-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dec9e-132">Exemplos do Azure Powershell adicionais para Web Apps do Azure App Service podem ser encontrados na Olá [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dec9e-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
