---
title: aaaMove ficheiros tooand de VMs do Linux do Azure com o SCP | Microsoft Docs
description: "Mover em segurança tooand de ficheiros de uma VM com Linux no Azure utilizando o SCP e um par de chaves SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="f917e-103">Mover tooand de ficheiros de uma VM com Linux através de SCP</span><span class="sxs-lookup"><span data-stu-id="f917e-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="f917e-104">Este artigo mostra como toomove ficheiros de cópia de segurança tooan VM do Linux do Azure a estação de trabalho ou de uma VM do Azure Linux baixo tooyour estação de trabalho, utilizando Secure cópia (SCP).</span><span class="sxs-lookup"><span data-stu-id="f917e-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="f917e-105">Mover ficheiros entre a estação de trabalho e de uma VM com Linux, rapidamente e segura, é essencial para gerir a sua infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f917e-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="f917e-106">Para este artigo, é necessário um Linux VM implementado no Azure com [ficheiros de chaves públicos e privados SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f917e-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f917e-107">Também precisa de um cliente de SCP para o seu computador local.</span><span class="sxs-lookup"><span data-stu-id="f917e-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="f917e-108">É desenvolvida com SSH e incluído na shell de deteção predefinidas Olá da maioria dos computadores Linux e Mac e algumas shells do Windows.</span><span class="sxs-lookup"><span data-stu-id="f917e-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="f917e-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="f917e-109">Quick commands</span></span>

<span data-ttu-id="f917e-110">Copiar um ficheiro de cópia de segurança toohello VM com Linux</span><span class="sxs-lookup"><span data-stu-id="f917e-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="f917e-111">Copie um ficheiro de Olá VM com Linux</span><span class="sxs-lookup"><span data-stu-id="f917e-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f917e-112">Instruções detalhadas</span><span class="sxs-lookup"><span data-stu-id="f917e-112">Detailed walkthrough</span></span>

<span data-ttu-id="f917e-113">Como exemplos, podemos mover um ficheiro de configuração do Azure se tooa VM com Linux e obtenha um diretório do ficheiro de registo, ambos utilizando chaves SCP e SSH.</span><span class="sxs-lookup"><span data-stu-id="f917e-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="f917e-114">Autenticação do par de chaves SSH</span><span class="sxs-lookup"><span data-stu-id="f917e-114">SSH key pair authentication</span></span>

<span data-ttu-id="f917e-115">SCP utiliza SSH para a camada de transporte Olá.</span><span class="sxs-lookup"><span data-stu-id="f917e-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="f917e-116">SSH identificadores Olá autenticação no anfitrião de destino Olá, e este move-Olá num túnel encriptado fornecido por predefinição com SSH.</span><span class="sxs-lookup"><span data-stu-id="f917e-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="f917e-117">Para a autenticação SSH, podem ser utilizadas nomes de utilizador e palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="f917e-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="f917e-118">No entanto, a autenticação de chave pública e privada SSH são recomendadas como melhor prática de segurança.</span><span class="sxs-lookup"><span data-stu-id="f917e-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="f917e-119">Uma vez SSH tem autenticado ligação Olá, o SCP começa, em seguida, ao copiar o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="f917e-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="f917e-120">Utilizar está corretamente configurada `~/.ssh/config` e SSH chaves públicas e privadas, ligação Olá SCP podem ser estabelecidas pela utilização de apenas um nome de servidor (ou endereço IP).</span><span class="sxs-lookup"><span data-stu-id="f917e-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="f917e-121">Se tiver apenas uma chave SSH, SCP procura-lo no Olá `~/.ssh/` diretório e utiliza-o por predefinição toolog no toohello VM.</span><span class="sxs-lookup"><span data-stu-id="f917e-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="f917e-122">Para obter mais informações sobre como configurar a sua `~/.ssh/config` e chaves públicas e privadas SSH, consulte [criar SSH chaves](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f917e-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="f917e-123">SCP tooa um ficheiro VM com Linux</span><span class="sxs-lookup"><span data-stu-id="f917e-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="f917e-124">Para o primeiro exemplo Olá, iremos copiar um ficheiro de configuração do Azure se tooa VM com Linux que é utilizado toodeploy automatização.</span><span class="sxs-lookup"><span data-stu-id="f917e-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="f917e-125">Porque este ficheiro contém credenciais de API do Azure, nomeadamente segredos, segurança, é importante.</span><span class="sxs-lookup"><span data-stu-id="f917e-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="f917e-126">túnel encriptados Olá fornecida pelo SSH protege o conteúdo de Olá do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="f917e-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="f917e-127">Olá, os seguintes comandos cópias Olá local *.azure/configuração* tooan VM do Azure com o FQDN do ficheiro *myserver.eastus.cloudapp.azure.com*. nome de utilizador de admin Olá no Olá VM do Azure é *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="f917e-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="f917e-128">Olá ficheiro é visado toohello */home/azureuser/* diretório.</span><span class="sxs-lookup"><span data-stu-id="f917e-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="f917e-129">Substitua os seus próprios valores neste comando.</span><span class="sxs-lookup"><span data-stu-id="f917e-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="f917e-130">SCP um diretório de uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="f917e-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="f917e-131">Neste exemplo, vamos copiar um diretório de ficheiros de registo de Olá VM com Linux para baixo tooyour estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f917e-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="f917e-132">Um ficheiro de registo pode ou não pode conter dados confidenciais ou secretos.</span><span class="sxs-lookup"><span data-stu-id="f917e-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="f917e-133">No entanto, utilizar o SCP garante conteúdo Olá Olá dos ficheiros de registo é encriptado.</span><span class="sxs-lookup"><span data-stu-id="f917e-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="f917e-134">A utilização de ficheiros do SCP tootransfer Olá é tooget de forma mais fácil Olá Olá diretório de registo e ficheiros baixo tooyour estação de trabalho tendo simultaneamente segura.</span><span class="sxs-lookup"><span data-stu-id="f917e-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="f917e-135">Olá seguinte comando copia ficheiros Olá */homeazureuser/registos/* diretório no diretório /tmp dos locais do Olá VM do Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="f917e-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="f917e-136">Olá `-r` cli sinalizador dá instruções ao ficheiros do SCP toorecursively cópia Olá e diretórios do ponto de Olá do diretório de Olá listado no comando Olá.</span><span class="sxs-lookup"><span data-stu-id="f917e-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="f917e-137">Tenha em atenção que Olá sintaxe da linha de comandos é também tooa semelhante `cp` copiar o comando.</span><span class="sxs-lookup"><span data-stu-id="f917e-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f917e-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f917e-138">Next steps</span></span>

* [<span data-ttu-id="f917e-139">Gerir utilizadores, SSH e verificação ou discos de reparação em VMs do Linux do Azure utilizando Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="f917e-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
