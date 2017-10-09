---
title: aaaQoS requisitos para o ExpressRoute | Microsoft Docs
description: "Esta página fornece os requisitos detalhados para configurar e gerir o QoS para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="c2c73-103">Requisitos do QoS do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c73-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="c2c73-104">O Skype para Empresas tem várias cargas de trabalho que exigem um tratamento do QoS diferenciado.</span><span class="sxs-lookup"><span data-stu-id="c2c73-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="c2c73-105">Se planear serviços de voz tooconsume através do ExpressRoute, deve cumprir os requisitos de toohello descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="c2c73-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="c2c73-106">Os requisitos do QoS aplicam-se toohello peering da Microsoft apenas.</span><span class="sxs-lookup"><span data-stu-id="c2c73-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="c2c73-107">valores DSCP Olá no seu tráfego de rede recebidos no peering público do Azure e peering privado do Azure será too0 de reposição.</span><span class="sxs-lookup"><span data-stu-id="c2c73-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="c2c73-108">Olá tabela seguinte fornece uma lista de marcações DSCP utilizadas pelo Skype para empresas.</span><span class="sxs-lookup"><span data-stu-id="c2c73-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="c2c73-109">Consulte demasiado[gerir QoS para Skype para empresas](https://technet.microsoft.com/library/gg405409.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c2c73-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="c2c73-110">**Classe de Tráfego**</span><span class="sxs-lookup"><span data-stu-id="c2c73-110">**Traffic Class**</span></span> | <span data-ttu-id="c2c73-111">**Tratamento (Marcação DSCP)**</span><span class="sxs-lookup"><span data-stu-id="c2c73-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="c2c73-112">**Cargas de trabalho do Skype para Empresas**</span><span class="sxs-lookup"><span data-stu-id="c2c73-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2c73-113">**Voz**</span><span class="sxs-lookup"><span data-stu-id="c2c73-113">**Voice**</span></span> |<span data-ttu-id="c2c73-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="c2c73-114">EF (46)</span></span> |<span data-ttu-id="c2c73-115">Voz do Skype/Lync</span><span class="sxs-lookup"><span data-stu-id="c2c73-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="c2c73-116">**Interativo**</span><span class="sxs-lookup"><span data-stu-id="c2c73-116">**Interactive**</span></span> |<span data-ttu-id="c2c73-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="c2c73-117">AF41 (34)</span></span> |<span data-ttu-id="c2c73-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="c2c73-118">Video, VBSS</span></span> |
| <span data-ttu-id="c2c73-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="c2c73-119">AF21 (18)</span></span> |<span data-ttu-id="c2c73-120">Partilha de aplicações</span><span class="sxs-lookup"><span data-stu-id="c2c73-120">App sharing</span></span> | |
| <span data-ttu-id="c2c73-121">**Predefinição**</span><span class="sxs-lookup"><span data-stu-id="c2c73-121">**Default**</span></span> |<span data-ttu-id="c2c73-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="c2c73-122">AF11 (10)</span></span> |<span data-ttu-id="c2c73-123">Transferência de ficheiros</span><span class="sxs-lookup"><span data-stu-id="c2c73-123">File transfer</span></span> |
| <span data-ttu-id="c2c73-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="c2c73-124">CS0 (0)</span></span> |<span data-ttu-id="c2c73-125">Tudo o resto</span><span class="sxs-lookup"><span data-stu-id="c2c73-125">Anything else</span></span> | |

* <span data-ttu-id="c2c73-126">Deve classificar as cargas de trabalho Olá e marcar os valores DSCP corretos do Olá.</span><span class="sxs-lookup"><span data-stu-id="c2c73-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="c2c73-127">Siga as orientações de Olá fornecida [aqui](https://technet.microsoft.com/library/gg405409.aspx) sobre marcações DSCP de tooset na sua rede.</span><span class="sxs-lookup"><span data-stu-id="c2c73-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="c2c73-128">Deve configurar e suportar várias filas do QoS na rede.</span><span class="sxs-lookup"><span data-stu-id="c2c73-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="c2c73-129">Voz tem de ser uma classe autónoma e receber o tratamento EF de Olá especificado no RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="c2c73-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="c2c73-130">Pode decidir Olá colocação mecanismo, a política de deteção de congestionamento e a alocação de largura de banda por classe de tráfego.</span><span class="sxs-lookup"><span data-stu-id="c2c73-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="c2c73-131">No entanto, hello marcação DSCP para o Skype para cargas de trabalho do negócio têm de ser preservado.</span><span class="sxs-lookup"><span data-stu-id="c2c73-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="c2c73-132">Se estiver a utilizar marcações DSCP não listadas acima, por exemplo, AF31 (26), terá de reescrever este too0 de valor DSCP antes de enviar Olá tooMicrosoft de pacote.</span><span class="sxs-lookup"><span data-stu-id="c2c73-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="c2c73-133">A Microsoft só envia pacotes marcados com Olá valor DSCP mostrado na Olá acima tabela.</span><span class="sxs-lookup"><span data-stu-id="c2c73-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c2c73-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c2c73-134">Next steps</span></span>
* <span data-ttu-id="c2c73-135">Consulte os requisitos de toohello para [encaminhamento](expressroute-routing.md) e [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="c2c73-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="c2c73-136">Consulte a seguinte Olá liga tooconfigure a ligação do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c73-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="c2c73-137">Crie um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c73-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="c2c73-138">Configure o encaminhamento</span><span class="sxs-lookup"><span data-stu-id="c2c73-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="c2c73-139">Associar um tooan VNet circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c73-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

