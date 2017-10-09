---
title: par de chaves aaaDetailed passos toocreate um SSH para VMs com Linux no Azure | Microsoft Docs
description: "Saiba mais passos adicionais toocreate um par de chaves público e privado SSH para VMs com Linux no Azure, juntamente com certificados específicos para os casos de utilização diferentes."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="724fb-103">Instruções detalhada sobre o toocreate um par de chaves SSH e certificados adicionais para uma VM com Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="724fb-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="724fb-104">Com um par de chaves SSH, pode criar máquinas virtuais no Azure predefinido toousing chaves SSH para a autenticação, eliminando a necessidade de Olá de palavras-passe toolog no.</span><span class="sxs-lookup"><span data-stu-id="724fb-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="724fb-105">As palavras-passe podem ser adivinhadas e abrir as suas VMs segurança toorelentless força bruta tentativas tooguess a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="724fb-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="724fb-106">VMs criadas com modelos de Olá CLI do Azure ou o Gestor de recursos podem incluir a chave pública SSH como parte da implementação de Olá, remover um passo de configuração de implementação de post da desativação de inícios de sessão de palavra-passe para SSH.</span><span class="sxs-lookup"><span data-stu-id="724fb-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="724fb-107">Este artigo fornece os passos detalhados e exemplos adicionais de geração de certificados, tal como para utilização com máquinas virtuais do Linux.</span><span class="sxs-lookup"><span data-stu-id="724fb-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="724fb-108">Se quiser tooquickly criar e utilizar um par de chaves SSH, consulte [como toocreate uma chave de pública e privada SSH emparelhe para VMs com Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="724fb-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="724fb-109">Noções sobre chaves SSH</span><span class="sxs-lookup"><span data-stu-id="724fb-109">Understanding SSH keys</span></span>

<span data-ttu-id="724fb-110">A utilização de chaves públicas e privadas de SSH é Olá toolog de forma mais fácil em servidores de Linux tooyour.</span><span class="sxs-lookup"><span data-stu-id="724fb-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="724fb-111">[Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de forma muito mais segura no tooyour Linux ou na VM BSD no Azure que as palavras-passe, que podem ser ataque de força bruta mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="724fb-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="724fb-112">A sua chave pública pode ser partilhada com qualquer pessoa; mas apenas o utilizador (ou a infraestrutura de segurança local) possui a chave privada.</span><span class="sxs-lookup"><span data-stu-id="724fb-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="724fb-113">a chave privada SSH Olá deve ter um [palavra-passe muito segura](https://www.xkcd.com/936/) (origem:[xkcd.com](https://xkcd.com)) toosafeguard-lo.</span><span class="sxs-lookup"><span data-stu-id="724fb-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="724fb-114">Esta palavra-passe é apenas tooaccess Olá SSH ficheiro de chave privada e **não é** palavra-passe de conta de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="724fb-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="724fb-115">Quando adiciona uma chave SSH tooyour palavra-passe, encripta a chave privada Olá utilizando AES de 128 bits, para que hello chave privada é inútil sem Olá palavra-passe toodecrypt-lo.</span><span class="sxs-lookup"><span data-stu-id="724fb-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="724fb-116">Se um atacante stole a chave privada e que a chave não tinha uma palavra-passe, este seria capaz de toouse ou privada chave toolog nos servidores de tooany ter Olá de chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="724fb-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="724fb-117">Se a chave privada for protegida por palavra-passe, não pode ser utilizada por esse atacante, fornecendo uma camada adicional de segurança à sua infraestrutura no Azure.</span><span class="sxs-lookup"><span data-stu-id="724fb-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="724fb-118">Este artigo cria uma versão de protocolo SSH que par de ficheiro de chave pública e privada do 2 RSA (também referida tooas "ssh-rsa" chaves), que é recomendados para implementações com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="724fb-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="724fb-119">*SSH-rsa* chaves são necessárias no Olá [portal](https://portal.azure.com) para implementações do Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="724fb-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="724fb-120">Utilização e vantagens das chaves SSH</span><span class="sxs-lookup"><span data-stu-id="724fb-120">SSH keys use and benefits</span></span>

<span data-ttu-id="724fb-121">O Azure requer, pelo menos, 2048 bits, o SSH protocolo versão 2 RSA formato chaves públicas e privadas; o ficheiro de chave pública Olá tem Olá `.pub` formato de contentor.</span><span class="sxs-lookup"><span data-stu-id="724fb-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="724fb-122">utilização de chaves toocreate Olá `ssh-keygen`, que pede-lhe uma série de perguntas e, em seguida, escreve uma chave privada e uma chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="724fb-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="724fb-123">Quando é criada uma VM do Azure, Azure cópias Olá toohello de chave pública `~/.ssh/authorized_keys` pasta Olá VM.</span><span class="sxs-lookup"><span data-stu-id="724fb-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="724fb-124">As chaves SSH no `~/.ssh/authorized_keys` são utilizados toochallenge Olá cliente toomatch Olá chave privada correspondente numa ligação de início de sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="724fb-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="724fb-125">Quando uma VM com Linux do Azure é criada a utilizar chaves SSH para a autenticação, o Azure configura Olá SSHD server toonot permite inícios de sessão de palavra-passe, apenas as chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="724fb-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="724fb-126">Por conseguinte, através da criação de VMs do Linux do Azure com chaves SSH, pode ajudar a proteger a implementação da VM Olá e guardar si próprio passo de configuração pós-implementação típica Olá da desativação de palavras-passe em Olá **sshd_config** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="724fb-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="724fb-127">Utilizar o ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="724fb-127">Using ssh-keygen</span></span>

<span data-ttu-id="724fb-128">Este comando cria uma palavra-passe protegida (encriptado) par de chaves SSH com o RSA de 2048 bits e é comentado tooeasily identificá-lo.</span><span class="sxs-lookup"><span data-stu-id="724fb-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="724fb-129">SSH chaves são por predefinição mantida na Olá `~/.ssh` diretório.</span><span class="sxs-lookup"><span data-stu-id="724fb-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="724fb-130">Se não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando criá-lo por si com Olá permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="724fb-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="724fb-131">*Comando explicado*</span><span class="sxs-lookup"><span data-stu-id="724fb-131">*Command explained*</span></span>

<span data-ttu-id="724fb-132">`ssh-keygen`= Olá programa utilizado toocreate Olá chaves</span><span class="sxs-lookup"><span data-stu-id="724fb-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="724fb-133">`-t rsa`= o tipo de chave toocreate que é o formato RSA Olá [wikipedia][parens no fim](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits da chave de Olá</span><span class="sxs-lookup"><span data-stu-id="724fb-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="724fb-134">`-C "azureuser@myserver"`= um comentário final toohello anexado tooeasily do ficheiro de chave pública de Olá identificá-lo.</span><span class="sxs-lookup"><span data-stu-id="724fb-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="724fb-135">Normalmente, uma mensagem de e-mail é utilizada como comentários de Olá, mas pode utilizar o que funciona melhor para a sua infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="724fb-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="724fb-136">Implementação clássica com `asm`</span><span class="sxs-lookup"><span data-stu-id="724fb-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="724fb-137">Se estiver a utilizar o modelo de implementação clássica Olá (`asm` modo no Olá CLI), pode utilizar uma chave pública SSH-RSA ou um RFC4716 formatado chave num contentor pem.</span><span class="sxs-lookup"><span data-stu-id="724fb-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="724fb-138">chave pública Olá SSH-RSA é o que foi criado anteriormente no utilizando artigo `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="724fb-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="724fb-139">toocreate um RFC4716 formatado chave a partir de uma chave pública SSH:</span><span class="sxs-lookup"><span data-stu-id="724fb-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="724fb-140">Exemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="724fb-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="724fb-141">Ficheiros de chave guardados:</span><span class="sxs-lookup"><span data-stu-id="724fb-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="724fb-142">nome do par de chaves de Olá para este artigo.</span><span class="sxs-lookup"><span data-stu-id="724fb-142">hello key pair name for this article.</span></span>  <span data-ttu-id="724fb-143">Ter um par de chaves com o nome **id_rsa** Olá predefinido e algumas ferramentas podem contar Olá **id_rsa** nome de ficheiro de chave privada, de modo que é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="724fb-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="724fb-144">diretório de Olá `~/.ssh/` é Olá localização predefinida pares de chaves SSH e o ficheiro de configuração SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="724fb-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="724fb-145">Se não for especificado com um caminho completo, `ssh-keygen` cria chaves Olá no diretório de trabalho atual Olá, não predefinido de Olá `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="724fb-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="724fb-146">Obter uma listagem de Olá `~/.ssh` diretório.</span><span class="sxs-lookup"><span data-stu-id="724fb-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="724fb-147">Palavra-passe da chave:</span><span class="sxs-lookup"><span data-stu-id="724fb-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="724fb-148">`ssh-keygen`refere-se a palavra-passe de tooa para o ficheiro de chave privada Olá como "uma frase de acesso."</span><span class="sxs-lookup"><span data-stu-id="724fb-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="724fb-149">É *vivamente* recomendado tooadd uma chave privada de tooyour de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="724fb-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="724fb-150">Sem um palavra-passe proteção Olá ficheiro de chave, qualquer pessoa com ficheiros Olá pode utilizá-la toolog no servidor de tooany que tem Olá de chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="724fb-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="724fb-151">Adicionar uma palavra-passe (frase de acesso) proporciona proteção mais no caso de alguém toogain capaz de acesso tooyour ficheiro de chave privada, dando-lhe as chaves do tempo toochange Olá utilizado tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="724fb-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="724fb-152">Utilizar o ssh-agent toostore a palavra-passe da chave privada</span><span class="sxs-lookup"><span data-stu-id="724fb-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="724fb-153">tooavoid escrever a palavra-passe do ficheiro de chave privada com cada início de sessão SSH, pode utilizar `ssh-agent` toocache a palavra-passe do ficheiro de chave privada.</span><span class="sxs-lookup"><span data-stu-id="724fb-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="724fb-154">Se estiver a utilizar um Mac, Olá OSX Keychain armazena Olá privada chave palavras-passe em segurança quando invocar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="724fb-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="724fb-155">Certifique-se e utilizar o ssh-agent e ssh-adicionar tooinform Olá SSH sistema sobre ficheiros de chave Olá, para que o frase de acesso de Olá não terá de toobe utilizado de forma interativa.</span><span class="sxs-lookup"><span data-stu-id="724fb-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="724fb-156">Agora adicione chave privada Olá demasiado`ssh-agent` utilizando o comando de Olá `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="724fb-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="724fb-157">Olá chave palavra-passe privada está agora armazenado numa `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="724fb-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="724fb-158">Utilizar `ssh-copy-id` toocopy Olá tooan chave existente VM</span><span class="sxs-lookup"><span data-stu-id="724fb-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="724fb-159">Se já tiver criado uma VM pode instalar Olá novo SSH pública chave tooyour VM com Linux com:</span><span class="sxs-lookup"><span data-stu-id="724fb-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="724fb-160">Criar e configurar um ficheiro de configuração SSH</span><span class="sxs-lookup"><span data-stu-id="724fb-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="724fb-161">É um toocreate de melhores práticas recomendadas e configurar um `~/.ssh/config` toospeed de ficheiro dos inícios de sessão e para otimizar o seu comportamento do cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="724fb-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="724fb-162">Olá seguinte exemplo mostra uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="724fb-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="724fb-163">Criar ficheiro de Olá</span><span class="sxs-lookup"><span data-stu-id="724fb-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="724fb-164">Edite Olá ficheiro tooadd Olá nova configuração de SSH:</span><span class="sxs-lookup"><span data-stu-id="724fb-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="724fb-165">Ficheiro `~/.ssh/config` de exemplo:</span><span class="sxs-lookup"><span data-stu-id="724fb-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="724fb-166">Esta configuração SSH fornecem lhe secções para cada servidor tooenable cada toohave seu próprio par de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="724fb-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="724fb-167">Olá predefinições (`Host *`) são para quaisquer anfitriões que não corresponde a nenhum dos Olá anfitriões específicos superiores cópias de segurança no ficheiro de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="724fb-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="724fb-168">Ficheiro de configuração explicado</span><span class="sxs-lookup"><span data-stu-id="724fb-168">Config file explained</span></span>

<span data-ttu-id="724fb-169">`Host`= o nome de Olá do anfitrião de Olá a ser chamado no Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="724fb-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="724fb-170">`ssh fedora22`indica `SSH` valores de Olá toouse no bloco de definições de Olá etiquetadas `Host fedora22` Nota: anfitrião pode ser qualquer etiqueta que seja lógica para a sua utilização e não representa o nome do anfitrião real Olá de qualquer servidor.</span><span class="sxs-lookup"><span data-stu-id="724fb-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="724fb-171">`Hostname 102.160.203.241`= o endereço IP de Olá ou nome DNS para o servidor de Olá acedido.</span><span class="sxs-lookup"><span data-stu-id="724fb-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="724fb-172">`User ahmet`= toouse de conta de utilizador remoto Olá quando iniciam sessão no servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="724fb-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="724fb-173">`PubKeyAuthentication yes`= Indica a SSH pretende toouse um toolog de chave SSH.</span><span class="sxs-lookup"><span data-stu-id="724fb-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="724fb-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= a chave privada SSH Olá e correspondente toouse de chave pública para autenticação.</span><span class="sxs-lookup"><span data-stu-id="724fb-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="724fb-175">SSH no Linux sem uma palavra-passe</span><span class="sxs-lookup"><span data-stu-id="724fb-175">SSH into Linux without a password</span></span>

<span data-ttu-id="724fb-176">Agora que tem um par de chaves SSH e um ficheiro de configuração SSH configurado, é capaz de toolog no tooyour VM com Linux rapidamente e em segurança.</span><span class="sxs-lookup"><span data-stu-id="724fb-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="724fb-177">Olá pela primeira vez que iniciar a sessão no servidor de tooa utilizando um linhas de comandos de Olá chave SSH, para a frase de acesso de Olá para esse ficheiro de chave.</span><span class="sxs-lookup"><span data-stu-id="724fb-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="724fb-178">Comando explicado</span><span class="sxs-lookup"><span data-stu-id="724fb-178">Command explained</span></span>

<span data-ttu-id="724fb-179">Quando `ssh fedora22` é executado SSH primeiro localiza e carrega todas as definições de Olá `Host fedora22` bloco e, em seguida, carrega todas Olá restantes definições do Olá último bloqueio, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="724fb-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="724fb-180">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="724fb-180">Next Steps</span></span>

<span data-ttu-id="724fb-181">Em seguida cópias de segurança é toocreate VMs do Linux do Azure utilizando Olá nova chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="724fb-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="724fb-182">As VMs do Azure que são criadas com uma chave pública SSH como início de sessão Olá melhor são protegidas que VMs criadas com o método de início de sessão predefinido de Olá, palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="724fb-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="724fb-183">As VMs do Azure criadas com chaves SSH são, por predefinição, configuradas com as palavras-passe desativadas, evitando tentativas de adivinhação forçadas.</span><span class="sxs-lookup"><span data-stu-id="724fb-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="724fb-184">Criar uma VM do Linux segura com um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="724fb-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="724fb-185">Criar uma VM com Linux segura utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="724fb-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="724fb-186">Criar uma VM com Linux segura utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="724fb-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
