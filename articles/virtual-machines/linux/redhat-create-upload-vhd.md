---
title: "aaaCreate e carregar um VHD do Red Hat Enterprise Linux para utilização no Azure | Microsoft Docs"
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operativo Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Preparar uma máquina virtual baseada em Red Hat para o Azure
Neste artigo, ficará a saber como tooprepare uma máquina virtual do Red Hat Enterprise Linux (RHEL) para utilização no Azure. versões de Olá do RHEL que são abordadas neste artigo são 6.7 + e 7.1 +. Olá hipervisores de preparação, que são abordadas neste artigo são Hyper-V, com base em kernel a máquina virtual (KVM) e VMware. Para obter mais informações sobre os requisitos de elegibilidade para participar no programa de acesso à nuvem do Red Hat, consulte [Web site de acesso à nuvem do Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e [RHEL em execução no Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Preparar uma máquina de virtual baseado no Red Hat a partir do Gestor de Hyper-V

### <a name="prerequisites"></a>Pré-requisitos
Esta secção assume que já tenham obteve um ficheiro ISO do Web site do Red Hat Olá e Olá instalado RHEL imagem tooa disco rígido virtual (VHD). Para obter mais detalhes sobre como toouse Gestor de Hyper-V tooinstall uma imagem do sistema operativo, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalação do RHEL**

* Azure não suporta o formato VHDX Olá. Azure suporta apenas fixo VHD. Pode utilizar o formato de tooVHD do Gestor de Hyper-V tooconvert Olá disco ou, pode utilizar o cmdlet do Olá convert-vhd. Se utilizar VirtualBox, selecione **um tamanho fixo** por oposição ao predefinido de toohello dinamicamente atribuído opção ao criar o disco de Olá.
* Azure suporta apenas máquinas de virtuais de geração 1. Pode converter uma máquina virtual de geração 1 formato de ficheiro VHD de toohello VHDX e de disco de tamanho fixo tooa de expansão dinâmica. Não é possível alterar a geração de uma máquina virtual. Para obter mais informações, consulte [deve criar máquinas virtuais de geração 1 ou 2 no Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* Olá tamanho máximo permitido para Olá VHD é 1,023 GB.
* Quando instalar o sistema de operativo Linux Olá, recomendamos que utilize partições padrão em vez de Gestor de Volume lógica (LVM), que é frequentemente predefinição de Olá para várias instalações. Esta prática evitará LVM nome entra em conflito com as máquinas virtuais Clonadas, particularmente se alguma vez precisar de tooattach uma máquina de virtual idênticas do sistema operativo disco tooanother para resolução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados.
* É necessário suporte de kernel para montar a sistemas de ficheiros de formato de disco Universal (UDF). No primeiro arranque no, Olá formatado UDF Media Services do Azure que é anexado toohello convidado transmite Olá aprovisionamento configuração toohello máquina virtual com Linux. Olá agente Linux do Azure tem de ser capaz de toomount Olá UDF ficheiro sistema tooread respetiva configuração e aprovisionar a máquina virtual de Olá.
* Versões de kernel de Linux Olá anteriores ao 2.6.37 não suportam acesso não uniforme memória (NUMA) no Hyper-V com maior tamanhos de máquina virtual. Isto emitir principalmente impactos distribuições mais antigas que utilizam Olá upstream kernel do Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504). Sistemas que executam kernels personalizados que são mais antigos do que 2.6.37 ou baseado em RHEL kernels que são mais antigas do que 2.6.32-504 tem de definir Olá `numa=off` arranque parâmetro na linha de comandos de kernel Olá no grub.conf. Para obter mais informações, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Configure uma partição de comutação em disco do sistema operativo Olá. Olá agente Linux pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.  Podem encontrar mais informações sobre esta no Olá os seguintes passos.
* Todos os VHDs têm de ter tamanhos que estão em múltiplos de 1 MB.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Preparar uma máquina virtual do RHEL 6 a partir do Gestor de Hyper-V

1. No Gestor de Hyper-V, selecione a máquina virtual de Olá.

2. Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.

3. No RHEL 6, NetworkManager pode interferir com agente Linux do Azure de Olá. Desinstale este pacote executando Olá os seguintes comandos:
   
        # sudo rpm -e --nodeps NetworkManager

4. Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Mova (ou remova) Olá udev regras tooavoid gerar regras estáticas para a interface da Ethernet Olá. Estas regras provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:

        # sudo chkconfig network on

8. Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat. Ative o repositório de extras Olá executando Olá os seguintes comandos:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo esta modificação, abra `/boot/grub/menu.lst` num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.
    
    Além disso, recomendamos que remova Olá os seguintes parâmetros:
    
        rhgb quiet crashkernel=auto
    
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.  Pode deixar Olá `crashkernel` opção configurada se assim o desejar. Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais. Esta configuração pode ser problemática em tamanhos de máquinas virtuais mais pequenos.

    >[!Important]
    RHEL 6.5 e anterior também tem de definir Olá `numa=off` parâmetro de kernel. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

11. Certifique-se de que servidor de secure shell (SSH) Olá está instalado e configurado toostart no momento do arranque, que é normalmente predefinido Olá. Modificar /etc/ssh/sshd_config tooinclude Olá seguinte linha:

        ClientAliveInterval 180

12. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Instalar pacote de WALinuxAgent Olá remove Olá NetworkManager e pacotes de NetworkManager gnome se estes não foram removidos no passo 3.

13. Não crie o espaço de comutação em disco do sistema operativo Olá.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure. Tenha em atenção que Olá local disco de recursos é um disco temporário e que-lo poderá de ser esvaziada quando a máquina virtual de Olá é desaprovisionada. Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modifique Olá adequadamente os seguintes parâmetros /etc/waagent.conf:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:

        # sudo subscription-manager unregister

15. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Clique em **ação** > **Encerrar** no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Preparar uma máquina virtual do RHEL 7 a partir do Gestor de Hyper-V

1. No Gestor de Hyper-V, selecione a máquina virtual de Olá.

2. Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.

3. Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:

        # sudo chkconfig network on

6. Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo esta modificação, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. Esta configuração também desativa-se Olá novo RHEL 7 convenções de nomenclatura para NICs. Além disso, recomendamos que remova Olá os seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série. Pode deixar Olá `crashkernel` opção configurada se assim o desejar. Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.

8. Depois de terminar edição `/etc/default/grub`, execute hello os seguintes comandos toorebuild Olá grub configuração:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Certifique-se de que servidor SSH Olá está instalado e configurado toostart no momento do arranque, que é normalmente predefinido Olá. Modificar `/etc/ssh/sshd_config` Olá tooinclude seguinte linha:

        ClientAliveInterval 180

10. pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat. Ative o repositório de extras Olá executando Olá os seguintes comandos:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Não crie o espaço de comutação em disco do sistema operativo Olá.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure. Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada. Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Se pretender que a subscrição de Olá toounregister, execute Olá os seguintes comandos:

        # sudo subscription-manager unregister

14. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Clique em **ação** > **Encerrar** no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Preparar uma máquina de virtual baseado no Red Hat do KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Preparar uma máquina virtual do RHEL 6 do KVM

1. Transferir imagem KVM Olá do RHEL 6 do Web site do Red Hat Olá.

2. Defina uma palavra-passe de raiz.

    Gerar uma palavra-passe encriptada e copiar Olá resultado do comando de Olá:

        # openssl passwd -1 changeme

    Defina uma palavra-passe de raiz com guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Campo de segundo Olá alteração do utilizador raiz Olá "!" toohello encriptados palavra-passe.

3. Crie uma máquina virtual no KVM da imagem de qcow2 de Olá. Definir o tipo de disco Olá demasiado**qcow2**e definir o modelo de dispositivo de interface de rede virtual Olá demasiado**virtio**. Em seguida, iniciar a máquina virtual de Olá e inicie sessão como raiz.

4. Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Mova (ou remova) Olá udev regras tooavoid gerar regras estáticas para a interface da Ethernet Olá. Estas regras provocar problemas ao clonar uma máquina virtual no Azure ou do Hyper-v:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:

        # chkconfig network on

8. Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo nesta configuração, abra `/boot/grub/menu.lst` num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.
    
    Além disso, recomendamos que remova Olá os seguintes parâmetros:
    
        rhgb quiet crashkernel=auto
    
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série. Pode deixar Olá `crashkernel` opção configurada se assim o desejar. Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.

    >[!Important]
    RHEL 6.5 e anterior também tem de definir Olá `numa=off` parâmetro de kernel. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

10. Adicione tooinitramfs de módulos do Hyper-V:  

    Editar `/etc/dracut.conf`e adicione Olá seguinte conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Reconstrua initramfs:

        # dracut -f -v

11. Desinstale init de cloud:

        # yum remove cloud-init

12. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque:

        # chkconfig sshd on

    Modificar /etc/ssh/sshd_config tooinclude Olá seguintes linhas:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat. Ative o repositório de extras Olá executando Olá os seguintes comandos:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure. Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada. Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no **/etc/waagent.conf** corretamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:

        # subscription-manager unregister

17. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Encerre a máquina virtual Olá KVM.

19. Converta o formato VHD do Olá qcow2 imagem toohello.

    Comece por converter o formato de tooraw Olá imagem:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB. Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter tooa de disco em bruto de Olá fixo tamanho VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Preparar uma máquina virtual do RHEL 7 do KVM

1. Transferir imagem KVM Olá RHEL 7 do Web site do Red Hat Olá. Este procedimento utiliza RHEL 7 como exemplo de Olá.

2. Defina uma palavra-passe de raiz.

    Gerar uma palavra-passe encriptada e copiar Olá resultado do comando de Olá:

        # openssl passwd -1 changeme

    Defina uma palavra-passe de raiz com guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Campo de segundo Olá alteração de utilizador de raiz de "!" toohello encriptados palavra-passe.

3. Crie uma máquina virtual no KVM da imagem de qcow2 de Olá. Definir o tipo de disco Olá demasiado**qcow2**e definir o modelo de dispositivo de interface de rede virtual Olá demasiado**virtio**. Em seguida, iniciar a máquina virtual de Olá e inicie sessão como raiz.

4. Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:

        # chkconfig network on

7. Registe a instalação do Red Hat subscrição tooenable de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo nesta configuração, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Este comando também garante que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. comando Olá também desativa-se Olá novo RHEL 7 convenções de nomenclatura para NICs. Além disso, recomendamos que remova Olá os seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série. Pode deixar Olá `crashkernel` opção configurada se assim o desejar. Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.

9. Depois de terminar edição `/etc/default/grub`, execute hello os seguintes comandos toorebuild Olá grub configuração:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Adicione módulos do Hyper-V em initramfs.

    Editar `/etc/dracut.conf` e adicionar conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Reconstrua initramfs:

        # dracut -f -v

11. Desinstale init de cloud:

        # yum remove cloud-init

12. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque:

        # systemctl enable sshd

    Modificar /etc/ssh/sshd_config tooinclude Olá seguintes linhas:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat. Ative o repositório de extras Olá executando Olá os seguintes comandos:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:

        # yum install WALinuxAgent

    Ative o serviço de waagent Olá:

        # systemctl enable waagent.service

15. Não crie o espaço de comutação em disco do sistema operativo Olá.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure. Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada. Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:

        # subscription-manager unregister

17. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Encerre a máquina virtual Olá KVM.

19. Converta o formato VHD do Olá qcow2 imagem toohello.

    Comece por converter o formato de tooraw Olá imagem:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB. Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter tooa de disco em bruto de Olá fixo tamanho VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Preparar uma máquina de virtual baseado no Red Hat do VMware
### <a name="prerequisites"></a>Pré-requisitos
Esta secção assume que já instalou uma máquina virtual do RHEL no VMware. Para obter detalhes sobre como tooinstall um sistema operativo no VMware, consulte o artigo [guia de instalação de sistema operativo de convidado de VMware](http://partnerweb.vmware.com/GOSIG/home.html).

* Quando instalar o sistema de operativo Linux Olá, recomendamos que utilize partições padrão em vez de LVM, que é frequentemente predefinição de Olá para várias instalações. Evitará LVM nome entra em conflito com a máquina virtual clonada, particularmente se um disco de sistema operativo tem alguma vez toobe ligado tooanother máquinas para resolução de problemas. LVM RAID pode ser utilizado ou em discos de dados se preferencial.
* Configure uma partição de comutação em disco do sistema operativo Olá. Pode configurar Olá Linux agente toocreate um ficheiro de comutação no disco de recursos temporário Olá. Pode encontrar mais informações sobre esta nos passos de Olá que se seguem.
* Quando criar o disco de rígido virtual Olá, selecione **disco virtual de armazenamento como um único ficheiro**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Preparar uma máquina virtual do RHEL 6 do VMware
1. No RHEL 6, NetworkManager pode interferir com agente Linux do Azure de Olá. Desinstale este pacote executando Olá os seguintes comandos:
   
        # sudo rpm -e --nodeps NetworkManager

2. Crie um ficheiro denominado **rede** Olá /etc/hosts/sysconfig/diretório que contém Olá seguinte texto:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Mova (ou remova) Olá udev regras tooavoid gerar regras estáticas para a interface da Ethernet Olá. Estas regras provocar problemas ao clonar uma máquina virtual no Azure ou do Hyper-v:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:

        # sudo chkconfig network on

6. Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat. Ative o repositório de extras Olá executando Olá os seguintes comandos:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. Além disso, recomendamos que remova Olá os seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série. Pode deixar Olá `crashkernel` opção configurada se assim o desejar. Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.

9. Adicione tooinitramfs de módulos do Hyper-V:

    Editar `/etc/dracut.conf`e adicione Olá seguinte conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Reconstrua initramfs:

        # dracut -f -v

10. Certifique-se de que servidor SSH Olá está instalado e configurado toostart no momento do arranque, que é normalmente predefinido Olá. Modificar `/etc/ssh/sshd_config` Olá tooinclude seguinte linha:

    ClientAliveInterval 180

11. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Não crie o espaço de comutação em disco do sistema operativo Olá.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure. Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada. Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:

        # sudo subscription-manager unregister

14. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Encerre a máquina virtual de Olá e converta o ficheiro de. vhd do Olá VMDK ficheiro tooa.

    Comece por converter o formato de tooraw Olá imagem:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB. Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter tooa de disco em bruto de Olá fixo tamanho VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Preparar uma máquina virtual do RHEL 7 do VMware
1. Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:

        # sudo chkconfig network on

4. Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure. toodo esta modificação, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Esta configuração também garante que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração. É também desativa Olá novo RHEL 7 convenções de nomenclatura para NICs. Além disso, recomendamos que remova Olá os seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série. Pode deixar Olá `crashkernel` opção configurada se assim o desejar. Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.

6. Depois de terminar edição `/etc/default/grub`, execute hello os seguintes comandos toorebuild Olá grub configuração:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Adicione tooinitramfs de módulos do Hyper-V.

    Editar `/etc/dracut.conf`, adicionar conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Reconstrua initramfs:

        # dracut -f -v

8. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque. Esta é normalmente Olá predefinição. Modificar `/etc/ssh/sshd_config` Olá tooinclude seguinte linha:

        ClientAliveInterval 180

9. pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat. Ative o repositório de extras Olá executando Olá os seguintes comandos:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Instale Olá agente Linux do Azure executando Olá os seguintes comandos:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Não crie o espaço de comutação em disco do sistema operativo Olá.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure. Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada. Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Se pretender que a subscrição de Olá toounregister, execute Olá os seguintes comandos:

        # sudo subscription-manager unregister

13. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Encerre a máquina virtual de Olá e converter Olá ficheiro toohello VHD no formato VMDK.

    Comece por converter o formato de tooraw Olá imagem:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB. Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter tooa de disco em bruto de Olá fixo tamanho VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Preparar uma máquina de virtual baseado no Red Hat a partir de um ficheiro ISO utilizando um ficheiro de kickstart automaticamente
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Preparar uma máquina virtual de RHEL 7 de um ficheiro de kickstart

1.  Criar um ficheiro de kickstart que inclui Olá seguir o conteúdo e guarde o ficheiro Olá. Para obter mais informações sobre a instalação de kickstart, consulte Olá [guia de instalação Kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Coloque o ficheiro de kickstart olá onde o sistema de instalação de Olá consegue aceder-lhe.

3. No Gestor de Hyper-V, crie uma nova máquina virtual. No Olá **ligar disco rígido Virtual** página, selecione **anexar um disco rígido virtual mais tarde**e concluída Olá Assistente Nova Máquina Virtual.

4. Abra as definições da máquina virtual de Olá:

    a.  Anexe uma nova máquina de virtual toohello de disco rígido virtual. Certifique-se de que tooselect **formato VHD** e **de tamanho fixo**.

    b.  Anexe unidade de DVD toohello ISO de instalação de Olá.

    c.  Definir Olá BIOS tooboot a partir do CD.

5. Inicie máquina virtual de Olá. Quando for apresentado o guia de instalação de Olá, prima **separador** opções de arranque de Olá tooconfigure.

6. Introduza `inst.ks=<hello location of hello kickstart file>` no fim de Olá de opções de arranque Olá e prima **Enter**.

7. Aguarde Olá toofinish de instalação. Quando estiver concluída, máquina virtual de Olá será automaticamente encerrada. O VHD de Linux está agora pronto toobe carregado tooAzure.

## <a name="known-issues"></a>Problemas conhecidos
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>controlador de Hyper-V Olá não foi incluído na inicial do disco de RAM Olá quando utilizar um hipervisor não Hyper-V

Em alguns casos, programas de instalação do Linux podem não incluir controladores de Olá do Hyper-V no Olá inicial RAM do disco (initrd ou initramfs), a menos que Linux Deteta que está em execução num ambiente Hyper-V.

Quando estiver a utilizar um tooprepare de sistema (ou seja, Virtualbox Xen, etc.) de Virtualização diferentes a imagem do Linux, poderá ser necessário toorebuild initrd tooensure que, pelo menos, Olá hv_vmbus e módulos de kernel hv_storvsc estão disponíveis no disco de RAM inicial Olá. Este é um problema conhecido, pelo menos, em sistemas baseados no montante de distribuição Red Hat Olá.

tooresolve este problema, adicione tooinitramfs de módulos do Hyper-V e reconstrui-lo:

Editar `/etc/dracut.conf`e adicione Olá seguinte conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Reconstrua initramfs:

        # dracut -f -v

Para obter mais detalhes, consulte as informações de Olá [reconstruir initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Passos seguintes
Está agora pronto toouse das Red Hat Enterprise Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Para obter mais detalhes sobre Olá hipervisores que são certificadas toorun Red Hat Enterprise Linux, consulte [Web site do Red Hat Olá](https://access.redhat.com/certified-hypervisors).
