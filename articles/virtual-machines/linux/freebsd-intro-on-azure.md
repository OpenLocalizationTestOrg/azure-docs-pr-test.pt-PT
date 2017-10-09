---
title: aaaIntroduction tooFreeBSD no Azure | Microsoft Docs
description: "Saiba como utilizar FreeBSD máquinas de virtuais no Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="5c4e6-103">Introdução tooFreeBSD no Azure</span><span class="sxs-lookup"><span data-stu-id="5c4e6-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="5c4e6-104">Este tópico fornece uma descrição geral da execução de uma máquina virtual de FreeBSD no Azure.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="5c4e6-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5c4e6-105">Overview</span></span>
<span data-ttu-id="5c4e6-106">FreeBSD do Microsoft Azure é que um sistema operativo do computador avançadas utilizada servidores moderna toopower, ambientes de trabalho e plataformas incorporadas.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="5c4e6-107">Microsoft Corporation é disponibilizar imagens de FreeBSD no Azure com Olá [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) pré-configurados.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="5c4e6-108">Atualmente, hello seguintes versões de FreeBSD são oferecidas como imagens pela Microsoft:</span><span class="sxs-lookup"><span data-stu-id="5c4e6-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="5c4e6-109">FreeBSD 10.3-versão</span><span class="sxs-lookup"><span data-stu-id="5c4e6-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="5c4e6-110">FreeBSD 11.0-versão</span><span class="sxs-lookup"><span data-stu-id="5c4e6-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="5c4e6-111">agente de Olá é responsável pela comunicação entre Olá FreeBSD VM e Olá recursos de infraestrutura do Azure para operações como aprovisionamento Olá VM na primeira utilização (nome de utilizador, palavra-passe ou chave SSH, o nome do anfitrião, etc.) e a funcionalidade de ativação para extensões VM seletivos.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="5c4e6-112">Para versões futuras do FreeBSD, estratégia Olá é toostay atual e disponibilizar versões mais recentes de Olá pouco tempo depois de serem publicados pela equipa de engenharia Olá FreeBSD versão.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="5c4e6-113">Implementar uma máquina virtual de FreeBSD</span><span class="sxs-lookup"><span data-stu-id="5c4e6-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="5c4e6-114">Implementar uma máquina virtual de FreeBSD é um processo simples utilizando uma imagem de Olá Azure Marketplace da Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="5c4e6-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="5c4e6-115">10.3 FreeBSD em Olá Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5c4e6-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="5c4e6-116">11.0 FreeBSD em Olá Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5c4e6-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="5c4e6-117">Criar uma VM de FreeBSD através da CLI do Azure 2.0 no FreeBSD</span><span class="sxs-lookup"><span data-stu-id="5c4e6-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="5c4e6-118">Primeiro tem de tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) apesar de os seguintes comandos numa máquina FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="5c4e6-119">Se bash não está instalado no seu computador FreeBSD, execute os seguintes comandos antes da instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="5c4e6-120">Se o python não está instalado no seu computador FreeBSD, execute os seguintes comandos antes da instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="5c4e6-121">Durante a instalação de Olá, é-lhe perguntado `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="5c4e6-122">Se responder `y` e introduza `/etc/rc.conf` como `a path tooan rc file tooupdate`, pode satisfazer problema Olá `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="5c4e6-123">tooresolve este problema, só deverá conceder Olá escrita toocurrent direita utilizador ficheiro Olá `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="5c4e6-124">Agora pode iniciar sessão no Azure e criar a VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="5c4e6-125">Segue-se um exemplo toocreate FreeBSD 11.0 VM.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="5c4e6-126">Também pode adicionar parâmetro Olá `--public-ip-address-dns-name` com um nome globalmente exclusivo de DNS para um IP público criado recentemente.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="5c4e6-127">Em seguida, pode iniciar sessão no tooyour FreeBSD VM através do endereço de ip de Olá impresso na saída de Olá de acima implementação.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="5c4e6-128">Extensões VM para FreeBSD</span><span class="sxs-lookup"><span data-stu-id="5c4e6-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="5c4e6-129">Seguem-se as extensões de VM suportadas no FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="5c4e6-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="5c4e6-130">VMAccess</span></span>
<span data-ttu-id="5c4e6-131">Olá [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extensão pode:</span><span class="sxs-lookup"><span data-stu-id="5c4e6-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="5c4e6-132">Repor Olá palavra-passe de utilizador de sudo original Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="5c4e6-133">Crie um novo utilizador de sudo com palavra-passe de Olá especificada.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="5c4e6-134">Definir a chave de anfitrião público de Olá com a chave de Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="5c4e6-135">Repor chave de anfitrião público Olá fornecido durante a chave de anfitrião Olá é se não for indicado de aprovisionamento de VM.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="5c4e6-136">Abra a porta SSH Olá (22) e restaurar Olá sshd_config se reset_ssh estiver definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="5c4e6-137">Remova Olá de utilizador existente.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-137">Remove hello existing user.</span></span>
* <span data-ttu-id="5c4e6-138">Verifique os discos.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-138">Check disks.</span></span>
* <span data-ttu-id="5c4e6-139">Repare um disco adicionado.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="5c4e6-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="5c4e6-140">CustomScript</span></span>
<span data-ttu-id="5c4e6-141">Olá [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extensão pode:</span><span class="sxs-lookup"><span data-stu-id="5c4e6-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="5c4e6-142">Se for indicado, transfira scripts de Olá personalizado do Storage do Azure ou armazenamento público externo (por exemplo, o GitHub).</span><span class="sxs-lookup"><span data-stu-id="5c4e6-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="5c4e6-143">Execute script de ponto de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-143">Run hello entry point script.</span></span>
* <span data-ttu-id="5c4e6-144">Suporta comandos inline.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-144">Support inline commands.</span></span>
* <span data-ttu-id="5c4e6-145">Converta o estilo de Windows tabulação na shell e Python scripts automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="5c4e6-146">Remova automaticamente LM na shell e Python scripts.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="5c4e6-147">Proteger os dados confidenciais do CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="5c4e6-148">FreeBSD VM só suporta CustomScript versão 1. x, por agora.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="5c4e6-149">Autenticação: os nomes de utilizador, palavras-passe e chaves SSH</span><span class="sxs-lookup"><span data-stu-id="5c4e6-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="5c4e6-150">Quando estiver a criar uma máquina virtual de FreeBSD utilizando Olá portal do Azure, tem de fornecer um nome de utilizador, palavra-passe ou chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="5c4e6-151">Para implementar uma máquina virtual de FreeBSD no Azure, os nomes de utilizador não tem de corresponder ao nomes das contas de sistema (UID < 100) já está presente na máquina virtual de Olá ("raiz", por exemplo).</span><span class="sxs-lookup"><span data-stu-id="5c4e6-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="5c4e6-152">Atualmente, apenas Olá RSA chave SSH é suportado.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="5c4e6-153">Tem de começar com uma chave SSH com várias linhas `---- BEGIN SSH2 PUBLIC KEY ----` e terminar com `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="5c4e6-154">A obtenção de privilégios de Superutilizador</span><span class="sxs-lookup"><span data-stu-id="5c4e6-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="5c4e6-155">conta de utilizador Olá, que é especificada durante a implementação da instância de máquina virtual no Azure é uma conta com privilégios.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="5c4e6-156">Olá pacote de sudo foi instalado no Olá publicados FreeBSD imagem.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="5c4e6-157">Depois de que tem sessão iniciada através desta conta de utilizador, pode executar comandos como raiz utilizando a sintaxe do comando Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="5c4e6-158">Opcionalmente, pode obter uma shell de raiz utilizando `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5c4e6-159">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="5c4e6-159">Known issues</span></span>
<span data-ttu-id="5c4e6-160">Olá [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.2 tem um [problema conhecido] (https://github.com/Azure/WALinuxAgent/pull/517) que faz com que a falha de aprovisionar Olá para FreeBSD VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="5c4e6-161">Olá correção capturada pelos [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.3 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c4e6-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5c4e6-162">Next steps</span></span>
* <span data-ttu-id="5c4e6-163">Aceda demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate uma VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5c4e6-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="5c4e6-164">Se pretender que toobring o seus próprios tooAzure FreeBSD, consulte demasiado[criar e carregar um FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e6-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span></span>
