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
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="21155-103">Como tooreset Linux palavra-passe local em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="21155-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="21155-104">Este artigo apresenta várias métodos tooreset local Linux Máquina Virtual (VM) palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="21155-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="21155-105">Se a conta de utilizador Olá expirou ou deseje apenas toocreate uma nova conta, pode utilizar Olá seguintes métodos toocreate uma nova conta de administrador local e obterem novamente acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="21155-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="21155-106">Sintomas</span><span class="sxs-lookup"><span data-stu-id="21155-106">Symptoms</span></span>

<span data-ttu-id="21155-107">Não é possível iniciar sessão toohello VM e receberá uma mensagem que indica essa palavra-passe de Olá que utilizou está incorreto.</span><span class="sxs-lookup"><span data-stu-id="21155-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="21155-108">Além disso, é possível utilizar VMAgent tooreset a palavra-passe no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="21155-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="21155-109">Procedimento de palavra-passe de reposição manual</span><span class="sxs-lookup"><span data-stu-id="21155-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="21155-110">Eliminar Olá VM e manter os discos de Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="21155-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="21155-111">Anexar unidade de SO como um tooanother de disco de dados de Olá temporal VM Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="21155-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="21155-112">Execute Olá seguindo o comando SSH do Olá temporal VM toobecome um utilizador Super-obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="21155-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="21155-113">Executar **fdisk -l** ou vista de olhos Olá de toofind de registos de sistema anexado recentemente disco.</span><span class="sxs-lookup"><span data-stu-id="21155-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="21155-114">Localize toomount de nome de unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="21155-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="21155-115">Em seguida, no Olá VM temporal, procure no Olá relevante ficheiro de registo.</span><span class="sxs-lookup"><span data-stu-id="21155-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="21155-116">Olá que se segue exemplo da saída do comando de grep Olá:</span><span class="sxs-lookup"><span data-stu-id="21155-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="21155-117">Criar um ponto de montagem chamado **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="21155-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="21155-118">Monte o disco de SO de Olá no ponto de montagem Olá.</span><span class="sxs-lookup"><span data-stu-id="21155-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="21155-119">Normalmente, terá de toomount sdc1 ou sdc2.</span><span class="sxs-lookup"><span data-stu-id="21155-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="21155-120">Isto irá depender Olá partição no diretório de /etc/hosts do disco de máquina quebrada Olá de alojamento.</span><span class="sxs-lookup"><span data-stu-id="21155-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="21155-121">Efetue uma cópia de segurança antes de efetuar alterações:</span><span class="sxs-lookup"><span data-stu-id="21155-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="21155-122">Palavra-passe utilizador de Olá a reposição de que precisa de:</span><span class="sxs-lookup"><span data-stu-id="21155-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="21155-123">Mover Olá modificar ficheiros toohello correto localização Olá quebrada disco da máquina.</span><span class="sxs-lookup"><span data-stu-id="21155-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="21155-124">CD / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="21155-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
