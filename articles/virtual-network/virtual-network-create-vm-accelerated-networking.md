---
title: "aaaCreate uma máquina virtual do Azure com acelerados rede | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual com acelerados da rede."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="2d1c3-103">Criar uma máquina virtual com acelerados da rede</span><span class="sxs-lookup"><span data-stu-id="2d1c3-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="2d1c3-104">Neste tutorial, saiba como toocreate uma Máquina Virtual do Azure (VM) a com acelerados da rede.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="2d1c3-105">Redes na melhoria são GA para Windows e numa pré-visualização pública para as distribuições do Linux específicas.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="2d1c3-106">Redes na melhoria permite tooa de Virtualização (SR-IOV) de e/s de raiz única VM, melhorando em grande medida o desempenho de rede.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="2d1c3-107">Este caminho de elevado desempenho ignora o anfitrião Olá datapath Olá, reduzindo a latência, interferência e utilização da CPU, para utilização com Olá mais pedir o seu trabalho rede cargas de trabalho em tipos VM suportados.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="2d1c3-108">Olá seguinte imagem mostra comunicação entre duas máquinas virtuais (VM), com e sem redes na melhoria:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Comparação](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="2d1c3-110">Sem redes na melhoria, todo o tráfego de rede que entra e sai Olá VM tem atravessar anfitrião Olá e do comutador virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="2d1c3-111">comutador virtual Olá fornece a imposição de políticas de todos os, tais como grupos de segurança de rede acedam listas de controlo, isolamento e outro tráfego de toonetwork de serviços de rede virtualizado.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="2d1c3-112">mais informações sobre comutadores virtuais, leia Olá toolearn [Virtualização de rede do Hyper-V e do comutador virtual](https://technet.microsoft.com/library/jj945275.aspx) artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="2d1c3-113">Com redes na melhoria, o tráfego de rede chega à interface de rede da VM Olá (NIC) e, em seguida, é reencaminhado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="2d1c3-114">Aplica-se todas as políticas de rede que Olá comutador virtual sem redes na melhoria são descarregadas sendo aplicada no hardware.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="2d1c3-115">Aplicar a política de hardware permite Olá NIC tooforward tráfego de rede diretamente toohello VM, ignorando anfitrião Olá e do comutador virtual de Olá, enquanto mantém todos os Olá política-aplicada no anfitrião de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="2d1c3-116">Olá vantagens do funcionamento em rede na melhoria só se aplicam toohello VM que está ativada no.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="2d1c3-117">Para obter melhores resultados Olá, é ideal tooenable esta funcionalidade em, pelo menos, duas VMs ligado toohello mesma rede Virtual do Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="2d1c3-118">Quando a comunicação entre VNets ou ligação no local, esta funcionalidade tem a latência de toooverall um impacto mínimo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="2d1c3-119">Este Linux pré-visualização pública pode não ter Olá mesmo nível de disponibilidade e fiabilidade, tal como as funcionalidades que estão em geral lançamento de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="2d1c3-120">funcionalidade de Olá não é suportada, pode ter restrita capacidades e poderão não estar disponível em todas as localizações do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="2d1c3-121">Para notificações mais atualizadas à sua Olá, disponibilidade e o estado desta funcionalidade, verificar atualizações Olá de rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="2d1c3-122">Benefícios</span><span class="sxs-lookup"><span data-stu-id="2d1c3-122">Benefits</span></span>
* <span data-ttu-id="2d1c3-123">**Reduzir a latência / superiores pacotes por segundo (pps):** remover comutador virtual de Olá de Olá datapath remove tempo Olá gastam de pacotes no anfitrião de Olá para processamento da política e aumenta Olá número de pacotes que podem ser processados no interior Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="2d1c3-124">**Reduzido interferência:** comutador Virtual de processamento depende da quantidade de Olá de política que tem toobe aplicada e Olá carga de trabalho de Olá da CPU que está a fazer o processamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="2d1c3-125">A descarga de hardware de toohello de imposição de política de Olá remove esse variabilidade fornecendo pacotes diretamente toohello VM, a remoção de comunicação de tooVM Olá anfitrião e todas as interrupções de software e contexto muda.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="2d1c3-126">**Diminuir a utilização da CPU:** Bypassing Olá virtual comutador do anfitrião de Olá leva a utilização da CPU tooless para processar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="2d1c3-127"><a name="Limitations"></a>Limitações</span><span class="sxs-lookup"><span data-stu-id="2d1c3-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="2d1c3-128">Quando utilizar esta capacidade de existir Olá seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="2d1c3-129">**Criação de interface de rede:** Accelerated redes só podem ser ativada para uma NIC de novo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="2d1c3-130">Não pode ser ativada para uma NIC que existente.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="2d1c3-131">**A criação de VM:** A NIC com redes na melhoria ativada pode apenas ser anexada tooa VM ao hello é criada a VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="2d1c3-132">Olá NIC não pode ser anexado tooan existente VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="2d1c3-133">**Regiões:** VMs do Windows com redes na melhoria são disponibilizadas em regiões mais do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="2d1c3-134">VMs com Linux com redes na melhoria são disponibilizadas em várias regiões.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="2d1c3-135">está a expandir as regiões de Olá esta capacidade está disponível.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="2d1c3-136">Consulte o blogue de atualizações de rede Virtual do Azure Olá abaixo para obter informações mais recentes do Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="2d1c3-137">**Sistemas operativos suportados:** Windows: Centro de dados do Microsoft Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="2d1c3-138">Linux: Ubuntu Server 16.04 LTS com 4.4.0-77 de kernel ou superior, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (publicado por "Não autorizado Wave Software").</span><span class="sxs-lookup"><span data-stu-id="2d1c3-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="2d1c3-139">**Tamanho da VM:** fins gerais e os tamanhos de instância com otimização de computação com oito ou vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="2d1c3-140">Para obter mais informações, consulte Olá [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="2d1c3-141">Olá conjunto de tamanhos de instância VM suportados irá expandir no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="2d1c3-142">**Apenas a implementação através do Azure Resource Manager (ARM):** acelerados redes não está disponível para implementação através da ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="2d1c3-143">Limitações de toothese as alterações sejam anunciadas através de Olá [a rede Virtual do Azure atualiza](https://azure.microsoft.com/updates/accelerated-networking-in-preview) página.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="2d1c3-144">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="2d1c3-144">Create a Windows VM</span></span>
<span data-ttu-id="2d1c3-145">Pode utilizar Olá portal do Azure ou para o Azure [PowerShell](#windows-powershell) toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="2d1c3-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="2d1c3-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="2d1c3-147">A partir do browser da Internet, abra Olá Azure [portal](https://portal.azure.com) e inicie sessão com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2d1c3-148">Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="2d1c3-149">No portal de Olá, clique em **+ novo** > **computação** > **Datacenter do Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="2d1c3-150">No Olá **Datacenter do Windows Server 2016** painel que aparece, deixe *Resource Manager* selecionado em **selecionar um modelo de implementação**e clique em **criar** .</span><span class="sxs-lookup"><span data-stu-id="2d1c3-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="2d1c3-151">No Olá **Noções básicas** painel apresentado, introduza os seguintes valores de Olá, deixe as restantes opções predefinidas de Olá ou selecione ou introduza os seus próprios valores e clique em Olá **OK** botão:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="2d1c3-152">Definição</span><span class="sxs-lookup"><span data-stu-id="2d1c3-152">Setting</span></span>|<span data-ttu-id="2d1c3-153">Valor</span><span class="sxs-lookup"><span data-stu-id="2d1c3-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="2d1c3-154">Nome</span><span class="sxs-lookup"><span data-stu-id="2d1c3-154">Name</span></span>|<span data-ttu-id="2d1c3-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="2d1c3-155">MyVm</span></span>|
    |<span data-ttu-id="2d1c3-156">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2d1c3-156">Resource group</span></span>|<span data-ttu-id="2d1c3-157">Deixe **criar nova** selecionada e introduza *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="2d1c3-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="2d1c3-158">Localização</span><span class="sxs-lookup"><span data-stu-id="2d1c3-158">Location</span></span>|<span data-ttu-id="2d1c3-159">EUA Oeste 2</span><span class="sxs-lookup"><span data-stu-id="2d1c3-159">West US 2</span></span>|

    <span data-ttu-id="2d1c3-160">Se tiver tooAzure novo, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscrições](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [localizações](https://azure.microsoft.com/regions) (que também são denominados tooas regiões).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="2d1c3-161">No Olá **escolher um tamanho** painel apresentado, introduza *8* no Olá **núcleos mínimo** caixa, em seguida, clique em **ver todos os**.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="2d1c3-162">Clique em **DS4_V2 padrão**, ou suportada qualquer uma VM, em seguida, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="2d1c3-163">No Olá **definições** painel que aparece, deixe todas as definições como-é, exceto clique **ativado** em **acelerados redes**, em seguida, clique em Olá **OK** botão.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="2d1c3-164">**Nota:** se, nos passos anteriores, selecionou os valores de tamanho VM, sistema operativo ou localização que não estão listados no Olá [limitações](#Limitations) secção deste artigo, **Accelerated redes**não está visível.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="2d1c3-165">No Olá **resumo** painel apresentado, clique em Olá **OK** botão.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="2d1c3-166">Azure inicia a criação de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="2d1c3-167">Criação de VM demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="2d1c3-168">Olá tooinstall acelerados controlador de rede para o Windows, Olá concluir os passos em Olá [configurar Windows](#configure-windows) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="2d1c3-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d1c3-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="2d1c3-170">Instale a versão mais recente do Olá do Olá Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="2d1c3-171">Se tiver tooAzure nova do PowerShell, leia Olá [descrição geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="2d1c3-172">Inicie uma sessão do PowerShell, clicando em botão Iniciar do Windows hello, escrevendo **powershell**, em seguida, clicar em **PowerShell** de resultados da pesquisa Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="2d1c3-173">Na janela do PowerShell, introduza Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2d1c3-174">Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="2d1c3-175">No seu browser, copie Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="2d1c3-176">Na janela do PowerShell, faça duplo clique script de Olá toopaste e iniciar a execução-lo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="2d1c3-177">Lhe for pedido um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-177">You are prompted for a username and password.</span></span> <span data-ttu-id="2d1c3-178">Utilize estas credenciais toolog toohello VM ao ligar tooit no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="2d1c3-179">Se o script de Olá falha e alterar os valores no script de Olá antes de executar este, confirme valores Olá que utilizou para o tamanho da VM, sistema operativo, e localização estão listadas no Olá [limitações](#Limitations) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="2d1c3-180">Olá tooinstall acelerados controlador de rede para o Windows, Olá concluir os passos em Olá [configurar Windows](#configure-windows) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="2d1c3-181"><a name="configure-windows"></a>Configurar o Windows</span><span class="sxs-lookup"><span data-stu-id="2d1c3-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="2d1c3-182">Depois de criar Olá VM no Azure, tem de instalar o controlador de rede na melhoria de Olá para Windows.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="2d1c3-183">Antes de concluir os seguintes passos de Olá, tem de ter criado uma VM do Windows com redes na melhoria utilizando qualquer um dos Olá [portal](#windows-portal) ou [PowerShell](#windows-powershell) passos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="2d1c3-184">A partir do browser da Internet, abra Olá Azure [portal](https://portal.azure.com) e inicie sessão com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2d1c3-185">Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="2d1c3-186">Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="2d1c3-187">Quando **MyVm** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="2d1c3-188">No Olá **MyVm** painel apresentado, clique em Olá **Connect** botão no canto esquerdo superior do painel de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="2d1c3-189">**Nota:** se **criar** é visível em Olá **Connect** botão, Azure não ainda acabou de criar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="2d1c3-190">Clique em **Connect** apenas depois de já não vê **criar** em Olá **Connect** botão.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="2d1c3-191">Permitir o Olá toodownload do browser **MyVm.rdp** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="2d1c3-192">Depois de transferido, clique em Olá ficheiro tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="2d1c3-193">Clique em Olá **Connect** botão no Olá **ligação ao ambiente de trabalho remoto** caixa que aparece, notificam que Olá não seja possível identificar o publicador da ligação remota Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="2d1c3-194">No Olá **segurança do Windows** caixa apresentada, clique em **mais opções**, em seguida, clique em **utilizar uma conta diferente**.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="2d1c3-195">Introduza Olá nome de utilizador e palavra-passe que introduziu no passo 4, em seguida, clique em Olá **OK** botão.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="2d1c3-196">Clique em Olá **Sim** botão na caixa de ligação de ambiente de trabalho remoto Olá que aparece, notificam que não é possível verificar a identidade de Olá do computador remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="2d1c3-197">Clique no botão de iniciar o Windows hello e clique em **Gestor de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="2d1c3-198">Expanda Olá **adaptadores de rede** nós.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="2d1c3-199">Confirme que Olá **adaptador de Ethernet de função Virtual Mellanox ConnectX 3** for apresentada, conforme mostrado na Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Gestor de dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="2d1c3-201">Na melhoria de redes está agora ativada para a VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="2d1c3-202">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="2d1c3-202">Create a Linux VM</span></span>
<span data-ttu-id="2d1c3-203">Pode utilizar Olá portal do Azure ou para o Azure [PowerShell](#linux-powershell) toocreate um Ubuntu ou SLES VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="2d1c3-204">Para RHEL e CentOS VMs é um fluxo de trabalho diferentes.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="2d1c3-205">Consulte as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="2d1c3-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="2d1c3-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="2d1c3-207">Registar-se Olá acelerado redes para pré-visualização do Linux, efetuando os passos 1 a 5 para Olá [criar uma VM com Linux - PowerShell](#linux-powershell) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="2d1c3-208">Não é possível registar para a pré-visualização de Olá no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="2d1c3-209">Concluir os passos 1-8 de Olá em [criar uma VM do Windows - portal](#windows-portal) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="2d1c3-210">No passo 2, clique em **Ubuntu Server 16.04 LTS** em vez de **Datacenter do Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="2d1c3-211">Para este tutorial, escolha toouse uma palavra-passe, em vez de uma chave SSH, embora para implementações de produção, pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="2d1c3-212">Se **acelerados redes** não aparecer quando concluir o passo 7 Olá [criar uma VM do Windows - portal](#windows-portal) secção deste artigo, é provável para uma das Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="2d1c3-213">Ainda não está registado para a pré-visualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="2d1c3-214">Confirme que o seu estado de registo é **registada**, conforme explicado no passo 4 do Olá [criar uma VM com Linux - Powershell](#linux-powershell) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="2d1c3-215">**Nota:** se participaram no Olá Accelerated de rede para a pré-visualização de VMs do Windows (respetivo não toouse tooregister necessários mais acelerado redes para VMs do Windows), não está automaticamente registados para Olá Accelerated redes para Pré-visualização de VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="2d1c3-216">Tem de registar para Olá Accelerated redes para VMs com Linux pré-visualizar tooparticipate no mesmo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="2d1c3-217">Não selecionou um tamanho de VM, o sistema operativo ou a localização indicada na Olá [limitações](#limitations) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="2d1c3-218">Olá tooinstall acelerados controlador de rede para o Linux, Olá concluir os passos em Olá [configurar Linux](#configure-linux) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="2d1c3-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d1c3-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="2d1c3-220">Se criar VMs com Linux com redes na melhoria numa subscrição e, em seguida, tente toocreate uma VM do Windows com redes na melhoria no Olá mesma subscrição, Olá a criação de Windows VM-la poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="2d1c3-221">Durante esta pré-visualização, recomenda-se que teste o Linux e VMs do Windows com redes na melhoria em subscrições diferentes.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="2d1c3-222">Instale a versão mais recente do Olá do Olá Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="2d1c3-223">Se tiver tooAzure nova do PowerShell, leia Olá [descrição geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="2d1c3-224">Inicie uma sessão do PowerShell, clicando em botão Iniciar do Windows hello, escrevendo **powershell**, em seguida, clicar em **PowerShell** de resultados da pesquisa Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="2d1c3-225">Na janela do PowerShell, introduza Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2d1c3-226">Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="2d1c3-227">Registar-se Olá acelerado redes para o Azure pré-visualização concluindo Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="2d1c3-228">Enviar um e-mail demasiado[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) com o ID de subscrição do Azure e a utilização pretendida.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="2d1c3-229">Aguarde um e-mail de confirmação da Microsoft sobre a sua subscrição que está a ser ativada.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="2d1c3-230">Introduza Olá tooconfirm comandos que estão registados para pré-visualização Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="2d1c3-231">Não continue com o passo 5 até **registada** aparece no Olá depois de introduzir o comando anterior Olá de saída.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="2d1c3-232">O resultado tem aspeto seguinte Olá saída antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="2d1c3-233">Se participaram no Olá Accelerated de rede para a pré-visualização de VMs do Windows (respetivo não toouse tooregister necessários mais acelerado redes para VMs do Windows), não está automaticamente registados para Olá Accelerated de rede para a pré-visualização de VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="2d1c3-234">Tem de registar para Olá Accelerated redes para VMs com Linux pré-visualizar tooparticipate no mesmo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="2d1c3-235">No seu browser, copie Olá seguinte script substituindo Ubuntu ou SLES conforme pretendido.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="2d1c3-236">Novamente, VM de Redhat e CentOS têm um fluxo de trabalho diferentes descrito abaixo:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="2d1c3-237">Na janela do PowerShell, faça duplo clique script de Olá toopaste e iniciar a execução-lo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="2d1c3-238">Lhe for pedido um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-238">You are prompted for a username and password.</span></span> <span data-ttu-id="2d1c3-239">Utilize estas credenciais toolog toohello VM ao ligar tooit no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="2d1c3-240">Se o script de Olá falhar, confirme se a:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="2d1c3-241">Estão registados para pré-visualização Olá, conforme explicado no passo 4</span><span class="sxs-lookup"><span data-stu-id="2d1c3-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="2d1c3-242">Se alterar o tamanho da VM, tipo de sistema operativo ou valores da localização do script Olá antes de executar este, que os valores de Olá estão listados na Olá [limitações](#Limitations) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="2d1c3-243">Olá tooinstall acelerados controlador de rede para o Linux, Olá concluir os passos em Olá [configurar Linux](#configure-linux) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="2d1c3-244"><a name="configure-linux"></a>Configurar Linux</span><span class="sxs-lookup"><span data-stu-id="2d1c3-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="2d1c3-245">Depois de criar Olá VM no Azure, tem de instalar o controlador de rede na melhoria de Olá para Linux.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="2d1c3-246">Antes de concluir os seguintes passos de Olá, tem de ter criado uma VM com Linux com redes na melhoria utilizando qualquer um dos Olá [portal](#linux-portal) ou [PowerShell](#linux-powershell) passos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="2d1c3-247">A partir do browser da Internet, abra Olá Azure [portal](https://portal.azure.com) e inicie sessão com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2d1c3-248">Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="2d1c3-249">Olá parte superior do portal, toohello direito Olá de Olá *procurar recursos* barra, clique em Olá **> _** ícone toostart numa shell de nuvem de deteção (pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="2d1c3-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="2d1c3-250">Olá painel de shell de nuvem de Bash aparece na parte inferior de Olá do portal de Olá e após alguns segundos, apresenta um  **username@Azure:~ $** linha.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="2d1c3-251">Embora pode SSH toohello VM do seu computador, em vez de shell de nuvem Olá, instruções Olá deste tutorial partem do princípio de que está a utilizar a shell de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="2d1c3-252">Olá parte superior do portal de Olá, na caixa de Olá que contém texto Olá *procurar recursos*, tipo *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="2d1c3-253">Quando **MyVm** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="2d1c3-254">No Olá **MyVm** painel apresentado, clique em Olá **Connect** botão no canto esquerdo superior do painel de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="2d1c3-255">**Nota:** se **criar** é visível em Olá **Connect** botão, Azure não ainda acabou de criar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="2d1c3-256">Clique em **Connect** apenas depois de já não vê **criar** em Olá **Connect** botão.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="2d1c3-257">Azure abre uma caixa informá-lo tooenter Olá `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="2d1c3-258">Introduza este comando Olá nuvem shell (ou cópia a partir da caixa de Olá que antes eram no passo 4 e colá-lo na shell de nuvem toohello), em seguida, prima Enter.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="2d1c3-259">Introduza **Sim** pergunta toohello solicitar que se pretender ligar toocontinue, em seguida, prima Enter.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="2d1c3-260">Introduza a palavra-passe de Olá que introduziu durante a criação de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="2d1c3-261">Uma vez iniciado sessão com êxito toohello VM, verá um adminuser@MyVm:~ linha$.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="2d1c3-262">Agora são registados no toohello VM através de sessão de shell Olá na nuvem.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="2d1c3-263">**Nota:** nuvem shell tempo limite de sessões após 10 minutos de inatividade.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="2d1c3-264">Neste momento, as instruções de Olá variam com base na distribuição Olá que estiver a utilizar.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="2d1c3-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="2d1c3-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="2d1c3-266">Na linha de Olá, introduza `uname -r` e confirmar a versão de Olá para:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="2d1c3-267">Ubuntu é "4.4.0-77-generic", ou superior</span><span class="sxs-lookup"><span data-stu-id="2d1c3-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="2d1c3-268">SLES é "4.4.59-92.20-default" ou superior</span><span class="sxs-lookup"><span data-stu-id="2d1c3-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="2d1c3-269">Crie um bond entre Olá vNIC de rede padrão e Olá acelerado vNIC de rede ao executar comandos de Olá que se seguem.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="2d1c3-270">Tráfego de rede utiliza Olá superior efetuar vNIC na melhoria de rede, enquanto bond Olá garante que o tráfego de rede não é interrompido em determinadas alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="2d1c3-271">Depois de executar o script Olá Olá VM será reiniciado depois de um segundo 60 colocar em pausa.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="2d1c3-272">Uma vez Olá VM é reiniciada, restabeleça a ligação tooit, efetuando os passos 5 a 7 novamente.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="2d1c3-273">Executar Olá `ifconfig` comando e confirme que tem pensar bond0 e interface Olá está a ser mostrada como cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="2d1c3-274">As aplicações que utilizam redes na melhoria têm de comunicar através de Olá *bond0* interface, não *eth0*.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="2d1c3-275">Pode alterar o nome da interface Olá antes de rede na melhoria atinge disponibilidade geral.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="2d1c3-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="2d1c3-276">RHEL/CentOS</span></span>

<span data-ttu-id="2d1c3-277">Criar um Red Hat Enterprise Linux ou VM do CentOS 7.3 requer alguns extra os controladores de mais recentes de tooload Olá necessárias para a SR-IOV e Olá Virtual função (vf) para a placa de rede Olá passos.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="2d1c3-278">Olá primeira fase de instruções de Olá prepara uma imagem que pode ser utilizado toomake um ou mais máquinas virtuais que tenham controladores de Olá previamente carregadas.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="2d1c3-279">A primeira fase: preparar uma imagem de base do Red Hat Enterprise Linux ou CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="2d1c3-280">Aprovisionar um não - SRIOV CentOS 7.3 VM no Azure</span><span class="sxs-lookup"><span data-stu-id="2d1c3-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="2d1c3-281">Instale o LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="2d1c3-282">Transferir ficheiros de configuração</span><span class="sxs-lookup"><span data-stu-id="2d1c3-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="2d1c3-283">Desaprovisionar esta VM</span><span class="sxs-lookup"><span data-stu-id="2d1c3-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="2d1c3-284">No portal do Azure, parar esta VM; e aceda "Discos" do tooVM, o URI do VHD do Olá OSDisk de captura.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="2d1c3-285">Este URI contém o nome do VHD da imagem base Olá e a respetiva conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="2d1c3-286">Fase dois: aprovisionar novas VMs no Azure</span><span class="sxs-lookup"><span data-stu-id="2d1c3-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="2d1c3-287">Aprovisionar novas VMs com base com o New-AzureRMVMConfig utilizando Olá imagem base do VHD capturado na primeira fase, com AcceleratedNetworking ativada em vNIC Olá:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="2d1c3-288">Depois de VMs efetuar o arranque, verifique o dispositivo de VF Olá por "lspci" e verifique Olá Mellanox entrada.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="2d1c3-289">Por exemplo, deveremos ver este item de saída de lspci Olá:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="2d1c3-290">Execute o script bonding Olá:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="2d1c3-291">Reiniciar Olá novas VMs:</span><span class="sxs-lookup"><span data-stu-id="2d1c3-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="2d1c3-292">Olá VM deverá começar com bond0 configurado e Olá caminho acelerados rede ativado.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="2d1c3-293">Executar `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="2d1c3-293">Run `ifconfig` tooconfirm.</span></span>
