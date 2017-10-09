---
title: "acesso de aaaReset em VMs do Linux do Azure utilizando Olá extensão VMAccess | Microsoft Docs"
description: "Reponha o acesso em VMs do Linux do Azure utilizando Olá extensão VMAccess."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="7ada0-103">Gerir utilizadores, SSH e verificação ou discos de reparação em VMs do Linux do Azure utilizando Olá extensão VMAccess com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7ada0-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="7ada0-104">Este artigo mostra-lhe como toouse Olá Azure VMAcesss extensão toocheck ou reparar um disco, reponha o acesso de utilizador, gerir contas de utilizador ou reponha a configuração de SSHD Olá no Linux.</span><span class="sxs-lookup"><span data-stu-id="7ada0-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="7ada0-105">artigo de Olá requer:</span><span class="sxs-lookup"><span data-stu-id="7ada0-105">hello article requires:</span></span>

* <span data-ttu-id="7ada0-106">uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="7ada0-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="7ada0-107">Olá [CLI do Azure](../../cli-install-nodejs.md) registado com `azure login`.</span><span class="sxs-lookup"><span data-stu-id="7ada0-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="7ada0-108">Olá CLI do Azure *tem de constar* modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="7ada0-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7ada0-109">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="7ada0-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="7ada0-110">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="7ada0-111">[Azure CLI 1.0](#quick-commands)– nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="7ada0-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7ada0-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="7ada0-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="7ada0-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="7ada0-113">Quick commands</span></span>
<span data-ttu-id="7ada0-114">Existem duas formas toouse VMAccess em VMs do Linux:</span><span class="sxs-lookup"><span data-stu-id="7ada0-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="7ada0-115">Utilizar Olá CLI do Azure 1.0 e Olá necessários parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7ada0-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="7ada0-116">A utilizar não processados ficheiros JSON que VMAccess processa e, em seguida, agir em.</span><span class="sxs-lookup"><span data-stu-id="7ada0-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="7ada0-117">Para a secção do comando rápido Olá, vamos toouse Olá CLI do Azure 1.0 `azure vm reset-access` método.</span><span class="sxs-lookup"><span data-stu-id="7ada0-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="7ada0-118">No Olá seguintes exemplos de comando, substitua os valores de Olá que contêm "exemplo" com valores de Olá do seu próprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="7ada0-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="7ada0-119">Criar um grupo de recursos e uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="7ada0-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="7ada0-120">Criar uma VM Debian</span><span class="sxs-lookup"><span data-stu-id="7ada0-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="7ada0-121">Repor palavra-passe de raiz</span><span class="sxs-lookup"><span data-stu-id="7ada0-121">Reset root password</span></span>
<span data-ttu-id="7ada0-122">palavra-passe da raiz do Olá tooreset:</span><span class="sxs-lookup"><span data-stu-id="7ada0-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="7ada0-123">Repor chave SSH</span><span class="sxs-lookup"><span data-stu-id="7ada0-123">SSH key reset</span></span>
<span data-ttu-id="7ada0-124">tooreset Olá a chave SSH de um utilizador não raiz:</span><span class="sxs-lookup"><span data-stu-id="7ada0-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="7ada0-125">Criar um utilizador</span><span class="sxs-lookup"><span data-stu-id="7ada0-125">Create a user</span></span>
<span data-ttu-id="7ada0-126">toocreate um utilizador:</span><span class="sxs-lookup"><span data-stu-id="7ada0-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="7ada0-127">Remover um utilizador</span><span class="sxs-lookup"><span data-stu-id="7ada0-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="7ada0-128">Repor SSHD</span><span class="sxs-lookup"><span data-stu-id="7ada0-128">Reset SSHD</span></span>
<span data-ttu-id="7ada0-129">configuração do tooreset Olá SSHD:</span><span class="sxs-lookup"><span data-stu-id="7ada0-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="7ada0-130">Instruções detalhadas</span><span class="sxs-lookup"><span data-stu-id="7ada0-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="7ada0-131">VMAccess definida:</span><span class="sxs-lookup"><span data-stu-id="7ada0-131">VMAccess defined:</span></span>
<span data-ttu-id="7ada0-132">disco Olá no Linux VM é Mostrar erros.</span><span class="sxs-lookup"><span data-stu-id="7ada0-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="7ada0-133">Examinar Repor palavra-passe de raiz de Olá para a VM com Linux ou a chave privada SSH sejam eliminados acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="7ada0-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="7ada0-134">Se o que aconteceu regresso dias Olá do Centro de dados de Olá, seria necessário toodrive existe e abra Olá KVM tooget na consola de hello do servidor.</span><span class="sxs-lookup"><span data-stu-id="7ada0-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="7ada0-135">Considere Olá extensão VMAccess do Azure como esse comutador KVM que permite-lhe tooaccess Olá consola tooreset acesso tooLinux ou efetuar a manutenção de nível de disco.</span><span class="sxs-lookup"><span data-stu-id="7ada0-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="7ada0-136">Para Olá detalhadas explicação passo a passo, vamos toouse Olá ditada de VMAccess, que utiliza ficheiros JSON não processados.</span><span class="sxs-lookup"><span data-stu-id="7ada0-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="7ada0-137">Estes ficheiros VMAccess JSON também podem ser chamados a partir de modelos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ada0-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="7ada0-138">Utilizar o VMAccess toocheck ou reparação Olá o disco de uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="7ada0-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="7ada0-139">Utilizar o VMAccess para fazer uma fsck executar no disco Olá sob a VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="7ada0-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="7ada0-140">Também pode efetuar uma verificação de disco e a reparação do disco utilizando um VMAccess.</span><span class="sxs-lookup"><span data-stu-id="7ada0-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="7ada0-141">toocheck e, em seguida, reparação Olá disco utilizam este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7ada0-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="7ada0-142">Execute script de VMAccess Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="7ada0-143">Utilizar o VMAccess tooreset utilizador acesso tooLinux</span><span class="sxs-lookup"><span data-stu-id="7ada0-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="7ada0-144">Se tiver perdido tooroot de acesso na sua VM do Linux, pode iniciar uma palavra-passe do VMAccess script tooreset Olá raiz.</span><span class="sxs-lookup"><span data-stu-id="7ada0-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="7ada0-145">palavra-passe da raiz do Olá tooreset, utilize este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7ada0-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="7ada0-146">Execute script de VMAccess Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="7ada0-147">chave SSH Olá tooreset de um utilizador não raiz, utilize este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7ada0-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="7ada0-148">Execute script de VMAccess Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="7ada0-149">Utilizar contas de utilizador de toomanage VMAccess no Linux</span><span class="sxs-lookup"><span data-stu-id="7ada0-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="7ada0-150">VMAccess é um script de Python que pode ser utilizados toomanage utilizadores na sua VM do Linux sem iniciar sessão e utilizando a conta de raiz de sudo ou Olá.</span><span class="sxs-lookup"><span data-stu-id="7ada0-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="7ada0-151">toocreate um utilizador, utilize este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7ada0-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="7ada0-152">Execute script de VMAccess Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="7ada0-153">toodelete um utilizador, utilize este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7ada0-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="7ada0-154">Execute script de VMAccess Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="7ada0-155">Utilizar VMAccess tooreset Olá SSHD configuração</span><span class="sxs-lookup"><span data-stu-id="7ada0-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="7ada0-156">Se efetuar a configuração de Linux VMs SSHD toohello de alterações e ligação de SSH Olá fechar antes de a verificar as alterações de Olá, pode ser impedidos por SSH'ing novamente.</span><span class="sxs-lookup"><span data-stu-id="7ada0-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="7ada0-157">VMAccess pode ser utilizado tooreset Olá SSHD configuração tooa back-conhecida boa configuração sem a ser registado através de SSH.</span><span class="sxs-lookup"><span data-stu-id="7ada0-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="7ada0-158">configuração do tooreset Olá SSHD utilizar este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7ada0-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="7ada0-159">Execute script de VMAccess Olá:</span><span class="sxs-lookup"><span data-stu-id="7ada0-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="7ada0-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7ada0-160">Next steps</span></span>
<span data-ttu-id="7ada0-161">Atualizar Linux utilizar extensões de VMAccess do Azure é um método toomake as alterações uma VM com Linux em execução.</span><span class="sxs-lookup"><span data-stu-id="7ada0-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="7ada0-162">Também pode utilizar ferramentas como init de nuvem e modelos do Azure toomodify na VM com Linux no arranque.</span><span class="sxs-lookup"><span data-stu-id="7ada0-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="7ada0-163">Sobre as funcionalidades e as extensões de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ada0-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="7ada0-164">Criação de modelos Azure Resource Manager com extensões de VM com Linux</span><span class="sxs-lookup"><span data-stu-id="7ada0-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="7ada0-165">Nuvem init toocustomize uma VM com Linux a utilizar durante a criação</span><span class="sxs-lookup"><span data-stu-id="7ada0-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

