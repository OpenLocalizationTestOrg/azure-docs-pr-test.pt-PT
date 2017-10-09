---
title: "aaaConfigure endereços IP privados para as VMs (clássica) - portal do Azure | Microsoft Docs"
description: "Saiba como endereços IP privados tooconfigure para máquinas virtuais (clássicas) utilizando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="f17ed-103">Configurar endereços IP privados para uma máquina virtual (clássica) utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f17ed-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f17ed-104">Este artigo abrange o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="f17ed-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="f17ed-105">Também pode [gerir um endereço IP privado estático no modelo de implementação do Resource Manager Olá](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="f17ed-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="f17ed-106">passos de exemplo de Olá abaixo esperam num ambiente simple que já criado.</span><span class="sxs-lookup"><span data-stu-id="f17ed-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="f17ed-107">Se pretender que os passos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá descrito [criar uma vnet](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="f17ed-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="f17ed-108">Como toospecify um privada endereços IP estáticos quando criar uma VM</span><span class="sxs-lookup"><span data-stu-id="f17ed-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="f17ed-109">toocreate uma VM chamada *DNS01* no Olá *front-end* sub-rede de uma VNet com o nome *TestVNet* com um IP privado estático de *192.168.1.101*, Siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="f17ed-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="f17ed-110">Num browser, navegue toohttp://portal.azure.com e, se necessário, inicie sessão com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f17ed-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="f17ed-111">Clique em **novo** > **computação** > **Windows Server 2012 R2 Datacenter**, tenha em atenção que Olá **selecionar um modelo de implementação** já lista mostra **clássico**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f17ed-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="f17ed-113">No Olá **criar VM** painel, introduza o nome de Olá de Olá VM toobe criado (*DNS01* no nosso cenário), Olá conta de administrador local e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="f17ed-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="f17ed-115">Clique em **configuração opcional** > **rede** > **rede Virtual**e, em seguida, clique em **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="f17ed-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="f17ed-116">Se **TestVNet** não está disponível, certifique-se de que está a utilizar Olá *EUA Central* localização e tiver criado o ambiente de teste de Olá descrita no início de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f17ed-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="f17ed-118">No Olá **rede** painel, marca de sub-rede Olá se, atualmente selecionada é *front-end*, em seguida, clique em **endereços IP**, em **aatribuiçãodeendereçosIP** clique **estático**e, em seguida, introduza *192.168.1.101* para **endereço IP** como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="f17ed-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="f17ed-120">Clique em **OK** no Olá **endereços IP** painel, em seguida, clique em **OK** no Olá **rede** painel e clique em **OK**no Olá **configuração opcional** painel.</span><span class="sxs-lookup"><span data-stu-id="f17ed-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="f17ed-121">No Olá **criar VM** painel, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f17ed-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="f17ed-122">Tenha em atenção Olá mosaico abaixo apresentado no dashboard.</span><span class="sxs-lookup"><span data-stu-id="f17ed-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="f17ed-124">Como as informações de uma VM do endereço IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="f17ed-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="f17ed-125">tooview Olá privadas informações endereços IP estáticos para Olá VM criada com os passos de Olá acima, executar passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="f17ed-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="f17ed-126">No portal do Azure do Azure Olá, clique em **Procurar tudo** > **máquinas virtuais (clássicas)** > **DNS01**  >   **Todas as definições** > **endereços IP** e repare Olá atribuição de endereços IP e o endereço IP, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="f17ed-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="f17ed-128">Como tooremove um privada endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="f17ed-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="f17ed-129">tooremove Olá endereço IP privado estático de Olá VM criada acima, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="f17ed-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="f17ed-130">De Olá **endereços IP** painel mostrado acima, clique em **dinâmica** toohello à direita dos **atribuição de endereços IP**, em seguida, clique em **guardar**e, em seguida, Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f17ed-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Criar a VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="f17ed-132">Como tooadd um IP privado estático endereços tooan existente VM</span><span class="sxs-lookup"><span data-stu-id="f17ed-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="f17ed-133">tooadd um estático privada IP endereço toohello VM criada utilizando Olá passos acima, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="f17ed-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="f17ed-134">De Olá **endereços IP** painel mostrado acima, clique em **estático** toohello à direita dos **atribuição de endereços IP**.</span><span class="sxs-lookup"><span data-stu-id="f17ed-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="f17ed-135">Tipo *192.168.1.101* para **endereço IP**, em seguida, clique em **guardar**e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f17ed-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f17ed-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f17ed-136">Next steps</span></span>
* <span data-ttu-id="f17ed-137">Saiba mais sobre [reservado de IP público](virtual-networks-reserved-public-ip.md) endereços.</span><span class="sxs-lookup"><span data-stu-id="f17ed-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="f17ed-138">Saiba mais sobre [instância ao nível do IP público (ILPIP)](virtual-networks-instance-level-public-ip.md) endereços.</span><span class="sxs-lookup"><span data-stu-id="f17ed-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="f17ed-139">Consulte Olá [as APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="f17ed-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

