---
title: "ferramentas de aaaCommunity - mover recursos clássicos tooAzure Resource Manager | Microsoft Docs"
description: "Este artigo catálogos Olá ferramentas tem sido fornecidas pelo Olá Comunidade toohelp migre recursos IaaS do modelo de implementação Azure Resource Manager toohello clássico."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="f5bea-103">Comunidade ferramentas toomigrate IaaS recursos do Gestor de recursos de tooAzure clássico</span><span class="sxs-lookup"><span data-stu-id="f5bea-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="f5bea-104">Este artigo catálogos Olá ferramentas que foram fornecidos pelo Olá Comunidade tooassist com a migração de recursos IaaS do modelo de implementação Azure Resource Manager toohello clássico.</span><span class="sxs-lookup"><span data-stu-id="f5bea-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="f5bea-105">Estas ferramentas não são suportadas oficialmente por Support da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5bea-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="f5bea-106">Por conseguinte, estão abertos obtido no GitHub e estamos tooaccept satisfeito PRs para correções ou cenários adicionais.</span><span class="sxs-lookup"><span data-stu-id="f5bea-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="f5bea-107">tooreport um problema, utilize Olá GitHub emite funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f5bea-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="f5bea-108">Migrar com estas ferramentas irá causar período de indisponibilidade para a Máquina Virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="f5bea-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="f5bea-109">Se estiver à procura de migração de plataforma suportada, visite</span><span class="sxs-lookup"><span data-stu-id="f5bea-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="f5bea-110">Migração de plataforma suportada dos recursos IaaS da pilha do clássico tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5bea-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="f5bea-111">Técnica detalhada da plataforma suportada a migração de clássico tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5bea-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="f5bea-112">Migrar os recursos IaaS de clássico tooAzure Gestor de recursos com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5bea-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="f5bea-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="f5bea-113">AsmMetadataParser</span></span>
<span data-ttu-id="f5bea-114">Esta é uma coleção de ferramentas de programa auxiliar criada como parte da empresa as migrações do tooAzure de gestão de serviço do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5bea-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="f5bea-115">Esta ferramenta permite-lhe tooreplicate a infraestrutura para outra subscrição que pode ser utilizada para fins de teste de migração e iron eventuais problemas antes de executar a migração de Olá na sua subscrição de produção.</span><span class="sxs-lookup"><span data-stu-id="f5bea-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="f5bea-116">Documentação da ferramenta de ligação toohello</span><span class="sxs-lookup"><span data-stu-id="f5bea-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="f5bea-117">migAz</span><span class="sxs-lookup"><span data-stu-id="f5bea-117">migAz</span></span>
<span data-ttu-id="f5bea-118">migAz é uma opção adicional de toomigrate um conjunto completo de recursos do Resource Manager IaaS de tooAzure de recursos do clássicos IaaS.</span><span class="sxs-lookup"><span data-stu-id="f5bea-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="f5bea-119">Olá migração pode ocorrer em Olá mesma subscrição ou entre subscrições e tipos de subscrição (ex: subscrições de CSP).</span><span class="sxs-lookup"><span data-stu-id="f5bea-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="f5bea-120">Documentação da ferramenta de ligação toohello</span><span class="sxs-lookup"><span data-stu-id="f5bea-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="f5bea-121">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="f5bea-121">Next Steps</span></span>

* [<span data-ttu-id="f5bea-122">Descrição geral da migração de plataforma suportada dos recursos IaaS do clássico tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5bea-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5bea-123">Técnica detalhada da plataforma suportada a migração do Gestor de recursos de tooAzure clássico</span><span class="sxs-lookup"><span data-stu-id="f5bea-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5bea-124">Planeamento da migração de recursos IaaS do clássico tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5bea-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5bea-125">Utilizar o PowerShell toomigrate IaaS recursos do Gestor de recursos de tooAzure clássico</span><span class="sxs-lookup"><span data-stu-id="f5bea-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5bea-126">Utilizar recursos de IaaS toomigrate CLI do clássico tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5bea-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5bea-127">Consultar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="f5bea-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5bea-128">Olá revisão mais perguntas mais frequentes sobre a migração de IaaS de recursos do Gestor de recursos de tooAzure clássico</span><span class="sxs-lookup"><span data-stu-id="f5bea-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

