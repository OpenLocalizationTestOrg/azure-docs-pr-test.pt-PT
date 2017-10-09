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
# <a name="configuring-dhcpv6-for-linux-vms"></a>Configurar DHCPv6 para VMs do Linux

Algumas das imagens da máquina virtual Linux Olá no Olá Azure Marketplace não dispõe de DHCPv6 configurado por predefinição. toosupport IPv6, DHCPv6 tem de ser configurado no dentro de distribuição de SO Linux Olá que está a utilizar. Diferentes formas de configurar DHCPv6 porque utilizam diferentes pacotes de ter diversas distribuições de Linux.

> [!NOTE]
> Recentes imagens do SUSE Linux e CoreOS no Olá Azure Marketplace tem sido previamente configuradas com DHCPv6. Não existem alterações adicionais são necessárias quando utilizar essas imagens.

Este documento descreve como tooenable DHCPv6 para que a máquina virtual do Linux obtém um endereço IPv6.

> [!WARNING]
> Incorretamente editar ficheiros de configuração de rede pode fazer com toolose rede acesso tooyour VM. Recomendamos que teste as alterações de configuração nos sistemas de não produção. instruções de Olá neste artigo foi testadas em versões mais recentes do Olá das imagens de Linux Olá na Olá Azure Marketplace. Consulte a documentação de Olá para a versão específica do Linux para obter instruções mais detalhadas.

## <a name="ubuntu"></a>Ubuntu

1. Edite o ficheiro de Olá `/etc/dhcp/dhclient6.conf` e adicione Olá seguinte linha:

        timeout 10;

2. Edite configuração de rede Olá para a interface de eth0 Olá com Olá a seguinte configuração:

   * No **Ubuntu 12.04 e 14.04**, edite o ficheiro de Olá`/etc/network/interfaces.d/eth0.cfg`
   * No **Ubuntu 16.04**, edite o ficheiro de Olá`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renove o endereço IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Edite o ficheiro de Olá `/etc/dhcp/dhclient6.conf` e adicione Olá seguinte linha:

        timeout 10;

2. Edite o ficheiro de Olá `/etc/network/interfaces` e adicione Olá a seguinte configuração:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renove o endereço IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Edite o ficheiro de Olá `/etc/sysconfig/network` e adicione Olá seguinte parâmetro:

        NETWORKING_IPV6=yes

2. Edite o ficheiro de Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá seguir dois parâmetros:

        IPV6INIT=yes
        DHCPV6C=yes

3. Renove o endereço IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 & openSUSE 13

As imagens recentes SLES e openSUSE no Azure tem sido previamente configuradas com DHCPv6. Não existem alterações adicionais são necessárias quando utilizar essas imagens. Se tiver uma VM com base numa imagem SUSE anterior ou personalizada, utilize Olá os seguintes passos:

1. Instalar Olá `dhcp-client` do pacote, se necessário:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Edite o ficheiro de Olá `/etc/sysconfig/network/ifcfg-eth0` e adicione Olá seguinte parâmetro:

        DHCLIENT6_MODE='managed'

3. Renove endereço Olá IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 e openSUSE bissexto

As imagens recentes SLES e openSUSE no Azure tem sido previamente configuradas com DHCPv6. Não existem alterações adicionais são necessárias quando utilizar essas imagens. Se tiver uma VM com base numa imagem SUSE anterior ou personalizada, utilize Olá os seguintes passos:

1. Edite o ficheiro de Olá `/etc/sysconfig/network/ifcfg-eth0` e substitua este parâmetro

        #BOOTPROTO='dhcp4'

    com Olá seguinte valor:

        BOOTPROTO='dhcp'

2. Adicionar Olá seguir parâmetro demasiado`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Renove endereço Olá IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Recentes CoreOS imagens no Azure tem sido previamente configuradas com DHCPv6. Não existem alterações adicionais são necessárias quando utilizar essas imagens. Se tiver uma VM com base numa imagem de CoreOS anterior ou personalizada, utilize Olá os seguintes passos:

1. Edite o ficheiro de Olá`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Renove endereço Olá IPv6:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
