---
title: Como repor o Linux palavra-passe local em VMs do Azure | Microsoft Docs
description: Introduzir os passos para repor o Linux palavra-passe local na VM do Azure
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
ms.date: 11/03/2017
ms.author: delhan
ms.openlocfilehash: b9182ec2a974de06c2bd45928b9964f253653bf6
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/03/2018
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a>Como repor o Linux palavra-passe local em VMs do Azure

Este artigo apresenta vários métodos para repor palavras-passe de Linux Máquina Virtual (VM) local. Se a conta de utilizador expirou ou se pretende criar uma nova conta, pode utilizar os seguintes métodos para criar uma nova conta de administrador local e obter novamente acesso à VM.

## <a name="symptoms"></a>Sintomas

Não é possível iniciar sessão para a VM e receberá uma mensagem que indica que a palavra-passe que utilizou está incorreta. Além disso, não é possível utilizar VMAgent para repor a palavra-passe no Portal do Azure. 

## <a name="manual-password-reset-procedure"></a>Procedimento de palavra-passe de reposição manual

1.  Elimine a VM e manter os discos anexados.

2.  Anexe o disco de SO como um disco de dados para outra VM temporal na mesma localização.

3.  Execute o seguinte comando SSH na VM para se tornar um utilizador Super-obrigatórios temporal.


    ~~~~
    sudo su
    ~~~~

4.  Executar **fdisk -l** ou consulte os registos de sistema para localizar o disco anexado recentemente. Localize o nome de unidade para montar. Em seguida, na temporal VM, procure no ficheiro de registo relevantes.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Exemplo de saída do comando grep é o seguinte:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Criar um ponto de montagem chamado **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Monte o disco do SO no ponto de montagem. Normalmente, terá de montagem sdc1 ou sdc2. Isto irá depender a partição de alojamento no diretório de /etc/hosts do disco de máquina interrompida.

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

8.  Repor palavra-passe do utilizador que precisa de:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Mova os ficheiros de modificação para a localização correta no disco da máquina interrompida.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    ~~~~

10. Volte para a raiz e desmontar o disco.

    ~~~~
    cd /
    umount /tempmount
    ~~~~

11. Desligar o disco do portal de gestão.

12. Recrie a VM.

## <a name="next-steps"></a>Passos Seguintes

* [Resolver problemas de VM do Azure ao anexar o disco do SO para outra VM do Azure](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [CLI do Azure: Como eliminar e voltar a implementar uma VM a partir de VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
