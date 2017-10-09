---
title: aaaCreate e carregar um VHD de Linux CentOS baseado no Azure
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operativo baseado em CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Preparar uma máquina virtual baseada em CentOS para o Azure
* [Preparar uma máquina de virtual do CentOS 6. x para o Azure](#centos-6x)
* [Preparar uma máquina virtual do CentOS 7.0 + Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que já tem instalado um CentOS (ou semelhante derivativo) Linux sistema operativo tooa disco virtual. Várias ferramentas existem toocreate os ficheiros. vhd, por exemplo uma solução de virtualização, tais como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalação do centOS**

* Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.
* formato VHDX Olá não é suportado no Azure, apenas **fixo VHD**.  Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá convert-vhd cmdlet. Se estiver a utilizar VirtualBox significa que a seleção **um tamanho fixo** como opposed predefinido toohello dinamicamente atribuído ao criar o disco de Olá.
* Ao instalar o sistema de Linux Olá é *recomendado* que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos). Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco de SO alguma vez precisar de toobe ligado tooanother VM idêntico para resolução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados.
* É necessário suporte de kernel para montar a sistemas de ficheiros UDF. No primeiro arranque no Azure Olá configuração aprovisionamento é transmitida toohello VM com Linux através do UDF formatado suporte de dados é anexado toohello convidado. agente Linux do Azure de Olá tem de ser capaz de toomount Olá UDF ficheiro sistema tooread respetiva configuração e aprovisionar Olá VM.
* Versões de kernel do Linux abaixo 2.6.37 não suportam no Hyper-V com tamanhos de VM maiores. Isto emitir principalmente impactos distribuições anteriores utilizando Olá upstream kernel do Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504). Sistemas com kernels personalizados anteriores 2.6.37 ou baseado em RHEL kernels mais antigos que tem de definir 2.6.32-504 Olá parâmetro arranque `numa=off` no kernel Olá da linha de comandos no grub.conf. Para obter mais informações consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Configure uma partição de comutação em disco do SO Olá. agente do Linux Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.  Podem encontrar mais informações sobre esta nos passos Olá abaixo.
* Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.

## <a name="centos-6x"></a>CentOS 6. x

1. No Gestor de Hyper-V, selecione a máquina virtual de Olá.

2. Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.

3. No 6 do CentOS, NetworkManager pode interferir com agente Linux do Azure de Olá. Desinstale este pacote executando Olá os seguintes comandos:
   
        # sudo rpm -e --nodeps NetworkManager

4. Criar ou editar o ficheiro de Olá `/etc/sysconfig/network` e adicione Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar o ficheiro de Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá seguinte texto:
   
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
   
        # sudo chkconfig network on

8. Se quiser espelhos de OpenLogic de Olá toouse que estão alojados no Olá centros de dados do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` ficheiro com Olá repositórios a seguir.  Também irá adicionar Olá **[openlogic]** repositório inclui pacotes adicionais, tais como o agente Linux do Azure de Olá:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Olá guia restante será partem do princípio de que está a utilizar, pelo menos, Olá `[openlogic]` repositório, que será utilizado tooinstall Olá Azure agente do Linux abaixo.


9. Adicione Olá linha too/etc/yum.conf os seguintes:
    
        http_caching=packages

10. Execute Olá comando tooclear Olá yum metadados e atualização Olá sistema atual com pacotes mais recentes Olá os seguintes:
    
        # yum clean all

    A menos que estiver a criar uma imagem para uma versão antiga do CentOS, recomenda-se tooupdate que Olá, todos os pacotes toohello mais recentes:

        # sudo yum -y update

    Reiniciar o computador poderá ser necessário depois de executar este comando.

11. (Opcional) Instale os controladores de Olá para Olá serviços de integração Linux (LIS).
   
    >[!IMPORTANT]
    passo Olá é **necessário** para CentOS 6.3 e anteriores e opcionais para versões posteriores.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Em alternativa, pode seguir as instruções de instalação manual de Olá no Olá [página de transferência de LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Olá RPM para a VM.
 
12. Instale Olá agente Linux do Azure e as dependências:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    pacote de WALinuxAgent Olá irá remover Olá NetworkManager e pacotes de NetworkManager gnome se estes não foram já removidas conforme descrito no passo 3.


13. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo, abra `/boot/grub/menu.lst` num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.
    
    Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:
    
        rhgb quiet crashkernel=auto
    
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.  Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.

    >[!Important]
    CentOS 6.5 e anteriores também devem definir o parâmetro de kernel Olá `numa=off`. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

14. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.  Isto é normalmente predefinido Olá.

15. Não crie o espaço de comutação em disco do SO Olá.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure. Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada. Depois de instalar Olá agente Linux do Azure (consulte o passo anterior), modifique Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Clique em **ação -> encerrar baixo** no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0 +
**Alterações no CentOS 7 (e derivados semelhantes)**

Preparar uma máquina virtual do CentOS 7 para o Azure é muito semelhante tooCentOS 6, no entanto, existem várias diferenças importantes vale a pena realçar:

* Olá NetworkManager do pacote já não está em conflito com o agente do Olá Linux do Azure. Este pacote é instalado por predefinição e recomendamos que não é removida.
* GRUB2 agora ser utilizada como Olá bootloader predefinido, para que o procedimento de Olá para editar os parâmetros de kernel foi alterada (ver abaixo).
* XFS é agora o sistema de ficheiros Olá predefinido. sistema de ficheiros de ext4 Olá ainda pode ser utilizado se assim o desejar.

**Passos de configuração**

1. No Gestor de Hyper-V, selecione a máquina virtual de Olá.

2. Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.

3. Criar ou editar o ficheiro de Olá `/etc/sysconfig/network` e adicione Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Criar ou editar o ficheiro de Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Se quiser espelhos de OpenLogic de Olá toouse que estão alojados no Olá centros de dados do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` ficheiro com Olá repositórios a seguir.  Também irá adicionar Olá **[openlogic]** repositório inclui pacotes de agente Linux do Azure de Olá:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Olá guia restante será partem do princípio de que está a utilizar, pelo menos, Olá `[openlogic]` repositório, que será utilizado tooinstall Olá Azure agente do Linux abaixo.

7. Executar Olá os seguintes comandos tooclear Olá atual yum metadados e instalar quaisquer atualizações:
   
        # sudo yum clean all

    A menos que estiver a criar uma imagem para uma versão antiga do CentOS, recomenda-se tooupdate que Olá, todos os pacotes toohello mais recentes:

        # sudo yum -y update

    Reiniciar o computador pode ser necessário depois de executar este comando.

8. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo, abra `/etc/default/grub` no Olá de editor e edição de texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. É também desativa Olá novo CentOS 7 convenções de nomenclatura para NICs. Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série. Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.

9. Quando tiver terminado edição `/etc/default/grub` por acima, execute Olá configuração do comando toorebuild Olá grub os seguintes:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Se criar a imagem de Olá de **VMWare, VirtualBox ou KVM:** Certifique-se de controladores de Olá Hyper-V estão incluídos no Olá initramfs:
   
   Editar `/etc/dracut.conf`, adicionar conteúdo:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Reconstrua Olá initramfs:
   
        # sudo dracut –f -v

11. Instale Olá agente Linux do Azure e as dependências:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Não crie o espaço de comutação em disco do SO Olá.
   
   Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure. Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada. Depois de instalar Olá agente Linux do Azure (consulte o passo anterior), modifique Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:
   
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

## <a name="next-steps"></a>Passos seguintes
Está agora pronto toouse sua CentOS Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

