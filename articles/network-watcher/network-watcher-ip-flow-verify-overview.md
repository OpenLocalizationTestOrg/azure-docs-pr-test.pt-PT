---
title: Certifique-se de aaaIntroduction tooIP fluxo no observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma descrição geral de Olá IP de observador de rede fluxo Certifique-se de capacidade"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="f7931-103">Certifique-se de fluxo de tooIP de introdução no observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="f7931-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="f7931-104">Fluxo IP Certifique-se verifica se um pacote é permitido ou negado tooor a partir de uma máquina virtual com base nas informações de 5 cadeias de identificação.</span><span class="sxs-lookup"><span data-stu-id="f7931-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="f7931-105">Esta informação é constituído por direção, protocolo, local IP, remoto IP, porta local e porta remota.</span><span class="sxs-lookup"><span data-stu-id="f7931-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="f7931-106">Se pacotes hello é negado por um grupo de segurança, é devolvido o nome de Olá da regra Olá negado pacotes hello de.</span><span class="sxs-lookup"><span data-stu-id="f7931-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="f7931-107">Enquanto qualquer IP de origem ou de destino pode ser selecionado, esta funcionalidade ajuda os administradores Diagnostique rapidamente problemas de conectividade do ou toohello internet e da ou toohello num ambiente no local.</span><span class="sxs-lookup"><span data-stu-id="f7931-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="f7931-108">Fluxo IP verificar destina-se uma interface de rede de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7931-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="f7931-109">Fluxo de tráfego, em seguida, é verificado com base nas definições de Olá configurado tooor dessa interface de rede.</span><span class="sxs-lookup"><span data-stu-id="f7931-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="f7931-110">Esta funcionalidade é útil para confirmar se uma regra num grupo de segurança de rede está a bloquear tooor de tráfego de entrada ou saída de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7931-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="f7931-111">Certifique-se de uma instância do observador de rede necessidades toobe criada em todas as regiões que planeia toorun fluxo IP.</span><span class="sxs-lookup"><span data-stu-id="f7931-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="f7931-112">Observador de rede é um serviço regional e só pode ser executada relativamente aos recursos na Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="f7931-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="f7931-113">Isto não afeta Olá resultados do fluxo IP, certifique-se como rota Olá associada Olá que NIC ainda vai ser devolvido.</span><span class="sxs-lookup"><span data-stu-id="f7931-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="f7931-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f7931-115">Next steps</span></span>

<span data-ttu-id="f7931-116">Visite Olá seguinte artigo toolearn se um pacote é permitido ou negado para uma máquina virtual específica através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="f7931-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="f7931-117">Verifique se o tráfego é permitido numa VM com o IP fluxo verificar através do portal Olá</span><span class="sxs-lookup"><span data-stu-id="f7931-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












