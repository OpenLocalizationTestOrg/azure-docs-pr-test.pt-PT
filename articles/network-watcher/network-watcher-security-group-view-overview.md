---
title: Vista de grupo toosecurity aaaIntroduction no observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma descrição geral de Olá capacidade de vista de segurança do observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="92715-103">Vista do grupo de segurança do introdução toonetwork no observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="92715-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="92715-104">Grupos de segurança de rede estão associados a um nível de sub-rede ou um nível de NIC.</span><span class="sxs-lookup"><span data-stu-id="92715-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="92715-105">Quando associados a um nível de sub-rede, aplica-se as instâncias VM de Olá tooall na sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="92715-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="92715-106">Vista de grupo de segurança de rede devolve todos os NSGs Olá configurado e regras que estão associadas a um nível NIC e a sub-rede para uma máquina virtual que fornecem informações sobre a configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="92715-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="92715-107">Além disso, as regras de segurança eficaz Olá são devolvidas para cada um dos Olá NICs numa VM.</span><span class="sxs-lookup"><span data-stu-id="92715-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="92715-108">Vista de grupo de segurança de rede a utilizar, pode avaliar uma VM para vulnerabilidades de rede, tais como portas abertas.</span><span class="sxs-lookup"><span data-stu-id="92715-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="92715-109">Também pode validar se o grupo de segurança de rede está a funcionar conforme esperado com base num [comparação entre Olá configurado e Olá regras de segurança eficaz](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="92715-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="92715-110">Um caso de utilização expandido mais está em conformidade de segurança e de auditoria.</span><span class="sxs-lookup"><span data-stu-id="92715-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="92715-111">Pode definir um conjunto de regras de segurança prescritiva como um modelo para a governação de segurança na sua organização.</span><span class="sxs-lookup"><span data-stu-id="92715-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="92715-112">Uma auditoria periódica de compatibilidade pode ser implementada de forma programática através da comparação regras de prescritiva Olá com regras Efetivo Olá para cada uma das VMs Olá na sua rede.</span><span class="sxs-lookup"><span data-stu-id="92715-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="92715-113">Olá regras portais são divididas por eficaz, sub-rede, Interface de rede e predefinido.</span><span class="sxs-lookup"><span data-stu-id="92715-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="92715-114">Isto proporciona uma vista simple numa máquina virtual do Olá regras aplicadas tooa.</span><span class="sxs-lookup"><span data-stu-id="92715-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="92715-115">Um botão de transferência é fornecida tooeasily transferir todas as regras de segurança de Olá, independentemente do separador Olá para um ficheiro CSV.</span><span class="sxs-lookup"><span data-stu-id="92715-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![vista do grupo de segurança][1]

<span data-ttu-id="92715-117">As regras podem ser selecionadas e um novo painel abre-se as prefixos tooshow Olá grupo de segurança de rede e de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="92715-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="92715-118">A partir deste painel pode navegar diretamente toohello recursos de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="92715-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![pesquisa][2]

### <a name="next-steps"></a><span data-ttu-id="92715-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="92715-120">Next steps</span></span>

<span data-ttu-id="92715-121">Saiba como tooaudit a segurança de rede de grupo de definições, visitando [definições do grupo de segurança de rede de auditoria com o PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="92715-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









