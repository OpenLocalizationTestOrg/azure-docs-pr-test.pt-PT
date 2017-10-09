---
title: "os NSGs aaaManage utilizando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toomanage existente NSGs utilizando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="cda90-103">Gerir os NSGs através do portal Olá</span><span class="sxs-lookup"><span data-stu-id="cda90-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cda90-104">Portal</span><span class="sxs-lookup"><span data-stu-id="cda90-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="cda90-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cda90-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="cda90-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cda90-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="cda90-107">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cda90-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cda90-108">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="cda90-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="cda90-109">Obter as informações</span><span class="sxs-lookup"><span data-stu-id="cda90-109">Retrieve Information</span></span>
<span data-ttu-id="cda90-110">Pode ver os seus NSGs existentes, obter as regras para um NSG existente e descobrir os recursos que um NSG é associado a.</span><span class="sxs-lookup"><span data-stu-id="cda90-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="cda90-111">Ver os NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="cda90-111">View existing NSGs</span></span>

<span data-ttu-id="cda90-112">todos os tooview existente NSGs numa subscrição, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-113">Num browser, navegue toohttp://portal.azure.com e, se necessário, inicie sessão com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cda90-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="cda90-114">Clique em **Procurar >** > **grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="cda90-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="cda90-116">Verifique a lista de Olá de NSGs em Olá **grupos de segurança de rede** painel.</span><span class="sxs-lookup"><span data-stu-id="cda90-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="cda90-118">Vista NSGs num grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cda90-118">View NSGs in a resource group</span></span>

<span data-ttu-id="cda90-119">lista de Olá tooview de NSGs em Olá **RG NSG** grupo de recursos, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-120">Clique em **grupos de recursos >** > **RG NSG** > **...** .</span><span class="sxs-lookup"><span data-stu-id="cda90-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="cda90-122">Na lista de Olá de recursos, procure itens a apresentar o ícone NSG Olá, conforme mostrado no Olá **recursos** painel abaixo.</span><span class="sxs-lookup"><span data-stu-id="cda90-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="cda90-124">Listar todas as regras para um NSG</span><span class="sxs-lookup"><span data-stu-id="cda90-124">List all rules for an NSG</span></span>

<span data-ttu-id="cda90-125">regras de Olá tooview de um NSG denominado **NSG-front-end**, completa Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-126">De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="cda90-127">No Olá **definições** separador, clique em **regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="cda90-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="cda90-129">Olá **regras de segurança de entrada** painel é apresentado como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cda90-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="cda90-131">No Olá **definições** separador, clique em **regras de segurança de saída** toosee Olá regras de saída.</span><span class="sxs-lookup"><span data-stu-id="cda90-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cda90-132">regras de predefinidas tooview, clique em Olá **predefinido regras** ícone, Olá parte superior do painel de Olá que apresenta as regras de Olá.</span><span class="sxs-lookup"><span data-stu-id="cda90-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="cda90-133">Ver as associações de NSGs</span><span class="sxs-lookup"><span data-stu-id="cda90-133">View NSGs associations</span></span>

<span data-ttu-id="cda90-134">tooview que Olá recursos **NSG-front-end** NSG é Olá associar com, concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-135">De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="cda90-136">No Olá **definições** separador, clique em **sub-redes** tooview são as sub-redes associados toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="cda90-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="cda90-138">No Olá **definições** separador, clique em **interfaces de rede** tooview que estão associados NICs toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="cda90-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="cda90-139">Gerir as regras</span><span class="sxs-lookup"><span data-stu-id="cda90-139">Manage rules</span></span>
<span data-ttu-id="cda90-140">Pode adicionar tooan regras existentes NSG, editar regras existentes e remova regras.</span><span class="sxs-lookup"><span data-stu-id="cda90-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="cda90-141">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="cda90-141">Add a rule</span></span>
<span data-ttu-id="cda90-142">tooadd uma regra que permite **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-143">De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="cda90-144">No Olá **definições** separador, clique em **regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="cda90-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="cda90-145">No Olá **regras de segurança de entrada** painel, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cda90-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="cda90-146">Em seguida, no Olá **Adicionar regra de segurança de entrada** painel, preencher valores de Olá, conforme mostrado abaixo e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cda90-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="cda90-148">Após alguns segundos, repare a nova regra de Olá no Olá **regras de segurança de entrada** painel.</span><span class="sxs-lookup"><span data-stu-id="cda90-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="cda90-150">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="cda90-150">Change a rule</span></span>
<span data-ttu-id="cda90-151">regra de Olá toochange criada acima tooallow de entrada do tráfego de Olá **Internet** Olá concluída, apenas os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-152">De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="cda90-153">No Olá **definições** separador, clique em regras de Olá criada acima.</span><span class="sxs-lookup"><span data-stu-id="cda90-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="cda90-154">No Olá **https permitir** painel, alteração Olá **origem** propriedade conforme mostrado abaixo e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="cda90-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="cda90-156">Eliminar uma regra</span><span class="sxs-lookup"><span data-stu-id="cda90-156">Delete a rule</span></span>

<span data-ttu-id="cda90-157">toodelete Olá regra criado acima, completa Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-158">De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="cda90-159">No Olá **definições** separador, clique em regras de Olá criada acima.</span><span class="sxs-lookup"><span data-stu-id="cda90-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="cda90-160">No Olá **https permitir** painel, clique em **eliminar**e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="cda90-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="cda90-162">Gerir as associações</span><span class="sxs-lookup"><span data-stu-id="cda90-162">Manage associations</span></span>
<span data-ttu-id="cda90-163">Pode associar um NSG toosubnets e NICs.</span><span class="sxs-lookup"><span data-stu-id="cda90-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="cda90-164">Também pode desassociar um NSG a partir de qualquer recurso que está associado.</span><span class="sxs-lookup"><span data-stu-id="cda90-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="cda90-165">Associar um NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="cda90-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="cda90-166">Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-167">De Olá **grupos de segurança de rede** painel ou Olá **recursos** painel mostrado acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="cda90-168">No Olá **definições** separador, clique em **interfaces de rede** > **associar** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="cda90-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="cda90-170">Desassociar um NSG a partir de uma NIC</span><span class="sxs-lookup"><span data-stu-id="cda90-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="cda90-171">Olá toodissociate **NSG-front-end** NSG de Olá **TestNICWeb1** NIC, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-172">No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="cda90-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="cda90-173">No Olá **TestNICWeb1** painel, clique em **alterar segurança...**   >  **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="cda90-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="cda90-175">Também pode utilizar este painel tooassociate Olá NIC tooany existente NSG.</span><span class="sxs-lookup"><span data-stu-id="cda90-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="cda90-176">Desassociar um NSG de sub-rede</span><span class="sxs-lookup"><span data-stu-id="cda90-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="cda90-177">Olá toodissociate **NSG-front-end** NSG de Olá **front-end** sub-rede, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-178">No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="cda90-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="cda90-179">No Olá **definições** painel, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="cda90-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="cda90-181">No Olá **front-end** painel, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="cda90-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="cda90-183">Associar uma sub-rede de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="cda90-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="cda90-184">Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cda90-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="cda90-185">No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="cda90-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="cda90-186">No Olá **definições** painel, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="cda90-187">No Olá **front-end** painel, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="cda90-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="cda90-188">Também pode associar uma sub-rede de tooa NSG das thh NSG **definições** painel.</span><span class="sxs-lookup"><span data-stu-id="cda90-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="cda90-189">Eliminar um NSG</span><span class="sxs-lookup"><span data-stu-id="cda90-189">Delete an NSG</span></span>
<span data-ttu-id="cda90-190">Só é possível eliminar um NSG se tooany recurso não está associado.</span><span class="sxs-lookup"><span data-stu-id="cda90-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="cda90-191">toodelete um NSG, Olá concluir os passos seguintes:.</span><span class="sxs-lookup"><span data-stu-id="cda90-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="cda90-192">No portal do Azure Olá, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="cda90-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="cda90-193">No Olá **definições** painel, clique em **interfaces de rede**.</span><span class="sxs-lookup"><span data-stu-id="cda90-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="cda90-194">Se existirem quaisquer NICs listados, clique em Olá NIC e siga o passo 2 [desassociar um NSG a partir de uma NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="cda90-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="cda90-195">Repita o passo 3 para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="cda90-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="cda90-196">No Olá **definições** painel, clique em **sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="cda90-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="cda90-197">Se existirem quaisquer sub-redes listados, clique em sub-rede Olá e siga os passos 2 e 3 na [desassociar um NSG de sub-rede](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="cda90-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="cda90-198">Desloca toohello esquerdo **NSG-front-end** painel, em seguida, clique em **eliminar** > **Sim**.</span><span class="sxs-lookup"><span data-stu-id="cda90-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portal do Azure – NSGs](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="cda90-200">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cda90-200">Next steps</span></span>
* <span data-ttu-id="cda90-201">[Ativar o registo](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="cda90-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
