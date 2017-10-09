---
title: par de chaves aaaCreate um SSH para VMs com Linux no Azure | Microsoft Docs
description: "Criar um par de chaves pública e privada SSH para as VMs do Azure Linux de forma segura."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="1d7d2-103">Criar um par de chaves pública e privada SSH para as VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="1d7d2-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="1d7d2-104">Este artigo mostra como toogenerate uma protocol versão 2 RSA pública e privada chave SSH ficheiro par toouse com VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="1d7d2-105">Com um par de chaves SSH, pode criar máquinas virtuais no Azure predefinido toousing chaves SSH para a autenticação, eliminando a necessidade de Olá de palavras-passe toolog no.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="1d7d2-106">As palavras-passe podem ser adivinhadas e abrir as suas VMs segurança toorelentless força bruta tentativas tooguess a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="1d7d2-107">VMs criadas com modelos do Azure ou Olá `azure-cli` podem incluir a chave pública SSH como parte da implementação de Olá, remover um passo de configuração de implementação de post da desativação de inícios de sessão de palavra-passe para SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1d7d2-108">Comandos Rápidos</span><span class="sxs-lookup"><span data-stu-id="1d7d2-108">Quick Commands</span></span>

<span data-ttu-id="1d7d2-109">Execute Olá os seguintes comandos da shell de deteção, substituindo os exemplos de Olá com as seus próprios opções.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="1d7d2-110">O ficheiro de chave pública SSH é criado por predefinição em `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="1d7d2-111">Quando lhe for pedido Olá os seguintes comandos a utilizar, deve criar uma "frase de acesso" toosecure a chave privada.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="1d7d2-112">(o frase de acesso de Olá é que uma palavra-passe utilizada tooencrypt a chave privada.)</span><span class="sxs-lookup"><span data-stu-id="1d7d2-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="1d7d2-113">Adicionar chave de Olá recém-criado demasiado`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="1d7d2-114">Olá acima trabalho comandos em sistemas operativos Linux quase todas as distribuições, mas não necessariamente funcionam nos contentores, como o ambiente de Olá pode forma radicalmente restrita.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="1d7d2-115">Instruções Detalhadas</span><span class="sxs-lookup"><span data-stu-id="1d7d2-115">Detailed Walkthrough</span></span>

<span data-ttu-id="1d7d2-116">A utilização de chaves públicas e privadas de SSH é Olá toolog de forma mais fácil em servidores de Linux tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="1d7d2-117">[Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de forma muito mais segura no tooyour Linux ou na VM BSD no Azure que as palavras-passe, que podem ser ataque de força bruta mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d7d2-118">A sua chave pública pode ser partilhada com qualquer pessoa; mas apenas o utilizador (ou a infraestrutura de segurança local) possui a chave privada.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="1d7d2-119">a chave privada SSH Olá deve ter um [palavra-passe muito segura](https://www.xkcd.com/936/) (origem:[xkcd.com](https://xkcd.com)) toosafeguard-lo.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="1d7d2-120">Esta palavra-passe é a chave privada de SSH do tooaccess apenas Olá e **não é** palavra-passe de conta de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="1d7d2-121">Quando adiciona uma chave SSH tooyour palavra-passe, encripta a chave privada Olá utilizando AES de 128 bits, para que hello chave privada é inútil sem Olá palavra-passe toodecrypt-lo.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="1d7d2-122">Se um atacante stole a chave privada e que a chave não tinha uma palavra-passe, este seria capaz de toouse ou privada chave toolog nos servidores de tooany ter Olá de chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="1d7d2-123">Se a chave privada for protegida por palavra-passe, não pode ser utilizada por esse atacante, fornecendo uma camada adicional de segurança à sua infraestrutura no Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="1d7d2-124">Este artigo cria a versão do protocolo SSH 2 RSA públicos e privados ficheiros de chaves, que são recomendados para implementações em Olá Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="1d7d2-125">*SSH-rsa* chaves são necessárias no Olá [portal](https://portal.azure.com) para implementações do Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="1d7d2-126">Desativar as palavras-passe SSH com as chaves SSH</span><span class="sxs-lookup"><span data-stu-id="1d7d2-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="1d7d2-127">O Azure requer, pelo menos, 2048 bits e chaves públicas e privadas com o formato ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="1d7d2-128">utilização de chaves toocreate Olá `ssh-keygen`, que pede-lhe uma série de perguntas e, em seguida, escreve uma chave privada e uma chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="1d7d2-129">Quando é criada uma VM do Azure, chave pública Olá é copiado demasiado`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="1d7d2-130">As chaves SSH no `~/.ssh/authorized_keys` são utilizados toochallenge Olá cliente toomatch Olá chave privada correspondente numa ligação de início de sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="1d7d2-131">Quando uma VM com Linux do Azure é criada a utilizar chaves SSH para a autenticação, o Azure configura Olá SSHD server toonot permite inícios de sessão de palavra-passe, apenas as chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="1d7d2-132">Por conseguinte, através da criação de VMs do Linux do Azure com chaves SSH, pode ajudar a implementação da VM Olá segura e guardar pessoalmente o passo de configuração pós-implementação típica Olá da desativação de palavras-passe no ficheiro de configuração de sshd_config Olá.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="1d7d2-133">Utilizar o ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1d7d2-133">Using ssh-keygen</span></span>

<span data-ttu-id="1d7d2-134">Este comando cria uma palavra-passe protegida (encriptado) par de chaves SSH com o RSA de 2048 bits e é comentado tooeasily identificá-lo.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="1d7d2-135">SSH chaves são por predefinição mantida na Olá `~/.ssh` diretório.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="1d7d2-136">Se não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando criá-lo por si com Olá permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="1d7d2-137">*Comando explicado*</span><span class="sxs-lookup"><span data-stu-id="1d7d2-137">*Command explained*</span></span>

<span data-ttu-id="1d7d2-138">`ssh-keygen`= Olá programa utilizado toocreate Olá chaves</span><span class="sxs-lookup"><span data-stu-id="1d7d2-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="1d7d2-139">`-t rsa`= o tipo de chave toocreate que é o formato RSA Olá [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="1d7d2-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="1d7d2-140">`-b 2048`= bits da chave de Olá</span><span class="sxs-lookup"><span data-stu-id="1d7d2-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="1d7d2-141">Portal clássico e certificados X.509</span><span class="sxs-lookup"><span data-stu-id="1d7d2-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="1d7d2-142">Se estiver a utilizar Olá Azure [portal clássico](https://manage.windowsazure.com/), necessita de certificados x. 509 para chaves SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="1d7d2-143">Não existem outros tipos de chaves públicas SSH permitidas, estas *devem* ser certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="1d7d2-144">toocreate um certificado x. 509 da sua chave privada de SSH-RSA existente:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="1d7d2-145">Implementação clássica com `asm`</span><span class="sxs-lookup"><span data-stu-id="1d7d2-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="1d7d2-146">Se estiver a utilizar clássico Olá implementar a modelo (gestão de serviço do Azure CLI `asm`), pode utilizar uma chave pública SSH-RSA ou um RFC4716 formatado chave num **. pem** contentor.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="1d7d2-147">chave pública Olá SSH-RSA é o que foi criado anteriormente no utilizando artigo `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="1d7d2-148">toocreate um RFC4716 formatado chave a partir de uma chave pública SSH:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="1d7d2-149">Exemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1d7d2-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="1d7d2-150">Ficheiros de chave guardados:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="1d7d2-151">nome do par de chaves de Olá para este artigo.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-151">hello key pair name for this article.</span></span>  <span data-ttu-id="1d7d2-152">Ter um par de chaves com o nome **id_rsa** Olá predefinido e algumas ferramentas podem contar Olá **id_rsa** nome de ficheiro de chave privada, de modo que é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="1d7d2-153">diretório de Olá `~/.ssh/` é Olá localização predefinida pares de chaves SSH e o ficheiro de configuração SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="1d7d2-154">Se não for especificado com um caminho completo, `ssh-keygen` irá criar chaves Olá no diretório de trabalho atual Olá, não Olá predefinido `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="1d7d2-155">Obter uma listagem de Olá `~/.ssh` diretório.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="1d7d2-156">Palavra-passe da chave:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="1d7d2-157">`ssh-keygen`refere-se a chave privada do tooa palavra-passe utilizada tooencrypt Olá como "uma frase de acesso."</span><span class="sxs-lookup"><span data-stu-id="1d7d2-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="1d7d2-158">É *vivamente* recomendado tooadd pares de chaves de tooyour uma frase de acesso.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="1d7d2-159">Sem uma frase de acesso proteção Olá chave privada, qualquer pessoa com o ficheiro de chave Olá pode utilizá-la toolog no servidor de tooany que tem Olá de chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="1d7d2-160">Adicionar uma frase de acesso oferece mais proteção no caso de alguém toogain capaz de acesso tooyour ficheiro de chave privada, dando-lhe as chaves do tempo toochange Olá utilizado tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="1d7d2-161">Utilizar o ssh-agent toostore a palavra-passe da chave privada</span><span class="sxs-lookup"><span data-stu-id="1d7d2-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="1d7d2-162">frase de acesso do ficheiro tooavoid escrever a sua chave privada com cada início de sessão SSH, pode utilizar `ssh-agent` toocache a palavra-passe do ficheiro de chave privada.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="1d7d2-163">Se estiver a utilizar um Mac, Olá OSX Keychain armazena Olá privada chave palavras-passe em segurança quando invocar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="1d7d2-164">Certifique-se e utilizar `ssh-agent` e `ssh-add` tooinform Olá SSH sistema sobre ficheiros de chave Olá, para que o frase de acesso de Olá não terá de toobe utilizado de forma interativa.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="1d7d2-165">Agora adicione chave privada Olá demasiado`ssh-agent` utilizando o comando de Olá `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="1d7d2-166">Olá chave palavra-passe privada está agora armazenado numa `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="1d7d2-167">Utilizar `ssh-copy-id` nova chave de tooinstall Olá</span><span class="sxs-lookup"><span data-stu-id="1d7d2-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="1d7d2-168">Se já tiver criado uma VM pode instalar Olá novo SSH pública chave tooyour VM com Linux com Olá comando a seguir, substituindo o nome de utilizador do Olá VM e o endereço do servidor Olá com os seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="1d7d2-169">Criar e configurar um ficheiro de configuração SSH</span><span class="sxs-lookup"><span data-stu-id="1d7d2-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="1d7d2-170">É uma melhor toocreate de prática e configurar um `~/.ssh/config` toospeed de ficheiro dos inícios de sessão e para otimizar o seu comportamento do cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="1d7d2-171">Olá seguinte exemplo mostra uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="1d7d2-172">Criar ficheiro de Olá</span><span class="sxs-lookup"><span data-stu-id="1d7d2-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="1d7d2-173">Edite Olá ficheiro tooadd Olá nova configuração de SSH:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="1d7d2-174">Ficheiro `~/.ssh/config` de exemplo:</span><span class="sxs-lookup"><span data-stu-id="1d7d2-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="1d7d2-175">Esta configuração SSH fornecem lhe secções para cada servidor tooenable cada toohave seu próprio par de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="1d7d2-176">Olá predefinições (`Host *`) são para quaisquer anfitriões que não corresponde a nenhum dos Olá anfitriões específicos superiores cópias de segurança no ficheiro de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="1d7d2-177">Ficheiro de configuração explicado</span><span class="sxs-lookup"><span data-stu-id="1d7d2-177">Config file explained</span></span>

<span data-ttu-id="1d7d2-178">`Host`= o nome de Olá do anfitrião de Olá a ser chamado no Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="1d7d2-179">`ssh fedora22`indica `SSH` valores de Olá toouse no bloco de definições de Olá etiquetadas `Host fedora22` Nota: anfitrião pode ser qualquer etiqueta que seja lógica para a sua utilização e não representa o nome do anfitrião real Olá de qualquer servidor.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="1d7d2-180">`Hostname 102.160.203.241`= o endereço IP de Olá ou nome DNS para o servidor de Olá acedido.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="1d7d2-181">`User ahmet`= toouse de conta de utilizador remoto Olá quando iniciam sessão no servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="1d7d2-182">`PubKeyAuthentication yes`= Indica a SSH pretende toouse um toolog de chave SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="1d7d2-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= a chave privada SSH Olá e correspondente toouse de chave pública para autenticação.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="1d7d2-184">SSH no Linux sem uma palavra-passe</span><span class="sxs-lookup"><span data-stu-id="1d7d2-184">SSH into Linux without a password</span></span>

<span data-ttu-id="1d7d2-185">Agora que tem um par de chaves SSH e um ficheiro de configuração SSH configurado, é capaz de toolog no tooyour VM com Linux rapidamente e em segurança.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="1d7d2-186">Olá pela primeira vez que iniciar a sessão no servidor de tooa utilizando um linhas de comandos de Olá chave SSH, para a frase de acesso de Olá para esse ficheiro de chave.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="1d7d2-187">Comando explicado</span><span class="sxs-lookup"><span data-stu-id="1d7d2-187">Command explained</span></span>

<span data-ttu-id="1d7d2-188">Quando `ssh fedora22` é executado SSH primeiro localiza e carrega todas as definições de Olá `Host fedora22` bloco e, em seguida, carrega todas Olá restantes definições do Olá último bloqueio, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d7d2-189">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="1d7d2-189">Next Steps</span></span>

<span data-ttu-id="1d7d2-190">Em seguida cópias de segurança é toocreate VMs do Linux do Azure utilizando Olá nova chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="1d7d2-191">As VMs do Azure que são criadas com uma chave pública SSH como início de sessão Olá melhor são protegidas que VMs criadas com o método de início de sessão predefinido de Olá, palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="1d7d2-192">As VMs do Azure criadas com chaves SSH são, por predefinição, configuradas com as palavras-passe desativadas, evitando tentativas de adivinhação forçadas.</span><span class="sxs-lookup"><span data-stu-id="1d7d2-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="1d7d2-193">Se necessitar de mais assistência na criação do par de chaves SSH ou necessitam de certificados adicionais, tais como para utilização com o portal clássico Olá, consulte [detalhadas pares de chaves SSH do passos toocreate e certificados](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="1d7d2-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="1d7d2-194">Criar uma VM do Linux segura com um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="1d7d2-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1d7d2-195">Criar uma VM com Linux segura utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1d7d2-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1d7d2-196">Criar uma VM com Linux segura utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1d7d2-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
