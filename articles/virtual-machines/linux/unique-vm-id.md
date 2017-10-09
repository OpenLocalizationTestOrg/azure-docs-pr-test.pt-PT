---
title: aaaGet um ID de VM do Linux do Azure | Microsoft Docs
description: "Descreve como tooget e utilizar um único de VM do Azure Linux ID."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="f7bd9-103">Aceder e utilizar ID exclusivo da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="f7bd9-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="f7bd9-104">ID exclusivo de VM do Azure é um identificador de 128bits codificado armazenados em GUID do SMBIOS do todas as do Azure IaaS VMS e atualmente pode ser lidos utilizando comandos de BIOS da plataforma.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="f7bd9-105">ID exclusivo de VM do Azure é uma propriedade só de leitura.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="f7bd9-106">ID exclusivo de VM do Azure não mudará após encerramento de reinício (está a ser planeada não planeada), iniciar/parar anula a alocação, autorrecuperação do serviço ou restaure no local.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="f7bd9-107">No entanto, se Olá VM é um instantâneo e copiado toocreate uma nova instância, o novo ID de VM do Azure está configurado.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="f7bd9-108">Se tiver VMs mais antigas, criadas e, em execução, uma vez que esta nova funcionalidade foi implementada (18 de Setembro de 2014), reinicie o seu tooautomatically VM obter um ID exclusivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="f7bd9-109">tooaccess Azure VM um ID exclusivo do dentro Olá VM:</span><span class="sxs-lookup"><span data-stu-id="f7bd9-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="f7bd9-110">Criar uma VM</span><span class="sxs-lookup"><span data-stu-id="f7bd9-110">Create a VM</span></span>
<span data-ttu-id="f7bd9-111">Para obter mais informações, consulte [criar uma Máquina Virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f7bd9-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="f7bd9-112">Ligar toohello VM</span><span class="sxs-lookup"><span data-stu-id="f7bd9-112">Connect toohello VM</span></span>
<span data-ttu-id="f7bd9-113">Para obter mais informações, consulte [SSH do Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f7bd9-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="f7bd9-114">ID exclusivo de VM de consulta</span><span class="sxs-lookup"><span data-stu-id="f7bd9-114">Query VM Unique ID</span></span>
<span data-ttu-id="f7bd9-115">Comando (exemplo utiliza **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="f7bd9-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="f7bd9-116">Exemplo esperado resultados:</span><span class="sxs-lookup"><span data-stu-id="f7bd9-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="f7bd9-117">Devido a tooBig bit Endian ordenação, hello real ID exclusivo da VM neste caso, serão:</span><span class="sxs-lookup"><span data-stu-id="f7bd9-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="f7bd9-118">ID exclusivo de VM do Azure pode ser utilizado em cenários diferentes se Olá VM está em execução no Azure ou no local e pode ajudar os seus requisitos de controlo de licenciamento, relatórios ou gerais que pode ter de implementações do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="f7bd9-119">Muitos fornecedores independentes de software de criação de aplicações e certificá-las no Azure podem exigir tooidentify uma VM do Azure ao longo do respetivo ciclo de vida e tootell se Olá VM está em execução no Azure, no local ou outros fornecedores de nuvem.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="f7bd9-120">Este identificador de plataforma por exemplo pode ajudar a detetar se o software de Olá está devidamente licenciado ou ajudar toocorrelate qualquer origem de tooits de dados VM, tais como tooassist sobre a configuração de métricas de direito de Olá para plataforma direita Olá e tootrack e correlacionar estas métricas entre outras utilizações.</span><span class="sxs-lookup"><span data-stu-id="f7bd9-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

