---
title: "Balanceador de carga aaaCreate um-para a Internet - portal do Azure clássico | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga com acesso à Internet no modelo de implementação clássica utilizando Olá portal clássico do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="36777-103">Introdução à criação de um Internet com o Balanceador de carga (clássica) na Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="36777-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="36777-104">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="36777-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="36777-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36777-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="36777-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="36777-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="36777-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="36777-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="36777-108">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure tem atualmente dois modelos de implementação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="36777-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="36777-109">Confirme que compreende os [modelos e ferramentas de implementação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="36777-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="36777-110">Pode ver a documentação de Olá de diversas ferramentas clicando Olá nos separadores na parte superior de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="36777-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="36777-111">Este artigo abrange o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="36777-112">Também pode [Saiba como o utilizando o Gestor de recursos do Azure de Balanceador de carga de toocreate um para a Internet](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="36777-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="36777-113">Configurar um balanceador de carga com acesso à Internet para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="36777-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="36777-114">Na ordem tooload equilibrar o tráfego de rede de Olá Internet em Olá máquinas de virtuais de um serviço em nuvem, terá de criar um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="36777-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="36777-115">Este procedimento assume que já criou máquinas de virtuais Olá e que estão todos os dentro Olá mesmo serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="36777-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="36777-116">**tooconfigure um conjunto com balanceamento de carga para as máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="36777-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="36777-117">No portal clássico do Azure Olá, clique em **máquinas virtuais**e, em seguida, clique no nome de Olá de uma máquina virtual no conjunto com balanceamento de carga de Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="36777-118">Clique em **Pontos finais** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36777-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="36777-119">No Olá **adicionar uma máquina de virtual do ponto final tooa** página, clique em seta para a direita Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="36777-120">No Olá **especificar detalhes de Olá do ponto final de Olá** página:</span><span class="sxs-lookup"><span data-stu-id="36777-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="36777-121">No **nome**, escreva um nome para o ponto final de Olá ou selecione nome Olá Olá lista de pontos finais predefinidos para protocolos comuns.</span><span class="sxs-lookup"><span data-stu-id="36777-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="36777-122">No **protocolo**, selecione o protocolo de Olá necessário pelo tipo de Olá de ponto final, TCP ou UDP, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="36777-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="36777-123">No **Porta pública e privada porta**, escreva os números de porta Olá que pretende Olá toouse de máquina virtual, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="36777-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="36777-124">Pode utilizar uma porta privada Olá e regras de firewall no tráfego de tooredirect Olá máquinas virtuais de uma forma que é adequado para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="36777-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="36777-125">Porta privada Olá pode Olá igual a porta pública Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="36777-126">Por exemplo, para um ponto final para o tráfego web (HTTP), pode atribuir porta 80 tooboth Olá públicas e privadas porta.</span><span class="sxs-lookup"><span data-stu-id="36777-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="36777-127">Selecione **criar um conjunto com balanceamento de carga**e, em seguida, clique em seta para a direita Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="36777-128">No Olá **configurar conjunto com balanceamento de carga de Olá** página, escreva um nome para o conjunto com balanceamento de carga de Olá e, em seguida, atribuir valores de Olá para o comportamento de sonda de Olá Balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="36777-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="36777-129">Olá Load Balancer utiliza sondas toodetermine se Olá máquinas de virtuais em conjunto com balanceamento de carga de Olá estiverem disponíveis tooreceive tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="36777-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="36777-130">Clique em Olá marca de verificação toocreate Olá com balanceamento de carga ponto final.</span><span class="sxs-lookup"><span data-stu-id="36777-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="36777-131">Verá **Sim** no Olá **o nome do conjunto com balanceamento de carga** coluna Olá **pontos finais** página para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="36777-132">No portal de Olá, clique em **máquinas virtuais**, clique no nome de Olá de uma máquina virtual adicional no conjunto com balanceamento de carga de Olá, clique em **pontos finais**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36777-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="36777-133">No Olá **adicionar uma máquina de virtual do ponto final tooa** página, clique em **adicionar ponto final tooan com balanceamento de carga conjunto existente**, selecione o nome de Olá do conjunto de balanceamento de carga Olá e, em seguida, clique em seta para a direita Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="36777-134">No Olá **especificar detalhes de Olá do ponto final de Olá** página, escreva um nome para o ponto final de Olá e, em seguida, clique em marca de verificação Olá.</span><span class="sxs-lookup"><span data-stu-id="36777-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="36777-135">Para Olá outras máquinas virtuais em conjunto com balanceamento de carga de Olá, repita os passos 8 a 10.</span><span class="sxs-lookup"><span data-stu-id="36777-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36777-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="36777-136">Next steps</span></span>

[<span data-ttu-id="36777-137">Começar a configurar um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="36777-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="36777-138">Configurar um modo de distribuição de balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="36777-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="36777-139">Configurar definições de tempo limite TCP inativo para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="36777-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
