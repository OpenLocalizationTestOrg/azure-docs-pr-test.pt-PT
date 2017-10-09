---
title: infraestrutura aaaAzure nomenclatura diretrizes - Windows | Microsoft Docs
description: "Saiba mais sobre Olá chaves design e implementação diretrizes de nomenclatura nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="f734d-103">Infraestrutura do Azure diretrizes de nomenclatura para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="f734d-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="f734d-104">Este artigo foca-se em compreender como as convenções de nomenclatura tooapproach para todos os seus toobuild de recursos do Azure vários a lógica e facilmente identificável conjunto de recursos em todo o ambiente.</span><span class="sxs-lookup"><span data-stu-id="f734d-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="f734d-105">Diretrizes de implementação para as convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="f734d-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="f734d-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="f734d-106">Decisions:</span></span>

* <span data-ttu-id="f734d-107">Quais são as convenções de nomenclatura para recursos do Azure?</span><span class="sxs-lookup"><span data-stu-id="f734d-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="f734d-108">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="f734d-108">Tasks:</span></span>

* <span data-ttu-id="f734d-109">Defina Olá affixes toouse entre a consistência de toomaintain de recursos.</span><span class="sxs-lookup"><span data-stu-id="f734d-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="f734d-110">Defina a conta de armazenamento nomes fornecidos Olá requisito para os mesmos toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f734d-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="f734d-111">Olá documento toobe Convenção de nomenclatura utilizado e distribuir tooall entidades envolvidas tooensure consistência entre implementações.</span><span class="sxs-lookup"><span data-stu-id="f734d-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="f734d-112">Convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="f734d-112">Naming conventions</span></span>
<span data-ttu-id="f734d-113">Deve ter uma convenção de nomenclatura boa no local antes de criar nada no Azure.</span><span class="sxs-lookup"><span data-stu-id="f734d-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="f734d-114">Uma convenção de nomenclatura garante que todos os recursos de Olá têm um nome previsível, que ajuda-o fardo administrativo inferior do Olá, associado à gestão esses recursos.</span><span class="sxs-lookup"><span data-stu-id="f734d-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="f734d-115">Poderá escolher toofollow um conjunto específico de convenções de nomenclatura definidos para toda a organização ou para uma subscrição do Azure específica ou a conta.</span><span class="sxs-lookup"><span data-stu-id="f734d-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="f734d-116">Embora seja mais fácil para os indivíduos dentro das regras implícita de organizações tooestablish ao trabalhar com recursos do Azure, quando precisa de uma equipa toowork num projeto no Azure, esse modelo não dimensiona bem.</span><span class="sxs-lookup"><span data-stu-id="f734d-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, when a team needs toowork on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="f734d-117">Aceita num conjunto de convenções de nomenclatura adiantado.</span><span class="sxs-lookup"><span data-stu-id="f734d-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="f734d-118">Existem algumas considerações sobre as convenções de nomenclatura que cortar entre este conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="f734d-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="f734d-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="f734d-119">Affixes</span></span>
<span data-ttu-id="f734d-120">Como ver toodefine uma convenção de nomenclatura, uma decisão vem se affix Olá é:</span><span class="sxs-lookup"><span data-stu-id="f734d-120">As you look toodefine a naming convention, one decision comes whether hello affix is at:</span></span>

* <span data-ttu-id="f734d-121">início de Olá do nome de Olá (prefixo)</span><span class="sxs-lookup"><span data-stu-id="f734d-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="f734d-122">fim de Olá do nome de Olá (sufixo)</span><span class="sxs-lookup"><span data-stu-id="f734d-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="f734d-123">Por exemplo, seguem-se dois nomes possíveis para um grupo de recursos com Olá `rg` affix:</span><span class="sxs-lookup"><span data-stu-id="f734d-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="f734d-124">RG-WebApp (prefixo)</span><span class="sxs-lookup"><span data-stu-id="f734d-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="f734d-125">WebApp-Rg (sufixo)</span><span class="sxs-lookup"><span data-stu-id="f734d-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="f734d-126">Affixes podem referir-se toodifferent aspetos que descrevem a recursos específicos Olá.</span><span class="sxs-lookup"><span data-stu-id="f734d-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="f734d-127">Olá tabela seguinte mostra alguns exemplos normalmente utilizados.</span><span class="sxs-lookup"><span data-stu-id="f734d-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="f734d-128">Aspeto</span><span class="sxs-lookup"><span data-stu-id="f734d-128">Aspect</span></span> | <span data-ttu-id="f734d-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f734d-129">Examples</span></span> | <span data-ttu-id="f734d-130">Notas</span><span class="sxs-lookup"><span data-stu-id="f734d-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f734d-131">Ambiente</span><span class="sxs-lookup"><span data-stu-id="f734d-131">Environment</span></span> |<span data-ttu-id="f734d-132">Dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="f734d-132">dev, stg, prod</span></span> |<span data-ttu-id="f734d-133">Consoante o objetivo de Olá e o nome de cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="f734d-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="f734d-134">Localização</span><span class="sxs-lookup"><span data-stu-id="f734d-134">Location</span></span> |<span data-ttu-id="f734d-135">usw (EUA oeste), utilize (EUA Leste 2)</span><span class="sxs-lookup"><span data-stu-id="f734d-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="f734d-136">Consoante a região de Olá Olá datacenter ou a região de Olá da organização Olá do.</span><span class="sxs-lookup"><span data-stu-id="f734d-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="f734d-137">Componente do Azure, serviço ou produto</span><span class="sxs-lookup"><span data-stu-id="f734d-137">Azure component, service, or product</span></span> |<span data-ttu-id="f734d-138">RG para o grupo de recursos, VNet para a rede virtual</span><span class="sxs-lookup"><span data-stu-id="f734d-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="f734d-139">Consoante o produto de Olá para que Olá recurso fornece suporte.</span><span class="sxs-lookup"><span data-stu-id="f734d-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="f734d-140">Função</span><span class="sxs-lookup"><span data-stu-id="f734d-140">Role</span></span> |<span data-ttu-id="f734d-141">SQL Server, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="f734d-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="f734d-142">Dependendo da função de Olá da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="f734d-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="f734d-143">Instância</span><span class="sxs-lookup"><span data-stu-id="f734d-143">Instance</span></span> |<span data-ttu-id="f734d-144">01, 02, 03, etc.</span><span class="sxs-lookup"><span data-stu-id="f734d-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="f734d-145">Para os recursos que tem mais do que uma instância.</span><span class="sxs-lookup"><span data-stu-id="f734d-145">For resources that have more than one instance.</span></span> <span data-ttu-id="f734d-146">Por exemplo, com balanceamento de carga servidores web num serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="f734d-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="f734d-147">Ao estabelecer as convenções de nomenclatura, certifique-se de que estes claramente que affixes toouse para cada tipo de recurso e, na qual posição (sufixo de vs prefixo).</span><span class="sxs-lookup"><span data-stu-id="f734d-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="f734d-148">datas</span><span class="sxs-lookup"><span data-stu-id="f734d-148">Dates</span></span>
<span data-ttu-id="f734d-149">É, frequentemente, data de Olá toodetermine importante da criação do nome de Olá de um recurso.</span><span class="sxs-lookup"><span data-stu-id="f734d-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="f734d-150">Recomendamos que o formato de data do Olá AAAAMMDD.</span><span class="sxs-lookup"><span data-stu-id="f734d-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="f734d-151">Este formato garante que não só data completa Olá é registada, mas também que dois recursos cujos nomes só diferem data Olá é ordenada alfabeticamente e chronologically em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f734d-151">This format ensures that not only hello full date is recorded, but also that two resources whose names differ only on hello date is sorted alphabetically and chronologically at hello same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="f734d-152">Recursos de atribuição de nomes</span><span class="sxs-lookup"><span data-stu-id="f734d-152">Naming resources</span></span>
<span data-ttu-id="f734d-153">Defina cada tipo de recurso na Convenção de nomenclatura Olá, que deve ter regras que definem como tooassign os nomes de recursos de tooeach que é criado.</span><span class="sxs-lookup"><span data-stu-id="f734d-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="f734d-154">Estas regras devem ser aplicada tooall tipos de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f734d-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="f734d-155">Subscrições</span><span class="sxs-lookup"><span data-stu-id="f734d-155">Subscriptions</span></span>
* <span data-ttu-id="f734d-156">Contas</span><span class="sxs-lookup"><span data-stu-id="f734d-156">Accounts</span></span>
* <span data-ttu-id="f734d-157">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f734d-157">Storage accounts</span></span>
* <span data-ttu-id="f734d-158">Redes virtuais</span><span class="sxs-lookup"><span data-stu-id="f734d-158">Virtual networks</span></span>
* <span data-ttu-id="f734d-159">Sub-redes</span><span class="sxs-lookup"><span data-stu-id="f734d-159">Subnets</span></span>
* <span data-ttu-id="f734d-160">Conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="f734d-160">Availability sets</span></span>
* <span data-ttu-id="f734d-161">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="f734d-161">Resource groups</span></span>
* <span data-ttu-id="f734d-162">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f734d-162">Virtual machines</span></span>
* <span data-ttu-id="f734d-163">Pontos Finais</span><span class="sxs-lookup"><span data-stu-id="f734d-163">Endpoints</span></span>
* <span data-ttu-id="f734d-164">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f734d-164">Network security groups</span></span>
* <span data-ttu-id="f734d-165">Funções</span><span class="sxs-lookup"><span data-stu-id="f734d-165">Roles</span></span>

<span data-ttu-id="f734d-166">tooensure Olá nome fornece suficiente recursos toowhich do toodetermine de informações refere-se, deverá utilizar nomes descritivos.</span><span class="sxs-lookup"><span data-stu-id="f734d-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="f734d-167">Nomes de computador</span><span class="sxs-lookup"><span data-stu-id="f734d-167">Computer names</span></span>
<span data-ttu-id="f734d-168">Quando cria uma máquina virtual (VM), o Microsoft Azure requer um nome de VM de cópia de segurança too15 carateres que é utilizado Olá no nome de recurso.</span><span class="sxs-lookup"><span data-stu-id="f734d-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up too15 characters which is used for hello resource name.</span></span> <span data-ttu-id="f734d-169">Azure utiliza Olá o mesmo nome para o sistema de operativo Olá instalado no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f734d-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="f734d-170">No entanto, estes nomes poderá não sempre ser Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="f734d-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="f734d-171">No caso de uma VM é criada a partir de um ficheiro de imagem VHD que já contém um sistema operativo, nome da VM Olá no Azure pode ser diferente do Olá nome de computador do sistema operativo da VM.</span><span class="sxs-lookup"><span data-stu-id="f734d-171">In case a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="f734d-172">Esta situação pode adicionar um grau de gestão de tooVM dificuldade em, que, por conseguinte, não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="f734d-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="f734d-173">Atribua Olá Olá de recurso de VM do Azure mesmo nome como nome do computador Olá que atribuir o sistema operativo toohello essa VM.</span><span class="sxs-lookup"><span data-stu-id="f734d-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="f734d-174">Recomendamos que esse nome de VM do Azure Olá é Olá igual Olá subjacente nome de computador do sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f734d-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="f734d-175">Nomes das contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f734d-175">Storage account names</span></span>
<span data-ttu-id="f734d-176">Esta secção não se aplica demasiado[Azure geridos discos](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), uma vez que não crie uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="f734d-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="f734d-177">Para discos não geridos, as contas de armazenamento têm regras especiais que rege os respetivos nomes.</span><span class="sxs-lookup"><span data-stu-id="f734d-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="f734d-178">Pode utilizar apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="f734d-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="f734d-179">Para obter mais informações, consulte [criar uma conta de armazenamento](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f734d-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="f734d-180">Além disso, o nome de conta do storage Olá, juntamente com core.windows.net, deve ser um nome DNS globalmente válido e exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f734d-180">Additionally, hello storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="f734d-181">Por exemplo, se a conta de armazenamento Olá for chamada mystorageaccount, hello seguintes nomes de DNS resultantes devem ser exclusivos:</span><span class="sxs-lookup"><span data-stu-id="f734d-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="f734d-182">mystorageaccount.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="f734d-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="f734d-183">mystorageaccount.TABLE.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="f734d-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="f734d-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="f734d-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="f734d-185">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f734d-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

