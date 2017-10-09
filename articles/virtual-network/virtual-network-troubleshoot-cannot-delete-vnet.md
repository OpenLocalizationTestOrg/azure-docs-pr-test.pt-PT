---
title: aaaCannot eliminar uma rede virtual no Azure | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema em que não é possível eliminar uma rede virtual no Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="453f6-103">Resolução de problemas: Falha toodelete uma rede virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="453f6-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="453f6-104">Poderá receber erros quando tenta toodelete uma rede virtual no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="453f6-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="453f6-105">Este artigo fornece a resolução de problemas de passos toohelp resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="453f6-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="453f6-106">Orientação na resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="453f6-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="453f6-107">[Verifique se um gateway de rede virtual está em execução na rede virtual Olá](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="453f6-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="453f6-108">[Verifique se um gateway de aplicação está em execução na rede virtual Olá](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="453f6-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="453f6-109">[Verifique se o serviço de domínio do Active Directory do Azure está ativado na rede virtual Olá](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="453f6-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="453f6-110">[Verifique se a rede virtual Olá está ligado tooother recursos](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="453f6-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="453f6-111">[Verifique se uma máquina virtual ainda está em execução na rede virtual Olá](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="453f6-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="453f6-112">[Verifique se a rede virtual Olá está encravada no migração](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="453f6-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="453f6-113">Passos de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="453f6-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="453f6-114">Verifique se um gateway de rede virtual está em execução na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="453f6-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="453f6-115">rede virtual do Olá tooremove, deverá remover primeiro o gateway de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="453f6-116">Para redes virtuais clássicas, visite toohello **descrição geral** página de rede virtual clássica Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="453f6-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="453f6-117">No Olá **ligações VPN** secção, se o gateway de Olá está em execução na rede virtual Olá, verá Olá IP endereço de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Verifique se o gateway está em execução](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="453f6-119">Para as redes virtuais, aceda toohello **descrição geral** página de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="453f6-120">Verifique **dispositivos ligados** Olá virtual gateway de rede.</span><span class="sxs-lookup"><span data-stu-id="453f6-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Verifique o dispositivo ligado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="453f6-122">Antes de poder remover gateway Olá, remova primeiro qualquer **ligação** objetos no gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="453f6-123">Verifique se um gateway de aplicação está em execução na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="453f6-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="453f6-124">Aceda toohello **descrição geral** página de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="453f6-125">Verifique Olá **dispositivos ligados** Olá gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="453f6-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Verifique o dispositivo ligado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="453f6-127">Se existir um gateway de aplicação, tem de removê-lo antes de poder eliminar a rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="453f6-128">Verifique se o serviço de domínio do Active Directory do Azure está ativado na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="453f6-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="453f6-129">Se Olá os serviços de domínio do Active Directory é ativado e ligado toohello rede virtual, não é possível eliminar esta rede virtual.</span><span class="sxs-lookup"><span data-stu-id="453f6-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Verifique o dispositivo ligado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="453f6-131">toodisable Olá serviço, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="453f6-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="453f6-132">Aceda toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="453f6-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="453f6-133">No painel esquerdo Olá, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="453f6-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="453f6-134">Selecione o diretório do Azure Active Directory (Azure AD) de Olá que tenha o serviço de domínio do Active Directory ativada.</span><span class="sxs-lookup"><span data-stu-id="453f6-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="453f6-135">Selecione Olá **configurar** separador.</span><span class="sxs-lookup"><span data-stu-id="453f6-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="453f6-136">Em **dos serviços de domínio**, alterar Olá **ativar os serviços de domínio para este diretório** opção demasiado**não**.</span><span class="sxs-lookup"><span data-stu-id="453f6-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="453f6-137">Verifique se a rede virtual Olá está ligado tooother recursos</span><span class="sxs-lookup"><span data-stu-id="453f6-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="453f6-138">Verifique a existência de ligações de circuito, ligações e peerings de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="453f6-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="453f6-139">Qualquer uma destas unidades podem provocar um toofail de eliminação de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="453f6-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="453f6-140">Olá ordem de eliminação recomendada é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="453f6-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="453f6-141">Ligações de gateway</span><span class="sxs-lookup"><span data-stu-id="453f6-141">Gateway connections</span></span>
2. <span data-ttu-id="453f6-142">Gateways</span><span class="sxs-lookup"><span data-stu-id="453f6-142">Gateways</span></span>
3. <span data-ttu-id="453f6-143">IPs</span><span class="sxs-lookup"><span data-stu-id="453f6-143">IPs</span></span>
4. <span data-ttu-id="453f6-144">Peerings de rede virtual</span><span class="sxs-lookup"><span data-stu-id="453f6-144">Virtual network peerings</span></span>
5. <span data-ttu-id="453f6-145">Ambiente de serviço de aplicações (ASE)</span><span class="sxs-lookup"><span data-stu-id="453f6-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="453f6-146">Verifique se uma máquina virtual ainda está em execução na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="453f6-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="453f6-147">Certifique-se de que nenhuma máquina virtual na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="453f6-148">Verifique se a rede virtual Olá está encravada no migração</span><span class="sxs-lookup"><span data-stu-id="453f6-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="453f6-149">Se a rede virtual Olá está encravada no estado de migração, não pode ser eliminada.</span><span class="sxs-lookup"><span data-stu-id="453f6-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="453f6-150">Execute Olá migração de Olá tooabort de comando a seguir e, em seguida, elimine a rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="453f6-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="453f6-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="453f6-151">Next steps</span></span>

- [<span data-ttu-id="453f6-152">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="453f6-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="453f6-153">Perguntas mais frequentes (FAQ) da Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="453f6-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)