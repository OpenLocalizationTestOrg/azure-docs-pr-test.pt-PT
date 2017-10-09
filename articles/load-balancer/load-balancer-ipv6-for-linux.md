---
title: aaaConfiguring DHCPv6 para VMs com Linux | Microsoft Docs
description: Como tooconfigure DHCPv6 para VMs com Linux.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, o Balanceador de carga do azure, pilha dupla, ip público, ipv6 nativo, móveis, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="97ddf-104">Configurar DHCPv6 para VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="97ddf-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="97ddf-105">Algumas das imagens da máquina virtual Linux Olá no Olá Azure Marketplace não dispõe de DHCPv6 configurado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="97ddf-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="97ddf-106">toosupport IPv6, DHCPv6 tem de ser configurado no dentro de distribuição de SO Linux Olá que está a utilizar.</span><span class="sxs-lookup"><span data-stu-id="97ddf-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="97ddf-107">Diferentes formas de configurar DHCPv6 porque utilizam diferentes pacotes de ter diversas distribuições de Linux.</span><span class="sxs-lookup"><span data-stu-id="97ddf-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="97ddf-108">Recentes imagens do SUSE Linux e CoreOS no Olá Azure Marketplace tem sido previamente configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="97ddf-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="97ddf-109">Não existem alterações adicionais são necessárias quando utilizar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="97ddf-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="97ddf-110">Este documento descreve como tooenable DHCPv6 para que a máquina virtual do Linux obtém um endereço IPv6.</span><span class="sxs-lookup"><span data-stu-id="97ddf-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="97ddf-111">Incorretamente editar ficheiros de configuração de rede pode fazer com toolose rede acesso tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="97ddf-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="97ddf-112">Recomendamos que teste as alterações de configuração nos sistemas de não produção.</span><span class="sxs-lookup"><span data-stu-id="97ddf-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="97ddf-113">instruções de Olá neste artigo foi testadas em versões mais recentes do Olá das imagens de Linux Olá na Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="97ddf-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="97ddf-114">Consulte a documentação de Olá para a versão específica do Linux para obter instruções mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="97ddf-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="97ddf-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="97ddf-115">Ubuntu</span></span>

1. <span data-ttu-id="97ddf-116">Edite o ficheiro de Olá `/etc/dhcp/dhclient6.conf` e adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="97ddf-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="97ddf-117">Edite configuração de rede Olá para a interface de eth0 Olá com Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="97ddf-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="97ddf-118">No **Ubuntu 12.04 e 14.04**, edite o ficheiro de Olá`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="97ddf-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="97ddf-119">No **Ubuntu 16.04**, edite o ficheiro de Olá`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="97ddf-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="97ddf-120">Renove o endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="97ddf-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="97ddf-121">Debian</span><span class="sxs-lookup"><span data-stu-id="97ddf-121">Debian</span></span>

1. <span data-ttu-id="97ddf-122">Edite o ficheiro de Olá `/etc/dhcp/dhclient6.conf` e adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="97ddf-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="97ddf-123">Edite o ficheiro de Olá `/etc/network/interfaces` e adicione Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="97ddf-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="97ddf-124">Renove o endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="97ddf-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="97ddf-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="97ddf-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="97ddf-126">Edite o ficheiro de Olá `/etc/sysconfig/network` e adicione Olá seguinte parâmetro:</span><span class="sxs-lookup"><span data-stu-id="97ddf-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="97ddf-127">Edite o ficheiro de Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá seguir dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="97ddf-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="97ddf-128">Renove o endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="97ddf-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="97ddf-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="97ddf-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="97ddf-130">As imagens recentes SLES e openSUSE no Azure tem sido previamente configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="97ddf-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="97ddf-131">Não existem alterações adicionais são necessárias quando utilizar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="97ddf-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="97ddf-132">Se tiver uma VM com base numa imagem SUSE anterior ou personalizada, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="97ddf-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="97ddf-133">Instalar Olá `dhcp-client` do pacote, se necessário:</span><span class="sxs-lookup"><span data-stu-id="97ddf-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="97ddf-134">Edite o ficheiro de Olá `/etc/sysconfig/network/ifcfg-eth0` e adicione Olá seguinte parâmetro:</span><span class="sxs-lookup"><span data-stu-id="97ddf-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="97ddf-135">Renove endereço Olá IPv6:</span><span class="sxs-lookup"><span data-stu-id="97ddf-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="97ddf-136">SLES 12 e openSUSE bissexto</span><span class="sxs-lookup"><span data-stu-id="97ddf-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="97ddf-137">As imagens recentes SLES e openSUSE no Azure tem sido previamente configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="97ddf-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="97ddf-138">Não existem alterações adicionais são necessárias quando utilizar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="97ddf-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="97ddf-139">Se tiver uma VM com base numa imagem SUSE anterior ou personalizada, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="97ddf-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="97ddf-140">Edite o ficheiro de Olá `/etc/sysconfig/network/ifcfg-eth0` e substitua este parâmetro</span><span class="sxs-lookup"><span data-stu-id="97ddf-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="97ddf-141">com Olá seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="97ddf-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="97ddf-142">Adicionar Olá seguir parâmetro demasiado`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="97ddf-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="97ddf-143">Renove endereço Olá IPv6:</span><span class="sxs-lookup"><span data-stu-id="97ddf-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="97ddf-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="97ddf-144">CoreOS</span></span>

<span data-ttu-id="97ddf-145">Recentes CoreOS imagens no Azure tem sido previamente configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="97ddf-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="97ddf-146">Não existem alterações adicionais são necessárias quando utilizar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="97ddf-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="97ddf-147">Se tiver uma VM com base numa imagem de CoreOS anterior ou personalizada, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="97ddf-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="97ddf-148">Edite o ficheiro de Olá`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="97ddf-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="97ddf-149">Renove endereço Olá IPv6:</span><span class="sxs-lookup"><span data-stu-id="97ddf-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
