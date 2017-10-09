---
title: "aaaAzure exemplo de Script do PowerShell - Adicionar aplicação cert tooa cluster | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - adicionar o cluster do Service Fabric certificado tooa uma aplicação."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="f5fee-103">Adicionar o cluster do Service Fabric certificado tooa uma aplicação</span><span class="sxs-lookup"><span data-stu-id="f5fee-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="f5fee-104">Este script de exemplo cria um certificado autoassinado no Cofre de chaves do Azure especificado Olá e instala-tooall nós de cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="f5fee-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="f5fee-105">certificado de Olá também transfere tooa de pasta local.</span><span class="sxs-lookup"><span data-stu-id="f5fee-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="f5fee-106">nome de Olá do certificado de Olá transferido é Olá igual ao nome de Olá Olá do certificado de no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="f5fee-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="f5fee-107">Personalize parâmetros Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f5fee-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="f5fee-108">Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` toocreate uma ligação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fee-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f5fee-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f5fee-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="f5fee-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="f5fee-110">Script explanation</span></span>

<span data-ttu-id="f5fee-111">Este script utiliza Olá os seguintes comandos: cada comando na tabela de Olá ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="f5fee-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f5fee-112">Comando</span><span class="sxs-lookup"><span data-stu-id="f5fee-112">Command</span></span> | <span data-ttu-id="f5fee-113">Notas</span><span class="sxs-lookup"><span data-stu-id="f5fee-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5fee-114">AzureRmServiceFabricApplicationCertificate adicionar</span><span class="sxs-lookup"><span data-stu-id="f5fee-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="f5fee-115">Adicione que um nova aplicação certificado toohello dimensionamento da máquina virtual definir que constituem cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="f5fee-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="f5fee-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f5fee-116">Next steps</span></span>

<span data-ttu-id="f5fee-117">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5fee-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f5fee-118">Amostras de Azure Powershell adicionais para o Azure Service Fabric podem ser encontradas na Olá [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f5fee-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
