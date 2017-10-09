---
title: aaaAdd tooa um utilizador VM com Linux no Azure | Microsoft Docs
description: Adicione um utilizador tooa VM com Linux no Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Adicionar um utilizador tooan VM do Azure
Uma das tarefas primeiro Olá qualquer nova VM do Linux é toocreate um novo utilizador.  Neste artigo, iremos guiá-lo através da criação de uma conta de utilizador de sudo, a palavra-passe Olá definição adicionar SSH as chaves públicas e, finalmente, utilize `visudo` tooallow sudo sem uma palavra-passe.

Pré-requisitos são: [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/), [chaves públicas e privadas do SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), um grupo de recursos do Azure e Olá CLI do Azure instalados e mudada tooAzure Resource Manager utilizar o modo `azure config mode arm`.

## <a name="quick-commands"></a>Comandos Rápidos
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Instruções Detalhadas
### <a name="introduction"></a>Introdução
Uma das tarefas de primeira e mais comuns de Olá com um novo servidor é tooadd uma conta de utilizador.  Inícios de sessão de raiz devem ser desativados e conta de raiz de Olá propriamente dito não deve ser utilizada com o seu servidor Linux, apenas o sudo.  Dar um Escalamento de raiz do utilizador com privilégios utilizando sudo Olá tooadminister de forma adequada e utilizar Linux.

Utilizando o comando de Olá `useradd` que estamos a adicionar as contas de utilizador toohello VM com Linux.  Executar `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group`, e `/etc/gshadow`.  Que estamos a adicionar uma linha de comandos sinalizador toohello `useradd` comando tooalso adicionar Olá novo toohello sudo adequada grupo de utilizadores no Linux.  Mesmo thou `useradd` cria uma entrada para `/etc/passwd` -não conceder Olá nova conta de utilizador uma palavra-passe.  Estamos a criar uma palavra-passe inicial para o utilizador novo Olá utilizando Olá simples `passwd` comando.  último passo de Olá é toomodify Olá sudo regras tooallow comandos de tooexecute esse utilizador com privilégios sudo sem ter tooenter uma palavra-passe para cada comando.  Iniciar sessão com a chave privada Olá iremos são partindo do princípio de que conta de utilizador é seguro de mal-intencionadas e vai tooallow sudo acesso sem uma palavra-passe.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Adicionar um tooan de utilizador de sudo única VM do Azure
Inicie sessão no toohello VM do Azure com chaves SSH.  Se tiver não configuração SSH chave acesso público, concluir este artigo primeiro [utilizando a autenticação de chave pública com o Azure](http://link.to/article).  

Olá `useradd` comando for concluído Olá seguintes tarefas:

* criar uma nova conta de utilizador
* criar um novo grupo de utilizadores com Olá mesmo nome
* Adicionar uma entrada em branco demasiado`/etc/passwd`
* Adicionar uma entrada em branco demasiado`/etc/gpasswd`

Olá `-G` sinalizador da linha de comandos adiciona Olá novo utilizador conta toohello adequado grupo Linux conceder privilégios de escalamento de raiz de nova conta de utilizador Olá.

#### <a name="add-hello-user"></a>Adicionar utilizador Olá
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Definir uma palavra-passe
Olá `useradd` comando cria utilizador Olá e adiciona uma entrada tooboth `/etc/passwd` e `/etc/gpasswd` mas realmente não definir a palavra-passe de Olá.  Olá palavra-passe é adicionar toohello entrada utilizando Olá `passwd` comando.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Temos um utilizador com privilégios sudo agora no servidor de Olá.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Adicionar a chave pública SSH toohello nova conta de utilizador
A partir do seu computador, utilize Olá `ssh-copy-id` comando com a nova palavra-passe Olá.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Utilizando a utilização de sudo tooallow visudo sem uma palavra-passe
Utilizar `visudo` tooedit Olá `/etc/sudoers` ficheiro adiciona alguns camadas de proteção contra incorretamente modificar este ficheiro importante.  Após executar `visudo`, Olá `/etc/sudoers` ficheiro está bloqueado tooensure nenhum outro utilizador pode efetuar alterações ao ativamente está a ser editado.  Olá `/etc/sudoers` ficheiro também é analisado relativamente à prende por `visudo` quando tentam toosave ou sair, pelo que não é possível guardar um ficheiro de sudoers interrompida.

Temos já utilizadores no grupo de predefinição correto Olá para acesso de sudo.  Agora, vamos tooenable sudo de toouse esses grupos com nenhuma palavra-passe.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Certifique-se de utilizador de Olá, ssh chaves e sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
