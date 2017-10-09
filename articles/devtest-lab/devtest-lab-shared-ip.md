---
title: "aaaUnderstand partilhado endereços IP no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como Azure DevTest Labs utiliza partilhado IP endereços toominimize Olá pública IP endereços necessários tooaccess o laboratório VMs."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="24c16-103">Compreender os endereços IP partilhados no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="24c16-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="24c16-104">Laboratório de permite do Azure DevTest Labs VMs partilha Olá mesma pública IP endereço toominimize Olá diversas pública tooaccess necessária de endereços IP individuais laboratório VMs.</span><span class="sxs-lookup"><span data-stu-id="24c16-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="24c16-105">Este artigo descreve como partilhado de IPs de trabalho e as opções de configuração relacionados.</span><span class="sxs-lookup"><span data-stu-id="24c16-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="24c16-106">Partilhado a definição de IP</span><span class="sxs-lookup"><span data-stu-id="24c16-106">Shared IP setting</span></span>

<span data-ttu-id="24c16-107">Quando criar um laboratório, reside numa sub-rede de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="24c16-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="24c16-108">Por predefinição, esta sub-rede é criada com **ativar partilhado IP público** definido demasiado*Sim*.</span><span class="sxs-lookup"><span data-stu-id="24c16-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="24c16-109">Esta configuração cria um endereço IP público para a sub-rede Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="24c16-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="24c16-110">Para obter mais informações sobre como configurar redes virtuais e sub-redes, consulte [configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="24c16-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nova sub-rede de laboratório](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="24c16-112">Para laboratórios existentes, pode ativar esta opção, selecionando **políticas de configuração e > redes virtuais**.</span><span class="sxs-lookup"><span data-stu-id="24c16-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="24c16-113">Em seguida, selecione uma rede virtual da lista de Olá e escolha **ATIVAR PARTILHADO IP público** para uma sub-rede selecionada.</span><span class="sxs-lookup"><span data-stu-id="24c16-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="24c16-114">Também pode desativar esta opção em qualquer laboratório se não quiser tooshare um endereço IP público em laboratório VMs.</span><span class="sxs-lookup"><span data-stu-id="24c16-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="24c16-115">Quaisquer VMs criadas no toousing de predefinição laboratório um IP partilhado.</span><span class="sxs-lookup"><span data-stu-id="24c16-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="24c16-116">Ao criar Olá VM, esta definição pode ser observada em Olá **definições avançadas** painel em **configuração do endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="24c16-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nova VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="24c16-118">**Partilhado:** todas as VMs criadas como **partilhados** são colocados de um grupo de recursos (RG).</span><span class="sxs-lookup"><span data-stu-id="24c16-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="24c16-119">Um único endereço IP é atribuído para que o RG e todas as VMs no Olá RG irão utilizar esse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="24c16-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="24c16-120">**Público:** cada VM que cria tem o seu próprio endereço IP e é criado no seu próprio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="24c16-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="24c16-121">**Privados:** cada VM que criar utiliza um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="24c16-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="24c16-122">Não será capaz de tooconnect toothis VM diretamente a partir de Olá internet com o ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="24c16-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="24c16-123">Sempre que uma VM com o IP partilhado ativada é adicionada toohello sub-rede, DevTest Labs adiciona o Balanceador de carga do Olá VM tooa automaticamente e atribui um número de porta TCP no endereço IP público Olá, reencaminhamento toohello porta RDP num Olá VM.</span><span class="sxs-lookup"><span data-stu-id="24c16-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="24c16-124">Utilizar Olá partilhado de IP</span><span class="sxs-lookup"><span data-stu-id="24c16-124">Using hello shared IP</span></span>

- <span data-ttu-id="24c16-125">**Os utilizadores do Linux:** SSH toohello VM utilizando o endereço IP Olá ou o nome de domínio completamente qualificado, seguido por um vírgula, seguido de porta de Olá.</span><span class="sxs-lookup"><span data-stu-id="24c16-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="24c16-126">Por exemplo, numa imagem de Olá abaixo, Olá RDP endereços toohello tooconnect VM é `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="24c16-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Exemplo VM](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="24c16-128">**Utilizadores do Windows:** Olá selecione **Connect** botão no Olá toodownload portal do Azure, um ficheiro RDP previamente configurado e aceder Olá VM.</span><span class="sxs-lookup"><span data-stu-id="24c16-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24c16-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="24c16-129">Next steps</span></span>

* [<span data-ttu-id="24c16-130">Definir políticas de laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="24c16-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="24c16-131">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="24c16-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





