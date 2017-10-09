---
title: "Serviços de domínio do Azure Active Directory: Introdução | Microsoft Docs"
description: "Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="dabd9-103">Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="dabd9-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="dabd9-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="dabd9-104">Before you begin</span></span>
<span data-ttu-id="dabd9-105">Consulte demasiado[considerações de redes para o Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="dabd9-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="dabd9-106">Tarefa 2: Configurar definições de rede</span><span class="sxs-lookup"><span data-stu-id="dabd9-106">Task 2: configure network settings</span></span>
<span data-ttu-id="dabd9-107">tarefa de configuração seguinte Olá é toocreate uma Azure virtual network e uma sub-rede dedicada dentro da mesma.</span><span class="sxs-lookup"><span data-stu-id="dabd9-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="dabd9-108">O Azure Active Directory Domain Services é ativado nesta sub-rede dentro da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="dabd9-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="dabd9-109">Também pode escolher uma rede virtual existente e criar a sub-rede Olá dedicado dentro da mesma.</span><span class="sxs-lookup"><span data-stu-id="dabd9-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="dabd9-110">Clique em **rede Virtual** tooselect uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="dabd9-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="dabd9-111">No Olá **escolha de rede virtual** painel, pode ver todas as redes virtuais existentes.</span><span class="sxs-lookup"><span data-stu-id="dabd9-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="dabd9-112">Consulte apenas Olá redes virtuais que pertencem toohello grupo de recursos e localização do Azure que selecionou no Olá **Noções básicas** página do assistente.</span><span class="sxs-lookup"><span data-stu-id="dabd9-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="dabd9-113">Escolha a rede virtual Olá em que os serviços de domínio do Azure AD devem ser ativados.</span><span class="sxs-lookup"><span data-stu-id="dabd9-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="dabd9-114">Clique em **criar nova**, se preferir toocreate uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="dabd9-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="dabd9-115">Recomendamos vivamente a utilização de uma sub-rede dedicada para os serviços de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dabd9-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="dabd9-116">Se escolher uma rede virtual existente, [criar uma sub-rede dedicada utilizando a extensão de redes virtuais Olá](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e, em seguida, escolha dessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="dabd9-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Escolha a rede virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="dabd9-118">Clique em **sub-rede** toopick Olá dedicado sub-rede nesta rede virtual, no qual tooenable a nova geridos por domínio.</span><span class="sxs-lookup"><span data-stu-id="dabd9-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="dabd9-119">No Olá **criar sub-rede** painel, especifique um nome para a sub-rede de Olá e clique em **OK** quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="dabd9-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="dabd9-120">Por exemplo, crie uma sub-rede com o nome de Olá 'DomainServices', tornando mais fácil para os outro administradores toounderstand o que é implementado dentro de sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="dabd9-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Escolha a sub-rede numa rede virtual Olá](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="dabd9-122">**Diretrizes para selecionar uma sub-rede**</span><span class="sxs-lookup"><span data-stu-id="dabd9-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="dabd9-123">Utilize uma sub-rede dedicada para os serviços de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dabd9-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="dabd9-124">Não implemente quaisquer outra máquinas virtuais toothis sub-rede.</span><span class="sxs-lookup"><span data-stu-id="dabd9-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="dabd9-125">Esta configuração permite-lhe tooconfigure grupos de segurança de rede (NSGs) para as suas máquinas virtuais/cargas de trabalho sem perturbar o seu domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="dabd9-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="dabd9-126">Para obter mais informações, consulte [redes considerações para o Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="dabd9-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="dabd9-127">Não selecione a sub-rede do Gateway Olá para implementar os serviços de domínio do Azure AD, porque não é uma configuração suportada.</span><span class="sxs-lookup"><span data-stu-id="dabd9-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="dabd9-128">Certifique-se de que essa sub-rede de Olá que selecionou tem suficiente espaço de endereço disponível - endereços IP disponíveis, pelo menos, 3 a 5.</span><span class="sxs-lookup"><span data-stu-id="dabd9-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="dabd9-129">Quando tiver terminado, clique em **OK** toomove no toohello **grupo Administrador** página do Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="dabd9-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="dabd9-130">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="dabd9-130">Next step</span></span>
[<span data-ttu-id="dabd9-131">Tarefa 3: configurar o grupo administrativo e ativar os serviços de domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dabd9-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
