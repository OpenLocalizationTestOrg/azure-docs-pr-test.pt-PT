---
title: "débito de rede VM aaaOptimize | Microsoft Docs"
description: "Saiba como o débito de rede de toooptimize máquina virtual do Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="77ffd-103">Otimizar o débito de rede para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="77ffd-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="77ffd-104">Máquinas virtuais do Azure (VM) tem predefinições de rede que podem ser mais otimizadas para débito de rede.</span><span class="sxs-lookup"><span data-stu-id="77ffd-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="77ffd-105">Este artigo descreve como toooptimize rede débito para o Microsoft Azure Windows e VMs do Linux, incluindo as distribuições principais como Ubuntu, CentOS e Red Hat.</span><span class="sxs-lookup"><span data-stu-id="77ffd-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="77ffd-106">VM do Windows</span><span class="sxs-lookup"><span data-stu-id="77ffd-106">Windows VM</span></span>

<span data-ttu-id="77ffd-107">Se a VM do Windows é suportada com [acelerados redes](virtual-network-create-vm-accelerated-networking.md), ativar essa funcionalidade seria configuração ideal de Olá para débito.</span><span class="sxs-lookup"><span data-stu-id="77ffd-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="77ffd-108">Para todas as outras VMs do Windows, utilizar o dimensionamento do lado da receção (RSS) pode contactar um maior débito garantido que uma VM sem RSS.</span><span class="sxs-lookup"><span data-stu-id="77ffd-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="77ffd-109">O RSS pode estar desativado por predefinição numa VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="77ffd-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="77ffd-110">Concluir Olá os seguintes passos toodetermine se RSS está ativado e tooenable-lo se está desativada.</span><span class="sxs-lookup"><span data-stu-id="77ffd-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="77ffd-111">Introduza Olá `Get-NetAdapterRss` toosee de comando do PowerShell se RSS está ativado para um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="77ffd-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="77ffd-112">No Olá seguinte exemplo de resultado devolvido pelo Olá `Get-NetAdapterRss`, o RSS não está ativado.</span><span class="sxs-lookup"><span data-stu-id="77ffd-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="77ffd-113">Introduza Olá comando tooenable RSS os seguintes:</span><span class="sxs-lookup"><span data-stu-id="77ffd-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="77ffd-114">comando anterior Olá não possui uma saída.</span><span class="sxs-lookup"><span data-stu-id="77ffd-114">hello previous command does not have an output.</span></span> <span data-ttu-id="77ffd-115">comando Olá alterar definições da NIC, a causar a perda de conectividade temporário para cerca de um minuto.</span><span class="sxs-lookup"><span data-stu-id="77ffd-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="77ffd-116">É apresentada uma caixa de diálogo de Reconnecting durante a perda de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="77ffd-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="77ffd-117">Conectividade normalmente é restaurada após tentativa terceira Olá.</span><span class="sxs-lookup"><span data-stu-id="77ffd-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="77ffd-118">Confirme que o RSS está ativado no Olá VM introduzindo Olá `Get-NetAdapterRss` novamente o comando.</span><span class="sxs-lookup"><span data-stu-id="77ffd-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="77ffd-119">Se tiver êxito, é devolvido Olá saídas de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="77ffd-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="77ffd-120">VM com Linux</span><span class="sxs-lookup"><span data-stu-id="77ffd-120">Linux VM</span></span>

<span data-ttu-id="77ffd-121">O RSS está sempre ativado por predefinição no VM Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ffd-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="77ffd-122">Kernels Linux lançadas desde de Janeiro de 2017 incluem novas opções de otimização de rede que permitem o débito de rede superior uma VM com Linux tooachieve.</span><span class="sxs-lookup"><span data-stu-id="77ffd-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="77ffd-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="77ffd-123">Ubuntu</span></span>

<span data-ttu-id="77ffd-124">Otimização da ordem tooget Olá, primeiro Atualize versão toohello suportada mais recente, a partir de Junho de 2017, que é:</span><span class="sxs-lookup"><span data-stu-id="77ffd-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="77ffd-125">Após a conclusão da atualização de Olá, introduza Olá kernel mais recente do comandos tooget Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="77ffd-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="77ffd-126">Comando opcional:</span><span class="sxs-lookup"><span data-stu-id="77ffd-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="77ffd-127">Kernel de pré-visualização do Ubuntu do Azure</span><span class="sxs-lookup"><span data-stu-id="77ffd-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="77ffd-128">Esta pré-visualização de Linux do Azure pode não ter kernel Olá mesmo nível de disponibilidade e fiabilidade como imagens do Marketplace e kernels que são, em geral, a versão de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="77ffd-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="77ffd-129">funcionalidade Olá não é suportada, pode ter restrita capacidades e não pode ser tão fiável como kernel do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="77ffd-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="77ffd-130">Não utilize este kernel para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="77ffd-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="77ffd-131">Desempenho de débito significativas pode ser conseguido através da instalação Olá propostas kernel Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ffd-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="77ffd-132">tootry este kernel, adicione esta linha too/etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="77ffd-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="77ffd-133">Em seguida, execute estes comandos como raiz.</span><span class="sxs-lookup"><span data-stu-id="77ffd-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="77ffd-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="77ffd-134">CentOS</span></span>

<span data-ttu-id="77ffd-135">Otimização da ordem tooget Olá, primeiro Atualize versão toohello suportada mais recente, a partir de Julho de 2017, que é:</span><span class="sxs-lookup"><span data-stu-id="77ffd-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="77ffd-136">Após a conclusão da atualização de Olá, instalação hello mais recentes serviços de integração de Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="77ffd-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="77ffd-137">Otimização de débito Olá está a ser LIS, começando 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="77ffd-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="77ffd-138">Introduza Olá comandos tooinstall LIS os seguintes:</span><span class="sxs-lookup"><span data-stu-id="77ffd-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="77ffd-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="77ffd-139">Red Hat</span></span>

<span data-ttu-id="77ffd-140">Otimização da ordem tooget Olá, primeiro Atualize versão toohello suportada mais recente, a partir de Julho de 2017, que é:</span><span class="sxs-lookup"><span data-stu-id="77ffd-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="77ffd-141">Após a conclusão da atualização de Olá, instalação hello mais recentes serviços de integração de Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="77ffd-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="77ffd-142">Otimização de débito Olá está a ser LIS, começando 4.2.</span><span class="sxs-lookup"><span data-stu-id="77ffd-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="77ffd-143">Introduza Olá toodownload de comandos a seguir e instalar o LIS:</span><span class="sxs-lookup"><span data-stu-id="77ffd-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="77ffd-144">Saiba mais sobre 4.2 de versão de serviços de integração Linux para Hyper-V através da visualização Olá [página de transferência](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="77ffd-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="77ffd-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="77ffd-145">Next steps</span></span>
* <span data-ttu-id="77ffd-146">Agora que hello VM é otimizada, consulte o resultado de Olá com [testar VM do Azure de largura de banda/débito](virtual-network-bandwidth-testing.md) para o seu cenário.</span><span class="sxs-lookup"><span data-stu-id="77ffd-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="77ffd-147">Saiba mais com [Azure Virtual Network perguntas mais frequentes sobre (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="77ffd-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
