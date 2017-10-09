---
title: "problemas de ligação de SSH aaaTroubleshoot tooan VM do Azure | Microsoft Docs"
description: "Como tootroubleshoot problemas, tais como 'falha de ligação SSH' ou ' SSH ligação recusada' para uma VM do Azure com o Linux."
keywords: "SSH ligação recusada, ssh erro, azure ssh, ligação SSH falhou"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Resolver problemas de SSH ligações tooan VM com Linux do Azure que falhe, erros de saída, ou é recusada
Existem várias razões se encontrar erros de Secure Shell (SSH), falhas de ligação de SSH, ou SSH é recusada quando tenta tooconnect tooa máquina de virtual com Linux (VM). Este artigo ajuda-o a localizar e problemas de Olá correto. Pode utilizar Olá portal do Azure, CLI do Azure ou a extensão de acesso de VM para tootroubleshoot de Linux e resolver problemas de ligação.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](http://azure.microsoft.com/support/forums/). Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](http://azure.microsoft.com/support/options/) e selecione **obter suporte**. Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Passos rápidos de resolução de problemas
Depois de cada passo de resolução de problemas, tente restabelecer a ligação toohello VM.

1. Repor a configuração de SSH Olá.
2. Repor Olá as credenciais de utilizador de Olá.
3. Certifique-se Olá [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) regras permitem tráfego SSH.
   * Certifique-se de que o grupo de segurança de rede existe uma regra de tráfego SSH toopermit (por predefinição, a porta TCP 22).
   * Não é possível utilizar o redirecionamento de porta / mapeamento sem utilizar um balanceador de carga do Azure.
4. Verifique Olá [estado de funcionamento de recursos VM](../../resource-health/resource-health-overview.md). 
   * Certifique-se de que Olá VM relatórios como estando em bom estado.
   * Se tiver de diagnóstico de arranque ativado, certifique-se de Olá VM não está a comunicar erros de arranque nos registos de Olá.
5. Reinicie Olá VM.
6. Reimplemente Olá VM.

Continue a ler para explicações e passos de resolução de problemas mais detalhados.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Problemas de ligação do métodos disponíveis tootroubleshoot SSH
Pode repor as credenciais ou configuração de SSH utilizando um dos seguintes métodos de Olá:

* [Portal do Azure](#use-the-azure-portal) - ótimo se precisar de tooquickly repor a configuração de SSH Olá ou chave SSH e não ter Olá instalar as ferramentas do Azure.
* [Azure CLI 2.0](#use-the-azure-cli-20) - se de que já está na linha de comandos Olá, rapidamente configuração de SSH Olá de reposição ou credenciais. Também pode utilizar Olá [CLI do Azure 1.0](#use-the-azure-cli-10)
* [Azure extensão VMAccessForLinux](#use-the-vmaccess-extension) - criar e reutilizar json definição ficheiros tooreset Olá utilizador ou de configuração de credenciais de SSH.

Depois de cada passo de resolução de problemas, tente ligar novamente tooyour VM. Se ainda não é possível estabelecer ligação, repita o passo seguinte Olá.

## <a name="use-hello-azure-portal"></a>Utilizar Olá portal do Azure
Olá portal do Azure fornece um Olá tooreset de forma rápida credenciais de utilizador ou de configuração de SSH sem instalar quaisquer ferramentas no seu computador local.

Selecione a VM Olá portal do Azure. Desloque para baixo toohello **suporte + resolução de problemas** secção e selecione **Repor palavra-passe** como no seguinte exemplo de Olá:

![Repor configuração SSH ou as credenciais no Olá portal do Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Repor a configuração de SSH Olá
Como primeiro passo, selecione `Reset configuration only` de Olá **modo** menu pendente de Olá anterior a captura de ecrã, em seguida, clique em Olá **repor** botão. Quando esta ação tiver sido concluída, repita tooaccess a VM.

### <a name="reset-ssh-credentials-for-a-user"></a>Repor as credenciais de SSH para um utilizador
as credenciais de Olá tooreset de um utilizador existente, selecione `Reset SSH public key` ou `Reset password` de Olá **modo** menu pendente que aparece Olá anterior a captura de ecrã. Especifique o nome de utilizador Olá e uma chave SSH ou nova palavra-passe, em seguida, clique em Olá **repor** botão.

Também pode criar um utilizador com privilégios sudo no Olá VM a partir deste menu. Introduza um novo nome de utilizador e palavra-passe associada ou chave SSH e, em seguida, clique em Olá **repor** botão.

## <a name="use-hello-azure-cli-20"></a>Utilizar Olá Azure CLI 2.0
Se ainda não o fez, instale Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login).

Se criar e carregar uma imagem de disco do Linux personalizada, certifique-se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado. Para VMs criadas com imagens Gallery, esta extensão de acesso já está instalado e configurado por si.

### <a name="reset-ssh-configuration"></a>Repor configuração SSH
Pode inicialmente tente repor Olá SSH toodefault dos valores de configuração e reiniciando Olá SSH servidor Olá VM. Tenha em atenção que isto não alterar o nome de conta de utilizador Olá, palavra-passe ou chaves SSH.
Olá exemplo seguinte utiliza [az vm utilizador reposição-ssh](/cli/azure/vm/user#reset-ssh) tooreset Olá SSH configuração Olá VM com o nome `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Repor as credenciais de SSH para um utilizador
Olá exemplo seguinte utiliza [atualização de utilizador de vm az](/cli/azure/vm/user#update) tooreset Olá credenciais para `myUsername` toohello o valor especificado na `myPassword`, na VM com o nome de Olá `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Se utilizar a autenticação de chave SSH, pode repor a chave SSH Olá para um determinado utilizador. Olá exemplo seguinte utiliza **az vm acesso de utilizador do linux do conjunto** tooupdate Olá SSH chave armazenada num `~/.ssh/id_rsa.pub` para com o nome de utilizador de Olá `myUsername`, na VM com o nome de Olá `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Utilizar Olá VMAccess extensão
lê Olá extensão de acesso de VM para Linux num ficheiro json que define ações toocarry enviados. Estas ações incluem repor SSHD, repor uma chave SSH ou adicionar um utilizador. Continuar a utilizar Olá de toocall Olá CLI do Azure extensão VMAccess, mas pode reutilizar ficheiros json de Olá através de várias VMs se assim o desejar. Esta abordagem permite-lhe toocreate um repositório de ficheiros json que pode ser chamado para fornecido cenários.

### <a name="reset-sshd"></a>Repor SSHD
Crie um ficheiro denominado `settings.json` com Olá seguinte conteúdo:

```json
{  
    "reset_ssh":"True"
}
```

Utilizar Olá CLI do Azure,, em seguida, chame Olá `VMAccessForLinux` extensão tooreset a ligação de SSHD especificando o ficheiro json. Olá exemplo seguinte utiliza [conjunto de extensão de vm az](/cli/azure/vm/extension#set) tooreset SSHD na VM com o nome de Olá `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Repor as credenciais de SSH para um utilizador
Se SSHD aparece toofunction corretamente, pode redefini Olá as credenciais para um utilizador giver. palavra-passe Olá de tooreset para um utilizador, crie um ficheiro denominado `settings.json`. Olá exemplo seguinte repõe as credenciais Olá `myUsername` toohello o valor especificado na `myPassword`. Introduza Olá seguintes linhas no seu `settings.json` ficheiro, utilizando os seus próprios valores:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Ou tooreset Olá chave SSH para um utilizador, primeiro crie um ficheiro denominado `settings.json`. Olá exemplo seguinte repõe as credenciais Olá `myUsername` toohello o valor especificado na `myPassword`, na VM com o nome de Olá `myVM` no `myResourceGroup`. Introduza Olá seguintes linhas no seu `settings.json` ficheiro, utilizando os seus próprios valores:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Depois de criar o ficheiro json, utilize Olá do Olá CLI do Azure toocall `VMAccessForLinux` tooreset extensão, as credenciais do utilizador do SSH, especificando o ficheiro json. Olá exemplo seguinte repõe as credenciais no Olá VM com o nome `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Utilizar Olá CLI do Azure 1.0
Se ainda não o fez, [instalar Olá CLI do Azure 1.0 e ligar tooyour subscrição do Azure](../../cli-install-nodejs.md). Certifique-se de que estiver a utilizar o modo Resource Manager da seguinte forma:

```azurecli
azure config mode arm
```

Se criar e carregar uma imagem de disco do Linux personalizada, certifique-se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado. Para VMs criadas com imagens Gallery, esta extensão de acesso já está instalado e configurado por si.

### <a name="reset-ssh-configuration"></a>Repor configuração SSH
configuração de SSHD Olá próprio pode estar configurado incorretamente ou Olá serviço encontrou um erro. Só pode repor SSHD toomake se configuração de SSH Olá em si é válida. Repor SSHD deve ser Olá primeiro resolução de problemas passo que tomar.

Olá exemplo seguinte repõe SSHD numa VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`. Utilize os seus próprios nomes de grupo de recursos e de VM da seguinte forma:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Repor as credenciais de SSH para um utilizador
Se SSHD aparece toofunction corretamente, pode redefini Olá palavra-passe para um utilizador giver. Olá exemplo seguinte repõe as credenciais Olá `myUsername` toohello o valor especificado na `myPassword`, na VM com o nome de Olá `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Se utilizar a autenticação de chave SSH, pode repor a chave SSH Olá para um determinado utilizador. Olá seguintes atualizações de exemplo Olá SSH chave armazenada num `~/.ssh/id_rsa.pub` para com o nome de utilizador de Olá `myUsername`, na VM com o nome de Olá `myVM` no `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Reiniciar uma VM
Se tiver de repor as credenciais de utilizador e a configuração de SSH do Olá ou encontrou um erro na fazê-lo, pode tentar reiniciar Olá VM tooaddress subjacente problemas de computação.

### <a name="azure-portal"></a>Portal do Azure
toorestart uma VM utilizando Olá do Azure selecione portal, a VM e clique em Olá **reiniciar** botão como no seguinte exemplo de Olá:

![Reiniciar uma VM no Olá portal do Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>CLI do Azure 1.0
Olá reinícios de exemplo a seguir Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>CLI 2.0 do Azure
Olá exemplo seguinte utiliza [reinício de vm az](/cli/azure/vm#restart) toorestart Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Reimplementar uma VM
Pode voltar a implementar um nó de tooanother VM no Azure, o que poderá corrigir problemas de rede subjacentes. Para obter informações sobre voltar a implementar uma VM, consulte [Reimplementar toonew de máquina virtual do Azure nó](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Depois de concluída esta operação, dados do disco efémeras serão perdidos e endereços IP dinâmicos que estão associados a máquina virtual de Olá serão atualizados.
> 
> 

### <a name="azure-portal"></a>Portal do Azure
tooredeploy uma VM utilizando hello do Azure selecione portal, a VM e desloque para baixo toohello **suporte + resolução de problemas** secção. Clique em Olá **Reimplementar** botão como no seguinte exemplo de Olá:

![Volte a implementar uma VM no Olá portal do Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>CLI do Azure 1.0
Olá seguir redeploys exemplo Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>CLI 2.0 do Azure
Olá seguinte exemplo, utilize [volte a implementar az vm](/cli/azure/vm#redeploy) tooredeploy Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`. Utilize os seus próprios valores da seguinte forma:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>VMs criadas utilizando o modelo de implementação clássica Olá
Repita estes passos tooresolve Olá mais comuns SSH falhas de ligação para VMs que foram criadas utilizando o modelo de implementação clássica Olá. Depois de cada passo, tente restabelecer a ligação toohello VM.

* Reponha o acesso remoto de Olá [portal do Azure](https://portal.azure.com). No Olá portal do Azure, selecione a VM e clique em Olá **repor remoto...**  botão.
* Reinicie Olá VM. No Olá [portal do Azure](https://portal.azure.com), selecione a VM e clique em Olá **reiniciar** botão.
    
* Reimplemente Olá VM tooa novo Azure nó. Para obter informações sobre como tooredeploy uma VM, consulte [Reimplementar toonew de máquina virtual do Azure nó](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Depois de concluída esta operação, dados do disco efémeras serão perdidos e endereços IP dinâmicos que estão associados a máquina virtual de Olá serão atualizados.
* Siga as instruções de Olá em [como tooreset uma palavra-passe ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:
  
  * Olá de reposição de palavra-passe ou chave SSH.
  * Criar um *sudo* conta de utilizador.
  * Repor a configuração de SSH Olá.
* Verificar o estado de funcionamento de recursos de uma VM Olá para quaisquer problemas de plataforma.<br>
     Selecione a VM e desloque para baixo **definições** > **verificar o estado de funcionamento**.

## <a name="additional-resources"></a>Recursos adicionais
* Se ainda não é possível tooSSH tooyour VM após seguinte Olá após passos, consulte o artigo [mais passos de resolução de problemas](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview adicional passos tooresolve seu problema.
* Para obter mais informações sobre resolução de problemas de acesso de aplicação, consulte [aplicação tooan acesso de resolução de problemas em execução numa máquina virtual do Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Para obter mais informações sobre resolução de problemas de máquinas virtuais que foram criadas utilizando o modelo de implementação clássica Olá, consulte [como tooreset uma palavra-passe ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

