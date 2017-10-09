---
title: Perguntas mais frequentes (FAQ) acerca dos discos de VM do IaaS do Azure | Microsoft Docs
description: "Perguntas mais frequentes sobre os discos de VM do IaaS do Azure e os discos premium (geridos e não gerido)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="4adac-103">Perguntas mais frequentes sobre os discos de VM do IaaS do Azure e os discos premium geridas e não geridas</span><span class="sxs-lookup"><span data-stu-id="4adac-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="4adac-104">Este artigo responde a algumas perguntas mais frequentes sobre discos gerida do Azure e o Premium Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="4adac-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="4adac-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="4adac-105">Managed Disks</span></span>

<span data-ttu-id="4adac-106">**O que é discos gerida do Azure?**</span><span class="sxs-lookup"><span data-stu-id="4adac-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="4adac-107">Discos geridos é uma funcionalidade que simplifica a gestão de discos para VMs IaaS do Azure, processando gestão de contas de armazenamento para si.</span><span class="sxs-lookup"><span data-stu-id="4adac-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="4adac-108">Para obter mais informações, consulte Olá [descrição geral de discos geridos](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4adac-108">For more information, see hello [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="4adac-109">**Se criar um disco gerido standard de um VHD existente que é 80 GB, quanto será que custo-me?**</span><span class="sxs-lookup"><span data-stu-id="4adac-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="4adac-110">Um disco gerido standard criado a partir de um VHD de 80 GB é tratado como o tamanho de disco padrão disponível seguinte Olá, que é um disco de S10.</span><span class="sxs-lookup"><span data-stu-id="4adac-110">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="4adac-111">Está a cobrada de acordo com toohello S10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="4adac-111">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="4adac-112">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4adac-112">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4adac-113">**Existem quaisquer custos de transação para discos geridos padrão?**</span><span class="sxs-lookup"><span data-stu-id="4adac-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="4adac-114">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-114">Yes.</span></span> <span data-ttu-id="4adac-115">Está a cobrado para cada transação.</span><span class="sxs-lookup"><span data-stu-id="4adac-115">You're charged for each transaction.</span></span> <span data-ttu-id="4adac-116">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4adac-116">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4adac-117">**Para um disco gerido standard, será posso cobrado para o tamanho real do Olá dos dados de Olá no disco Olá ou para a capacidade de Olá aprovisionado de disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="4adac-117">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="4adac-118">Está a cobrados com base na capacidade de Olá aprovisionado de disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="4adac-118">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="4adac-119">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4adac-119">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4adac-120">**Como é preços dos discos premium gerido diferente dos discos não geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="4adac-121">Olá preços dos discos premium gerido é Olá, mesmo que os discos premium não gerido.</span><span class="sxs-lookup"><span data-stu-id="4adac-121">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="4adac-122">**Pode alterar Olá armazenamento tipo de conta (Standard ou Premium) do meu discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-122">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="4adac-123">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-123">Yes.</span></span> <span data-ttu-id="4adac-124">Pode alterar o tipo de conta de armazenamento Olá dos seus discos geridos utilizando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4adac-124">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="4adac-125">**Existe alguma forma posso pode copiar ou exportar uma conta de armazenamento privada do disco gerido tooa?**</span><span class="sxs-lookup"><span data-stu-id="4adac-125">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="4adac-126">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-126">Yes.</span></span> <span data-ttu-id="4adac-127">Pode exportar os discos geridos utilizando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4adac-127">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="4adac-128">**Pode utilizar um ficheiro VHD num toocreate de conta de armazenamento do Azure um disco gerido com uma subscrição diferente?**</span><span class="sxs-lookup"><span data-stu-id="4adac-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="4adac-129">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-129">No.</span></span>

<span data-ttu-id="4adac-130">**Pode utilizar um ficheiro VHD num toocreate de conta de armazenamento do Azure um disco gerido numa região diferente?**</span><span class="sxs-lookup"><span data-stu-id="4adac-130">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="4adac-131">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-131">No.</span></span>

<span data-ttu-id="4adac-132">**Existem algumas limitações de dimensionamento para os clientes que utilizam discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="4adac-133">Discos geridos elimina os limites de Olá associados a contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4adac-133">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="4adac-134">No entanto, o número de Olá de gerido discos por subscrição é limitado too2, 000 por predefinição.</span><span class="sxs-lookup"><span data-stu-id="4adac-134">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="4adac-135">Pode chamar suporte tooincrease este número.</span><span class="sxs-lookup"><span data-stu-id="4adac-135">You can call support tooincrease this number.</span></span>

<span data-ttu-id="4adac-136">**Pode tirar um instantâneo incremental de um disco gerido?**</span><span class="sxs-lookup"><span data-stu-id="4adac-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="4adac-137">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-137">No.</span></span> <span data-ttu-id="4adac-138">capacidade de instantâneos atual Olá faz uma cópia completa de um disco gerido.</span><span class="sxs-lookup"><span data-stu-id="4adac-138">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="4adac-139">No entanto, iremos estiver a planear toosupport instantâneos incrementais no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="4adac-139">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="4adac-140">**VMs num conjunto de disponibilidade podem consistir de uma combinação de discos geridos e?**</span><span class="sxs-lookup"><span data-stu-id="4adac-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="4adac-141">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-141">No.</span></span> <span data-ttu-id="4adac-142">Olá VMs num conjunto de disponibilidade tem de utilizar discos de todos os geridos ou todos os discos não geridos.</span><span class="sxs-lookup"><span data-stu-id="4adac-142">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="4adac-143">Quando criar um conjunto de disponibilidade, pode escolher o tipo de discos que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="4adac-143">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="4adac-144">**É a opção de predefinida de Olá de gerido discos no Olá portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="4adac-144">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="4adac-145">Atualmente não, mas irá tornar-se predefinição de Olá no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="4adac-145">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="4adac-146">**Pode criar um disco vazio gerido?**</span><span class="sxs-lookup"><span data-stu-id="4adac-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="4adac-147">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-147">Yes.</span></span> <span data-ttu-id="4adac-148">Pode criar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="4adac-148">You can create an empty disk.</span></span> <span data-ttu-id="4adac-149">Um disco gerido pode ser criado independentemente de uma VM, por exemplo, sem tooa VM a ligá-la.</span><span class="sxs-lookup"><span data-stu-id="4adac-149">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="4adac-150">**O que é o número de domínios de falhas de Olá suportada para um conjunto de disponibilidade que utiliza discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-150">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="4adac-151">Consoante a região de olá onde está localizado o conjunto de disponibilidade de Olá que utiliza discos geridos, o número de domínios de falhas de Olá suportado é 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="4adac-151">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="4adac-152">**Como é a conta de armazenamento standard Olá para configurar o diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="4adac-152">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="4adac-153">Configurar uma conta de armazenamento privada para diagnósticos da VM.</span><span class="sxs-lookup"><span data-stu-id="4adac-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="4adac-154">Olá futura, vamos planear tooswitch diagnóstico tooManaged discos bem.</span><span class="sxs-lookup"><span data-stu-id="4adac-154">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="4adac-155">**Que tipo de suporte de controlo de acesso baseado em funções está disponível para discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="4adac-156">Gerido funções do discos suporta três predefinido de chaves:</span><span class="sxs-lookup"><span data-stu-id="4adac-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="4adac-157">O proprietário: Podem gerir tudo, incluindo o acesso</span><span class="sxs-lookup"><span data-stu-id="4adac-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="4adac-158">Contribuidor: Podem gerir tudo, exceto acesso</span><span class="sxs-lookup"><span data-stu-id="4adac-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="4adac-159">Leitor: Podem ver tudo, mas não é possível efetuar alterações</span><span class="sxs-lookup"><span data-stu-id="4adac-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="4adac-160">**Existe alguma forma posso pode copiar ou exportar uma conta de armazenamento privada do disco gerido tooa?**</span><span class="sxs-lookup"><span data-stu-id="4adac-160">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="4adac-161">Pode obter uma assinatura de acesso partilhado só de leitura URI para Olá gerido em disco e utilizá-la toocopy Olá conteúdo tooa armazenamento privada conta local ou na armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4adac-161">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="4adac-162">**Pode criar uma cópia do meu disco gerido?**</span><span class="sxs-lookup"><span data-stu-id="4adac-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="4adac-163">Os clientes podem tirar um instantâneo os respetivos discos geridos e, em seguida, utilizar Olá instantâneo toocreate outro disco gerido.</span><span class="sxs-lookup"><span data-stu-id="4adac-163">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="4adac-164">**Os discos não geridos ainda são suportados?**</span><span class="sxs-lookup"><span data-stu-id="4adac-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="4adac-165">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-165">Yes.</span></span> <span data-ttu-id="4adac-166">Suportamos discos não geridos e geridos.</span><span class="sxs-lookup"><span data-stu-id="4adac-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="4adac-167">Recomendamos que utilize discos geridos para novas cargas de trabalho e migre os discos de toomanaged cargas de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="4adac-167">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="4adac-168">**Se criar um disco de 128 GB e, em seguida, aumentar Olá tamanho too130 GB, será posso cobrado Olá seguinte tamanho do disco (GB de 512)?**</span><span class="sxs-lookup"><span data-stu-id="4adac-168">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="4adac-169">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-169">Yes.</span></span>

<span data-ttu-id="4adac-170">**Posso criar armazenamento localmente redundante, armazenamento georredundante, e discos geridos pelo armazenamento com redundância de zona?**</span><span class="sxs-lookup"><span data-stu-id="4adac-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="4adac-171">Discos gerida do Azure suporta atualmente os discos de armazenamento apenas localmente redundante gerido.</span><span class="sxs-lookup"><span data-stu-id="4adac-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="4adac-172">**Pode reduzir ou downsize meu discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="4adac-173">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-173">No.</span></span> <span data-ttu-id="4adac-174">Esta funcionalidade não é suportada atualmente.</span><span class="sxs-lookup"><span data-stu-id="4adac-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="4adac-175">**Posso alterar as propriedades de nome de computador Olá quando um especializadas (não criada utilizando a ferramenta de preparação do sistema de Olá ou generalizado) disco do sistema de operativo tooprovision utilizado uma VM?**</span><span class="sxs-lookup"><span data-stu-id="4adac-175">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="4adac-176">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-176">No.</span></span> <span data-ttu-id="4adac-177">Não é possível atualizar a propriedade de nome de computador Olá.</span><span class="sxs-lookup"><span data-stu-id="4adac-177">You can't update hello computer name property.</span></span> <span data-ttu-id="4adac-178">Olá nova VM herda-Olá VM principal, que era o disco do sistema operativo utilizada toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="4adac-178">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="4adac-179">**Onde posso encontrar exemplo do Azure Resource Manager modelos toocreate VMs com discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-179">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="4adac-180">Lista de modelos utilizando discos geridos</span><span class="sxs-lookup"><span data-stu-id="4adac-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="4adac-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="4adac-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="4adac-182">Geridos discos e a encriptação do serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4adac-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="4adac-183">**É encriptação do serviço de armazenamento do Azure ativada por predefinição quando criar um disco gerido?**</span><span class="sxs-lookup"><span data-stu-id="4adac-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="4adac-184">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-184">Yes.</span></span>

<span data-ttu-id="4adac-185">**Quem gere as chaves de encriptação de Olá?**</span><span class="sxs-lookup"><span data-stu-id="4adac-185">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="4adac-186">Microsoft gere as chaves de encriptação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4adac-186">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="4adac-187">**Pode desativar encriptação do serviço de armazenamento para os meus discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="4adac-188">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-188">No.</span></span>

<span data-ttu-id="4adac-189">**Encriptação do serviço de armazenamento só está disponível em regiões específicas?**</span><span class="sxs-lookup"><span data-stu-id="4adac-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="4adac-190">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-190">No.</span></span> <span data-ttu-id="4adac-191">Está disponível em todas as regiões de olá onde discos geridos está disponível.</span><span class="sxs-lookup"><span data-stu-id="4adac-191">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="4adac-192">Discos geridos está disponível em todas as regiões públicas e na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="4adac-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="4adac-193">**Como posso saber se se o meu disco gerido é encriptado?**</span><span class="sxs-lookup"><span data-stu-id="4adac-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="4adac-194">Pode encontrar tempo Olá quando um disco gerido foi criado a partir Olá portal do Azure, Olá CLI do Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4adac-194">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="4adac-195">Se houver tempo Olá após 9 de Junho de 2017, o disco está encriptado.</span><span class="sxs-lookup"><span data-stu-id="4adac-195">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="4adac-196">**Como encriptar o meu discos existentes que foram criados antes de 10 de Junho de 2017?**</span><span class="sxs-lookup"><span data-stu-id="4adac-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="4adac-197">A partir de 10 de Junho de 2017, os novos dados escritos discos tooexisting gerido é encriptados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4adac-197">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="4adac-198">Podemos também estiver a planear tooencrypt de dados existente e encriptação Olá acontecerá assíncrona no fundo Olá.</span><span class="sxs-lookup"><span data-stu-id="4adac-198">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="4adac-199">Se tem de encriptar dados existentes agora, crie uma cópia do seu disco.</span><span class="sxs-lookup"><span data-stu-id="4adac-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="4adac-200">Novos discos serão encriptados.</span><span class="sxs-lookup"><span data-stu-id="4adac-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="4adac-201">Copiar discos geridos utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4adac-201">Copy managed disks by using hello Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="4adac-202">Copiar discos geridos utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4adac-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="4adac-203">**São gerido instantâneos e imagens encriptadas?**</span><span class="sxs-lookup"><span data-stu-id="4adac-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="4adac-204">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-204">Yes.</span></span> <span data-ttu-id="4adac-205">Gerido todos os instantâneos e as imagens criadas após 9 de Junho de 2017, são encriptadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4adac-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="4adac-206">**Pode converter VMs com discos não geridos que estão localizados em contas de armazenamento que estão ou que foram anteriormente encriptados toomanaged discos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="4adac-207">Sim</span><span class="sxs-lookup"><span data-stu-id="4adac-207">Yes</span></span>

<span data-ttu-id="4adac-208">**Será um VHD exportado a partir de um disco gerido ou um instantâneo também será encriptado?**</span><span class="sxs-lookup"><span data-stu-id="4adac-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="4adac-209">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-209">No.</span></span> <span data-ttu-id="4adac-210">Mas se exportar uma tooan VHD encriptados conta de armazenamento de um disco gerido encriptado ou instantâneos, em seguida, são encriptado.</span><span class="sxs-lookup"><span data-stu-id="4adac-210">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="4adac-211">Os discos Premium: geridos e não geridas</span><span class="sxs-lookup"><span data-stu-id="4adac-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="4adac-212">**Se uma VM utiliza uma série de tamanho que suporte o Premium Storage, tais como uma série DSv2, posso anexar os discos de dados standard e premium?**</span><span class="sxs-lookup"><span data-stu-id="4adac-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="4adac-213">Sim.</span><span class="sxs-lookup"><span data-stu-id="4adac-213">Yes.</span></span>

<span data-ttu-id="4adac-214">**Posso anexar premium e série tamanho de tooa de discos de dados padrão que não suporta o Premium Storage, tais como a série de D, Dv2, G ou F?**</span><span class="sxs-lookup"><span data-stu-id="4adac-214">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="4adac-215">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-215">No.</span></span> <span data-ttu-id="4adac-216">Pode anexar apenas padrão a dados discos tooVMs que não utilizem uma série de tamanho que suporte o Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="4adac-216">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="4adac-217">**Se criar um disco de dados premium a partir de um VHD existente que estava 80 GB, quanto será que custo?**</span><span class="sxs-lookup"><span data-stu-id="4adac-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="4adac-218">Um disco de dados premium criado a partir de um VHD de 80 GB é tratado como Olá disponível a seguinte tamanho do disco premium, que é um disco de P10.</span><span class="sxs-lookup"><span data-stu-id="4adac-218">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="4adac-219">Está a cobrada de acordo com toohello P10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="4adac-219">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="4adac-220">**Existem custos de transação toouse Premium Storage?**</span><span class="sxs-lookup"><span data-stu-id="4adac-220">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="4adac-221">Não há um custo fixo para cada tamanho de disco, o que é aprovisionado com limites específicos no IOPS e débito.</span><span class="sxs-lookup"><span data-stu-id="4adac-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="4adac-222">Olá outros custos são largura de banda de saída e a capacidade de instantâneos, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="4adac-222">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="4adac-223">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4adac-223">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4adac-224">**Quais são Olá os limites de IOPS e débito que pode receber de cache em disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="4adac-224">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="4adac-225">Olá combinados limites para a cache e SSD local para uma série DS são 4000 IOPS por núcleos e 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="4adac-225">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="4adac-226">Olá série GS oferece 5000 IOPS por núcleos e 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="4adac-226">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="4adac-227">**É Olá que local SSD suportado para uma VM de discos geridos?**</span><span class="sxs-lookup"><span data-stu-id="4adac-227">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="4adac-228">Olá local SSD é armazenamento temporário que está incluído com uma VM de discos geridos.</span><span class="sxs-lookup"><span data-stu-id="4adac-228">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="4adac-229">Existe um custo extra para este armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="4adac-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="4adac-230">Recomendamos que não utilize este toostore SSD local os dados da aplicação porque este não é continuada no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="4adac-230">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="4adac-231">**São não existe qualquer repercussions para Olá a utilização de operações de COMPACTAÇÃO em discos premium?**</span><span class="sxs-lookup"><span data-stu-id="4adac-231">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="4adac-232">Não há nenhuma utilização toohello downside cortar nos discos do Azure premium o ou os discos padrão.</span><span class="sxs-lookup"><span data-stu-id="4adac-232">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="4adac-233">Novos tamanhos de disco: geridos e não geridas</span><span class="sxs-lookup"><span data-stu-id="4adac-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="4adac-234">**O que é Olá maior tamanho do disco suportado para o sistema operativo e os discos de dados?**</span><span class="sxs-lookup"><span data-stu-id="4adac-234">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="4adac-235">tipo de partição de Olá que suporta o Azure para um disco de sistema operativo é registo Olá de arranque principal (MBR).</span><span class="sxs-lookup"><span data-stu-id="4adac-235">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="4adac-236">formato MBR Olá suporta um tamanho de disco segurança too2 TB.</span><span class="sxs-lookup"><span data-stu-id="4adac-236">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="4adac-237">Olá a maior dimensão possível que suporta o Azure para um disco de sistema operativo é 2 TB.</span><span class="sxs-lookup"><span data-stu-id="4adac-237">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="4adac-238">Azure suporta até too4 TB para discos de dados.</span><span class="sxs-lookup"><span data-stu-id="4adac-238">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="4adac-239">**O que é Olá maior blob tamanho de página que é suportado?**</span><span class="sxs-lookup"><span data-stu-id="4adac-239">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="4adac-240">Olá maior página tamanho do blob que suporte do Azure é de 8 TB (8,191 GB).</span><span class="sxs-lookup"><span data-stu-id="4adac-240">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="4adac-241">Não é suportada com mais de 4 TB (4,095 GB) ligado tooa VM como discos de sistema operativo ou de dados de blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="4adac-241">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="4adac-242">**É necessário toouse uma nova versão das ferramentas do Azure toocreate, anexar, redimensionar e carregar discos superiores a 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="4adac-242">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="4adac-243">Não precisa de tooupgrade sua toocreate de ferramentas do Azure existente, anexar ou redimensionar discos superiores a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="4adac-243">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="4adac-244">tooupload o VHD de ficheiros no local diretamente tooAzure como um blob de página ou disco não gerido, tem de conjuntos de ferramenta mais recentes do toouse Olá:</span><span class="sxs-lookup"><span data-stu-id="4adac-244">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="4adac-245">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="4adac-245">Azure tools</span></span>      | <span data-ttu-id="4adac-246">Versões suportadas</span><span class="sxs-lookup"><span data-stu-id="4adac-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="4adac-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4adac-247">Azure PowerShell</span></span> | <span data-ttu-id="4adac-248">Número de versão 4.1.0: versão de Junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="4adac-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="4adac-249">CLI do Azure v1</span><span class="sxs-lookup"><span data-stu-id="4adac-249">Azure CLI v1</span></span>     | <span data-ttu-id="4adac-250">Número de versão 0.10.13: versão de Maio de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="4adac-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="4adac-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="4adac-251">AzCopy</span></span>           | <span data-ttu-id="4adac-252">Número de versão 6.1.0: versão de Junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="4adac-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="4adac-253">suporte de Olá para v2 CLI do Azure e o Explorador de armazenamento do Azure está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="4adac-253">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="4adac-254">**P4 e P6 tamanhos de disco são suportados para os discos não geridos ou blobs de página?**</span><span class="sxs-lookup"><span data-stu-id="4adac-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="4adac-255">Não.</span><span class="sxs-lookup"><span data-stu-id="4adac-255">No.</span></span> <span data-ttu-id="4adac-256">P4 (32 GB) e P6 tamanhos de disco (64 GB) são suportados apenas para discos geridos.</span><span class="sxs-lookup"><span data-stu-id="4adac-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="4adac-257">Suporte para discos não geridos e blobs de páginas está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="4adac-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="4adac-258">**Se a minha premium existente gerido disco inferior a 64 GB foi criado antes de disco pequeno Olá foi ativado (em torno do dia 15 de Junho de 2017), como é é faturada?**</span><span class="sxs-lookup"><span data-stu-id="4adac-258">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="4adac-259">Discos premium pequeno existentes inferior a 64 GB continuar toobe cobrado de acordo com toohello P10 escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="4adac-259">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="4adac-260">**Como posso mudar a camada de disco de Olá dos discos premium pequeno inferior a 64 GB de P10 tooP4 ou P6?**</span><span class="sxs-lookup"><span data-stu-id="4adac-260">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="4adac-261">Pode tirar um instantâneo os discos pequenos e, em seguida, criar um Olá de comutador do disco tooautomatically tooP4 do escalão de preço ou P6 com base no tamanho de Olá aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="4adac-261">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="4adac-262">E se a minha pergunta não é atendida aqui?</span><span class="sxs-lookup"><span data-stu-id="4adac-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="4adac-263">Se a sua pergunta não está listada aqui, informe-nos e vamos ajudá-lo a encontrar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="4adac-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="4adac-264">Pode colocar uma pergunta no final deste artigo Olá nos comentários de Olá.</span><span class="sxs-lookup"><span data-stu-id="4adac-264">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="4adac-265">tooengage com a equipa de armazenamento do Azure Olá e outros membros da Comunidade sobre neste artigo, utilize Olá MSDN [fórum de armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="4adac-265">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="4adac-266">funcionalidades de toorequest, submeter o pedidos e ideias toohello [fórum de comentários do Storage do Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="4adac-266">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
