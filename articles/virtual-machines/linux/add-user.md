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
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="8bbf1-103">Adicionar um utilizador tooan VM do Azure</span><span class="sxs-lookup"><span data-stu-id="8bbf1-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="8bbf1-104">Uma das tarefas primeiro Olá qualquer nova VM do Linux é toocreate um novo utilizador.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="8bbf1-105">Neste artigo, iremos guiá-lo através da criação de uma conta de utilizador de sudo, a palavra-passe Olá definição adicionar SSH as chaves públicas e, finalmente, utilize `visudo` tooallow sudo sem uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="8bbf1-106">Pré-requisitos são: [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/), [chaves públicas e privadas do SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), um grupo de recursos do Azure e Olá CLI do Azure instalados e mudada tooAzure Resource Manager utilizar o modo `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8bbf1-107">Comandos Rápidos</span><span class="sxs-lookup"><span data-stu-id="8bbf1-107">Quick Commands</span></span>
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

## <a name="detailed-walkthrough"></a><span data-ttu-id="8bbf1-108">Instruções Detalhadas</span><span class="sxs-lookup"><span data-stu-id="8bbf1-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="8bbf1-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="8bbf1-109">Introduction</span></span>
<span data-ttu-id="8bbf1-110">Uma das tarefas de primeira e mais comuns de Olá com um novo servidor é tooadd uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="8bbf1-111">Inícios de sessão de raiz devem ser desativados e conta de raiz de Olá propriamente dito não deve ser utilizada com o seu servidor Linux, apenas o sudo.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="8bbf1-112">Dar um Escalamento de raiz do utilizador com privilégios utilizando sudo Olá tooadminister de forma adequada e utilizar Linux.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="8bbf1-113">Utilizando o comando de Olá `useradd` que estamos a adicionar as contas de utilizador toohello VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="8bbf1-114">Executar `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group`, e `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="8bbf1-115">Que estamos a adicionar uma linha de comandos sinalizador toohello `useradd` comando tooalso adicionar Olá novo toohello sudo adequada grupo de utilizadores no Linux.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="8bbf1-116">Mesmo thou `useradd` cria uma entrada para `/etc/passwd` -não conceder Olá nova conta de utilizador uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="8bbf1-117">Estamos a criar uma palavra-passe inicial para o utilizador novo Olá utilizando Olá simples `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="8bbf1-118">último passo de Olá é toomodify Olá sudo regras tooallow comandos de tooexecute esse utilizador com privilégios sudo sem ter tooenter uma palavra-passe para cada comando.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="8bbf1-119">Iniciar sessão com a chave privada Olá iremos são partindo do princípio de que conta de utilizador é seguro de mal-intencionadas e vai tooallow sudo acesso sem uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="8bbf1-120">Adicionar um tooan de utilizador de sudo única VM do Azure</span><span class="sxs-lookup"><span data-stu-id="8bbf1-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="8bbf1-121">Inicie sessão no toohello VM do Azure com chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="8bbf1-122">Se tiver não configuração SSH chave acesso público, concluir este artigo primeiro [utilizando a autenticação de chave pública com o Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="8bbf1-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="8bbf1-123">Olá `useradd` comando for concluído Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="8bbf1-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="8bbf1-124">criar uma nova conta de utilizador</span><span class="sxs-lookup"><span data-stu-id="8bbf1-124">create a new user account</span></span>
* <span data-ttu-id="8bbf1-125">criar um novo grupo de utilizadores com Olá mesmo nome</span><span class="sxs-lookup"><span data-stu-id="8bbf1-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="8bbf1-126">Adicionar uma entrada em branco demasiado`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="8bbf1-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="8bbf1-127">Adicionar uma entrada em branco demasiado`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="8bbf1-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="8bbf1-128">Olá `-G` sinalizador da linha de comandos adiciona Olá novo utilizador conta toohello adequado grupo Linux conceder privilégios de escalamento de raiz de nova conta de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="8bbf1-129">Adicionar utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="8bbf1-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="8bbf1-130">Definir uma palavra-passe</span><span class="sxs-lookup"><span data-stu-id="8bbf1-130">Set a password</span></span>
<span data-ttu-id="8bbf1-131">Olá `useradd` comando cria utilizador Olá e adiciona uma entrada tooboth `/etc/passwd` e `/etc/gpasswd` mas realmente não definir a palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="8bbf1-132">Olá palavra-passe é adicionar toohello entrada utilizando Olá `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="8bbf1-133">Temos um utilizador com privilégios sudo agora no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="8bbf1-134">Adicionar a chave pública SSH toohello nova conta de utilizador</span><span class="sxs-lookup"><span data-stu-id="8bbf1-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="8bbf1-135">A partir do seu computador, utilize Olá `ssh-copy-id` comando com a nova palavra-passe Olá.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="8bbf1-136">Utilizando a utilização de sudo tooallow visudo sem uma palavra-passe</span><span class="sxs-lookup"><span data-stu-id="8bbf1-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="8bbf1-137">Utilizar `visudo` tooedit Olá `/etc/sudoers` ficheiro adiciona alguns camadas de proteção contra incorretamente modificar este ficheiro importante.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="8bbf1-138">Após executar `visudo`, Olá `/etc/sudoers` ficheiro está bloqueado tooensure nenhum outro utilizador pode efetuar alterações ao ativamente está a ser editado.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="8bbf1-139">Olá `/etc/sudoers` ficheiro também é analisado relativamente à prende por `visudo` quando tentam toosave ou sair, pelo que não é possível guardar um ficheiro de sudoers interrompida.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="8bbf1-140">Temos já utilizadores no grupo de predefinição correto Olá para acesso de sudo.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="8bbf1-141">Agora, vamos tooenable sudo de toouse esses grupos com nenhuma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8bbf1-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

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

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="8bbf1-142">Certifique-se de utilizador de Olá, ssh chaves e sudo</span><span class="sxs-lookup"><span data-stu-id="8bbf1-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
