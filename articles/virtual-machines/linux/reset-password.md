---
title: aaaHow tooreset Linux palavra-passe local em VMs do Azure | Microsoft Docs
description: "Introduzir Olá passos tooreset Olá Linux palavra-passe local na VM do Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Como tooreset Linux palavra-passe local em VMs do Azure

Este artigo apresenta várias métodos tooreset local Linux Máquina Virtual (VM) palavras-passe. Se a conta de utilizador Olá expirou ou deseje apenas toocreate uma nova conta, pode utilizar Olá seguintes métodos toocreate uma nova conta de administrador local e obterem novamente acesso toohello VM.

## <a name="symptoms"></a>Sintomas

Não é possível iniciar sessão toohello VM e receberá uma mensagem que indica essa palavra-passe de Olá que utilizou está incorreto. Além disso, é possível utilizar VMAgent tooreset a palavra-passe no Olá Portal do Azure. 

## <a name="manual-password-reset-procedure"></a>Procedimento de palavra-passe de reposição manual

1.  Eliminar Olá VM e manter os discos de Olá ligado.

2.  Anexar unidade de SO como um tooanother de disco de dados de Olá temporal VM Olá mesma localização.

3.  Execute Olá seguindo o comando SSH do Olá temporal VM toobecome um utilizador Super-obrigatórios.


    ~~~~
    sudo su
    ~~~~

4.  Executar **fdisk -l** ou vista de olhos Olá de toofind de registos de sistema anexado recentemente disco. Localize toomount de nome de unidade de Olá. Em seguida, no Olá VM temporal, procure no Olá relevante ficheiro de registo.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Olá que se segue exemplo da saída do comando de grep Olá:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Criar um ponto de montagem chamado **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Monte o disco de SO de Olá no ponto de montagem Olá. Normalmente, terá de toomount sdc1 ou sdc2. Isto irá depender Olá partição no diretório de /etc/hosts do disco de máquina quebrada Olá de alojamento.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Efetue uma cópia de segurança antes de efetuar alterações:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Palavra-passe utilizador de Olá a reposição de que precisa de:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Mover Olá modificar ficheiros toohello correto localização Olá quebrada disco da máquina.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    CD / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
