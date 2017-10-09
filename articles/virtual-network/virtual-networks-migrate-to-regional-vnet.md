---
title: "aaaMigrate uma rede virtual do Azure (clássica) de uma região do grupo de afinidade tooa | Microsoft Docs"
description: "Saiba como uma rede virtual (clássica) de uma afinidade de toomigrate grupo tooa região."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="0482e-103">Migrar uma rede virtual (clássica) a partir de uma região de tooa do grupo de afinidade</span><span class="sxs-lookup"><span data-stu-id="0482e-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0482e-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0482e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0482e-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="0482e-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="0482e-106">A Microsoft recomenda que implementações mais novas utilizem o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="0482e-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="0482e-107">Grupos de afinidades Certifique-se de que os recursos criados no Olá mesmo grupo de afinidade fisicamente alojadas por servidores que estão fechar em conjunto, permitindo toocommunicate estes recursos mais rápida.</span><span class="sxs-lookup"><span data-stu-id="0482e-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="0482e-108">No passado, Olá, grupos de afinidade eram um requisito para criar redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="0482e-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="0482e-109">Nessa altura, o serviço do Gestor de rede Olá que geridos redes virtuais (clássicas) só pode funcionar dentro de um conjunto de servidores físicos ou unidade de escala.</span><span class="sxs-lookup"><span data-stu-id="0482e-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="0482e-110">Melhoramentos da arquitetura aumentou âmbito Olá da região de tooa de gestão de rede.</span><span class="sxs-lookup"><span data-stu-id="0482e-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="0482e-111">Como resultado estas melhorias da arquitetura, grupos de afinidades já não são recomendados, ou necessários para as redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="0482e-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="0482e-112">utilização de Olá de grupos de afinidade para redes virtuais (clássicas) é substituída pela regiões.</span><span class="sxs-lookup"><span data-stu-id="0482e-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="0482e-113">Redes virtuais (clássica) que estão associados a regiões são denominadas redes virtuais regionais.</span><span class="sxs-lookup"><span data-stu-id="0482e-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="0482e-114">Recomendamos que não utilize grupos de afinidade em geral.</span><span class="sxs-lookup"><span data-stu-id="0482e-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="0482e-115">Para além do requisito de rede virtual Olá, grupos de afinidades também estavam toouse importante tooensure recursos, tais como a computação (clássica) e armazenamento (clássica), foram colocadas perto de si.</span><span class="sxs-lookup"><span data-stu-id="0482e-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="0482e-116">No entanto, com a arquitetura de rede do Azure atual Olá, estes requisitos de posicionamento são já não são necessários.</span><span class="sxs-lookup"><span data-stu-id="0482e-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0482e-117">Embora seja tecnicamente possível toocreate uma rede virtual que está associada um grupo de afinidade, não há nenhum toodo razão apelativa para.</span><span class="sxs-lookup"><span data-stu-id="0482e-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="0482e-118">Muitas funcionalidades de rede virtual, tais como grupos de segurança de rede, só estão disponíveis ao utilizar uma rede virtual regional e não estão disponíveis para as redes virtuais que estão associados a grupos de afinidades.</span><span class="sxs-lookup"><span data-stu-id="0482e-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="0482e-119">Editar o ficheiro de configuração de rede Olá</span><span class="sxs-lookup"><span data-stu-id="0482e-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="0482e-120">Exporte ficheiro de configuração de rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="0482e-120">Export hello network configuration file.</span></span> <span data-ttu-id="0482e-121">toolearn como tooexport uma configuração de rede através do PowerShell de ficheiros ou Olá interface de linha de comandos do Azure (CLI) 1.0, consulte [configurar uma rede virtual com um ficheiro de configuração de rede](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="0482e-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="0482e-122">Editar o ficheiro de configuração de rede Olá, substituindo **AffinityGroup** com **localização**.</span><span class="sxs-lookup"><span data-stu-id="0482e-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="0482e-123">Especifique um Azure [região](https://azure.microsoft.com/regions) para **localização**.</span><span class="sxs-lookup"><span data-stu-id="0482e-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0482e-124">Olá **localização** Olá região que especificou para o grupo de afinidade de Olá que está associado a sua rede virtual (clássica).</span><span class="sxs-lookup"><span data-stu-id="0482e-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="0482e-125">Por exemplo, se a rede virtual (clássica) está associada um grupo de afinidade que está localizado em EUA oeste, ao migrar, o **localização** tem de apontar tooWest E.U.A..</span><span class="sxs-lookup"><span data-stu-id="0482e-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="0482e-126">Edite Olá seguintes linhas no ficheiro de configuração de rede, substituindo os valores de Olá com os seus próprios:</span><span class="sxs-lookup"><span data-stu-id="0482e-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="0482e-127">**Valor antigo:** \<VirtualNetworkSitename = AffinityGroup "VNetUSWest" = "VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="0482e-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="0482e-128">**Valor novo:** \<VirtualNetworkSitename = "VNetUSWest" localização "EUA Oeste" de =\></span><span class="sxs-lookup"><span data-stu-id="0482e-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="0482e-129">Guardar as alterações e [importar](virtual-networks-using-network-configuration-file.md#import) Olá tooAzure de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="0482e-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="0482e-130">Esta migração não irá causar qualquer período de inatividade tooyour serviços.</span><span class="sxs-lookup"><span data-stu-id="0482e-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="0482e-131">Que toodo se tiver uma VM (clássica) num grupo de afinidade</span><span class="sxs-lookup"><span data-stu-id="0482e-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="0482e-132">VMs (clássica) que estão atualmente a ser um grupo de afinidade não é necessário toobe removido do grupo de afinidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="0482e-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="0482e-133">Depois de uma VM for implementada, é a unidade de escala único tooa implementado.</span><span class="sxs-lookup"><span data-stu-id="0482e-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="0482e-134">Grupos de afinidades pode restringir o conjunto de Olá de tamanhos VM disponíveis para uma nova implementação de VM, mas qualquer VM existente que é implementada já está restringida toohello conjunto da VM tamanhos disponíveis na unidade de escala Olá que Olá VM é implementada.</span><span class="sxs-lookup"><span data-stu-id="0482e-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="0482e-135">Porque Olá que VM já se encontra implementada tooa unidade de escala, remover uma VM a partir de um grupo de afinidade não tem efeito em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0482e-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
