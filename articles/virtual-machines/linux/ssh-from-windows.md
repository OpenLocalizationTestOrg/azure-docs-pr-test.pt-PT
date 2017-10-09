---
title: as chaves de aaaUse SSH com o Windows para VMs com Linux | Microsoft Docs
description: "Saiba como chaves toogenerate e utilizar SSH no computador tooconnect tooa Linux máquina virtual do Windows no Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a><span data-ttu-id="974a9-103">Como chaves de tooUse SSH com o Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="974a9-103">How tooUse SSH keys with Windows on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="974a9-104">Windows</span><span class="sxs-lookup"><span data-stu-id="974a9-104">Windows</span></span>](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [<span data-ttu-id="974a9-105">Linux/Mac</span><span class="sxs-lookup"><span data-stu-id="974a9-105">Linux/Mac</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

<span data-ttu-id="974a9-106">Quando se liga tooLinux as máquinas virtuais (VMs) no Azure, deve utilizar [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide um toolog de forma mais segura no tooyour VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="974a9-106">When you connect tooLinux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide a more secure way toolog in tooyour Linux VM.</span></span> <span data-ttu-id="974a9-107">Este processo envolve uma troca de chaves pública e privada através de Olá secure shell (SSH) comando tooauthenticate por si em vez de um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="974a9-107">This process involves a public and private key exchange using hello secure shell (SSH) command tooauthenticate yourself rather than a username and password.</span></span> <span data-ttu-id="974a9-108">Palavras-passe são vulneráveis toobrute-force ataques, especialmente em VMs de acesso à Internet, tais como servidores web.</span><span class="sxs-lookup"><span data-stu-id="974a9-108">Passwords are vulnerable toobrute-force attacks, especially on Internet-facing VMs such as web servers.</span></span> <span data-ttu-id="974a9-109">Este artigo fornece uma descrição geral de chaves SSH e como toogenerate Olá chaves adequadas num computador Windows.</span><span class="sxs-lookup"><span data-stu-id="974a9-109">This article provides an overview of SSH keys and how toogenerate hello appropriate keys on a Windows computer.</span></span>

## <a name="overview-of-ssh-and-keys"></a><span data-ttu-id="974a9-110">Descrição geral de SSH e chaves</span><span class="sxs-lookup"><span data-stu-id="974a9-110">Overview of SSH and keys</span></span>
<span data-ttu-id="974a9-111">Pode iniciar com segurança no tooyour VM com Linux através da utilização de chaves públicas e privadas:</span><span class="sxs-lookup"><span data-stu-id="974a9-111">You can securely log in tooyour Linux VM by using public and private keys:</span></span>

* <span data-ttu-id="974a9-112">Olá **chave pública** é colocada na VM com Linux ou qualquer outro serviço que quiser toouse com a criptografia de chave pública.</span><span class="sxs-lookup"><span data-stu-id="974a9-112">hello **public key** is placed on your Linux VM, or any other service that you wish toouse with public-key cryptography.</span></span>
* <span data-ttu-id="974a9-113">Olá **chave privada** é que tooyour presente VM com Linux quando iniciar sessão, tooverify sua identidade.</span><span class="sxs-lookup"><span data-stu-id="974a9-113">hello **private key** is what you present tooyour Linux VM when you log in, tooverify your identity.</span></span> <span data-ttu-id="974a9-114">Proteja esta chave privada.</span><span class="sxs-lookup"><span data-stu-id="974a9-114">Protect this private key.</span></span> <span data-ttu-id="974a9-115">Não a partilhe.</span><span class="sxs-lookup"><span data-stu-id="974a9-115">Do not share it.</span></span>

<span data-ttu-id="974a9-116">Estas chaves públicas e privadas podem ser utilizados em várias VMs e serviços.</span><span class="sxs-lookup"><span data-stu-id="974a9-116">These public and private keys can be used on multiple VMs and services.</span></span> <span data-ttu-id="974a9-117">Não é necessário um par de chaves para cada VM ou serviço pretende tooaccess.</span><span class="sxs-lookup"><span data-stu-id="974a9-117">You do not need a pair of keys for each VM or service you wish tooaccess.</span></span> <span data-ttu-id="974a9-118">Para obter uma descrição mais detalhada, consulte [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography).</span><span class="sxs-lookup"><span data-stu-id="974a9-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="974a9-119">SSH é um protocolo de ligação encriptada que permite que os inícios de sessão seguros através de ligações não segura.</span><span class="sxs-lookup"><span data-stu-id="974a9-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span></span> <span data-ttu-id="974a9-120">É Olá predefinido protocolo para VMs com Linux alojados no Azure.</span><span class="sxs-lookup"><span data-stu-id="974a9-120">It is hello default connection protocol for Linux VMs hosted in Azure.</span></span> <span data-ttu-id="974a9-121">Apesar de SSH próprio fornece uma ligação encriptada, ainda utilizar palavras-passe com ligações SSH deixa Olá VM vulnerável toobrute-force ataques ou deteção de palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="974a9-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves hello VM vulnerable toobrute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="974a9-122">Um método mais seguro e preferencial de ligação tooa VM utilizando o SSH é utilizar estas chaves públicas e privadas, também conhecido como as chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="974a9-122">A more secure and preferred method of connecting tooa VM using SSH is by using these public and private keys, also known as SSH keys.</span></span>

<span data-ttu-id="974a9-123">Se não desejar toouse chaves SSH, pode ainda iniciar sessão no tooyour VMs com Linux utilizando uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="974a9-123">If you do not wish toouse SSH keys, you can still log in tooyour Linux VMs using a password.</span></span> <span data-ttu-id="974a9-124">Se a VM não for toohello exposto à Internet, a utilização de palavras-passe pode ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="974a9-124">If your VM is not exposed toohello Internet, using passwords may be sufficient.</span></span> <span data-ttu-id="974a9-125">No entanto, é ainda necessário toomanage as palavras-passe para cada VM com Linux e manter políticas de palavra-passe bom estado de funcionamento e práticas, como o comprimento mínimo da palavra-passe e a atualizar regularmente-los.</span><span class="sxs-lookup"><span data-stu-id="974a9-125">However, you still need toomanage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span></span> <span data-ttu-id="974a9-126">utilização de Olá de chaves SSH reduz o complexidade Olá da gestão de credenciais individuais através de várias VMs.</span><span class="sxs-lookup"><span data-stu-id="974a9-126">hello use of SSH keys reduces hello complexity of managing individual credentials across multiple VMs.</span></span>

## <a name="windows-packages-and-ssh-clients"></a><span data-ttu-id="974a9-127">Pacotes do Windows e clientes SSH</span><span class="sxs-lookup"><span data-stu-id="974a9-127">Windows packages and SSH clients</span></span>
<span data-ttu-id="974a9-128">Ligar tooand gerir VMs com Linux no Azure com um **cliente SSH**.</span><span class="sxs-lookup"><span data-stu-id="974a9-128">You connect tooand manage Linux VMs in Azure using an **SSH client**.</span></span> <span data-ttu-id="974a9-129">Computadores com o Windows não têm, normalmente, um cliente SSH instalado.</span><span class="sxs-lookup"><span data-stu-id="974a9-129">Windows computers do not typically have an SSH client installed.</span></span> <span data-ttu-id="974a9-130">Olá Windows 10 aniversário da atualização adicionados Bash para Windows e hello mais recente do Windows 10 criadores Update fornece atualizações adicionais.</span><span class="sxs-lookup"><span data-stu-id="974a9-130">hello Windows 10 Anniversary Update added Bash for Windows, and hello latest Windows 10 Creators Update provides additional updates.</span></span> <span data-ttu-id="974a9-131">Este subsistema Windows para Linux permite-lhe utilitários toorun e o acesso, por exemplo, um cliente SSH nativamente dentro de uma shell de deteção.</span><span class="sxs-lookup"><span data-stu-id="974a9-131">This Windows Subsystem for Linux allows you toorun and access utilities such as an SSH client natively within a Bash shell.</span></span> <span data-ttu-id="974a9-132">Pode seguir qualquer um dos documentos de Linux Olá, em seguida, como [como toogenerate SSH chave combinada para Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="974a9-132">You can then follow any of hello Linux docs, such as [How toogenerate SSH key pairs for Linux](mac-create-ssh-keys.md).</span></span> <span data-ttu-id="974a9-133">Bash para Windows está ainda em desenvolvimento e é considerado uma versão beta.</span><span class="sxs-lookup"><span data-stu-id="974a9-133">Bash for Windows is still under development, and is considered a beta release.</span></span> <span data-ttu-id="974a9-134">Para mais informações sobre Bash para Windows, consulte [Bash no Ubuntu no Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="974a9-134">For more information about Bash for Windows, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="974a9-135">Se desejar toouse algo que não sejam Bash para Windows, comuns SSH do Windows que pode instalar forem incluídos clientes em Olá os seguintes pacotes:</span><span class="sxs-lookup"><span data-stu-id="974a9-135">If you wish toouse something other than Bash for Windows, common Windows SSH clients you can install are included in hello following packages:</span></span>

* [<span data-ttu-id="974a9-136">Git para Windows</span><span class="sxs-lookup"><span data-stu-id="974a9-136">Git For Windows</span></span>](https://git-for-windows.github.io/)
* [<span data-ttu-id="974a9-137">puTTY</span><span class="sxs-lookup"><span data-stu-id="974a9-137">puTTY</span></span>](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [<span data-ttu-id="974a9-138">MobaXterm</span><span class="sxs-lookup"><span data-stu-id="974a9-138">MobaXterm</span></span>](http://mobaxterm.mobatek.net/)
* [<span data-ttu-id="974a9-139">Cygwin</span><span class="sxs-lookup"><span data-stu-id="974a9-139">Cygwin</span></span>](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a><span data-ttu-id="974a9-140">Ficheiros de chave que necessita de toocreate?</span><span class="sxs-lookup"><span data-stu-id="974a9-140">Which key files do you need toocreate?</span></span>
<span data-ttu-id="974a9-141">O Azure requer, pelo menos, 2048 bits, **ssh-rsa** formatado chaves públicas e privadas.</span><span class="sxs-lookup"><span data-stu-id="974a9-141">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span></span> <span data-ttu-id="974a9-142">Se estiver a gerir os recursos do Azure utilizando o modelo de implementação clássica Olá, terá também de toogenerate um PEM (`.pem` ficheiro).</span><span class="sxs-lookup"><span data-stu-id="974a9-142">If you are managing Azure resources using hello Classic deployment model, you also need toogenerate a PEM (`.pem` file).</span></span>

<span data-ttu-id="974a9-143">Seguem-se cenários de implementação de Olá e Olá tipos de ficheiros que utilizam em cada:</span><span class="sxs-lookup"><span data-stu-id="974a9-143">Here are hello deployment scenarios, and hello types of files you use in each:</span></span>

1. <span data-ttu-id="974a9-144">**SSH-rsa** chaves são necessárias para qualquer implementação utilizando Olá [portal do Azure](https://portal.azure.com)e implementações do Resource Manager utilizando Olá [CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="974a9-144">**ssh-rsa** keys are required for any deployment using hello [Azure portal](https://portal.azure.com), and Resource Manager deployments using hello [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="974a9-145">Estas chaves são normalmente, todos os maioria das pessoas ter.</span><span class="sxs-lookup"><span data-stu-id="974a9-145">These keys are usually all most people need.</span></span>
2. <span data-ttu-id="974a9-146">A `.pem` ficheiro é VMs toocreate necessárias utilizando a implementação do Olá clássico.</span><span class="sxs-lookup"><span data-stu-id="974a9-146">A `.pem` file is required toocreate VMs using hello Classic deployment.</span></span> <span data-ttu-id="974a9-147">Estas chaves são suportadas em implementações clássicas quando Olá [portal do Azure](https://portal.azure.com) ou [CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="974a9-147">These keys are supported in Classic deployments when using hello [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="974a9-148">Basta toocreate estas chaves adicionais e certificados se estiver a gerir os recursos criados utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="974a9-148">You only need toocreate these additional keys and certificates if you are managing resources created using hello Classic deployment model.</span></span>

## <a name="install-git-for-windows"></a><span data-ttu-id="974a9-149">Instalar o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="974a9-149">Install Git for Windows</span></span>
<span data-ttu-id="974a9-150">Olá secção anterior vários pacotes listados que incluem Olá `openssl` ferramenta para o Windows.</span><span class="sxs-lookup"><span data-stu-id="974a9-150">hello preceding section listed several packages that include hello `openssl` tool for Windows.</span></span> <span data-ttu-id="974a9-151">Esta ferramenta é chaves públicas e privadas de toocreate necessários.</span><span class="sxs-lookup"><span data-stu-id="974a9-151">This tool is needed toocreate public and private keys.</span></span> <span data-ttu-id="974a9-152">Olá, como os seguintes detalhes de exemplos tooinstall e utilizar **Git para Windows**, embora pode escolher qualquer pacote que preferir.</span><span class="sxs-lookup"><span data-stu-id="974a9-152">hello following examples detail how tooinstall and use **Git for Windows**, though you can choose whichever package you prefer.</span></span> <span data-ttu-id="974a9-153">**Git para Windows** dá-lhe acesso toosome o software open source adicional ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) ferramentas e utilitários que poderão ser útil à medida que trabalha com VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="974a9-153">**Git for Windows** gives you access toosome additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span></span>

1. <span data-ttu-id="974a9-154">Transfira e instale **Git para Windows** de Olá seguinte localização: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span><span class="sxs-lookup"><span data-stu-id="974a9-154">Download and install **Git for Windows** from hello following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span></span>
2. <span data-ttu-id="974a9-155">Aceitar o processo de instalação de opções predefinidas de Olá durante Olá não ser que necessite especificamente toochange-los.</span><span class="sxs-lookup"><span data-stu-id="974a9-155">Accept hello default options during hello install process unless you specifically need toochange them.</span></span>
3. <span data-ttu-id="974a9-156">Executar **Git Bash** de Olá **Menu Iniciar** > **Git** > **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="974a9-156">Run **Git Bash** from hello **Start Menu** > **Git** > **Git Bash**.</span></span> <span data-ttu-id="974a9-157">consola de Olá procura toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="974a9-157">hello console looks similar toohello following example:</span></span>

    ![Git para Windows Bash shell](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a><span data-ttu-id="974a9-159">Criar uma chave privada</span><span class="sxs-lookup"><span data-stu-id="974a9-159">Create a private key</span></span>
1. <span data-ttu-id="974a9-160">No seu **Git Bash** janela, utilize `openssl.exe` toocreate uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="974a9-160">In your **Git Bash** window, use `openssl.exe` toocreate a private key.</span></span> <span data-ttu-id="974a9-161">Olá exemplo seguinte cria uma chave denominada `myPrivateKey` e o certificado com o nome `myCert.pem`:</span><span class="sxs-lookup"><span data-stu-id="974a9-161">hello following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span></span>

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    <span data-ttu-id="974a9-162">saída de Olá procura toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="974a9-162">hello output looks similar toohello following example:</span></span>

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   <span data-ttu-id="974a9-163">Se bash reportar um erro, tente abrir um novo **Git Bash** janela com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="974a9-163">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span></span> <span data-ttu-id="974a9-164">Em seguida, volte a executar Olá `openssl` comando.</span><span class="sxs-lookup"><span data-stu-id="974a9-164">Then, rerun hello `openssl` command.</span></span>

2. <span data-ttu-id="974a9-165">Olá resposta solicita o nome do país, localização, nome da organização, etc.</span><span class="sxs-lookup"><span data-stu-id="974a9-165">Answer hello prompts for country name, location, organization name, etc.</span></span>
3. <span data-ttu-id="974a9-166">A nova chave privada e certificado são criados no seu diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="974a9-166">Your new private key and certificate are created in your current working directory.</span></span> <span data-ttu-id="974a9-167">Como medida de segurança, deve definir permissões de Olá na sua chave privada para que apenas tem acesso:</span><span class="sxs-lookup"><span data-stu-id="974a9-167">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. <span data-ttu-id="974a9-168">Olá [secção seguinte](#create-a-private-key-for-putty) detalhes utilizando PuTTYgen tooboth ver e utilizar a chave pública Olá e criar uma chave privada específico para utilizar o PuTTY tooSSH tooLinux VMs.</span><span class="sxs-lookup"><span data-stu-id="974a9-168">hello [next section](#create-a-private-key-for-putty) details using PuTTYgen tooboth view and use hello public key, and create a private key specific for using PuTTY tooSSH tooLinux VMs.</span></span> <span data-ttu-id="974a9-169">Olá seguinte comando gera um ficheiro de chave pública nomeado `myPublicKey.key` que pode utilizar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="974a9-169">hello following command generates a public key file named `myPublicKey.key` that you can use right away:</span></span>

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. <span data-ttu-id="974a9-170">Se precisar de recursos de clássico toomanage também, converter Olá `myCert.pem` demasiado`myCert.cer` (DER codificado X509 certificado).</span><span class="sxs-lookup"><span data-stu-id="974a9-170">If you also need toomanage Classic resources, convert hello `myCert.pem` too`myCert.cer` (DER encoded X509 certificate).</span></span> <span data-ttu-id="974a9-171">Execute este passo opcional apenas se precisar de toospecifically gerir recursos de clássico mais antigos.</span><span class="sxs-lookup"><span data-stu-id="974a9-171">Perform this optional step only if you need toospecifically manage older Classic resources.</span></span>

    <span data-ttu-id="974a9-172">Converter o certificado de Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="974a9-172">Convert hello certificate using hello following command:</span></span>

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a><span data-ttu-id="974a9-173">Criar uma chave privada para o PuTTY</span><span class="sxs-lookup"><span data-stu-id="974a9-173">Create a private key for PuTTY</span></span>
<span data-ttu-id="974a9-174">PuTTY for um cliente SSH comuns para o Windows.</span><span class="sxs-lookup"><span data-stu-id="974a9-174">PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="974a9-175">É gratuita toouse qualquer cliente SSH que desejar.</span><span class="sxs-lookup"><span data-stu-id="974a9-175">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="974a9-176">toouse PuTTY, terá de toocreate um tipo de chave - uma chave privada PuTTY (PPK) adicional.</span><span class="sxs-lookup"><span data-stu-id="974a9-176">toouse PuTTY, you need toocreate an additional type of key - a PuTTY Private Key (PPK).</span></span> <span data-ttu-id="974a9-177">Se não desejar toouse PuTTY, ignore esta secção.</span><span class="sxs-lookup"><span data-stu-id="974a9-177">If you do not wish toouse PuTTY, skip this section.</span></span>

<span data-ttu-id="974a9-178">Olá exemplo seguinte cria esta chave privada adicional especificamente para PuTTY toouse:</span><span class="sxs-lookup"><span data-stu-id="974a9-178">hello following example creates this additional private key specifically for PuTTY toouse:</span></span>

1. <span data-ttu-id="974a9-179">Utilize **Git Bash** tooconvert privada da sua chave para uma chave privada RSA que possa compreender PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="974a9-179">Use **Git Bash** tooconvert your private key into an RSA private key that PuTTYgen can understand.</span></span> <span data-ttu-id="974a9-180">Olá exemplo seguinte cria uma chave denominada `myPrivateKey_rsa` da chave existente Olá denominado `myPrivateKey`:</span><span class="sxs-lookup"><span data-stu-id="974a9-180">hello following example creates a key named `myPrivateKey_rsa` from hello existing key named `myPrivateKey`:</span></span>

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    <span data-ttu-id="974a9-181">Como medida de segurança, deve definir permissões de Olá na sua chave privada para que apenas tem acesso:</span><span class="sxs-lookup"><span data-stu-id="974a9-181">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. <span data-ttu-id="974a9-182">Transferir e executar PuTTYgen de Olá seguinte localização: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="974a9-182">Download and run PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
3. <span data-ttu-id="974a9-183">Clique em menu Olá: **ficheiro** > **chave privada de carga**</span><span class="sxs-lookup"><span data-stu-id="974a9-183">Click hello menu: **File** > **Load Private Key**</span></span>
4. <span data-ttu-id="974a9-184">Localize a chave privada (`myPrivateKey_rsa` no exemplo anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="974a9-184">Locate your private key (`myPrivateKey_rsa` in hello previous example).</span></span> <span data-ttu-id="974a9-185">diretório predefinido de Olá quando iniciar **Git Bash** é `C:\Users\%username%`.</span><span class="sxs-lookup"><span data-stu-id="974a9-185">hello default directory when you start **Git Bash** is `C:\Users\%username%`.</span></span> <span data-ttu-id="974a9-186">Alterar tooshow de filtro de ficheiro Olá **todos os ficheiros (\*.\*)** :</span><span class="sxs-lookup"><span data-stu-id="974a9-186">Change hello file filter tooshow **All Files (\*.\*)**:</span></span>

    ![Carregar a chave privada existente de Olá para PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. <span data-ttu-id="974a9-188">Clique em **abra**.</span><span class="sxs-lookup"><span data-stu-id="974a9-188">Click **Open**.</span></span> <span data-ttu-id="974a9-189">Numa linha indica que essa chave Olá foi importado com êxito:</span><span class="sxs-lookup"><span data-stu-id="974a9-189">A prompt indicates that hello key has been successfully imported:</span></span>

    ![Chave tooPuTTYgen foram importados com êxito](./media/ssh-from-windows/successfully-imported-key.png)
6. <span data-ttu-id="974a9-191">Clique em **OK** linha de comandos do tooclose Olá.</span><span class="sxs-lookup"><span data-stu-id="974a9-191">Click **OK** tooclose hello prompt.</span></span>
7. <span data-ttu-id="974a9-192">chave pública Olá é apresentada na parte superior Olá Olá **PuTTYgen** janela.</span><span class="sxs-lookup"><span data-stu-id="974a9-192">hello public key is displayed at hello top of hello **PuTTYgen** window.</span></span> <span data-ttu-id="974a9-193">Copie e cole esta chave pública Olá portal do Azure ou o modelo Azure Resource Manager ao criar uma VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="974a9-193">You copy and paste this public key into hello Azure portal or Azure Resource Manager template when you create a Linux VM.</span></span> <span data-ttu-id="974a9-194">Também pode clicar em **Guardar chave pública** toosave um computador de tooyour cópia:</span><span class="sxs-lookup"><span data-stu-id="974a9-194">You can also click **Save public key** toosave a copy tooyour computer:</span></span>

    ![Guarde o ficheiro de chave pública PuTTY](./media/ssh-from-windows/save-public-key.png)

    <span data-ttu-id="974a9-196">Olá exemplo seguinte mostra como poderia copiar e colar esta chave pública no Olá portal do Azure, quando criar uma VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="974a9-196">hello following example shows how you would copy and paste this public key into hello Azure portal when you create a Linux VM.</span></span> <span data-ttu-id="974a9-197">chave pública Olá, em seguida, é normalmente armazenado num `~/.ssh/authorized_keys` na sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="974a9-197">hello public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span></span>

    ![Utilize a chave pública, quando cria uma VM no Olá portal do Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. <span data-ttu-id="974a9-199">Novamente no **PuTTYgen**, clique em **guardar a chave privada**:</span><span class="sxs-lookup"><span data-stu-id="974a9-199">Back in **PuTTYgen**, Click **Save private Key**:</span></span>

    ![Guarde o ficheiro de chave privada do PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > <span data-ttu-id="974a9-201">Uma linha de comandos pede-lhe se pretende toocontinue sem introduzir uma frase de acesso para a sua chave.</span><span class="sxs-lookup"><span data-stu-id="974a9-201">A prompt asks if you wish toocontinue without entering a passphrase for your key.</span></span> <span data-ttu-id="974a9-202">Uma frase de acesso é como uma chave privada de tooyour anexado de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="974a9-202">A passphrase is like a password attached tooyour private key.</span></span> <span data-ttu-id="974a9-203">Mesmo se alguém foram tooobtain a chave privada, ainda não seria capaz de tooauthenticate utilizando apenas Olá chave.</span><span class="sxs-lookup"><span data-stu-id="974a9-203">Even if someone were tooobtain your private key, they still would not be able tooauthenticate using just hello key.</span></span> <span data-ttu-id="974a9-204">Deverá também precisam de Olá frase de acesso.</span><span class="sxs-lookup"><span data-stu-id="974a9-204">They would also need hello passphrase.</span></span> <span data-ttu-id="974a9-205">Sem uma frase de acesso, se alguém obtém a chave privada, podem iniciar sessão tooany VM ou serviço que utiliza essa chave.</span><span class="sxs-lookup"><span data-stu-id="974a9-205">Without a passphrase, if someone obtains your private key, they can log in tooany VM or service that uses that key.</span></span> <span data-ttu-id="974a9-206">Recomendamos que crie uma frase de acesso.</span><span class="sxs-lookup"><span data-stu-id="974a9-206">We recommend you create a passphrase.</span></span> <span data-ttu-id="974a9-207">No entanto, se se esquecer da frase de acesso de Olá, não há nenhuma forma toorecovê-lo.</span><span class="sxs-lookup"><span data-stu-id="974a9-207">However, if you forget hello passphrase, there is no way toorecover it.</span></span>
   >
   >

    <span data-ttu-id="974a9-208">Se desejar tooenter uma frase de acesso, clique em **não**, introduza uma frase de acesso na janela principal do PuTTYgen Olá e, em seguida, clique em **Guardar chave privada** novamente.</span><span class="sxs-lookup"><span data-stu-id="974a9-208">If you wish tooenter a passphrase, click **No**, enter a passphrase in hello main PuTTYgen window, and then click **Save private key** again.</span></span> <span data-ttu-id="974a9-209">Caso contrário, clique em **Sim** toocontinue sem fornecer Olá frase de acesso opcional.</span><span class="sxs-lookup"><span data-stu-id="974a9-209">Otherwise, click **Yes** toocontinue without providing hello optional passphrase.</span></span>
9. <span data-ttu-id="974a9-210">Introduza um nome e localização toosave o ficheiro PPK.</span><span class="sxs-lookup"><span data-stu-id="974a9-210">Enter a name and location toosave your PPK file.</span></span>

## <a name="use-putty-toossh-tooa-linux-machine"></a><span data-ttu-id="974a9-211">Utilizar o Putty tooSSH tooa máquina Linux</span><span class="sxs-lookup"><span data-stu-id="974a9-211">Use Putty tooSSH tooa Linux Machine</span></span>
<span data-ttu-id="974a9-212">Novamente, PuTTY for um cliente SSH comuns para o Windows.</span><span class="sxs-lookup"><span data-stu-id="974a9-212">Again, PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="974a9-213">É gratuita toouse qualquer cliente SSH que desejar.</span><span class="sxs-lookup"><span data-stu-id="974a9-213">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="974a9-214">Olá, como os seguintes detalhes de passos toouse sua tooauthenticate chave privada com a VM do Azure através do SSH.</span><span class="sxs-lookup"><span data-stu-id="974a9-214">hello following steps detail how toouse your private key tooauthenticate with your Azure VM using SSH.</span></span> <span data-ttu-id="974a9-215">passos de Olá serem semelhantes em outros clientes de chaves SSH em termos de necessitar tooload sua Olá tooauthenticate chave privada ligação SSH.</span><span class="sxs-lookup"><span data-stu-id="974a9-215">hello steps are similar in other SSH key clients in terms of needing tooload your private key tooauthenticate hello SSH connection.</span></span>

1. <span data-ttu-id="974a9-216">Olá, transferir e executar putty da seguinte localização: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="974a9-216">Download and run putty from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="974a9-217">Preencha o nome de anfitrião de Olá ou endereço IP da sua VM do Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="974a9-217">Fill in hello host name or IP address of your VM from hello Azure portal:</span></span>

    ![Abrir nova ligação PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. <span data-ttu-id="974a9-219">Antes de selecionar **abra**, clique em **ligação** > **SSH** > **Auth** separador. Procurar tooand selecione a chave privada:</span><span class="sxs-lookup"><span data-stu-id="974a9-219">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse tooand select your private key:</span></span>

    ![Selecione a sua chave privada do PuTTY para autenticação](./media/ssh-from-windows/putty-auth-dialog.png)
4. <span data-ttu-id="974a9-221">Clique em **abra** tooconnect tooyour máquina</span><span class="sxs-lookup"><span data-stu-id="974a9-221">Click **Open** tooconnect tooyour virtual machine</span></span>

## <a name="next-steps"></a><span data-ttu-id="974a9-222">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="974a9-222">Next steps</span></span>
<span data-ttu-id="974a9-223">Também pode gerar as chaves públicas e privadas do Olá [utilizando OS X e Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974a9-223">You can also generate hello public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="974a9-224">Para obter mais informações sobre Bash para Windows e os benefícios de Olá de ter as ferramentas de OSS prontamente disponíveis no seu computador Windows, consulte [Bash no Ubuntu no Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="974a9-224">For more information about Bash for Windows and hello benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="974a9-225">Se tiver problemas ao utilizar o SSH tooconnect tooyour VMs com Linux, consulte [resolver problemas de SSH ligações tooan VM do Linux do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974a9-225">If you have trouble using SSH tooconnect tooyour Linux VMs, see [Troubleshoot SSH connections tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
