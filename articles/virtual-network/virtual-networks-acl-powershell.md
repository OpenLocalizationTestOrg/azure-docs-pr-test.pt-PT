---
title: "listas de controlo de aaaManage acesso de ponto final do Azure | PowerShell | Clássico | Microsoft Docs"
description: Saiba como toomanage ACLs com o PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="7b297-103">Gerir listas de controlo de acesso de ponto final com o PowerShell no modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="7b297-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="7b297-104">Pode criar e gerir o controlo de acesso de rede lista (ACLs) para pontos finais utilizando o Azure PowerShell ou na Olá Portal de gestão.</span><span class="sxs-lookup"><span data-stu-id="7b297-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="7b297-105">Neste tópico, encontrará procedimentos para tarefas comuns de ACL que pode realizar com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b297-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="7b297-106">Para obter lista de Olá do Azure PowerShell cmdlets consulte [Cmdlets de gestão do Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="7b297-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="7b297-107">Para obter mais informações sobre as ACLs, consulte [o que é uma lista de controlo de acesso de rede (ACL)?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="7b297-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="7b297-108">Se pretender toomanage as ACLs utilizando o Portal de gestão de Olá, veja [como tooSet pontos finais de cópia de segurança tooa Máquina Virtual](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b297-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="7b297-109">Gerir ACLs de rede utilizando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b297-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="7b297-110">Pode utilizar o Azure PowerShell cmdlets toocreate, remova e configure (conjunto) rede acesso as listas de controlo (ACLs).</span><span class="sxs-lookup"><span data-stu-id="7b297-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="7b297-111">Iremos tiver incluído alguns exemplos de algumas formas de Olá que pode configurar uma ACL com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b297-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="7b297-112">tooretrieve uma lista completa dos cmdlets do PowerShell de ACL de Olá, pode utilizar qualquer um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="7b297-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="7b297-113">Criar uma ACL de rede com regras que permitem o acesso a partir de uma sub-rede remota</span><span class="sxs-lookup"><span data-stu-id="7b297-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="7b297-114">exemplo de Olá abaixo ilustra uma toocreate de forma uma que contém as regras de ACL de novo.</span><span class="sxs-lookup"><span data-stu-id="7b297-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="7b297-115">Em seguida, é aplicada esta ACL de ponto final de máquina virtual tooa.</span><span class="sxs-lookup"><span data-stu-id="7b297-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="7b297-116">regras de ACL de Olá no exemplo Olá abaixo permitirá o acesso a partir de uma sub-rede remota.</span><span class="sxs-lookup"><span data-stu-id="7b297-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="7b297-117">toocreate uma ACL de rede nova com regras de autorização para uma sub-rede remota, abra uma ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b297-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="7b297-118">Copie e cole o script Olá abaixo, configurando o script de Olá com os seus próprios valores e, em seguida, execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="7b297-119">Crie Olá novo objeto de ACL de rede.</span><span class="sxs-lookup"><span data-stu-id="7b297-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="7b297-120">Defina uma regra que permite acesso de sub-rede remota.</span><span class="sxs-lookup"><span data-stu-id="7b297-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="7b297-121">Exemplo de Olá abaixo, definir regra *100* (que tem prioridade sobre regra 200 e superior) sub-rede remota de Olá tooallow *10.0.0.0/8* aceder ao ponto final de máquina virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="7b297-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="7b297-122">Substitua os valores de Olá os seus requisitos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7b297-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="7b297-123">o nome de Olá "Configuração de ACL de SharePoint" deve ser substituído com o nome amigável Olá que pretende toocall esta regra.</span><span class="sxs-lookup"><span data-stu-id="7b297-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="7b297-124">Para as regras adicionais, repita o cmdlet Olá, substituindo os valores de Olá com os seus próprios requisitos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7b297-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="7b297-125">Ser se toochange Olá regra número Order tooreflect Olá ordem em que pretende Olá regras toobe aplicada.</span><span class="sxs-lookup"><span data-stu-id="7b297-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="7b297-126">número de regra inferior Olá tem precedência sobre o número mais alto Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="7b297-127">Em seguida, pode criar um novo ponto final (Add) ou definir Olá ACL para um ponto final existente (conjunto).</span><span class="sxs-lookup"><span data-stu-id="7b297-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="7b297-128">Neste exemplo, iremos adicionar que um novo ponto final da máquina virtual denominada "web" e a atualização Olá máquina virtual ponto final com Olá as definições de ACL.</span><span class="sxs-lookup"><span data-stu-id="7b297-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="7b297-129">Em seguida, combinar cmdlets Olá e execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="7b297-130">Para este exemplo Olá cmdlets combinados seria este aspeto:</span><span class="sxs-lookup"><span data-stu-id="7b297-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="7b297-131">Remover uma regra de ACL de rede que permite acesso de sub-rede remota</span><span class="sxs-lookup"><span data-stu-id="7b297-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="7b297-132">exemplo de Olá abaixo ilustra uma tooremove de forma uma regra ACL de rede.</span><span class="sxs-lookup"><span data-stu-id="7b297-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="7b297-133">tooremove uma regra de ACL de rede com permitir regras para uma sub-rede remota, abra uma ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b297-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="7b297-134">Copie e cole o script Olá abaixo, configurando o script de Olá com os seus próprios valores e, em seguida, execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="7b297-135">Primeiro passo é o objeto de ACL de rede de Olá tooget para o ponto final de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="7b297-136">Em seguida, removeremos a regra de ACL de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="7b297-137">Neste caso, estamos a removê-lo por ID de regra.</span><span class="sxs-lookup"><span data-stu-id="7b297-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="7b297-138">Isto removerá o ID de regra de Olá 0 apenas do Olá ACL.</span><span class="sxs-lookup"><span data-stu-id="7b297-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="7b297-139">Não remove objecto ACL de Olá do ponto final de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="7b297-140">Em seguida, tem de aplicar Olá ACL de rede objeto toohello virtual ponto final da máquina e atualizar a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="7b297-141">Remover uma ACL de rede de um ponto final da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7b297-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="7b297-142">Em certos cenários, pode querer tooremove um objeto de ACL de rede a partir de um ponto final da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7b297-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="7b297-143">toodo que, abra uma ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b297-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="7b297-144">Copie e cole o script Olá abaixo, configurando o script de Olá com os seus próprios valores e, em seguida, execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b297-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="7b297-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7b297-145">Next steps</span></span>
[<span data-ttu-id="7b297-146">O que é uma lista de controlo de acesso de rede (ACL)?</span><span class="sxs-lookup"><span data-stu-id="7b297-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

