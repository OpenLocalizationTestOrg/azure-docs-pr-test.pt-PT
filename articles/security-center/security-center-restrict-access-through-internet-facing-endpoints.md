---
title: "aaaRestrict acesso através de pontos finais de acesso à Internet no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * restringir o acesso através da Internet com o ponto final * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="b91f3-103">Restringir o acesso através de pontos finais de acesso à Internet no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="b91f3-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="b91f3-104">Centro de segurança do Azure recomendará que restringir o acesso através de pontos finais de acesso à Internet se qualquer um dos seus grupos de segurança de rede (NSGs) tem uma ou mais regras de entrada que permite o acesso de "qualquer" endereço IP de origem.</span><span class="sxs-lookup"><span data-stu-id="b91f3-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="b91f3-105">A abertura de acesso demasiado "nenhum" pode ativar os atacantes tooaccess os recursos.</span><span class="sxs-lookup"><span data-stu-id="b91f3-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="b91f3-106">Centro de segurança irá recomendar que edite estes endereços IP do regras de entrada toorestrict acesso toosource que, na verdade, precisam de acesso.</span><span class="sxs-lookup"><span data-stu-id="b91f3-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="b91f3-107">Esta recomendação é gerada para qualquer porta de web não tem "qualquer" como origem.</span><span class="sxs-lookup"><span data-stu-id="b91f3-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="b91f3-108">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="b91f3-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="b91f3-109">Não se trata de um guia passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="b91f3-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b91f3-110">Implementar a recomendação de Olá</span><span class="sxs-lookup"><span data-stu-id="b91f3-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="b91f3-111">No Olá **painel recomendações**, selecione **restringir o acesso através da Internet com o ponto final**.</span><span class="sxs-lookup"><span data-stu-id="b91f3-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restringir o acesso através de um ponto final com acesso à Internet][1]
2. <span data-ttu-id="b91f3-113">Esta ação abre o painel de Olá **restringir o acesso através da Internet com o ponto final**.</span><span class="sxs-lookup"><span data-stu-id="b91f3-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="b91f3-114">Este painel lista Olá máquinas de virtuais (VMs) com as regras de entrada que criam um potencial problema de segurança.</span><span class="sxs-lookup"><span data-stu-id="b91f3-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="b91f3-115">Selecione uma VM.</span><span class="sxs-lookup"><span data-stu-id="b91f3-115">Select a VM.</span></span>

   ![Selecione uma VM][2]
3. <span data-ttu-id="b91f3-117">Olá **NSG** painel mostra informações de grupo de segurança de rede, as regras de entrada relacionadas, e Olá associado à VM.</span><span class="sxs-lookup"><span data-stu-id="b91f3-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="b91f3-118">Selecione **editar regras de entrada** tooproceed com uma regra de entrada de edição.</span><span class="sxs-lookup"><span data-stu-id="b91f3-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Painel do grupo de segurança de rede][3]
4. <span data-ttu-id="b91f3-120">No Olá **regras de segurança de entrada** painel selecione Olá tooedit de regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="b91f3-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="b91f3-121">Neste exemplo, vamos selecione **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="b91f3-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Regras de segurança de entrada][4]

   <span data-ttu-id="b91f3-123">Tenha em atenção, também pode selecionar **predefinido regras** conjunto de Olá toosee de regras de predefinidas contido por todos os NSGs.</span><span class="sxs-lookup"><span data-stu-id="b91f3-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="b91f3-124">regras de predefinidas Olá não podem ser eliminadas, mas como lhes é atribuída uma prioridade mais baixa, podem ser substituídas pelas regras de Olá que criar.</span><span class="sxs-lookup"><span data-stu-id="b91f3-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="b91f3-125">Saiba mais sobre [predefinido regras](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="b91f3-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Regras predefinidas][5]
5. <span data-ttu-id="b91f3-127">No Olá **AllowWeb** painel, editar Olá propriedades da regra de entrada Olá, de modo que Olá **origem** é um endereço IP ou o bloco de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="b91f3-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="b91f3-128">toolearn mais informações sobre Olá as propriedades da regra de entrada Olá, consulte [regras do NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="b91f3-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Editar regra de entrada][6]

## <a name="see-also"></a><span data-ttu-id="b91f3-130">Consultar também</span><span class="sxs-lookup"><span data-stu-id="b91f3-130">See also</span></span>
<span data-ttu-id="b91f3-131">Este artigo mostrou como tooimplement Olá Centro de segurança recomendação "restringir o acesso através da Internet com o ponto final."</span><span class="sxs-lookup"><span data-stu-id="b91f3-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="b91f3-132">toolearn mais informações sobre a ativação NSGs e regras, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="b91f3-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="b91f3-133">O que é um Grupo de Segurança de Rede (NSG)? (What is a Network Security Group (NSG)?)</span><span class="sxs-lookup"><span data-stu-id="b91f3-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="b91f3-134">Como os NSGs toomanage utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b91f3-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="b91f3-135">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="b91f3-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b91f3-136">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md)– Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="b91f3-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b91f3-137">[Gerir recomendações de segurança no Centro de Segurança do Azure](security-center-recommendations.md) – Saiba como as recomendações o ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91f3-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b91f3-138">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="b91f3-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b91f3-139">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="b91f3-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b91f3-140">[Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="b91f3-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b91f3-141">[FAQ do Centro de segurança do Azure](security-center-faq.md)– encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="b91f3-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b91f3-142">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)-obter Olá mais recentes notícias de segurança do Azure e informações.</span><span class="sxs-lookup"><span data-stu-id="b91f3-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
