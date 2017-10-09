---
title: "aaaAzure encriptação de disco para o Windows e as VMs de IaaS Linux | Microsoft Docs"
description: "Este artigo fornece uma descrição geral do Microsoft Azure disco encriptação para o Windows e as VMs de IaaS Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="4b406-103">Encriptação de disco do Azure para o Windows e as VMs de Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="4b406-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="4b406-104">Microsoft Azure é vivamente consolidada tooensuring sua privacidade de dados, soberania de dados e permite-lhe toocontrol seu Azure alojadas dados através de uma variedade de tecnologias avançadas tooencrypt, controlar e gerir chaves de encriptação, controlo & auditar o acesso aos dados.</span><span class="sxs-lookup"><span data-stu-id="4b406-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="4b406-105">Isto proporciona aos clientes do Azure Olá flexibilidade toochoose Olá solução que melhor se adeque às suas necessidades de negócio.</span><span class="sxs-lookup"><span data-stu-id="4b406-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="4b406-106">Neste documento, vamos apresenta-lhe tooa nova tecnologia solução "Encriptação de disco do Azure para o Windows e da VM do IaaS Linux" toohelp proteger e salvaguardar o dados toomeet os compromissos de segurança e conformidade organizacionais.</span><span class="sxs-lookup"><span data-stu-id="4b406-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="4b406-107">documento de Olá fornece orientação detalhada no como toouse Olá disco Azure encriptação funcionalidades, incluindo Olá cenários e suportados Olá experiências de utilizador.</span><span class="sxs-lookup"><span data-stu-id="4b406-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-108">Algumas recomendações podem aumentar dados, a rede ou a utilização de recursos de computação, resultando em custos de licenciamento ou de subscrição adicionais.</span><span class="sxs-lookup"><span data-stu-id="4b406-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="4b406-109">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="4b406-109">Overview</span></span>
<span data-ttu-id="4b406-110">Encriptação de disco do Azure é uma nova capacidade que ajuda-o a encriptar os discos da máquina virtual do Windows e Linux IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="4b406-111">Tira partido do Azure Disk Encryption padrão da indústria de Olá [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funcionalidade do Windows e Olá [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funcionalidade de encriptação de volume do Linux tooprovide para Olá SO e discos de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="4b406-112">solução Olá está integrada [Cofre de chaves do Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar e gerir chaves de encriptação de disco Olá e segredos na sua subscrição do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="4b406-113">solução Olá também garante que todos os dados nos discos da máquina virtual de Olá sejam encriptados Inativos no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="4b406-114">Encriptação de disco do Azure para o Windows e as VMs de IaaS Linux está agora em **disponibilidade geral** em todas as regiões públicas do Azure e regiões de AzureGov para VMs padrão e VMs com o armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="4b406-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="4b406-115">Cenários de encriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-115">Encryption scenarios</span></span>
<span data-ttu-id="4b406-116">Olá solução da Azure Disk Encryption suporta Olá os seguintes cenários de cliente:</span><span class="sxs-lookup"><span data-stu-id="4b406-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="4b406-117">Ativar a encriptação em novas VMs de IaaS criados a partir de VHD previamente encriptado e chaves de encriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="4b406-118">Ativar a encriptação em novas VMs de IaaS criados a partir de imagens de galeria do Azure Olá suportado</span><span class="sxs-lookup"><span data-stu-id="4b406-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="4b406-119">Ativar a encriptação em VMs de IaaS existentes em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="4b406-120">Desativar a encriptação em VMs de IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="4b406-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="4b406-121">Desativar a encriptação em unidades de dados para as VMs de IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="4b406-122">Ativar a encriptação de disco gerido VMs</span><span class="sxs-lookup"><span data-stu-id="4b406-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="4b406-123">Atualizar as definições de encriptação de um armazenamento de premium não encriptado VM existente</span><span class="sxs-lookup"><span data-stu-id="4b406-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="4b406-124">Cópia de segurança e restauro de VMs encriptados, encriptada com a chave de encriptação de chaves</span><span class="sxs-lookup"><span data-stu-id="4b406-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="4b406-125">solução Olá suporta Olá os seguintes cenários para VMs de IaaS quando são ativados no Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="4b406-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="4b406-126">Integração com o Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="4b406-127">O escalão Standard VMs: [A, D, DS, G, GS, F e série Sim forth VMs do IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="4b406-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="4b406-128">Ativar a encriptação no Windows e Linux VMs de IaaS e as VMs de disco gerido de Olá suportada imagens de galeria do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="4b406-129">Desativar a encriptação em unidades de dados e SO Windows VMs de IaaS e as VMs de disco gerido</span><span class="sxs-lookup"><span data-stu-id="4b406-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="4b406-130">Desativar a encriptação em unidades de dados para VMs de disco gerido e as VMs de IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="4b406-131">Ativar a encriptação em VMs do IaaS SO de cliente do Windows em execução</span><span class="sxs-lookup"><span data-stu-id="4b406-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="4b406-132">Ativar a encriptação em volumes com caminhos de montagem</span><span class="sxs-lookup"><span data-stu-id="4b406-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="4b406-133">Ativar a encriptação em VMs do Linux configurado com o disco striping (RAID) utilizando mdadm</span><span class="sxs-lookup"><span data-stu-id="4b406-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="4b406-134">Ativar a encriptação em VMs do Linux utilizando LVM para discos de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="4b406-135">Ativar a encriptação em VMs do Windows configurado com espaços de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4b406-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="4b406-136">Atualizar as definições de encriptação de um armazenamento de premium não encriptado VM existente</span><span class="sxs-lookup"><span data-stu-id="4b406-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="4b406-137">Todos os público do Azure e AzureGov regiões são suportadas</span><span class="sxs-lookup"><span data-stu-id="4b406-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="4b406-138">solução Olá não suporta os seguintes cenários, funcionalidades e tecnologias de Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="4b406-139">Escalão básico VMs do IaaS</span><span class="sxs-lookup"><span data-stu-id="4b406-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="4b406-140">A desativação da encriptação numa unidade do SO para as VMs de IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="4b406-141">A desativação da encriptação numa unidade de dados se Olá disco do SO é encriptado para as VMs de Iaas Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="4b406-142">VMs de IaaS que são criados utilizando o método de criação de VM Olá clássico</span><span class="sxs-lookup"><span data-stu-id="4b406-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="4b406-143">Ative a encriptação em Windows e as VMs de Linux IaaS imagens personalizadas do cliente não é suportada.</span><span class="sxs-lookup"><span data-stu-id="4b406-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="4b406-144">Ativar enccryption com SO Linux LVM disco não é suportado atualmente.</span><span class="sxs-lookup"><span data-stu-id="4b406-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="4b406-145">Este suporte ficará em breve.</span><span class="sxs-lookup"><span data-stu-id="4b406-145">This support will come soon.</span></span>
* <span data-ttu-id="4b406-146">Integração com o serviço de gestão de chaves no local</span><span class="sxs-lookup"><span data-stu-id="4b406-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="4b406-147">Ficheiros do Azure (sistema de ficheiros partilhados), o sistema de ficheiros de rede (NFS), volumes dinâmicos e VMs do Windows que estão configurados com sistemas RAID baseados em software</span><span class="sxs-lookup"><span data-stu-id="4b406-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="4b406-148">Cópia de segurança e restauro de VMs encriptados, encriptados sem chave de encriptação de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="4b406-149">Atualize as definições de encriptação de uma VM do encriptados premium storage existente.</span><span class="sxs-lookup"><span data-stu-id="4b406-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-150">Cópia de segurança e restauro de VMs encriptadas só é suportada para VMs que estão encriptadas com a configuração de KEK Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="4b406-151">Não é suportada em VMs que são encriptadas sem KEK.</span><span class="sxs-lookup"><span data-stu-id="4b406-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="4b406-152">KEK é um parâmetro opcional que ativa a encriptação de VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="4b406-153">Este suporte está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="4b406-153">This support is coming soon.</span></span>
> <span data-ttu-id="4b406-154">Atualize as definições de encriptação de um armazenamento premium encriptado existente VM não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="4b406-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="4b406-155">Este suporte está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="4b406-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="4b406-156">Funcionalidades de encriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-156">Encryption features</span></span>
<span data-ttu-id="4b406-157">Ao ativar e implementar o Azure Disk Encryption para VMs IaaS do Azure, hello seguintes funcionalidades estão ativadas, consoante a configuração de Olá fornecida:</span><span class="sxs-lookup"><span data-stu-id="4b406-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="4b406-158">Encriptação de volume de arranque do Olá SO volume tooprotect Olá Inativos no armazenamento do</span><span class="sxs-lookup"><span data-stu-id="4b406-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="4b406-159">Encriptação de dados volumes tooprotect Olá os volumes de dados Inativos no armazenamento do</span><span class="sxs-lookup"><span data-stu-id="4b406-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="4b406-160">A desativação da encriptação Olá SO e dados unidades para as VMs de IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="4b406-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="4b406-161">A desativação da encriptação de dados Olá unidades para as VMs de IaaS Linux (apenas se o SO unidade é não encriptadas)</span><span class="sxs-lookup"><span data-stu-id="4b406-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="4b406-162">Proteger as chaves de encriptação de Olá e segredos na sua subscrição do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4b406-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="4b406-163">Relatório de estado de encriptação de Olá de Olá encriptados VM do IaaS</span><span class="sxs-lookup"><span data-stu-id="4b406-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="4b406-164">Remoção das definições de configuração de encriptação de disco da máquina de virtual IaaS Olá</span><span class="sxs-lookup"><span data-stu-id="4b406-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="4b406-165">Cópia de segurança e restauro de VMs encriptadas utilizando o serviço de cópia de segurança do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="4b406-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-166">Cópia de segurança e restauro de VMs encriptadas só é suportada para VMs que estão encriptadas com a configuração de KEK Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="4b406-167">Não é suportada em VMs que são encriptadas sem KEK.</span><span class="sxs-lookup"><span data-stu-id="4b406-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="4b406-168">KEK é um parâmetro opcional que ativa a encriptação de VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="4b406-169">Encriptação de disco do Azure para as VMS de IaaS para Windows e Linux solução inclui:</span><span class="sxs-lookup"><span data-stu-id="4b406-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="4b406-170">extensão de encriptação de disco de Olá para Windows.</span><span class="sxs-lookup"><span data-stu-id="4b406-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="4b406-171">extensão de encriptação de disco de Olá para Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="4b406-172">Olá, os cmdlets do PowerShell de encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="4b406-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="4b406-173">Olá cmdlets de interface de linha de comandos do Azure (CLI) de encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="4b406-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="4b406-174">Olá modelos do Azure Resource Manager de encriptação de disco.</span><span class="sxs-lookup"><span data-stu-id="4b406-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="4b406-175">Olá solução da Azure Disk Encryption é suportada em VMs de IaaS que estão a executar SO Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="4b406-176">Para obter mais informações sobre os sistemas de operativos Olá suportado, consulte Olá "pré-requisitos" secção.</span><span class="sxs-lookup"><span data-stu-id="4b406-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-177">Não há sem encargos adicionais para encriptar os discos da VM com o Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="4b406-178">Proposta de valor</span><span class="sxs-lookup"><span data-stu-id="4b406-178">Value proposition</span></span>
<span data-ttu-id="4b406-179">Quando aplica solução Olá encriptação-gestão de discos do Azure, pode satisfazer Olá seguintes necessidades comerciais:</span><span class="sxs-lookup"><span data-stu-id="4b406-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="4b406-180">VMs de IaaS são protegidas inativos, dado que pode utilizar a encriptação de norma da indústria tecnologia tooaddress segurança e conformidade requisitos organizacionais.</span><span class="sxs-lookup"><span data-stu-id="4b406-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="4b406-181">Arranque de VMs de IaaS em chaves controlado de cliente e as políticas e pode auditar a respetiva utilização no seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="4b406-182">Fluxo de trabalho de encriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-182">Encryption workflow</span></span>
<span data-ttu-id="4b406-183">encriptação de disco tooenable para o Windows e VMs do Linux, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="4b406-184">Escolha um cenário de encriptação entre Olá anterior a cenários de encriptação.</span><span class="sxs-lookup"><span data-stu-id="4b406-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="4b406-185">Optar ativamente por participar na encriptação de disco tooenabling através do modelo de encriptação de disco do Azure Resource Manager Olá, os cmdlets do PowerShell ou comando da CLI e especificar a configuração de encriptação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="4b406-186">Para o cenário encriptados de cliente do VHD Olá, carregue Olá encriptado VHD tooyour conta de armazenamento e o Cofre de chaves de tooyour materiais chave de encriptação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="4b406-187">Em seguida, fornece encriptação tooenable configuração por Olá sobre uma nova VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="4b406-188">Para novas VMs que são criadas a partir Olá Marketplace e VMs existentes que já estão em execução no Azure, fornece encriptação tooenable configuração por Olá no Olá VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="4b406-189">Conceda acesso toohello plataforma Azure tooread Olá chave de encriptação material (chaves de encriptação BitLocker para sistemas Windows) e o frase de acesso para Linux da encriptação de tooenable seu Cofre de chaves no Olá VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="4b406-190">Fornece Olá Azure Active Directory (Azure AD) aplicação identidade toowrite Olá encriptação chave tooyour materiais Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="4b406-191">Se o fizer, permite que a encriptação em Olá VM do IaaS para cenários de Olá mencionado no passo 2.</span><span class="sxs-lookup"><span data-stu-id="4b406-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="4b406-192">Azure atualiza o modelo de serviço VM Olá com a encriptação e a configuração do Cofre de chaves de Olá e configura o VM encriptado.</span><span class="sxs-lookup"><span data-stu-id="4b406-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="4b406-194">Fluxo de trabalho de desencriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-194">Decryption workflow</span></span>
<span data-ttu-id="4b406-195">encriptação de disco toodisable para VMs de IaaS, Olá concluir os seguintes passos de alto nível:</span><span class="sxs-lookup"><span data-stu-id="4b406-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="4b406-196">Escolha toodisable encriptação (desencriptação) numa VM IaaS em execução no Azure através do modelo de encriptação de disco do Azure Resource Manager Olá ou os cmdlets do PowerShell e especificar a configuração de desencriptação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="4b406-197">Este passo desativa a encriptação de volume de dados do SO ou Olá Olá ou ambos num Olá VM do IaaS Windows a executar.</span><span class="sxs-lookup"><span data-stu-id="4b406-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="4b406-198">No entanto, tal como mencionado na secção anterior Olá, a desativação da encriptação de disco de SO para Linux não é suportada.</span><span class="sxs-lookup"><span data-stu-id="4b406-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="4b406-199">passo de desencriptação de Olá só é permitido para unidades de dados em VMs do Linux, desde que o disco do SO Olá não está encriptado.</span><span class="sxs-lookup"><span data-stu-id="4b406-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="4b406-200">Atualizações do Azure Olá modelo de serviço da VM e Olá VM do IaaS está marcado como desencriptada.</span><span class="sxs-lookup"><span data-stu-id="4b406-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="4b406-201">conteúdo Olá Olá VM já não é encriptado em pausa.</span><span class="sxs-lookup"><span data-stu-id="4b406-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-202">operação de encriptação de desativar Olá não eliminar o Cofre e Olá encriptação chave material de chaves (chaves de encriptação BitLocker para sistemas Windows) ou o frase de acesso para Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="4b406-203">Não é suportada a desativação da encriptação de disco de SO do Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="4b406-204">passo de desencriptação de Olá só é permitido para unidades de dados em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="4b406-205">A desativação da encriptação de disco de dados para o Linux não é suportada se Olá disco do SO estiver encriptada.</span><span class="sxs-lookup"><span data-stu-id="4b406-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b406-206">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b406-206">Prerequisites</span></span>
<span data-ttu-id="4b406-207">Antes de ativar o Azure Disk Encryption em VMs do IaaS do Azure para cenários de Olá suportado que foram abordados na secção "Descrição geral" de Olá, consulte Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="4b406-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="4b406-208">Tem de ter recursos de toocreate uma subscrição do Azure Active Directory válido no Azure em regiões Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="4b406-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="4b406-209">Encriptação de disco do Azure é suportada em Olá seguintes versões do Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4b406-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="4b406-210">Encriptação de disco do Azure é suportada em Olá seguintes versões de cliente do Windows: Windows 8 e o cliente Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4b406-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-211">Para o Windows Server 2008 R2, tem de ter o .NET Framework 4.5 instalados antes de ativar a encriptação no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="4b406-212">Pode instalá-lo do Windows Update através da instalação de atualização opcional de Olá o Microsoft .NET Framework 4.5.2 para sistemas baseados em x64 do Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="4b406-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="4b406-213">A encriptação de disco do Azure é suportada no Olá seguir galeria do Azure com base distribuições de servidor Linux e versões:</span><span class="sxs-lookup"><span data-stu-id="4b406-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="4b406-214">Distribuição de Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-214">Linux Distribution</span></span> | <span data-ttu-id="4b406-215">Versão</span><span class="sxs-lookup"><span data-stu-id="4b406-215">Version</span></span> | <span data-ttu-id="4b406-216">Tipo de volume suportado para a encriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="4b406-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4b406-217">Ubuntu</span></span> | <span data-ttu-id="4b406-218">16.04-DIARIAMENTE-LTS</span><span class="sxs-lookup"><span data-stu-id="4b406-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="4b406-219">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-219">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4b406-220">Ubuntu</span></span> | <span data-ttu-id="4b406-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="4b406-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="4b406-222">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-222">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4b406-223">Ubuntu</span></span> | <span data-ttu-id="4b406-224">12.10</span><span class="sxs-lookup"><span data-stu-id="4b406-224">12.10</span></span> | <span data-ttu-id="4b406-225">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-225">Data disk</span></span> |
| <span data-ttu-id="4b406-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4b406-226">Ubuntu</span></span> | <span data-ttu-id="4b406-227">12.04</span><span class="sxs-lookup"><span data-stu-id="4b406-227">12.04</span></span> | <span data-ttu-id="4b406-228">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-228">Data disk</span></span> |
| <span data-ttu-id="4b406-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="4b406-229">RHEL</span></span> | <span data-ttu-id="4b406-230">7.3</span><span class="sxs-lookup"><span data-stu-id="4b406-230">7.3</span></span> | <span data-ttu-id="4b406-231">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-231">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="4b406-232">RHEL</span></span> | <span data-ttu-id="4b406-233">7.2</span><span class="sxs-lookup"><span data-stu-id="4b406-233">7.2</span></span> | <span data-ttu-id="4b406-234">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-234">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="4b406-235">RHEL</span></span> | <span data-ttu-id="4b406-236">6.8</span><span class="sxs-lookup"><span data-stu-id="4b406-236">6.8</span></span> | <span data-ttu-id="4b406-237">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-237">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="4b406-238">RHEL</span></span> | <span data-ttu-id="4b406-239">6.7</span><span class="sxs-lookup"><span data-stu-id="4b406-239">6.7</span></span> | <span data-ttu-id="4b406-240">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-240">Data disk</span></span> |
| <span data-ttu-id="4b406-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-241">CentOS</span></span> | <span data-ttu-id="4b406-242">7.3</span><span class="sxs-lookup"><span data-stu-id="4b406-242">7.3</span></span> | <span data-ttu-id="4b406-243">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-243">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-244">CentOS</span></span> | <span data-ttu-id="4b406-245">7.2N</span><span class="sxs-lookup"><span data-stu-id="4b406-245">7.2n</span></span> | <span data-ttu-id="4b406-246">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-246">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-247">CentOS</span></span> | <span data-ttu-id="4b406-248">6.8</span><span class="sxs-lookup"><span data-stu-id="4b406-248">6.8</span></span> | <span data-ttu-id="4b406-249">Disco do SO e dados</span><span class="sxs-lookup"><span data-stu-id="4b406-249">OS and Data disk</span></span> |
| <span data-ttu-id="4b406-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-250">CentOS</span></span> | <span data-ttu-id="4b406-251">7.1</span><span class="sxs-lookup"><span data-stu-id="4b406-251">7.1</span></span> | <span data-ttu-id="4b406-252">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-252">Data disk</span></span> |
| <span data-ttu-id="4b406-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-253">CentOS</span></span> | <span data-ttu-id="4b406-254">7.0</span><span class="sxs-lookup"><span data-stu-id="4b406-254">7.0</span></span> | <span data-ttu-id="4b406-255">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-255">Data disk</span></span> |
| <span data-ttu-id="4b406-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-256">CentOS</span></span> | <span data-ttu-id="4b406-257">6.7</span><span class="sxs-lookup"><span data-stu-id="4b406-257">6.7</span></span> | <span data-ttu-id="4b406-258">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-258">Data disk</span></span> |
| <span data-ttu-id="4b406-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-259">CentOS</span></span> | <span data-ttu-id="4b406-260">6.6</span><span class="sxs-lookup"><span data-stu-id="4b406-260">6.6</span></span> | <span data-ttu-id="4b406-261">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-261">Data disk</span></span> |
| <span data-ttu-id="4b406-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="4b406-262">CentOS</span></span> | <span data-ttu-id="4b406-263">6.5</span><span class="sxs-lookup"><span data-stu-id="4b406-263">6.5</span></span> | <span data-ttu-id="4b406-264">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-264">Data disk</span></span> |
| <span data-ttu-id="4b406-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4b406-265">openSUSE</span></span> | <span data-ttu-id="4b406-266">13.2</span><span class="sxs-lookup"><span data-stu-id="4b406-266">13.2</span></span> | <span data-ttu-id="4b406-267">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-267">Data disk</span></span> |
| <span data-ttu-id="4b406-268">SLES</span><span class="sxs-lookup"><span data-stu-id="4b406-268">SLES</span></span> | <span data-ttu-id="4b406-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="4b406-269">12 SP1</span></span> | <span data-ttu-id="4b406-270">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-270">Data disk</span></span> |
| <span data-ttu-id="4b406-271">SLES</span><span class="sxs-lookup"><span data-stu-id="4b406-271">SLES</span></span> | <span data-ttu-id="4b406-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="4b406-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="4b406-273">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-273">Data disk</span></span> |
| <span data-ttu-id="4b406-274">SLES</span><span class="sxs-lookup"><span data-stu-id="4b406-274">SLES</span></span> | <span data-ttu-id="4b406-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="4b406-275">HPC 12</span></span> | <span data-ttu-id="4b406-276">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-276">Data disk</span></span> |
| <span data-ttu-id="4b406-277">SLES</span><span class="sxs-lookup"><span data-stu-id="4b406-277">SLES</span></span> | <span data-ttu-id="4b406-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="4b406-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="4b406-279">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-279">Data disk</span></span> |
| <span data-ttu-id="4b406-280">SLES</span><span class="sxs-lookup"><span data-stu-id="4b406-280">SLES</span></span> | <span data-ttu-id="4b406-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="4b406-281">11 SP4</span></span> | <span data-ttu-id="4b406-282">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4b406-282">Data disk</span></span> |

* <span data-ttu-id="4b406-283">Encriptação de disco do Azure requer que o Cofre de chaves e VMs residem em Olá mesma subscrição e região do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-284">Configurar recursos de Olá em regiões separadas causa uma falha na ativação da funcionalidade de Azure Disk Encryption Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="4b406-285">tooset até e configurar o seu Cofre de chaves do Azure Disk Encryption, consulte a secção **definir configurar e configurar o seu Cofre de chaves do Azure Disk Encryption** no Olá *pré-requisitos* secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="4b406-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="4b406-286">tooset até e configurar a aplicação do Azure AD no Azure Active directory para o Azure Disk Encryption, consulte a secção **configurar aplicação Olá do Azure AD no Azure Active Directory** no Olá *pré-requisitos* secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="4b406-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="4b406-287">tooset até e configurar a política de acesso do Cofre de chaves Olá para aplicação Olá do Azure AD, consulte a secção **configurar a política de acesso do Cofre de chaves Olá para aplicação Olá do Azure AD** no Olá *pré-requisitos* secção Este artigo.</span><span class="sxs-lookup"><span data-stu-id="4b406-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="4b406-288">tooprepare um VHD do Windows previamente encriptado, consulte a secção **preparar um VHD do Windows previamente encriptado** no Olá *apêndice*.</span><span class="sxs-lookup"><span data-stu-id="4b406-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="4b406-289">tooprepare um VHD previamente encriptado do Linux, consulte a secção **preparar um VHD de Linux previamente encriptado** no Olá *apêndice*.</span><span class="sxs-lookup"><span data-stu-id="4b406-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="4b406-290">Olá plataforma Azure necessita de acesso toohello encriptação chaves ou segredos no seu Cofre de chaves toomake-los máquina de virtual toohello disponível quando se efetua o arranque e desencripta o volume de máquina virtual SO Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="4b406-291">toogrant permissões tooAzure plataforma do conjunto Olá **EnabledForDiskEncryption** propriedade no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="4b406-292">Para obter mais informações, consulte **definir configurar e configurar o seu Cofre de chaves do Azure Disk Encryption** no Olá anexo.</span><span class="sxs-lookup"><span data-stu-id="4b406-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="4b406-293">O segredo do Cofre de chaves e os KEK URLs tem de ser com a versão.</span><span class="sxs-lookup"><span data-stu-id="4b406-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="4b406-294">Azure impõe esta restrição do controlo de versões.</span><span class="sxs-lookup"><span data-stu-id="4b406-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="4b406-295">Para segredo válido e KEK URLs, consulte Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b406-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="4b406-296">Exemplo de um URL válido secreto: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4b406-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="4b406-297">Exemplo de um URL válido da KEK: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4b406-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="4b406-298">Azure Disk Encryption não suporta a especificação de números de porta como parte dos segredos do Cofre de chaves e KEK URLs.</span><span class="sxs-lookup"><span data-stu-id="4b406-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="4b406-299">Para obter exemplos de URLs do Cofre de chaves suportadas e não suportados, consulte o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="4b406-300">URL do Cofre de chaves inaceitável *https://contosovault.vault.azure.net:443/segredos/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4b406-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="4b406-301">URL do Cofre de chaves aceitável: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4b406-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="4b406-302">funcionalidade do Azure Disk Encryption de tooenable Olá, Olá VMs de IaaS tem de cumprir os requisitos de configuração de ponto final de rede de Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="4b406-303">tooget um token tooconnect tooyour Cofre de chaves, Olá VM do IaaS tem de ser tooconnect capaz de ponto final do Azure Active Directory de tooan, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="4b406-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="4b406-304">toowrite Olá encriptação chaves tooyour Cofre de chaves, Olá VM do IaaS tem de ser ponto final do Cofre de chaves de toohello tooconnect possível.</span><span class="sxs-lookup"><span data-stu-id="4b406-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="4b406-305">Olá VM do IaaS tem de ser capaz de tooconnect ponto final da storage do Azure de tooan que anfitriões Olá repositório de extensão do Azure e uma conta de armazenamento do Azure que anfitriões Olá ficheiros VHD.</span><span class="sxs-lookup"><span data-stu-id="4b406-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4b406-306">Se a política de segurança limita o acesso a partir de VMs do Azure toohello Internet, pode resolver Olá precedente URI e configurar um toohello de conectividade de saída de tooallow de regra específica IPs.</span><span class="sxs-lookup"><span data-stu-id="4b406-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="4b406-307">tooconfigure e acesso Cofre de chaves do Azure atrás de uma firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="4b406-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="4b406-308">Utilize a versão mais recente do Olá do SDK do Azure PowerShell versão tooconfigure Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="4b406-309">Transferir a versão mais recente do Olá do [Azure PowerShell versão](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="4b406-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="4b406-310">Encriptação de disco do Azure não é suportada em [SDK do Azure PowerShell versão 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="4b406-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="4b406-311">Se está a receber um erro relacionado com toousing Azure PowerShell 1.1.0, consulte [tooAzure Azure disco encriptação erro relacionados com o PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="4b406-312">toorun qualquer comando da CLI do Azure e associá-lo à sua subscrição do Azure, primeiro é necessário instalar a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4b406-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="4b406-313">tooinstall CLI do Azure e associá-lo à sua subscrição do Azure, consulte [como tooinstall e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4b406-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="4b406-314">toouse CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager, consulte [comandos da CLI do Azure no modo Resource Manager](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="4b406-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="4b406-315">Quando a encriptar um disco gerido, é obrigatório tootake pré-requisitos um instantâneo do disco de Olá gerido ou uma cópia de segurança de disco de Olá fora da encriptação do Azure Disk Encryption tooenabling anterior.</span><span class="sxs-lookup"><span data-stu-id="4b406-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="4b406-316">Sem uma cópia de segurança no local, qualquer falha inesperada durante a encriptação poderá fazer disco Olá e VM inacessível sem uma opção de recuperação.</span><span class="sxs-lookup"><span data-stu-id="4b406-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="4b406-317">Conjunto AzureRmVMDiskEncryptionExtension atualmente não cópia de segurança discos geridos e será erro se utilizada relativamente um disco gerido, a menos que o parâmetro - skipVmBackup de Olá foi especificado.</span><span class="sxs-lookup"><span data-stu-id="4b406-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="4b406-318">Este parâmetro é toouse não seguro, a menos que já foi efetuada uma cópia de segurança fora do Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="4b406-319">Quando Olá - skipVmBackup parâmetro for especificado, Olá cmdlet não irá fazer uma cópia de segurança tooencryption anterior do disco Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="4b406-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="4b406-320">Por este motivo, é considerada um toomake pré-requisitos obrigatório se uma cópia de segurança de disco gerido Olá que VM se encontra em vigor anterior tooenabling Azure Disk Encryption no caso de recuperação posterior necessária.</span><span class="sxs-lookup"><span data-stu-id="4b406-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="4b406-321">parâmetro de - skipVmBackup Olá nunca deve ser utilizado, a menos que um instantâneo ou uma cópia de segurança já sido efetuada fora do Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="4b406-322">Olá solução da Azure Disk Encryption utiliza protetor de chave externo Olá BitLocker para VMs IaaS do Windows.</span><span class="sxs-lookup"><span data-stu-id="4b406-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="4b406-323">Para o domínio associado ao VMs, não EFETUE emitir quaisquer políticas de grupo que impõem protetores TPM.</span><span class="sxs-lookup"><span data-stu-id="4b406-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="4b406-324">Para obter informações sobre a política de grupo Olá "Permitir que o BitLocker sem um TPM compatível", consulte [referência de política de grupo do BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="4b406-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="4b406-325">Política do BitLocker em máquinas de virtuais associados a um domínio com a política de grupo personalizado tem de incluir Olá definição os seguintes: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure Disk Encryption irá falhar quando as definições de política de grupo personalizada para o Bitlocker são incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="4b406-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="4b406-326">Nas máquinas que não tinha Olá correto definição de política, aplicar a nova política de Olá, forçando Olá nova política tooupdate (gpupdate.exe /force) e, em seguida, reiniciar poderão ser necessária.</span><span class="sxs-lookup"><span data-stu-id="4b406-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="4b406-327">toocreate uma aplicação do Azure AD, criar um cofre de chaves, ou configurar um cofre de chaves e ativar a encriptação, consulte Olá [script do PowerShell de pré-requisitos do Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="4b406-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="4b406-328">os pré-requisitos de encriptação de disco tooconfigure utilizando Olá CLI do Azure, consulte [este script de Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4b406-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="4b406-329">toouse Olá Azure Backup service tooback cópias de segurança e restauro encriptado VMs, quando é ativada a encriptação com o Azure Disk Encryption, encriptam as suas VMs utilizando a configuração da chave Olá Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="4b406-330">serviço de cópia de segurança de Olá suporta VMs que estão encriptadas com a configuração de KEK apenas.</span><span class="sxs-lookup"><span data-stu-id="4b406-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="4b406-331">Consulte [como tooback cópias de segurança e restauro encriptados máquinas virtuais com a encriptação da cópia de segurança do Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="4b406-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="4b406-332">Encriptar um volume com SO Linux, tenha em atenção de que está atualmente necessário no final de Olá do processo de Olá de um reinício VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="4b406-333">Isto pode ser feito através do portal de Olá, powershell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="4b406-334">progresso de Olá tootrack de encriptação, consultar mensagem de estado de saudação devolvida pelo Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus periodicamente.</span><span class="sxs-lookup"><span data-stu-id="4b406-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="4b406-335">Depois de concluída a encriptação, mensagem de estado de Olá Olá devolvida por este comando irá indicar isto.</span><span class="sxs-lookup"><span data-stu-id="4b406-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="4b406-336">Por exemplo, "ProgressMessage: disco do SO encriptados com êxito, reinicie Olá VM" neste Olá ponto VM pode ser reiniciada e utilizada.</span><span class="sxs-lookup"><span data-stu-id="4b406-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="4b406-337">Azure Disk Encryption para Linux necessita de discos de dados toohave um sistema de ficheiros montado no tooencryption anterior do Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="4b406-338">Recursivamente discos de dados montada não são suportados pelo Olá Azure Disk Encryption para Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="4b406-339">Por exemplo, se hello sistema de destino tem montado um disco em /foo/bar e, em seguida, outra no /foo/bar/baz, encriptação Olá de /foo/bar/baz será concluída com êxito, mas a encriptação de barra/foo/irá falhar.</span><span class="sxs-lookup"><span data-stu-id="4b406-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="4b406-340">Azure Disk Encryption só é suportado nas imagens de galeria do Azure suportada que cumpre os pré-requisitos acima mencionados Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="4b406-341">Imagens personalizadas do cliente não são suportadas devido toocustom esquemas de partição e comportamentos de processos que possam existir nestas imagens.</span><span class="sxs-lookup"><span data-stu-id="4b406-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="4b406-342">Além disso, mesmo Galeria baseia imagem de VM que inicialmente cumpridos pré-requisitos, mas que foram modificada após a criação poderão não ser compatíveis.</span><span class="sxs-lookup"><span data-stu-id="4b406-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="4b406-343">Para que motivo, Olá sugerida procedimento para encriptar uma VM com Linux é toostart a partir de uma imagem de galeria limpa, encriptar Olá VM e, em seguida, adicionar personalizadas de software ou dados toohello VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="4b406-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="4b406-344">Cópia de segurança e restauro de VMs encriptadas só é suportada para VMs que estão encriptadas com a configuração de KEK Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="4b406-345">Não é suportada em VMs que são encriptadas sem KEK.</span><span class="sxs-lookup"><span data-stu-id="4b406-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="4b406-346">KEK é um parâmetro opcional que permite que a VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="4b406-347">Configurar Olá aplicação do Azure AD no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b406-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="4b406-348">Quando precisar de toobe encriptação ativada numa VM em execução no Azure, Azure Disk Encryption gera e escreve Olá encriptação chaves tooyour cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="4b406-349">Gestão de chaves de encriptação no seu Cofre de chaves requer autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="4b406-350">Para este fim, crie uma aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="4b406-351">Pode encontrar passos detalhados para registar uma aplicação na secção de "Obter uma identidade para Olá aplicação" Olá da mensagem de blogue Olá [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="4b406-352">Esta mensagem também contém um número de exemplos útil para definir e configurar o seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="4b406-353">Para efeitos de autenticação, pode utilizar a autenticação baseada em segredo do cliente ou autenticação de cliente baseada em certificados do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="4b406-354">Autenticação baseada em segredo do cliente para o Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b406-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="4b406-355">as secções de Olá que se seguem podem ajudá-lo a configurar uma autenticação baseada em segredo de cliente para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="4b406-356">Criar uma aplicação do Azure AD utilizando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b406-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="4b406-357">Utilize Olá seguir toocreate de cmdlet do PowerShell uma aplicação do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4b406-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="4b406-358">$azureAdApplication.ApplicationId é Olá, Azure AD ClientID e $aadClientSecret é segredo do cliente Olá que deve utilizar tooenable posterior Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="4b406-359">Salvaguarde adequadamente o segredo do cliente Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="4b406-360">Configurar o ID de cliente Olá do Azure AD e o segredo de Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="4b406-361">Pode também configurar o ID de cliente do Azure AD e o segredo utilizando Olá [portal clássico do Azure]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4b406-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="4b406-362">tooperform esta tarefa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b406-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="4b406-363">Clique em Olá **do Active Directory** separador.</span><span class="sxs-lookup"><span data-stu-id="4b406-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="4b406-365">Clique em **Adicionar aplicação**e, em seguida, tipo Olá nome da aplicação.</span><span class="sxs-lookup"><span data-stu-id="4b406-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="4b406-367">Clique no botão de seta de Olá e, em seguida, configure as propriedades da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="4b406-369">Clique em marca de verificação Olá no Olá inferior esquerda canto toofinish.</span><span class="sxs-lookup"><span data-stu-id="4b406-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="4b406-370">é apresentada a página de configuração de aplicação Olá e ID de cliente do Azure AD Olá é apresentada na Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="4b406-372">Guardar o segredo do cliente Olá do Azure AD, clicando em Olá **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="4b406-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="4b406-373">Tenha em atenção o segredo do cliente Olá do Azure AD na caixa de texto Olá chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="4b406-374">Salvaguarde adequadamente.</span><span class="sxs-lookup"><span data-stu-id="4b406-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="4b406-376">Olá precedente fluxo não é suportada em Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="4b406-377">Utilizar uma aplicação existente</span><span class="sxs-lookup"><span data-stu-id="4b406-377">Use an existing application</span></span>
<span data-ttu-id="4b406-378">tooexecute Olá os seguintes comandos, obtenha e utilize Olá [módulo Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-379">Olá seguintes comandos tem de ser executados a partir de uma nova janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b406-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="4b406-380">Utilize o Azure PowerShell ou os comandos janela Olá do Azure Resource Manager tooexecute Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="4b406-381">Recomendamos esta abordagem porque estes cmdlets no módulo de MSOnline Olá ou do Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b406-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="4b406-382">Autenticação baseada em certificado para o Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b406-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="4b406-383">Autenticação baseada em certificado. do Azure AD não é atualmente suportada em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="4b406-384">Olá secções que se seguem mostram como tooconfigure uma autenticação baseada em certificado para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="4b406-385">Criar uma aplicação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b406-385">Create an Azure AD application</span></span>
<span data-ttu-id="4b406-386">toocreate uma aplicação do Azure AD, execute Olá os seguintes cmdlets do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4b406-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-387">Substitua o seguinte Olá `yourpassword` cadeia com a sua palavra-passe segura e a palavra-passe Olá de salvaguarda.</span><span class="sxs-lookup"><span data-stu-id="4b406-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="4b406-388">Depois de concluir este passo, carregar um cofre de chaves de tooyour de ficheiro PFX e ativar Olá acesso políticas necessárias toodeploy tooa esse certificado VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="4b406-389">Utilizar uma aplicação do Azure AD existente</span><span class="sxs-lookup"><span data-stu-id="4b406-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="4b406-390">Se estiver a configurar a autenticação baseada em certificado para uma aplicação existente, utilize os cmdlets do PowerShell Olá mostrados aqui.</span><span class="sxs-lookup"><span data-stu-id="4b406-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="4b406-391">Ser se tooexecute-las a partir de uma nova janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b406-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="4b406-392">Depois de concluir este passo, carregar um cofre de chaves de tooyour de ficheiro PFX e ativar política de acesso de Olá necessários toodeploy Olá certificado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="4b406-393">Carregar um cofre de chaves de tooyour de ficheiro PFX</span><span class="sxs-lookup"><span data-stu-id="4b406-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="4b406-394">Para obter uma explicação detalhada deste processo, consulte [Olá oficial blogue de equipa do Cofre de chaves do Azure](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="4b406-395">No entanto, os seguintes cmdlets do PowerShell de Olá é tudo o que precisa para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="4b406-396">Ser se tooexecute-las a partir da consola do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b406-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-397">Substitua o seguinte Olá `yourpassword` cadeia com a sua palavra-passe segura e a palavra-passe Olá de salvaguarda.</span><span class="sxs-lookup"><span data-stu-id="4b406-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="4b406-398">Implemente um certificado no seu tooan do Cofre de chaves existentes VM</span><span class="sxs-lookup"><span data-stu-id="4b406-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="4b406-399">Depois de concluir o carregamento Olá PFX, implemente um certificado no Olá Cofre de chaves tooan existente VM com o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="4b406-400">Configurar a política de acesso do Cofre de chaves Olá para aplicação Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b406-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="4b406-401">A aplicação do Azure AD tem de chaves de Olá direitos tooaccess ou segredos no Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="4b406-402">Olá utilize [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissões toohello aplicação, ID de cliente de Olá (que foi gerado quando a aplicação Olá foi registada) a utilizar como Olá _– ServicePrincipalName_ valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4b406-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="4b406-403">toolearn mais, consulte a mensagem de blogue de Olá [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="4b406-404">Eis um exemplo de como tooperform esta tarefa através do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4b406-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="4b406-405">Encriptação de disco do Azure requer Olá tooconfigure seguir a aplicação de cliente de tooyour do Azure AD de políticas de acesso: _WrapKey_ e _definir_ permissões.</span><span class="sxs-lookup"><span data-stu-id="4b406-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="4b406-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="4b406-406">Terminology</span></span>
<span data-ttu-id="4b406-407">toounderstand alguns dos termos comuns Olá utilizado por esta tecnologia, Olá utilize terminologia a tabela seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b406-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="4b406-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="4b406-408">Terminology</span></span> | <span data-ttu-id="4b406-409">Definição</span><span class="sxs-lookup"><span data-stu-id="4b406-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="4b406-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b406-410">Azure AD</span></span> | <span data-ttu-id="4b406-411">Azure AD [do Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="4b406-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="4b406-412">Uma conta do Azure AD é um pré-requisito para autenticar, armazenar e obter segredos a partir de um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="4b406-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4b406-413">Azure Key Vault</span></span> | <span data-ttu-id="4b406-414">O Cofre de chaves é um serviço de gestão de serviços de criptografia, chave baseada em módulos de segurança de hardware validados Federal Information Processing Standards FIPS, que ajudam a salvaguardar as chaves criptográficas e segredos confidenciais.</span><span class="sxs-lookup"><span data-stu-id="4b406-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="4b406-415">Para obter mais informações, consulte [Cofre de chaves](https://azure.microsoft.com/services/key-vault/) documentação.</span><span class="sxs-lookup"><span data-stu-id="4b406-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="4b406-416">ARM</span><span class="sxs-lookup"><span data-stu-id="4b406-416">ARM</span></span> | <span data-ttu-id="4b406-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b406-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="4b406-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="4b406-418">BitLocker</span></span> |<span data-ttu-id="4b406-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) é uma reconhecido do setor Windows volume encriptação tecnologia que tenha utilizado a encriptação de disco tooenable em VMs de IaaS do Windows.</span><span class="sxs-lookup"><span data-stu-id="4b406-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="4b406-420">BEK</span><span class="sxs-lookup"><span data-stu-id="4b406-420">BEK</span></span> | <span data-ttu-id="4b406-421">Chaves de encriptação do BitLocker são volume de arranque de Olá SO tooencrypt utilizado e os volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="4b406-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="4b406-422">chaves do BitLocker Olá são salvaguardadas no Cofre de chaves como segredos.</span><span class="sxs-lookup"><span data-stu-id="4b406-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="4b406-423">CLI</span><span class="sxs-lookup"><span data-stu-id="4b406-423">CLI</span></span> | <span data-ttu-id="4b406-424">Consulte [interface de linha de comandos do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4b406-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="4b406-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="4b406-425">DM-Crypt</span></span> |<span data-ttu-id="4b406-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) subsistema de encriptação de disco baseado em Linux, transparente Olá que tenha utilizado a encriptação de disco tooenable em VMs de IaaS Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="4b406-427">KEK</span><span class="sxs-lookup"><span data-stu-id="4b406-427">KEK</span></span> | <span data-ttu-id="4b406-428">Chave de encriptação de chaves é Olá chave assimétrica (RSA 2048) que pode utilizar tooprotect ou moldar segredo Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="4b406-429">Pode fornecer uma segurança de hardware (HSM) de módulos-chave ou de chave protegida por software protegidos.</span><span class="sxs-lookup"><span data-stu-id="4b406-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="4b406-430">Para obter mais detalhes, consulte [Cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/) documentação.</span><span class="sxs-lookup"><span data-stu-id="4b406-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="4b406-431">PS cmdlets</span><span class="sxs-lookup"><span data-stu-id="4b406-431">PS cmdlets</span></span> | <span data-ttu-id="4b406-432">Consulte [cmdlets Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b406-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="4b406-433">Definir e configurar o seu Cofre de chaves para o Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="4b406-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="4b406-434">Ajuda do Azure Disk Encryption chaves de encriptação de disco de Olá de salvaguarda e segredos no seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="4b406-435">tooset se o seu Cofre de chaves para o Azure Disk Encryption, Olá concluir os passos em cada uma das seguintes secções de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="4b406-436">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4b406-436">Create a key vault</span></span>
<span data-ttu-id="4b406-437">toocreate um cofre de chaves, utilize uma das seguintes opções de Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="4b406-438">Modelo de Gestor de recursos "101-chave-cofre-criar"</span><span class="sxs-lookup"><span data-stu-id="4b406-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="4b406-439">Cmdlets do Cofre de chaves do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b406-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="4b406-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b406-440">Azure Resource Manager</span></span>
* <span data-ttu-id="4b406-441">Como demasiado[proteger o seu Cofre de chaves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="4b406-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-442">Se já tiver configurado um cofre de chaves para a sua subscrição, ignore a secção seguinte toohello.</span><span class="sxs-lookup"><span data-stu-id="4b406-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="4b406-444">Configurar uma chave de encriptação de chaves (opcional)</span><span class="sxs-lookup"><span data-stu-id="4b406-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="4b406-445">Se pretender toouse um KEK para uma camada adicional de segurança de chaves de encriptação do BitLocker Olá, adicione um cofre de chaves de tooyour KEK.</span><span class="sxs-lookup"><span data-stu-id="4b406-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="4b406-446">Olá utilize [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate uma chave de encriptação de chaves no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="4b406-447">Também pode importar um KEK da sua gestão de chaves HSM no local.</span><span class="sxs-lookup"><span data-stu-id="4b406-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="4b406-448">Para obter mais detalhes, consulte [documentação do Cofre de chave](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="4b406-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="4b406-449">Pode adicionar Olá KEK acedendo tooAzure Resource Manager ou utilizando a interface do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="4b406-451">Definir permissões do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4b406-451">Set key vault permissions</span></span>
<span data-ttu-id="4b406-452">Olá plataforma Azure necessita de acesso toohello encriptação chaves ou segredos no seu Cofre de chaves toomake-los toohello disponível VM para arrancar e desencriptação de volumes de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="4b406-453">toogrant permissões toohello plataforma do Azure, conjunto Olá **EnabledForDiskEncryption** propriedade chave Olá cofre utilizando o cmdlet do PowerShell Olá Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4b406-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="4b406-454">Também pode definir Olá **EnabledForDiskEncryption** propriedade, visitando Olá [Explorador de recursos do Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b406-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="4b406-455">Conforme mencionado anteriormente, tem de definir Olá **EnabledForDiskEncryption** propriedade no seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="4b406-456">Caso contrário, Olá implementação irá falhar.</span><span class="sxs-lookup"><span data-stu-id="4b406-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="4b406-457">Pode configurar políticas de acesso para a sua aplicação do Azure AD da interface do Cofre de chaves de Olá, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="4b406-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="4b406-460">No Olá **políticas de acesso avançadas** separador, certifique-se de que o seu Cofre de chaves está ativada para a Azure Disk Encryption:</span><span class="sxs-lookup"><span data-stu-id="4b406-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Cofre de chaves do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="4b406-462">Cenários de implementação de encriptação de disco e as experiências de utilizador</span><span class="sxs-lookup"><span data-stu-id="4b406-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="4b406-463">Pode ativar vários cenários de encriptação de disco e passos de Olá podem variar de acordo com o cenário de toohello.</span><span class="sxs-lookup"><span data-stu-id="4b406-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="4b406-464">Olá secções seguintes abrangem os cenários de Olá mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="4b406-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="4b406-465">Ativar a encriptação em novas VMs de IaaS criados a partir de Olá Marketplace</span><span class="sxs-lookup"><span data-stu-id="4b406-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="4b406-466">Pode ativar a encriptação de disco em nova VM do IaaS Windows de Olá Marketplace no Azure utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="4b406-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="4b406-467">No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b406-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4b406-468">Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable encriptação numa nova VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-469">Este modelo cria uma nova VM do Windows encriptados que utiliza a imagem de galeria Olá Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="4b406-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="4b406-470">Pode ativar a encriptação de disco num novo IaaS VM de RedHat Linux 7.2 com uma matriz de RAID 0 200 GB ao utilizar este [modelo do Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="4b406-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="4b406-471">Depois de implementar a modelo Olá, verificar o estado de encriptação de VM Olá utilizando Olá `Get-AzureRmVmDiskEncryptionStatus` cmdlet, conforme descrito em [SO de encriptação de unidade numa VM com Linux em execução](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="4b406-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="4b406-472">Quando a máquina Olá devolve um Estado de _VMRestartPending_, reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="4b406-473">Olá tabela seguinte lista os parâmetros de modelo do Resource Manager Olá para novas VMs do cenário de Marketplace Olá utilizando o ID de cliente do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4b406-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="4b406-474">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4b406-474">Parameter</span></span> | <span data-ttu-id="4b406-475">Descrição</span><span class="sxs-lookup"><span data-stu-id="4b406-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b406-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="4b406-476">adminUserName</span></span> | <span data-ttu-id="4b406-477">Nome de utilizador de administrador para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="4b406-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="4b406-478">adminPassword</span></span> | <span data-ttu-id="4b406-479">Administração utilizador palavra-passe para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="4b406-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="4b406-480">newStorageAccountName</span></span> | <span data-ttu-id="4b406-481">Nome do toostore de conta de armazenamento Olá SO e dados os VHDs.</span><span class="sxs-lookup"><span data-stu-id="4b406-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="4b406-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="4b406-482">vmSize</span></span> | <span data-ttu-id="4b406-483">Tamanho do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-483">Size of hello VM.</span></span> <span data-ttu-id="4b406-484">Atualmente, é suportada apenas padrão A, D e G série.</span><span class="sxs-lookup"><span data-stu-id="4b406-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="4b406-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="4b406-485">virtualNetworkName</span></span> | <span data-ttu-id="4b406-486">Nome da VNet que Olá NIC de VM de Olá deverão pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="4b406-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="4b406-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="4b406-487">subnetName</span></span> | <span data-ttu-id="4b406-488">Nome da sub-rede Olá Olá VNet que Olá VM NIC deverão pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="4b406-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="4b406-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="4b406-489">AADClientID</span></span> | <span data-ttu-id="4b406-490">ID de cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos tooyour cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="4b406-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="4b406-491">AADClientSecret</span></span> | <span data-ttu-id="4b406-492">Segredo do cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos tooyour cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="4b406-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="4b406-493">keyVaultURL</span></span> | <span data-ttu-id="4b406-494">URL da chave de Olá cofre que Olá chave deve ser carregada para o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4b406-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="4b406-495">Pode obtê-lo utilizando o cmdlet Olá `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="4b406-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="4b406-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="4b406-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="4b406-497">URL da chave de encriptação de chaves de Olá que é utilizado tooencrypt Olá gerou a chave do BitLocker (opcional).</span><span class="sxs-lookup"><span data-stu-id="4b406-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="4b406-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b406-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="4b406-499">Grupo de recursos do Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="4b406-500">vmName</span><span class="sxs-lookup"><span data-stu-id="4b406-500">vmName</span></span> | <span data-ttu-id="4b406-501">Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa.</span><span class="sxs-lookup"><span data-stu-id="4b406-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="4b406-502">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="4b406-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="4b406-503">Pode colocar a sua própria chave de encriptação dados do KEK toofurther salvaguarda Olá (segredo frase de acesso) no seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="4b406-504">Ativar a encriptação em novas VMs de IaaS criados a partir de VHD encriptados de cliente e chaves de encriptação</span><span class="sxs-lookup"><span data-stu-id="4b406-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="4b406-505">Neste cenário, pode ativar a encriptação utilizando o modelo do Resource Manager Olá, os cmdlets do PowerShell ou comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="4b406-506">Olá secções seguintes explicam no modelo do Resource Manager maior Olá de detalhe e comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="4b406-507">Siga as instruções de Olá a partir de um nestas secções para preparar imagens previamente encriptadas, que podem ser utilizadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="4b406-508">Depois de criada a imagem de Olá, pode utilizar os passos de Olá no Olá seguinte secção toocreate encriptados VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="4b406-509">Preparar um VHD do Windows previamente encriptado</span><span class="sxs-lookup"><span data-stu-id="4b406-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="4b406-510">Preparar um VHD de Linux previamente encriptado</span><span class="sxs-lookup"><span data-stu-id="4b406-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="4b406-511">Utilizar o modelo do Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="4b406-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="4b406-512">Pode ativar a encriptação de disco no seu VHD encriptado utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="4b406-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="4b406-513">No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b406-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4b406-514">Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable encriptação em Olá nova VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="4b406-515">Olá tabela seguinte lista os parâmetros de modelo do Resource Manager Olá para o VHD encriptado:</span><span class="sxs-lookup"><span data-stu-id="4b406-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="4b406-516">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4b406-516">Parameter</span></span> | <span data-ttu-id="4b406-517">Descrição</span><span class="sxs-lookup"><span data-stu-id="4b406-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b406-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="4b406-518">newStorageAccountName</span></span> | <span data-ttu-id="4b406-519">Nome do Olá de toostore de conta de armazenamento Olá encriptados VHD de SO.</span><span class="sxs-lookup"><span data-stu-id="4b406-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="4b406-520">Esta conta de armazenamento deve já ter sido criada na Olá mesmo grupo de recursos e a mesma localização que Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="4b406-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="4b406-521">osVhdUri</span></span> | <span data-ttu-id="4b406-522">URI de Olá SO VHD a partir da conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="4b406-523">osType</span><span class="sxs-lookup"><span data-stu-id="4b406-523">osType</span></span> | <span data-ttu-id="4b406-524">Tipo de produto do SO (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="4b406-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="4b406-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="4b406-525">virtualNetworkName</span></span> | <span data-ttu-id="4b406-526">Nome da VNet que Olá NIC de VM de Olá deverão pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="4b406-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="4b406-527">Olá nome deve já ter sido criado na Olá mesmo grupo de recursos e a mesma localização que Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="4b406-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="4b406-528">subnetName</span></span> | <span data-ttu-id="4b406-529">Nome da sub-rede Olá no Olá VNet que Olá VM NIC deverão pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="4b406-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="4b406-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="4b406-530">vmSize</span></span> | <span data-ttu-id="4b406-531">Tamanho do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-531">Size of hello VM.</span></span> <span data-ttu-id="4b406-532">Atualmente, é suportada apenas padrão A, D e G série.</span><span class="sxs-lookup"><span data-stu-id="4b406-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="4b406-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="4b406-533">keyVaultResourceID</span></span> | <span data-ttu-id="4b406-534">Olá ResourceID que identifica o Cofre de chaves Olá no Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="4b406-535">Pode obtê-lo utilizando o cmdlet do PowerShell Olá `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="4b406-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="4b406-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="4b406-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="4b406-537">URL da chave de encriptação de disco de Olá que é definida no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="4b406-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="4b406-538">keyVaultKekUrl</span></span> | <span data-ttu-id="4b406-539">URL da chave de encriptação de chaves de Olá para encriptar a chave de encriptação de disco Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="4b406-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="4b406-540">vmName</span><span class="sxs-lookup"><span data-stu-id="4b406-540">vmName</span></span> | <span data-ttu-id="4b406-541">Nome do Olá VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="4b406-542">Utilizando os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b406-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="4b406-543">Pode ativar a encriptação de disco no seu VHD encriptado utilizando o cmdlet do PowerShell Olá [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="4b406-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="4b406-544">Utilizar comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="4b406-544">Using CLI commands</span></span>
<span data-ttu-id="4b406-545">encriptação de disco tooenable para este cenário através da utilização de comandos da CLI, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="4b406-546">Definir políticas de acesso no seu Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4b406-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="4b406-547">Conjunto Olá **EnabledForDiskEncryption** sinalizador:</span><span class="sxs-lookup"><span data-stu-id="4b406-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="4b406-548">Definir permissões tooAzure AD aplicação toowrite segredos tooyour Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4b406-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="4b406-549">encriptação de tooenable numa VM existente ou em execução, tipo:</span><span class="sxs-lookup"><span data-stu-id="4b406-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="4b406-550">Obter o estado de encriptação:</span><span class="sxs-lookup"><span data-stu-id="4b406-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="4b406-551">encriptação de tooenable numa VM nova do seu VHD encriptado, Olá utilize seguir os parâmetros com Olá `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="4b406-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="4b406-552">Ativar a encriptação em existente ou VM do IaaS Windows a executar no Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="4b406-553">Neste cenário, pode ativar a encriptação utilizando o modelo do Resource Manager Olá, os cmdlets do PowerShell ou comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="4b406-554">Olá secções seguintes explicam mais detalhadamente como tooenable-lo utilizando Olá modelo do Resource Manager e os comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="4b406-555">Utilizar o modelo do Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="4b406-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="4b406-556">Pode ativar a encriptação de disco existente ou VMs do IaaS Windows em execução no Azure utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="4b406-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="4b406-557">No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b406-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4b406-558">Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable a encriptação em Olá existente ou VM do IaaS a ser executado.</span><span class="sxs-lookup"><span data-stu-id="4b406-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="4b406-559">Olá tabela seguinte apresenta uma lista de parâmetros de modelo do Resource Manager Olá para existente ou executar as VMs que utilizam um ID de cliente do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4b406-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="4b406-560">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4b406-560">Parameter</span></span> | <span data-ttu-id="4b406-561">Descrição</span><span class="sxs-lookup"><span data-stu-id="4b406-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b406-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="4b406-562">AADClientID</span></span> | <span data-ttu-id="4b406-563">ID de cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos toohello cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="4b406-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="4b406-564">AADClientSecret</span></span> | <span data-ttu-id="4b406-565">Segredo do cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos toohello cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="4b406-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="4b406-566">keyVaultName</span></span> | <span data-ttu-id="4b406-567">Nome da chave de Olá cofre que Olá chave deve ser carregada para o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4b406-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="4b406-568">Pode obtê-lo utilizando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="4b406-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="4b406-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="4b406-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="4b406-570">URL da chave de encriptação de chaves de Olá que é utilizado tooencrypt Olá gerou a chave do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4b406-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="4b406-571">Este parâmetro é opcional se selecionar **nokek** na lista de Olá UseExistingKek lista pendente.</span><span class="sxs-lookup"><span data-stu-id="4b406-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="4b406-572">Se selecionar **kek** na lista de Olá pendente UseExistingKek, tem de introduzir Olá _keyEncryptionKeyURL_ valor.</span><span class="sxs-lookup"><span data-stu-id="4b406-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="4b406-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="4b406-573">volumeType</span></span> | <span data-ttu-id="4b406-574">Tipo de volume que é efetuar a operação de encriptação de Olá na.</span><span class="sxs-lookup"><span data-stu-id="4b406-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="4b406-575">Os valores válidos são _SO_, _dados_, e _todos os_.</span><span class="sxs-lookup"><span data-stu-id="4b406-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="4b406-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="4b406-576">sequenceVersion</span></span> | <span data-ttu-id="4b406-577">Versão de sequência de Olá BitLocker operação.</span><span class="sxs-lookup"><span data-stu-id="4b406-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="4b406-578">Aumentar este número de versão sempre que é efetuar uma operação de encriptação de disco no Olá mesma VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="4b406-579">vmName</span><span class="sxs-lookup"><span data-stu-id="4b406-579">vmName</span></span> | <span data-ttu-id="4b406-580">Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa.</span><span class="sxs-lookup"><span data-stu-id="4b406-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="4b406-581">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="4b406-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="4b406-582">Pode colocar a sua própria chave de encriptação dados do KEK toofurther salvaguarda Olá (segredo de encriptação do BitLocker) no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="4b406-583">Utilizando os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b406-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="4b406-584">Para obter informações sobre como ativar a encriptação com o Azure Disk Encryption utilizando cmdlets do PowerShell, consulte as mensagens de blogue Olá [explorar o Azure Disk Encryption com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar o Azure Disk Encryption com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="4b406-585">Utilizar comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="4b406-585">Using CLI commands</span></span>
<span data-ttu-id="4b406-586">encriptação de tooenable em existente ou VM do IaaS Windows a executar no Azure através de comandos da CLI, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="4b406-587">políticas de acesso de tooset no Cofre de chaves Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="4b406-588">Conjunto Olá **EnabledForDiskEncryption** sinalizador:</span><span class="sxs-lookup"><span data-stu-id="4b406-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="4b406-589">Definir permissões tooAzure AD aplicação toowrite segredos tooyour Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4b406-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="4b406-590">encriptação de tooenable numa VM existente ou em execução:</span><span class="sxs-lookup"><span data-stu-id="4b406-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="4b406-591">Estado de encriptação tooget:</span><span class="sxs-lookup"><span data-stu-id="4b406-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="4b406-592">encriptação de tooenable numa VM nova do seu VHD encriptado, Olá utilize seguir os parâmetros com Olá `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="4b406-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="4b406-593">Ativar a encriptação de uma VM do Linux IaaS existente ou em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="4b406-594">Pode ativar a encriptação de disco num VM do Linux IaaS existente ou em execução no Azure utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="4b406-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="4b406-595">Clique em **implementar tooAzure** no modelo de Olá início rápido do Azure, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b406-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4b406-596">Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable a encriptação em Olá existente ou VM do IaaS a ser executado.</span><span class="sxs-lookup"><span data-stu-id="4b406-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="4b406-597">Olá, a tabela seguinte lista os parâmetros do modelo do Resource Manager para existente ou executar as VMs que utilizam um ID de cliente do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4b406-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="4b406-598">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4b406-598">Parameter</span></span> | <span data-ttu-id="4b406-599">Descrição</span><span class="sxs-lookup"><span data-stu-id="4b406-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b406-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="4b406-600">AADClientID</span></span> | <span data-ttu-id="4b406-601">ID de cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos toohello cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="4b406-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="4b406-602">AADClientSecret</span></span> | <span data-ttu-id="4b406-603">Segredo do cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos tooyour cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="4b406-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="4b406-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="4b406-604">keyVaultName</span></span> | <span data-ttu-id="4b406-605">Nome da chave de Olá cofre que Olá chave deve ser carregada para o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4b406-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="4b406-606">Pode obtê-lo utilizando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="4b406-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="4b406-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="4b406-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="4b406-608">URL da chave de encriptação de chaves de Olá que é utilizado tooencrypt Olá gerou a chave do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4b406-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="4b406-609">Este parâmetro é opcional se selecionar **nokek** na lista de Olá UseExistingKek lista pendente.</span><span class="sxs-lookup"><span data-stu-id="4b406-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="4b406-610">Se selecionar **kek** na lista de Olá pendente UseExistingKek, tem de introduzir Olá _keyEncryptionKeyURL_ valor.</span><span class="sxs-lookup"><span data-stu-id="4b406-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="4b406-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="4b406-611">volumeType</span></span> | <span data-ttu-id="4b406-612">Tipo de volume que é efetuar a operação de encriptação de Olá na.</span><span class="sxs-lookup"><span data-stu-id="4b406-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="4b406-613">Os valores suportados válidos são _SO_ ou _todos os_ (para RHEL 7.2, CentOS 7.2 e Ubuntu 16.04), e _dados_ (para todos os outras distribuições).</span><span class="sxs-lookup"><span data-stu-id="4b406-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="4b406-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="4b406-614">sequenceVersion</span></span> | <span data-ttu-id="4b406-615">Versão de sequência de Olá BitLocker operação.</span><span class="sxs-lookup"><span data-stu-id="4b406-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="4b406-616">Aumentar este número de versão sempre que é efetuar uma operação de encriptação de disco no Olá mesma VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="4b406-617">vmName</span><span class="sxs-lookup"><span data-stu-id="4b406-617">vmName</span></span> | <span data-ttu-id="4b406-618">Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa.</span><span class="sxs-lookup"><span data-stu-id="4b406-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="4b406-619">frase de acesso</span><span class="sxs-lookup"><span data-stu-id="4b406-619">passPhrase</span></span> | <span data-ttu-id="4b406-620">Escreva uma frase de acesso forte como chave de encriptação de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="4b406-621">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="4b406-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="4b406-622">Pode colocar a sua própria chave de encriptação dados do KEK toofurther salvaguarda Olá (segredo frase de acesso) no seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="4b406-623">Comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="4b406-623">CLI commands</span></span>
<span data-ttu-id="4b406-624">Pode ativar a encriptação de disco no seu VHD encriptado através da instalação e utilização Olá [comando da CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4b406-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="4b406-625">encriptação de tooenable em existente ou VMs do IaaS Linux em execução no Azure através da utilização de comandos da CLI, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="4b406-626">Definir políticas de acesso no Cofre de chaves Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="4b406-627">Conjunto Olá **EnabledForDiskEncryption** sinalizador:</span><span class="sxs-lookup"><span data-stu-id="4b406-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="4b406-628">Definir permissões tooAzure AD aplicação toowrite segredos tooyour Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4b406-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="4b406-629">encriptação de tooenable numa VM existente ou em execução:</span><span class="sxs-lookup"><span data-stu-id="4b406-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="4b406-630">Obter o estado de encriptação:</span><span class="sxs-lookup"><span data-stu-id="4b406-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="4b406-631">encriptação de tooenable numa VM nova do seu VHD encriptado, Olá utilize seguir os parâmetros com Olá `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="4b406-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="4b406-632">Obter o estado de encriptação de Olá de uma VM do IaaS encriptados</span><span class="sxs-lookup"><span data-stu-id="4b406-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="4b406-633">Pode obter o estado de encriptação de Olá utilizando o Gestor de recursos do Azure, [cmdlets do PowerShell](/powershell/azure/overview), ou comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="4b406-634">Olá secções a seguir explica como toouse Olá portal clássico do Azure e tooget de comandos da CLI Olá estado de encriptação.</span><span class="sxs-lookup"><span data-stu-id="4b406-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="4b406-635">Obter o estado de encriptação de Olá de uma VM do Windows encriptada utilizando o Gestor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="4b406-636">Pode obter estado de encriptação de Olá de Olá VM do IaaS do Azure Resource Manager, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b406-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="4b406-637">Inicie sessão no toohello [portal clássico do Azure](https://portal.azure.com/)e, em seguida, clique em **máquinas virtuais** no painel esquerdo de Olá toosee uma vista de resumo de máquinas de virtuais Olá na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="4b406-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="4b406-638">Pode filtrar a vista de máquinas virtuais de Olá, selecionando o nome da subscrição Olá na Olá **subscrição** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="4b406-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="4b406-639">Na parte superior de Olá de Olá **máquinas virtuais** página, clique em **colunas**.</span><span class="sxs-lookup"><span data-stu-id="4b406-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="4b406-640">No Olá **escolha coluna** painel, selecione **encriptação de disco**e, em seguida, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="4b406-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="4b406-641">Deverá ver o estado de encriptação de Olá coluna Mostrar Olá encriptação de disco _ativado_ ou _não ativada_ para cada VM, conforme mostrado no Olá figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b406-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="4b406-643">Obter o estado de encriptação de Olá de uma VM do IaaS (Windows/Linux) encriptada utilizando o cmdlet do PowerShell de encriptação de disco de Olá</span><span class="sxs-lookup"><span data-stu-id="4b406-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="4b406-644">Pode obter o estado de encriptação de Olá de Olá VM do IaaS do cmdlet do PowerShell de encriptação de disco de Olá `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="4b406-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="4b406-645">definições de encriptação de Olá tooget para a VM, introduza o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="4b406-646">Pode inspecionar resultado Olá _Get-AzureRmVMDiskEncryptionStatus_ URLs da chave de encriptação.</span><span class="sxs-lookup"><span data-stu-id="4b406-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="4b406-647">Olá OSVolumeEncrypted e valores de definições de DataVolumesEncrypted estão definidos too_Encrypted_, que mostra que ambos os volumes são encriptados utilizando a Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="4b406-648">Para obter informações sobre como ativar a encriptação com o Azure Disk Encryption utilizando cmdlets do PowerShell, consulte as mensagens de blogue Olá [explorar o Azure Disk Encryption com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar o Azure Disk Encryption com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b406-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-649">Em VMs do Linux, três toofour de demora minutos Olá `Get-AzureRmVMDiskEncryptionStatus` estado de encriptação do cmdlet tooreport Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="4b406-650">Obter o estado de encriptação de Olá de Olá VM do IaaS do comando de CLI de encriptação de disco Olá</span><span class="sxs-lookup"><span data-stu-id="4b406-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="4b406-651">Pode obter o estado de encriptação de Olá de Olá VM do IaaS utilizando o comando CLI de encriptação de disco Olá `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="4b406-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="4b406-652">definições de encriptação de Olá tooget para a VM, introduza a sua sessão do CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4b406-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="4b406-653">Desativar a encriptação sobre a execução de VM do IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="4b406-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="4b406-654">Pode desativar a encriptação num Windows em execução ou VM do IaaS Linux através do modelo de encriptação de disco do Azure Resource Manager Olá ou os cmdlets do PowerShell e especificar a configuração de desencriptação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="4b406-655">VM do Windows</span><span class="sxs-lookup"><span data-stu-id="4b406-655">Windows VM</span></span>
<span data-ttu-id="4b406-656">passo de encriptação de desativar Olá desativa a encriptação de Olá SO, volume de dados de Olá ou ambos num Olá VM do IaaS Windows a executar.</span><span class="sxs-lookup"><span data-stu-id="4b406-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="4b406-657">Não é possível desativar o volume de SO Olá e deixe o volume de dados de Olá encriptado.</span><span class="sxs-lookup"><span data-stu-id="4b406-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="4b406-658">Quando for executado o passo de encriptação de desativar Olá, modelo de VM Olá do serviço de atualizações do modelo de implementação clássico do Azure Olá e Olá VM do IaaS Windows está marcado como desencriptada.</span><span class="sxs-lookup"><span data-stu-id="4b406-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="4b406-659">conteúdo Olá Olá VM já não é encriptado em pausa.</span><span class="sxs-lookup"><span data-stu-id="4b406-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="4b406-660">desencriptação de Olá não eliminar o Cofre e Olá encriptação chave material de chaves (chaves de encriptação BitLocker para Windows e o frase de acesso para Linux).</span><span class="sxs-lookup"><span data-stu-id="4b406-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="4b406-661">VM com Linux</span><span class="sxs-lookup"><span data-stu-id="4b406-661">Linux VM</span></span>
<span data-ttu-id="4b406-662">passo de encriptação de desativar Olá desativa a encriptação de volume de dados de Olá no Olá VM do IaaS Linux a executar.</span><span class="sxs-lookup"><span data-stu-id="4b406-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="4b406-663">Este passo só funciona se o disco do SO Olá não estiver encriptado.</span><span class="sxs-lookup"><span data-stu-id="4b406-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-664">A desativação da encriptação no disco do SO Olá não é permitida em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="4b406-665">Desativar a encriptação de uma VM do IaaS existente ou em execução</span><span class="sxs-lookup"><span data-stu-id="4b406-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="4b406-666">Pode desativar a encriptação de disco em execução VMs de IaaS do Windows utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="4b406-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="4b406-667">No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de desencriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b406-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4b406-668">Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable encriptação numa nova VM do IaaS.</span><span class="sxs-lookup"><span data-stu-id="4b406-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="4b406-669">Para VMs com Linux, pode desativar a encriptação utilizando Olá [desativar a encriptação de uma VM com Linux em execução](https://aka.ms/decrypt-linuxvm) modelo.</span><span class="sxs-lookup"><span data-stu-id="4b406-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="4b406-670">Olá tabela seguinte lista os parâmetros do modelo do Resource Manager para desativar a encriptação de uma VM do IaaS em execução:</span><span class="sxs-lookup"><span data-stu-id="4b406-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="4b406-671">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4b406-671">Parameter</span></span> | <span data-ttu-id="4b406-672">Descrição</span><span class="sxs-lookup"><span data-stu-id="4b406-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b406-673">vmName</span><span class="sxs-lookup"><span data-stu-id="4b406-673">vmName</span></span> | <span data-ttu-id="4b406-674">Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa.</span><span class="sxs-lookup"><span data-stu-id="4b406-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="4b406-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="4b406-675">volumeType</span></span> | <span data-ttu-id="4b406-676">Tipo de volume que é efetuar uma operação de desencriptação no.</span><span class="sxs-lookup"><span data-stu-id="4b406-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="4b406-677">Os valores válidos são _SO_, _dados_, e _todos os_.</span><span class="sxs-lookup"><span data-stu-id="4b406-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="4b406-678">Não é possível desativar a encriptação em com o volume de VM do IaaS Windows SO/arranque sem desativar a encriptação em Olá _dados_ volume.</span><span class="sxs-lookup"><span data-stu-id="4b406-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="4b406-679">Note também que a desativação da encriptação no disco do SO Olá não é permitida em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="4b406-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="4b406-680">sequenceVersion</span></span> | <span data-ttu-id="4b406-681">Versão de sequência de Olá BitLocker operação.</span><span class="sxs-lookup"><span data-stu-id="4b406-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="4b406-682">Aumentar este número de versão sempre que uma operação de desencriptação de disco for executada num Olá mesma VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="4b406-683">Desativar a encriptação de uma VM do IaaS existente ou em execução</span><span class="sxs-lookup"><span data-stu-id="4b406-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="4b406-684">encriptação de toodisable numa IaaS VM em execução ou existente utilizando o cmdlet do PowerShell Olá, consulte [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="4b406-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="4b406-685">Este cmdlet suporta o Windows e VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="4b406-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="4b406-686">encriptação de toodisable, instala uma extensão na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="4b406-687">Se hello _nome_ parâmetro não for especificado, uma extensão com o nome predefinido de Olá _AzureDiskEncryption para VMs do Windows_ é criado.</span><span class="sxs-lookup"><span data-stu-id="4b406-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="4b406-688">Em VMs do Linux, Olá AzureDiskEncryptionForLinux extensão é utilizado.</span><span class="sxs-lookup"><span data-stu-id="4b406-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="4b406-689">Este cmdlet é reiniciado Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="4b406-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="4b406-690">Ativar a encriptação em VM do IaaS previamente encriptado com o disco gerida do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="4b406-691">Utilizar Olá ARM do Azure gerida disco modelo toocreate uma VM encriptada a partir de um VHD previamente encriptado utilizando o modelo ARM Olá localizada em</span><span class="sxs-lookup"><span data-stu-id="4b406-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="4b406-692">[Criar um novo disco gerido encriptado a partir de um blob VHD/armazenamento previamente encriptado] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="4b406-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="4b406-693">Ativar a encriptação numa nova VM do IaaS Linux com o disco gerida do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="4b406-694">Utilizar toocreate de modelo de ARM do Azure gerida disco Olá que um novo encriptados VM do IaaS Linux utilizando o modelo ARM Olá localizado em</span><span class="sxs-lookup"><span data-stu-id="4b406-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="4b406-695">[Implementação do RHEL 7.2 com a encriptação de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="4b406-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="4b406-696">Ativar a encriptação numa nova VM do IaaS do Windows com o disco gerida do Azure</span><span class="sxs-lookup"><span data-stu-id="4b406-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="4b406-697">Utilizar toocreate de modelo de ARM do Azure gerida disco Olá que um novo encriptados VM do IaaS Linux utilizando o modelo ARM Olá localizado em</span><span class="sxs-lookup"><span data-stu-id="4b406-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="4b406-698">[Criar um novo encriptados IaaS geridos disco VM do Windows da imagem de galeria] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="4b406-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="4b406-699">É obrigatório toosnapshot e/ou a cópia de segurança um geridos com base em disco instância VM fora do e tooenabling anterior Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4b406-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="4b406-700">Pode ser obtido um instantâneo de disco gerido Olá do portal de Olá, ou cópia de segurança do Azure pode ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="4b406-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="4b406-701">As cópias de segurança garantir que uma opção de recuperação em caso de Olá de qualquer falha inesperada durante a encriptação.</span><span class="sxs-lookup"><span data-stu-id="4b406-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="4b406-702">Assim que for efetuada uma cópia de segurança, Olá conjunto AzureRmVMDiskEncryptionExtension cmdlet pode ser utilizado tooencrypt gerido discos especificando Olá - skipVmBackup parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4b406-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="4b406-703">Este comando irá falhar contra uma VM baseada em disco de gerido até que foi efetuada uma cópia de segurança e se este parâmetro foi especificado.</span><span class="sxs-lookup"><span data-stu-id="4b406-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="4b406-704">Atualizar as definições de encriptação de uma VM do premium não encriptada existente</span><span class="sxs-lookup"><span data-stu-id="4b406-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="4b406-705">Utilize Olá existentes disco Azure encriptação suportada interfaces para executar a VM [cmdlets de PS, CLI ou ARM modelos] tooupdate definições de encriptação de Olá como o cliente do AAD ID/segredo, chave de encriptação da chave [KEK], chave de encriptação do BitLocker para a VM do Windows ou o frase de acesso para Definição de encriptação do etc. de VM Linux Olá atualização só é suportada para VMs por armazenamento premium não.</span><span class="sxs-lookup"><span data-stu-id="4b406-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="4b406-706">É NNOT suportada para VMs por armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="4b406-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="4b406-707">Apêndice</span><span class="sxs-lookup"><span data-stu-id="4b406-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="4b406-708">Ligar tooyour subscrição</span><span class="sxs-lookup"><span data-stu-id="4b406-708">Connect tooyour subscription</span></span>
<span data-ttu-id="4b406-709">Antes de continuar, reveja Olá *pré-requisitos* secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="4b406-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="4b406-710">Depois de assegurar que todos os pré-requisitos tiverem sido cumpridos, ligar tooyour subscrição, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b406-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="4b406-711">Iniciar uma sessão do PowerShell do Azure e inicie sessão no tooyour conta do Azure com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4b406-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="4b406-712">Se tiver várias subscrições e pretender um toouse toospecify, escreva Olá subscrições de Olá toosee da sua conta os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="4b406-713">subscrição de Olá toospecify pretende toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="4b406-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="4b406-714">tooverify que subscrição Olá configurada está correta, escreva:</span><span class="sxs-lookup"><span data-stu-id="4b406-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="4b406-715">Olá tooconfirm Azure Disk Encryption os cmdlets estão instalados, tipo:</span><span class="sxs-lookup"><span data-stu-id="4b406-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="4b406-716">Olá seguinte resultado confirma que a instalação do Azure PowerShell de encriptação de disco de Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="4b406-717">Preparar um VHD do Windows previamente encriptado</span><span class="sxs-lookup"><span data-stu-id="4b406-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="4b406-718">as secções de Olá que se seguem são necessária tooprepare um VHD do Windows previamente encriptado para a implementação de um VHD encriptado no IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="4b406-719">Utilize Olá informações tooprepare e efetuar o arranque de uma nova VM (VHD do Windows) no Azure Site Recovery ou do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="4b406-720">Atualizar grupo política tooallow TPM não para a proteção de SO</span><span class="sxs-lookup"><span data-stu-id="4b406-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="4b406-721">Configurar a definição de política de grupo do BitLocker de Olá **encriptação de unidade BitLocker**, que encontrará em **política de computador Local** > **configuração do computador**  >  **Modelos administrativos** > **componentes do Windows**.</span><span class="sxs-lookup"><span data-stu-id="4b406-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="4b406-722">Alterar esta definição demasiado**unidades do sistema operativo** > **requer autenticação adicional durante o arranque** > **permitir BitLocker sem um TPM compatível**, conforme apresentado na Olá figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b406-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="4b406-724">Instalar componentes de funcionalidades do BitLocker</span><span class="sxs-lookup"><span data-stu-id="4b406-724">Install BitLocker feature components</span></span>
<span data-ttu-id="4b406-725">Para o Windows Server 2012 ou posterior, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4b406-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="4b406-726">Para o Windows Server 2008 R2, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4b406-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="4b406-727">Preparar o volume de SO Olá para o BitLocker utilizando`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="4b406-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="4b406-728">toocompress Olá partição de SO e preparar máquina Olá para o BitLocker, executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4b406-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="4b406-729">Proteger o volume de SO Olá ao utilizar o BitLocker</span><span class="sxs-lookup"><span data-stu-id="4b406-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="4b406-730">Olá utilize [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) encriptação tooenable de comando no volume de arranque de Olá com um protetor de chave externo.</span><span class="sxs-lookup"><span data-stu-id="4b406-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="4b406-731">Também colocar chave externa de Olá (ficheiro .bek) numa unidade externa Olá ou volume.</span><span class="sxs-lookup"><span data-stu-id="4b406-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="4b406-732">Encriptação está ativada num volume de arranque do sistema de Olá após o reinício seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="4b406-733">Prepare Olá VM com um separado/recurso de dados VHD para obter a chave externa Olá utilizando o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4b406-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="4b406-734">Encriptar uma unidade de SO numa VM com Linux em execução</span><span class="sxs-lookup"><span data-stu-id="4b406-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="4b406-735">Encriptação de uma unidade de SO numa VM com Linux em execução é suportada no Olá distribuições os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="4b406-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="4b406-736">RHEL 7.2</span></span>
* <span data-ttu-id="4b406-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="4b406-737">CentOS 7.2</span></span>
* <span data-ttu-id="4b406-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="4b406-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="4b406-739">Pré-requisitos para encriptação de disco do SO</span><span class="sxs-lookup"><span data-stu-id="4b406-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="4b406-740">Olá VM tem de ser criada de imagem do Marketplace Olá no Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="4b406-741">VM do Azure com, pelo menos, 4 GB de RAM (recomendado é de tamanho 7 GB).</span><span class="sxs-lookup"><span data-stu-id="4b406-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="4b406-742">(Para RHEL e CentOS) Desative SELinux.</span><span class="sxs-lookup"><span data-stu-id="4b406-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="4b406-743">toodisable SELinux, consulte "4.4.2 criação.</span><span class="sxs-lookup"><span data-stu-id="4b406-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="4b406-744">Desativar o SELinux"Olá [Guia do administrador e utilizador SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="4b406-745">Depois de desativar SELinux, reiniciar o computador Olá VM, pelo menos, uma vez.</span><span class="sxs-lookup"><span data-stu-id="4b406-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="4b406-746">Passos</span><span class="sxs-lookup"><span data-stu-id="4b406-746">Steps</span></span>
1. <span data-ttu-id="4b406-747">Crie uma VM ao utilizar uma das distribuições de Olá especificadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4b406-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="4b406-748">A CentOS 7.2, a encriptação de disco do SO é suportada através de uma imagem especial.</span><span class="sxs-lookup"><span data-stu-id="4b406-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="4b406-749">toouse esta imagem, especifique "7.2n" como Olá SKU quando criar Olá VM:</span><span class="sxs-lookup"><span data-stu-id="4b406-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="4b406-750">Configure Olá VM de acordo com tooyour às necessidades.</span><span class="sxs-lookup"><span data-stu-id="4b406-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="4b406-751">Se pretender tooencrypt todas as unidades de Olá (SO + dados), unidades de dados de Olá necessário toobe mountable de /etc/fstab e especificados.</span><span class="sxs-lookup"><span data-stu-id="4b406-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="4b406-752">Utilize o UUID =... toospecify unidades de dados no etc/fstab em vez de especificar o nome do dispositivo Olá blocos (por exemplo, /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="4b406-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="4b406-753">Durante a encriptação, a ordem de Olá de unidades de alterações num Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="4b406-754">Se a VM depende de uma ordem específica de impedir que os dispositivos, ocorrerá uma falha toomount-las após a encriptação.</span><span class="sxs-lookup"><span data-stu-id="4b406-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="4b406-755">Terminar sessões SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="4b406-756">Olá tooencrypt SO, especifique volumeType como **todos os** ou **SO** quando que [ativar a encriptação](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="4b406-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="4b406-757">Todos os processos de espaço do utilizador que não estão em execução como `systemd` serviços devem ser desativados com um `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="4b406-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="4b406-758">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-758">Reboot hello VM.</span></span> <span data-ttu-id="4b406-759">Quando ativar a encriptação de disco de SO numa VM em execução, planeie no período de indisponibilidade VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="4b406-760">Periodicamente monitorizar o progresso de Olá de encriptação, utilizando instruções Olá no Olá [secção seguinte](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="4b406-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="4b406-761">Depois de Get-AzureRmVmDiskEncryptionStatus mostra "VMRestartPending", reinicie a VM ao iniciar sessão tooit ou utilizando o portal de Olá, PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="4b406-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="4b406-762">Antes de reiniciar, recomendamos que guarde [diagnóstico de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="4b406-763">Monitorizar o progresso de encriptação do SO</span><span class="sxs-lookup"><span data-stu-id="4b406-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="4b406-764">Pode monitorizar o progresso de encriptação de SO de três formas diferentes:</span><span class="sxs-lookup"><span data-stu-id="4b406-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="4b406-765">Olá utilize `Get-AzureRmVmDiskEncryptionStatus` cmdlet e inspecionar o campo de ProgressMessage Olá:</span><span class="sxs-lookup"><span data-stu-id="4b406-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="4b406-766">Depois de Olá VM atinge "Foi iniciada de encriptação de disco de SO", que demora cerca de 40 minutos too50 num armazenamento Premium-cópia de VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="4b406-767">Porque [emitir #388](https://github.com/Azure/WALinuxAgent/issues/388) no WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted` apresentados como `Unknown` em algumas distribuições.</span><span class="sxs-lookup"><span data-stu-id="4b406-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="4b406-768">Com WALinuxAgent versão 2.1.5 e posterior, este problema é resolvido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4b406-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="4b406-769">Se vir `Unknown` no resultado de Olá, pode verificar o estado de encriptação de disco utilizando Olá Explorador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="4b406-770">Aceda demasiado[Explorador de recursos do Azure](https://resources.azure.com/)e, em seguida, expanda esta hierarquia no painel de seleção de Olá esquerda:</span><span class="sxs-lookup"><span data-stu-id="4b406-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="4b406-771">No Olá InstanceView, desloque para baixo do Estado de encriptação de Olá toosee das suas unidades.</span><span class="sxs-lookup"><span data-stu-id="4b406-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Vista de instância VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="4b406-773">Observe [diagnóstico de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="4b406-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="4b406-774">Mensagens de Olá extensão ADE devem ter o prefixo `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="4b406-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="4b406-775">Inicie sessão toohello VM através de SSH e obter o registo de extensão de Olá de:</span><span class="sxs-lookup"><span data-stu-id="4b406-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="4b406-776">/var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="4b406-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="4b406-777">Recomendamos que não iniciar sessão toohello VM enquanto encriptação do SO estiver em curso.</span><span class="sxs-lookup"><span data-stu-id="4b406-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="4b406-778">Copie registos de Olá apenas quando hello outros dois métodos falharem.</span><span class="sxs-lookup"><span data-stu-id="4b406-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="4b406-779">Preparar um VHD de Linux previamente encriptado</span><span class="sxs-lookup"><span data-stu-id="4b406-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="4b406-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="4b406-780">Ubuntu 16</span></span>
<span data-ttu-id="4b406-781">Configure a encriptação durante a instalação de distribuição Olá, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b406-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="4b406-782">Selecione **configurar volumes encriptados** quando de partição discos Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="4b406-784">Crie uma unidade de arranque separado, que não pode ser encriptada.</span><span class="sxs-lookup"><span data-stu-id="4b406-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="4b406-785">Encriptar a unidade de raiz.</span><span class="sxs-lookup"><span data-stu-id="4b406-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="4b406-787">Forneça uma frase de acesso.</span><span class="sxs-lookup"><span data-stu-id="4b406-787">Provide a passphrase.</span></span> <span data-ttu-id="4b406-788">Este é o frase de acesso de Olá que carregar toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="4b406-790">Conclua a criação de partições.</span><span class="sxs-lookup"><span data-stu-id="4b406-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="4b406-792">Quando efetuar o arranque Olá VM e são pedidas a uma frase de acesso, utilize o frase de acesso de Olá fornecido no passo 3.</span><span class="sxs-lookup"><span data-stu-id="4b406-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="4b406-794">Preparar Olá VM para carregar no Azure com [estas instruções](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="4b406-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="4b406-795">Ainda não executada último passo do Olá (Olá desaprovisionamento VM).</span><span class="sxs-lookup"><span data-stu-id="4b406-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="4b406-796">Configure toowork de encriptação com o Azure, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b406-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="4b406-797">Crie um ficheiro em /usr/local/sbin/azure_crypt_key.sh, com conteúdo Olá Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="4b406-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="4b406-798">Preste atenção toohello KeyFileName, porque é o nome de ficheiro Olá frase de acesso utilizada pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="4b406-799">Alterar a configuração de crypt Olá no *etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="4b406-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="4b406-800">Deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="4b406-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="4b406-801">Se estiver a editar *azure_crypt_key.sh* no Windows e é copiada-tooLinux, execute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="4b406-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="4b406-802">Adicione o script de toohello permissões executável:</span><span class="sxs-lookup"><span data-stu-id="4b406-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="4b406-803">Editar */etc/initramfs-tools/modules* acrescentando linhas:</span><span class="sxs-lookup"><span data-stu-id="4b406-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="4b406-804">Executar `update-initramfs -u -k all` Olá do tooupdate Olá initramfs toomake `keyscript` entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="4b406-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="4b406-805">Agora pode desaprovisionar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4b406-805">Now you can deprovision hello VM.</span></span>

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="4b406-807">Continuar passo seguinte toohello e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="4b406-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="4b406-808">openSUSE 13.2</span></span>
<span data-ttu-id="4b406-809">encriptação de tooconfigure durante a instalação de distribuição de Olá, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="4b406-810">Quando particionar discos Olá, selecione **encriptar o grupo de Volume**e, em seguida, introduza uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="4b406-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="4b406-811">Esta é a palavra-passe de Olá que irá carregar tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![o programa de configuração openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="4b406-813">Arranque Olá VM utilizando a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="4b406-813">Boot hello VM using your password.</span></span>

 ![o programa de configuração openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="4b406-815">Preparar hello VM para carregar tooAzure ao seguir as instruções Olá [preparar uma máquina virtual SLES ou openSUSE para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="4b406-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="4b406-816">Ainda não executada último passo do Olá (Olá desaprovisionamento VM).</span><span class="sxs-lookup"><span data-stu-id="4b406-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="4b406-817">tooconfigure toowork de encriptação com o Azure, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="4b406-818">Editar Olá /etc/dracut.conf e adicionar Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="4b406-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="4b406-819">Comente estas linhas pela extremidade de Olá da Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do ficheiro:</span><span class="sxs-lookup"><span data-stu-id="4b406-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="4b406-820">Acrescente Olá linha no início Olá Olá ficheiro /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="4b406-821">E altere todas as ocorrências de:</span><span class="sxs-lookup"><span data-stu-id="4b406-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="4b406-822">para:</span><span class="sxs-lookup"><span data-stu-id="4b406-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="4b406-823">Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e o acrescentem demasiado "device de abrir LUKS #":</span><span class="sxs-lookup"><span data-stu-id="4b406-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="4b406-824">Executar `/usr/sbin/dracut -f -v` tooupdate Olá initrd.</span><span class="sxs-lookup"><span data-stu-id="4b406-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="4b406-825">Agora pode desaprovisionar Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="4b406-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="4b406-826">CentOS 7</span></span>
<span data-ttu-id="4b406-827">encriptação de tooconfigure durante a instalação de distribuição de Olá, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="4b406-828">Selecione **encriptar os meus dados** quando de partição de discos.</span><span class="sxs-lookup"><span data-stu-id="4b406-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="4b406-830">Certifique-se **encriptar** está selecionado para a partição de raiz.</span><span class="sxs-lookup"><span data-stu-id="4b406-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="4b406-832">Forneça uma frase de acesso.</span><span class="sxs-lookup"><span data-stu-id="4b406-832">Provide a passphrase.</span></span> <span data-ttu-id="4b406-833">Este é o frase de acesso de Olá que irá carregar tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="4b406-835">Quando efetuar o arranque Olá VM e são pedidas a uma frase de acesso, utilize o frase de acesso de Olá fornecido no passo 3.</span><span class="sxs-lookup"><span data-stu-id="4b406-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="4b406-837">Preparar Olá VM para carregar no Azure, utilizando instruções "CentOS 7.0 +" Olá [preparar uma máquina de virtual com base em CentOS para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="4b406-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="4b406-838">Ainda não executada último passo do Olá (Olá desaprovisionamento VM).</span><span class="sxs-lookup"><span data-stu-id="4b406-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="4b406-839">Agora pode desaprovisionar Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b406-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="4b406-840">tooconfigure toowork de encriptação com o Azure, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="4b406-841">Editar Olá /etc/dracut.conf e adicionar Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="4b406-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="4b406-842">Comente estas linhas pela extremidade de Olá da Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do ficheiro:</span><span class="sxs-lookup"><span data-stu-id="4b406-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="4b406-843">Acrescente Olá linha no início Olá Olá ficheiro /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4b406-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="4b406-844">E altere todas as ocorrências de:</span><span class="sxs-lookup"><span data-stu-id="4b406-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="4b406-845">para</span><span class="sxs-lookup"><span data-stu-id="4b406-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="4b406-846">Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e de acréscimo isto após Olá "device de abrir LUKS #":</span><span class="sxs-lookup"><span data-stu-id="4b406-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="4b406-847">Executar Olá "/ sbin/usr/dracut - f - v" tooupdate Olá initrd.</span><span class="sxs-lookup"><span data-stu-id="4b406-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="4b406-849">Carregar a conta do storage do Azure encriptada tooan VHD</span><span class="sxs-lookup"><span data-stu-id="4b406-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="4b406-850">Depois de ativar a encriptação BitLocker ou a encriptação de DM-Crypt, Olá local encriptado VHD necessidades toobe carregado tooyour conta do storage.</span><span class="sxs-lookup"><span data-stu-id="4b406-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="4b406-851">Carregar o segredo de encriptação de disco Olá para Olá previamente encriptado VM tooyour Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4b406-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="4b406-852">segredo de encriptação de disco de Olá que obteve anteriormente deve ser também carregado como um segredo no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="4b406-853">Cofre de chaves Olá necessita de encriptação de disco toohave e permissões ativadas para o cliente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b406-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="4b406-854">Segredo de encriptação de disco não encriptado com uma KEK</span><span class="sxs-lookup"><span data-stu-id="4b406-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="4b406-855">tooset segurança segredo Olá no seu Cofre de chaves, utilize [conjunto AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="4b406-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="4b406-856">Se tiver uma máquina virtual do Windows, o ficheiro de bek Olá está codificado como uma cadeia base64 e, em seguida, carregada tooyour Cofre de chaves utilizando Olá `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b406-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="4b406-857">Para Linux Olá frase de acesso está codificado como uma cadeia base64 e, em seguida, carregada toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="4b406-858">Além disso, certifique-se de que Olá etiquetas a seguir são definidas quando cria o segredo de Olá no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="4b406-859">Olá utilize `$secretUrl` no passo seguinte do Olá para [expor o disco de SO de Olá sem utilizar KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="4b406-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="4b406-860">Segredo de encriptação de disco encriptado com uma KEK</span><span class="sxs-lookup"><span data-stu-id="4b406-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="4b406-861">Antes de carregar o Cofre da chave secreta toohello Olá, opcionalmente, pode encriptá-lo utilizando uma chave de encriptação de chaves.</span><span class="sxs-lookup"><span data-stu-id="4b406-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="4b406-862">Moldagem de Olá utilize [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encriptar o segredo de Olá utilizando a chave de encriptação de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="4b406-863">Olá resultado desta operação de moldagem é uma cadeia de URL codificado em base64, que, em seguida, pode carregar como um segredo utilizando Olá [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b406-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="4b406-864">Utilize `$KeyEncryptionKey` e `$secretUrl` no passo seguinte do Olá para [expor o disco Olá SO utilizando KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="4b406-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="4b406-865">Especifique um URL secreto quando anexar um disco de SO</span><span class="sxs-lookup"><span data-stu-id="4b406-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="4b406-866">Sem utilizar um KEK</span><span class="sxs-lookup"><span data-stu-id="4b406-866">Without using a KEK</span></span>
<span data-ttu-id="4b406-867">Enquanto estiver a anexar o disco de SO de Olá, terá de toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="4b406-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="4b406-868">URL de Olá foi gerado na secção de "segredo de encriptação de disco não encriptada com uma KEK" Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="4b406-869">Utilizar um KEK</span><span class="sxs-lookup"><span data-stu-id="4b406-869">Using a KEK</span></span>
<span data-ttu-id="4b406-870">Ao anexar o disco de SO de Olá, passe `$KeyEncryptionKey` e `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="4b406-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="4b406-871">URL de Olá foi gerado na secção de "segredo de encriptação de disco não encriptada com uma KEK" Olá.</span><span class="sxs-lookup"><span data-stu-id="4b406-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="4b406-872">Transferir este guia</span><span class="sxs-lookup"><span data-stu-id="4b406-872">Download this guide</span></span>
<span data-ttu-id="4b406-873">Pode transferir este guia da Olá [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="4b406-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="4b406-874">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="4b406-874">For more information</span></span>
[<span data-ttu-id="4b406-875">Explorar a encriptação de disco do Azure com o Azure PowerShell - parte 1</span><span class="sxs-lookup"><span data-stu-id="4b406-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="4b406-876">Explorar a encriptação de disco do Azure com o Azure PowerShell - parte 2</span><span class="sxs-lookup"><span data-stu-id="4b406-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
