---
title: "aaaReset palavra-passe de VM com Linux e SSH de chave de Olá CLI | Microsoft Docs"
description: "Como toouse Olá extensão VMAccess tooreset de Interface de linha de comandos do Azure (CLI) Olá uma palavra-passe de VM com Linux ou chave SSH, corrija a configuração de SSH Olá e verificar a consistência de disco"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="6a50e-103">Como tooreset uma palavra-passe de VM com Linux ou chave SSH, corrija a configuração de SSH Olá e verificação de consistência de disco com a extensão de VMAccess Olá</span><span class="sxs-lookup"><span data-stu-id="6a50e-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="6a50e-104">Se não conseguir ligar tooa máquina de virtual com Linux no Azure devido a uma palavra-passe esquecida, uma chave Secure Shell (SSH) incorreto ou um problema com a configuração de SSH Olá, utilizar Olá extensão VMAccessForLinux com palavra-passe do Olá CLI do Azure tooreset Olá ou chave SSH, corrigir Olá configuração SSH e verificação de consistência de disco.</span><span class="sxs-lookup"><span data-stu-id="6a50e-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="6a50e-105">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6a50e-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6a50e-106">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6a50e-107">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6a50e-108">Saiba como demasiado[executar estes passos, utilizando o modelo do Resource Manager Olá](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="6a50e-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="6a50e-109">Com Olá CLI do Azure, utilizar Olá **conjunto de extensão de vm do azure** comando a partir dos seus comandos de tooaccess de interface de linha de comandos (Bash, Terminal, linha de comandos).</span><span class="sxs-lookup"><span data-stu-id="6a50e-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="6a50e-110">Executar **conjunto de extensão de vm do azure ajuda** para utilização de extensão de detalhado.</span><span class="sxs-lookup"><span data-stu-id="6a50e-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="6a50e-111">Com Olá CLI do Azure, pode fazê-lo Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="6a50e-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="6a50e-112">Olá de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="6a50e-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="6a50e-113">Repor a chave SSH Olá</span><span class="sxs-lookup"><span data-stu-id="6a50e-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="6a50e-114">Repor Olá palavra-passe e Olá a chave SSH</span><span class="sxs-lookup"><span data-stu-id="6a50e-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="6a50e-115">Criar uma nova conta de utilizador de sudo</span><span class="sxs-lookup"><span data-stu-id="6a50e-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="6a50e-116">Repor a configuração de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="6a50e-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="6a50e-117">Eliminar um utilizador</span><span class="sxs-lookup"><span data-stu-id="6a50e-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="6a50e-118">Apresentar o estado de Olá de Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="6a50e-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="6a50e-119">Verificação de consistência de discos adicionados</span><span class="sxs-lookup"><span data-stu-id="6a50e-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="6a50e-120">Reparar discos adicionados na sua VM do Linux</span><span class="sxs-lookup"><span data-stu-id="6a50e-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="6a50e-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a50e-121">Prerequisites</span></span>
<span data-ttu-id="6a50e-122">Terá de seguinte de Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="6a50e-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="6a50e-123">Terá de demasiado[instalar Olá CLI do Azure](../../../cli-install-nodejs.md) e [ligar tooyour subscrição](../../../xplat-cli-connect.md) toouse Azure recursos associados à sua conta.</span><span class="sxs-lookup"><span data-stu-id="6a50e-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="6a50e-124">Conjunto Olá modo correto para o modelo de implementação clássica Olá, escrevendo o seguinte Olá Olá linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="6a50e-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="6a50e-125">Ter uma nova palavra-passe ou o conjunto de chaves SSH, se quiser tooreset uma.</span><span class="sxs-lookup"><span data-stu-id="6a50e-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="6a50e-126">Não precisa de estes se pretender que a configuração de SSH tooreset Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="6a50e-127"><a name="pwresetcli"></a>Olá de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="6a50e-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="6a50e-128">Crie um ficheiro no seu computador local com o nome PrivateConf.json com estas linhas.</span><span class="sxs-lookup"><span data-stu-id="6a50e-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="6a50e-129">Substitua **myUserName** e  **myP@ssW0rd**  com o seu nome de utilizador e palavra-passe e definir a sua própria data de expiração.</span><span class="sxs-lookup"><span data-stu-id="6a50e-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="6a50e-130">Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6a50e-131"><a name="sshkeyresetcli"></a>Repor a chave SSH Olá</span><span class="sxs-lookup"><span data-stu-id="6a50e-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="6a50e-132">Crie um ficheiro denominado PrivateConf.json com estes conteúdos.</span><span class="sxs-lookup"><span data-stu-id="6a50e-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="6a50e-133">Substitua Olá **myUserName** e **mySSHKey** valores pelas suas informações.</span><span class="sxs-lookup"><span data-stu-id="6a50e-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="6a50e-134">Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="6a50e-135"><a name="resetbothcli"></a>Repor palavra-passe de Olá e a chave SSH Olá</span><span class="sxs-lookup"><span data-stu-id="6a50e-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="6a50e-136">Crie um ficheiro denominado PrivateConf.json com estes conteúdos.</span><span class="sxs-lookup"><span data-stu-id="6a50e-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="6a50e-137">Substitua Olá **myUserName**, **mySSHKey** e  **myP@ssW0rd**  valores pelas suas informações.</span><span class="sxs-lookup"><span data-stu-id="6a50e-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="6a50e-138">Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6a50e-139"><a name="createnewsudocli"></a>Criar uma nova conta de utilizador de sudo</span><span class="sxs-lookup"><span data-stu-id="6a50e-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="6a50e-140">Se se esquecer da sua nome de utilizador, pode utilizar VMAccess toocreate um novo com a autoridade de sudo Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="6a50e-141">Neste caso, Olá existente nome de utilizador e palavra-passe não será modificado.</span><span class="sxs-lookup"><span data-stu-id="6a50e-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="6a50e-142">toocreate um novo utilizador de sudo com acesso de palavra-passe, utilize Olá script no [Olá de reposição de palavra-passe](#pwresetcli) e especifique o nome de utilizador novo Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="6a50e-143">toocreate um novo utilizador de sudo com acesso de chave SSH, utilize Olá script no [repor a chave SSH Olá](#sshkeyresetcli) e especifique o nome de utilizador novo Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="6a50e-144">Também pode utilizar [Repor palavra-passe de Olá e a chave SSH Olá](#resetbothcli) toocreate um novo utilizador com palavra-passe e acesso de chave SSH.</span><span class="sxs-lookup"><span data-stu-id="6a50e-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="6a50e-145"><a name="sshconfigresetcli"></a>Repor a configuração de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="6a50e-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="6a50e-146">Se a configuração de SSH Olá está num estado indesejado, poderá também perder acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="6a50e-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="6a50e-147">Pode utilizar Olá VMAccess extensão tooreset Olá configuração tooits estado predefinido.</span><span class="sxs-lookup"><span data-stu-id="6a50e-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="6a50e-148">toodo por isso, basta chave do tooset Olá "reset_ssh" demasiado "True".</span><span class="sxs-lookup"><span data-stu-id="6a50e-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="6a50e-149">extensão de Olá irá reiniciar o servidor SSH Olá, abra a porta SSH Olá na sua VM e repor os valores de toodefault de configuração de SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="6a50e-150">conta de utilizador Olá (nome, palavra-passe ou chaves SSH) não será alterada.</span><span class="sxs-lookup"><span data-stu-id="6a50e-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="6a50e-151">ficheiro de configuração de SSH Olá obtém repor está localizado em /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="6a50e-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="6a50e-152">Crie um ficheiro denominado PrivateConf.json com este conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6a50e-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="6a50e-153">Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6a50e-154"><a name="deletecli"></a>Eliminar um utilizador</span><span class="sxs-lookup"><span data-stu-id="6a50e-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="6a50e-155">Se quiser toodelete uma conta de utilizador sem iniciar sessão no toohello VM diretamente, pode utilizar este script.</span><span class="sxs-lookup"><span data-stu-id="6a50e-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="6a50e-156">Crie um ficheiro denominado PrivateConf.json com este conteúdo, substituindo Olá tooremove de nome de utilizador para **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="6a50e-157">Executar este comando, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6a50e-158"><a name="statuscli"></a>Apresentar o estado de Olá de Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="6a50e-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="6a50e-159">Estado de Olá toodisplay de Olá extensão VMAccess, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="6a50e-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="6a50e-160"><a name='checkdisk'></a>Verificação de consistência de discos adicionados</span><span class="sxs-lookup"><span data-stu-id="6a50e-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="6a50e-161">toorun ou a fsck em todos os discos na sua máquina virtual do Linux, será seguintes elementos terão toodo Olá:</span><span class="sxs-lookup"><span data-stu-id="6a50e-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="6a50e-162">Crie um ficheiro denominado PublicConf.json com este conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6a50e-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="6a50e-163">Verifique o que disco assume um valor booleano para se toocheck discos anexados a máquina virtual de tooyour ou não.</span><span class="sxs-lookup"><span data-stu-id="6a50e-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="6a50e-164">Execute este comando tooexecute, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="6a50e-165"><a name='repairdisk'></a>Discos de reparação</span><span class="sxs-lookup"><span data-stu-id="6a50e-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="6a50e-166">toorepair discos que não estão a montar ou que têm erros de configuração de montagem, utilize a configuração de montagem de Olá de tooreset extensão VMAccess Olá na sua máquina virtual do Linux.</span><span class="sxs-lookup"><span data-stu-id="6a50e-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="6a50e-167">Substituindo o nome de Olá do disco para **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="6a50e-168">Crie um ficheiro denominado PublicConf.json com este conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6a50e-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="6a50e-169">Execute este comando tooexecute, substituindo o nome de Olá da sua máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6a50e-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="6a50e-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6a50e-170">Next steps</span></span>
* <span data-ttu-id="6a50e-171">Se quiser toouse cmdlets do Azure PowerShell ou a palavra-passe do Azure Resource Manager modelos tooreset Olá ou a chave SSH, corrija a configuração de SSH Olá e verificar a consistência de disco, consulte Olá [documentação da extensão VMAccess no GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="6a50e-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="6a50e-172">Também pode utilizar Olá [portal do Azure](https://portal.azure.com) palavra-passe do tooreset Olá ou chave SSH de uma VM com Linux implementados no modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="6a50e-173">Atualmente não é possível utilizar Olá efetue portal toothis para implementar uma VM com Linux no modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="6a50e-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="6a50e-174">Consulte [sobre extensões de máquina virtual e funcionalidades](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre a utilização de extensões VM para máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a50e-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

