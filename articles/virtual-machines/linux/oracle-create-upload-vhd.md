---
title: aaaCreate e carregar um VHD do Oracle Linux | Microsoft Docs
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contenha um sistema de operativo Oracle Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Preparar uma máquina virtual do Oracle Linux para o Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que já tem instalado um disco de rígido virtual do Oracle Linux sistema operativo tooa. Várias ferramentas existem toocreate os ficheiros. vhd, por exemplo uma solução de virtualização, tais como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Notas de instalação do Oracle Linux
* Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.
* Kernel compatível do Red Hat do Oracle e os respetivos UEK3 (Unbreakable Enterprise Kernel) são ambas suportadas no Hyper-V e do Azure. Para obter os melhores resultados, ser tooupdate se toohello mais recente kernel ao preparar o VHD do Oracle Linux.
* UEK2 do Oracle não é suportado no Hyper-V e o Azure, não inclua controladores Olá necessário.
* formato VHDX Olá não é suportado no Azure, apenas **fixo VHD**.  Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá convert-vhd cmdlet.
* Ao instalar o sistema de Linux Olá é recomendado que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos). Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco do SO alguma vez necessidades toobe ligado tooanother VM para resolução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados se preferencial.
* NUMA não é suportada para tamanhos de VM maiores devido a erros de tooa nas versões anteriores de kernel do Linux ao 2.6.37. Isto emitir principalmente os impactos distribuições utilizando Olá Red montante kernel Hat 2.6.32. Instalação manual do agente Linux do Azure de Olá (waagent) desativará automaticamente na configuração de GRUB Olá para kernel do Olá Linux. Podem encontrar mais informações sobre esta nos passos Olá abaixo.
* Configure uma partição de comutação em disco do SO Olá. agente do Linux Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.  Podem encontrar mais informações sobre esta nos passos Olá abaixo.
* Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.
* Certifique-se de que Olá `Addons` repositório está ativado. Edite o ficheiro de Olá `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha de Olá `enabled=0` demasiado`enabled=1` em **[ol6_addons]** ou **[ol7_addons]** deste ficheiro.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4 +
Tem de concluir os passos de configuração específicos no sistema de operativo Olá para Olá toorun de máquina virtual no Azure.

1. No painel de centro de Olá do Gestor de Hyper-V, selecione a máquina virtual de Olá.
2. Clique em **Connect** janela de Olá tooopen para a máquina virtual de Olá.
3. Desinstale NetworkManager executando Olá os seguintes comandos:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Nota:** se pacote Olá já não estiver instalado, este comando irá falhar com uma mensagem de erro. Isto é esperado.
4. Crie um ficheiro denominado **rede** no Olá `/etc/sysconfig/` diretório que contém Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Crie um ficheiro denominado **ifcfg eth0** no Olá `/etc/sysconfig/network-scripts/` diretório que contém Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:
   
        # chkconfig network on
8. Instale o python pyasn1 executando Olá os seguintes comandos:
   
        # sudo yum install python-pyasn1
9. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo neste abrir "/ boot/grub/menu.lst" num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. Este procedimento desactivará NUMA devido a erros de tooa nas kernel compatível do Red Hat do Oracle.
   
   Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
   Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.
   
   Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.
10. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.  Isto é normalmente predefinido Olá.
11. Instale Olá agente Linux do Azure executando Olá os seguintes comandos. a versão mais recente Olá é 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Tenha em atenção que instalar pacote de WALinuxAgent Olá removerá Olá NetworkManager e pacotes de NetworkManager gnome se estes não foram já removidas conforme descrito no passo 2.
12. Não crie o espaço de comutação em disco do SO Olá.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure. Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada. Depois de instalar Olá agente Linux do Azure (consulte o passo anterior), modifique Olá adequadamente os seguintes parâmetros /etc/waagent.conf:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. Clique em **ação -> encerrar baixo** no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0 +
**Alterações no Oracle Linux 7**

Preparar uma máquina virtual do Oracle Linux 7 para o Azure é muito semelhante tooOracle Linux 6, no entanto, existem várias diferenças importantes vale a pena realçar:

* Kernel compatível do Red Hat Olá e UEK3 do Oracle são suportadas no Azure.  kernel de UEK3 Olá é recomendada.
* Olá NetworkManager do pacote já não está em conflito com o agente do Olá Linux do Azure. Este pacote é instalado por predefinição e recomendamos que não é removida.
* GRUB2 agora ser utilizada como Olá bootloader predefinido, para que o procedimento de Olá para editar os parâmetros de kernel foi alterada (ver abaixo).
* XFS é agora o sistema de ficheiros Olá predefinido. sistema de ficheiros de ext4 Olá ainda pode ser utilizado se assim o desejar.

**Passos de configuração**

1. No Gestor de Hyper-V, selecione a máquina virtual de Olá.
2. Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.
3. Crie um ficheiro denominado **rede** no Olá `/etc/sysconfig/` diretório que contém Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Crie um ficheiro denominado **ifcfg eth0** no Olá `/etc/sysconfig/network-scripts/` diretório que contém Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:
   
        # sudo chkconfig network on
7. Instale o pacote do python pyasn1 de Olá executando Olá os seguintes comandos:
   
        # sudo yum install python-pyasn1
8. Executar Olá os seguintes comandos tooclear Olá atual yum metadados e instalar quaisquer atualizações:
   
        # sudo yum clean all
        # sudo yum -y update
9. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo neste abrir "/ predefinido/etc/grub" no Olá de editor e edição de texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. É também desativa Olá novo OEL 7 convenções de nomenclatura para NICs. Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:
   
       rhgb quiet crashkernel=auto
   
   Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.
   
   Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.
10. Quando tiver terminado edição "/ predefinido/etc/grub" por acima, execute Olá configuração do comando toorebuild Olá grub os seguintes:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.  Isto é normalmente predefinido Olá.
12. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Não crie o espaço de comutação em disco do SO Olá.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure. Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada. Depois de instalar Olá agente Linux do Azure (consulte o passo anterior Olá), modifique Olá adequadamente os seguintes parâmetros /etc/waagent.conf:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Clique em **ação -> encerrar baixo** no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Passos seguintes
Está agora pronto toouse as Oracle Linux VHD toocreate novas máquinas virtuais no Azure. Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

