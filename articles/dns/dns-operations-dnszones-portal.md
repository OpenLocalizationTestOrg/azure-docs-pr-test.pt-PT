---
title: aaaManage DNS zonas no DNS do Azure - portal do Azure | Microsoft Docs
description: "Pode gerir zonas DNS utilizando Olá portal do Azure. Este artigo descreve como tooupdate, eliminar e criar zonas DNS no DNS do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="f1a8f-104">Como toomanage zonas de DNS no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a8f-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1a8f-105">Portal</span><span class="sxs-lookup"><span data-stu-id="f1a8f-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="f1a8f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1a8f-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="f1a8f-107">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f1a8f-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="f1a8f-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a8f-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="f1a8f-109">Este artigo mostra como toomanage seu DNS zonas utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="f1a8f-110">Também pode gerir as zonas DNS utilizando Olá plataforma [CLI do Azure](dns-operations-dnszones-cli.md) ou Olá Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="f1a8f-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="f1a8f-111">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="f1a8f-111">Create a DNS zone</span></span>

1. <span data-ttu-id="f1a8f-112">A iniciar sessão toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a8f-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="f1a8f-113">No menu do Hub de Olá, clique em e clique em **novo > rede >** e, em seguida, clique em **zona DNS** painel do tooopen Olá criar DNS zona.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="f1a8f-115">No Olá **zona DNS criar** painel introduza Olá valores a seguir, em seguida, clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="f1a8f-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="f1a8f-116">**Definição**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-116">**Setting**</span></span> | <span data-ttu-id="f1a8f-117">**Valor**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-117">**Value**</span></span> | <span data-ttu-id="f1a8f-118">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f1a8f-119">**Nome**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-119">**Name**</span></span>|<span data-ttu-id="f1a8f-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="f1a8f-120">contoso.com</span></span>|<span data-ttu-id="f1a8f-121">nome de Olá da zona DNS de Olá</span><span class="sxs-lookup"><span data-stu-id="f1a8f-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="f1a8f-122">**Subscrição**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-122">**Subscription**</span></span>|<span data-ttu-id="f1a8f-123">[A sua subscrição]</span><span class="sxs-lookup"><span data-stu-id="f1a8f-123">[Your subscription]</span></span>|<span data-ttu-id="f1a8f-124">Selecione uma zona DNS de Olá toocreate subscrição no.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="f1a8f-125">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-125">**Resource group**</span></span>|<span data-ttu-id="f1a8f-126">**Criar novo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="f1a8f-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="f1a8f-127">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-127">Create a resource group.</span></span> <span data-ttu-id="f1a8f-128">nome do grupo de recursos de Olá têm de ser exclusivo dentro da subscrição Olá que selecionou.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="f1a8f-129">mais informações sobre grupos de recursos, leia Olá toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de descrição geral.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="f1a8f-130">**Localização**</span><span class="sxs-lookup"><span data-stu-id="f1a8f-130">**Location**</span></span>|<span data-ttu-id="f1a8f-131">EUA Oeste</span><span class="sxs-lookup"><span data-stu-id="f1a8f-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="f1a8f-132">grupo de recursos de Olá refere-se a localização de toohello Olá do grupo de recursos e não tem impacto na zona DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="f1a8f-133">localização de zona DNS Olá está sempre "global" e não é apresentada.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="f1a8f-134">Zonas DNS de lista</span><span class="sxs-lookup"><span data-stu-id="f1a8f-134">List DNS zones</span></span>

<span data-ttu-id="f1a8f-135">No portal do Azure de Olá, navegue demasiado**mais serviços** > **redes** > **zonas DNS**.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="f1a8f-136">Cada zona DNS é é seus próprios recursos, informações como o número de conjuntos de registos e servidores de nomes são visíveis desta vista.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="f1a8f-137">coluna Olá **servidores de nomes** não se encontra na vista de predefinição Olá, tooadd clique **colunas**, selecione **nome servidores** e clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![listar zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="f1a8f-139">Eliminar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="f1a8f-139">Delete a DNS zone</span></span>

<span data-ttu-id="f1a8f-140">Navegue tooa zona DNS no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="f1a8f-141">No Olá **zona DNS** painel, clique em **eliminar zona**.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="f1a8f-142">São tooconfirm pedido são intenção zona DNS de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="f1a8f-143">Também eliminar uma zona DNS elimina todos os registos de Olá que estão contidos na zona de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1a8f-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1a8f-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f1a8f-144">Next steps</span></span>

<span data-ttu-id="f1a8f-145">Saiba como toowork com a sua zona DNS e os registos, visitando [introdução ao DNS do Azure utilizando o portal do Azure de Olá](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f1a8f-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
