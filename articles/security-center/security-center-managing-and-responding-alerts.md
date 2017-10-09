---
title: "aaaManage alertas de segurança no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o a toouse Centro de segurança do Azure capacidades toomanage e responder a alertas de toosecurity."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="d9435-103">Gerir e responder a alertas de toosecurity no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="d9435-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="d9435-104">Este documento ajuda-o a utilizar o Centro de segurança do Azure toomanage e responder a alertas de toosecurity.</span><span class="sxs-lookup"><span data-stu-id="d9435-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="d9435-105">deteções tooenable avançada, atualização tooAzure padrão de centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="d9435-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="d9435-106">Está disponível uma avaliação gratuita de 60 dias.</span><span class="sxs-lookup"><span data-stu-id="d9435-106">A free 60-day trial is available.</span></span> <span data-ttu-id="d9435-107">tooupgrade, selecione escalão de preço no Olá [política de segurança](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d9435-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="d9435-108">Consulte [preços do Centro de segurança do Azure](security-center-pricing.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="d9435-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="d9435-109">O que são alertas de segurança?</span><span class="sxs-lookup"><span data-stu-id="d9435-109">What are security alerts?</span></span>
<span data-ttu-id="d9435-110">Centro de segurança automaticamente recolhe, analisa e integra-se os dados de registo dos seus recursos do Azure, rede Olá, ligado soluções de parceiros, como soluções de proteção ponto final e firewall, toodetect de ameaças reais e reduzir os falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="d9435-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="d9435-111">Uma lista de alertas de segurança prioritários é apresentada no Centro de segurança juntamente com Olá informações necessárias tooquickly investigar o problema de Olá e recomendações sobre como tooremediate um ataque.</span><span class="sxs-lookup"><span data-stu-id="d9435-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="d9435-112">Para obter mais informações sobre como funcionam as capacidades de deteção do Centro de Segurança, leia [Capacidades de Deteção do Centro de Segurança do Azure](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d9435-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="d9435-113">Gerir alertas de segurança</span><span class="sxs-lookup"><span data-stu-id="d9435-113">Managing security alerts</span></span>
<span data-ttu-id="d9435-114">Pode rever os alertas atuais ao observar Olá **alertas de segurança** mosaico.</span><span class="sxs-lookup"><span data-stu-id="d9435-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="d9435-115">Abra o Portal do Azure e siga os passos de Olá abaixo toosee mais detalhes sobre cada alerta:</span><span class="sxs-lookup"><span data-stu-id="d9435-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="d9435-116">No dashboard do Centro de segurança de Olá, verá Olá **alertas de segurança** mosaico.</span><span class="sxs-lookup"><span data-stu-id="d9435-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Mosaico Alertas de segurança no Centro de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="d9435-118">Clique em Olá do Olá mosaico tooopen **alertas de segurança** painel que contém mais detalhes sobre Olá alertas como é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d9435-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![Painel de alertas de segurança de Olá no Centro de segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="d9435-120">Na parte inferior Olá deste painel encontram Olá os detalhes para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="d9435-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="d9435-121">toosort, clique em coluna Olá que pretende que sejam toosort pelo.</span><span class="sxs-lookup"><span data-stu-id="d9435-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="d9435-122">definição de Olá para cada coluna é indicada abaixo:</span><span class="sxs-lookup"><span data-stu-id="d9435-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="d9435-123">**Descrição**: uma explicação breve do alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="d9435-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="d9435-124">**Contagem**: uma lista de todos os alertas deste tipo específico que foram detetados num dia específico.</span><span class="sxs-lookup"><span data-stu-id="d9435-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="d9435-125">**Detetado por**: Olá serviço que foi responsável por ter acionado o alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9435-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="d9435-126">**Data**: Olá data esse evento Olá ocorreu.</span><span class="sxs-lookup"><span data-stu-id="d9435-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="d9435-127">**Estado**: Olá estado atual para esse alerta.</span><span class="sxs-lookup"><span data-stu-id="d9435-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="d9435-128">Existem dois tipos de estados:</span><span class="sxs-lookup"><span data-stu-id="d9435-128">There are two types of states:</span></span>
  * <span data-ttu-id="d9435-129">**Active Directory**: Olá alerta de segurança foi detetado.</span><span class="sxs-lookup"><span data-stu-id="d9435-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="d9435-130">**Gravidade**: nível de gravidade Olá, que pode ser alta, média ou baixa.</span><span class="sxs-lookup"><span data-stu-id="d9435-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="d9435-131">Filtragem de alertas</span><span class="sxs-lookup"><span data-stu-id="d9435-131">Filtering alerts</span></span>
<span data-ttu-id="d9435-132">Pode filtrar os alertas com base na data, no estado e na gravidade.</span><span class="sxs-lookup"><span data-stu-id="d9435-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="d9435-133">Filtragem de alertas pode ser útil para cenários onde necessita de âmbito de Olá toonarrow de mostrar alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="d9435-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="d9435-134">Por exemplo, pode pretender tooaddress alertas de segurança ocorridas no Olá últimas 24 horas porque está a investigar uma potencial violação no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9435-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="d9435-135">Clique em **filtro** no Olá **alertas de segurança** painel.</span><span class="sxs-lookup"><span data-stu-id="d9435-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="d9435-136">Olá **filtro** abre painel e selecionar valores de data, estado e gravidade de Olá desejar toosee.</span><span class="sxs-lookup"><span data-stu-id="d9435-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Filtragem de alertas no Centro de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="d9435-138">Responder a alertas de toosecurity</span><span class="sxs-lookup"><span data-stu-id="d9435-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="d9435-139">Selecione um toolearn de alerta de segurança mais informações sobre eventos de Olá que acionou o alerta Olá e o que, se aplicável, os passos precisam de tootake tooremediate um ataque.</span><span class="sxs-lookup"><span data-stu-id="d9435-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="d9435-140">Os alertas de segurança estão agrupados por tipo e data.</span><span class="sxs-lookup"><span data-stu-id="d9435-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="d9435-141">Ao clicar num alerta de segurança irá abrir um painel que contém uma lista de alertas de Olá agrupado.</span><span class="sxs-lookup"><span data-stu-id="d9435-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Responder a alertas de toosecurity no Centro de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="d9435-143">Neste caso, os alertas de Olá que foram acionados referem-se toosuspicious atividade do protocolo RDP (Remote Desktop Protocol).</span><span class="sxs-lookup"><span data-stu-id="d9435-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="d9435-144">Step-by-Olá primeira coluna mostra quais os recursos que foram atacados; Olá segundo mostra o número de vezes recursos Olá foi atacado; Olá terceira mostra o tempo de Olá de ataque de Olá; Olá fourth mostra o estado de alerta de Olá; e Olá fifth mostra a gravidade Olá de ataque de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9435-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="d9435-145">Depois de rever estas informações, clique em recursos de Olá que foi atacado e será aberto um novo painel.</span><span class="sxs-lookup"><span data-stu-id="d9435-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Sugestões para alertas que toodo sobre a segurança no Centro de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="d9435-147">No Olá **Descrição** campo deste painel irá encontrar mais detalhes sobre este evento.</span><span class="sxs-lookup"><span data-stu-id="d9435-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="d9435-148">Estes detalhes adicionais facultam informações aprofundadas que Olá accionadas segurança alerta, Olá recurso de destino, quando aplicável Olá origem endereço IP e as recomendações sobre como tooremediate.</span><span class="sxs-lookup"><span data-stu-id="d9435-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="d9435-149">Em alguns casos, endereço IP de origem Olá estará vazio (não disponível) porque nem todos os registos de eventos de segurança do Windows incluem o endereço IP Olá.</span><span class="sxs-lookup"><span data-stu-id="d9435-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="d9435-150">remediação de Olá sugerida pelo centro de segurança irá variar de acordo com toohello alerta de segurança.</span><span class="sxs-lookup"><span data-stu-id="d9435-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="d9435-151">Em alguns casos, poderá ter toouse tooimplement outras capacidades do Azure Olá recomendado remediação.</span><span class="sxs-lookup"><span data-stu-id="d9435-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="d9435-152">Por exemplo, Olá remediação para este ataque é o endereço IP de Olá tooblacklist que está a gerar este ataque ao utilizar um [ACL de rede](../virtual-network/virtual-networks-acl.md) ou um [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) regra.</span><span class="sxs-lookup"><span data-stu-id="d9435-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="d9435-153">Para obter mais informações sobre os diferentes tipos Olá de alertas, leia o artigo [alertas de segurança por tipo no Centro de segurança do Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="d9435-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="d9435-154">Consultar também</span><span class="sxs-lookup"><span data-stu-id="d9435-154">See also</span></span>
<span data-ttu-id="d9435-155">Neste documento, aprendeu como tooconfigure políticas de segurança no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="d9435-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="d9435-156">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="d9435-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="d9435-157">Lidar com Incidentes de Segurança no Centro de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="d9435-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="d9435-158">Capacidades de Deteção do Centro de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="d9435-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="d9435-159">Guia de Operações e Planeamento do Centro de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="d9435-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="d9435-160">[FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9435-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d9435-161">[Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9435-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
