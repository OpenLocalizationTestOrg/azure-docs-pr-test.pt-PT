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
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Otimizar o débito de rede para máquinas virtuais do Azure

Máquinas virtuais do Azure (VM) tem predefinições de rede que podem ser mais otimizadas para débito de rede. Este artigo descreve como toooptimize rede débito para o Microsoft Azure Windows e VMs do Linux, incluindo as distribuições principais como Ubuntu, CentOS e Red Hat.

## <a name="windows-vm"></a>VM do Windows

Se a VM do Windows é suportada com [acelerados redes](virtual-network-create-vm-accelerated-networking.md), ativar essa funcionalidade seria configuração ideal de Olá para débito. Para todas as outras VMs do Windows, utilizar o dimensionamento do lado da receção (RSS) pode contactar um maior débito garantido que uma VM sem RSS. O RSS pode estar desativado por predefinição numa VM do Windows. Concluir Olá os seguintes passos toodetermine se RSS está ativado e tooenable-lo se está desativada.

1. Introduza Olá `Get-NetAdapterRss` toosee de comando do PowerShell se RSS está ativado para um adaptador de rede. No Olá seguinte exemplo de resultado devolvido pelo Olá `Get-NetAdapterRss`, o RSS não está ativado.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Introduza Olá comando tooenable RSS os seguintes:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    comando anterior Olá não possui uma saída. comando Olá alterar definições da NIC, a causar a perda de conectividade temporário para cerca de um minuto. É apresentada uma caixa de diálogo de Reconnecting durante a perda de conectividade Olá. Conectividade normalmente é restaurada após tentativa terceira Olá.
3. Confirme que o RSS está ativado no Olá VM introduzindo Olá `Get-NetAdapterRss` novamente o comando. Se tiver êxito, é devolvido Olá saídas de exemplo a seguir:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>VM com Linux

O RSS está sempre ativado por predefinição no VM Linux do Azure. Kernels Linux lançadas desde de Janeiro de 2017 incluem novas opções de otimização de rede que permitem o débito de rede superior uma VM com Linux tooachieve.

### <a name="ubuntu"></a>Ubuntu

Otimização da ordem tooget Olá, primeiro Atualize versão toohello suportada mais recente, a partir de Junho de 2017, que é:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Após a conclusão da atualização de Olá, introduza Olá kernel mais recente do comandos tooget Olá os seguintes:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Comando opcional:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Kernel de pré-visualização do Ubuntu do Azure
> [!WARNING]
> Esta pré-visualização de Linux do Azure pode não ter kernel Olá mesmo nível de disponibilidade e fiabilidade como imagens do Marketplace e kernels que são, em geral, a versão de disponibilidade. funcionalidade Olá não é suportada, pode ter restrita capacidades e não pode ser tão fiável como kernel do Olá predefinido. Não utilize este kernel para cargas de trabalho de produção.

Desempenho de débito significativas pode ser conseguido através da instalação Olá propostas kernel Linux do Azure. tootry este kernel, adicione esta linha too/etc/apt/sources.list

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Em seguida, execute estes comandos como raiz.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Otimização da ordem tooget Olá, primeiro Atualize versão toohello suportada mais recente, a partir de Julho de 2017, que é:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Após a conclusão da atualização de Olá, instalação hello mais recentes serviços de integração de Linux (LIS).
Otimização de débito Olá está a ser LIS, começando 4.2.2-2. Introduza Olá comandos tooinstall LIS os seguintes:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Otimização da ordem tooget Olá, primeiro Atualize versão toohello suportada mais recente, a partir de Julho de 2017, que é:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Após a conclusão da atualização de Olá, instalação hello mais recentes serviços de integração de Linux (LIS).
Otimização de débito Olá está a ser LIS, começando 4.2. Introduza Olá toodownload de comandos a seguir e instalar o LIS:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Saiba mais sobre 4.2 de versão de serviços de integração Linux para Hyper-V através da visualização Olá [página de transferência](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Passos seguintes
* Agora que hello VM é otimizada, consulte o resultado de Olá com [testar VM do Azure de largura de banda/débito](virtual-network-bandwidth-testing.md) para o seu cenário.
* Saiba mais com [Azure Virtual Network perguntas mais frequentes sobre (FAQ)](virtual-networks-faq.md)
