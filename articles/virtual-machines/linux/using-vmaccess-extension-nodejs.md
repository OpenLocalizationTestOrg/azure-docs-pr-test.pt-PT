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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Gerir utilizadores, SSH e verificação ou discos de reparação em VMs do Linux do Azure utilizando Olá extensão VMAccess com Olá CLI do Azure 1.0
Este artigo mostra-lhe como toouse Olá Azure VMAcesss extensão toocheck ou reparar um disco, reponha o acesso de utilizador, gerir contas de utilizador ou reponha a configuração de SSHD Olá no Linux. artigo de Olá requer:

* uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).
* Olá [CLI do Azure](../../cli-install-nodejs.md) registado com `azure login`.
* Olá CLI do Azure *tem de constar* modo Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá
Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

- [Azure CLI 1.0](#quick-commands)– nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá


## <a name="quick-commands"></a>Comandos rápidos
Existem duas formas toouse VMAccess em VMs do Linux:

* Utilizar Olá CLI do Azure 1.0 e Olá necessários parâmetros.
* A utilizar não processados ficheiros JSON que VMAccess processa e, em seguida, agir em.

Para a secção do comando rápido Olá, vamos toouse Olá CLI do Azure 1.0 `azure vm reset-access` método. No Olá seguintes exemplos de comando, substitua os valores de Olá que contêm "exemplo" com valores de Olá do seu próprio ambiente.

## <a name="create-a-resource-group-and-linux-vm"></a>Criar um grupo de recursos e uma VM com Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Criar uma VM Debian
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

## <a name="reset-root-password"></a>Repor palavra-passe de raiz
palavra-passe da raiz do Olá tooreset:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Repor chave SSH
tooreset Olá a chave SSH de um utilizador não raiz:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Criar um utilizador
toocreate um utilizador:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Remover um utilizador
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Repor SSHD
configuração do tooreset Olá SSHD:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Instruções detalhadas
### <a name="vmaccess-defined"></a>VMAccess definida:
disco Olá no Linux VM é Mostrar erros. Examinar Repor palavra-passe de raiz de Olá para a VM com Linux ou a chave privada SSH sejam eliminados acidentalmente. Se o que aconteceu regresso dias Olá do Centro de dados de Olá, seria necessário toodrive existe e abra Olá KVM tooget na consola de hello do servidor. Considere Olá extensão VMAccess do Azure como esse comutador KVM que permite-lhe tooaccess Olá consola tooreset acesso tooLinux ou efetuar a manutenção de nível de disco.

Para Olá detalhadas explicação passo a passo, vamos toouse Olá ditada de VMAccess, que utiliza ficheiros JSON não processados.  Estes ficheiros VMAccess JSON também podem ser chamados a partir de modelos do Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Utilizar o VMAccess toocheck ou reparação Olá o disco de uma VM com Linux
Utilizar o VMAccess para fazer uma fsck executar no disco Olá sob a VM com Linux.  Também pode efetuar uma verificação de disco e a reparação do disco utilizando um VMAccess.

toocheck e, em seguida, reparação Olá disco utilizam este script de VMAccess:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Execute script de VMAccess Olá:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>Utilizar o VMAccess tooreset utilizador acesso tooLinux
Se tiver perdido tooroot de acesso na sua VM do Linux, pode iniciar uma palavra-passe do VMAccess script tooreset Olá raiz.

palavra-passe da raiz do Olá tooreset, utilize este script de VMAccess:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Execute script de VMAccess Olá:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

chave SSH Olá tooreset de um utilizador não raiz, utilize este script de VMAccess:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Execute script de VMAccess Olá:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Utilizar contas de utilizador de toomanage VMAccess no Linux
VMAccess é um script de Python que pode ser utilizados toomanage utilizadores na sua VM do Linux sem iniciar sessão e utilizando a conta de raiz de sudo ou Olá.

toocreate um utilizador, utilize este script de VMAccess:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Execute script de VMAccess Olá:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete um utilizador, utilize este script de VMAccess:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Execute script de VMAccess Olá:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>Utilizar VMAccess tooreset Olá SSHD configuração
Se efetuar a configuração de Linux VMs SSHD toohello de alterações e ligação de SSH Olá fechar antes de a verificar as alterações de Olá, pode ser impedidos por SSH'ing novamente.  VMAccess pode ser utilizado tooreset Olá SSHD configuração tooa back-conhecida boa configuração sem a ser registado através de SSH.

configuração do tooreset Olá SSHD utilizar este script de VMAccess:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Execute script de VMAccess Olá:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Passos seguintes
Atualizar Linux utilizar extensões de VMAccess do Azure é um método toomake as alterações uma VM com Linux em execução.  Também pode utilizar ferramentas como init de nuvem e modelos do Azure toomodify na VM com Linux no arranque.

[Sobre as funcionalidades e as extensões de máquina virtual](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Criação de modelos Azure Resource Manager com extensões de VM com Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Nuvem init toocustomize uma VM com Linux a utilizar durante a criação](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

