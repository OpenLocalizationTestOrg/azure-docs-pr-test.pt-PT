---
title: aaaMount File storage do Azure em VMs do Linux utilizando o SMB com a CLI do Azure 1.0 | Microsoft Docs
description: Como toomount File storage do Azure em VMs do Linux utilizando o SMB
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="ee381-103">Montagem File storage do Azure em VMs do Linux utilizando o SMB com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ee381-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="ee381-104">Este artigo mostra como toomount File storage do Azure numa VM com Linux utilizando Olá protocolo Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="ee381-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="ee381-105">O File storage oferece partilhas de ficheiros na nuvem de Olá através do protocolo SMB padrão do Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="ee381-106">requisitos de Olá são:</span><span class="sxs-lookup"><span data-stu-id="ee381-106">hello requirements are:</span></span>

* <span data-ttu-id="ee381-107">Um [conta do Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="ee381-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="ee381-108">Secure Shell (SSH) pública e privada dos ficheiros de chaves</span><span class="sxs-lookup"><span data-stu-id="ee381-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="ee381-109">CLI versões toouse</span><span class="sxs-lookup"><span data-stu-id="ee381-109">CLI versions toouse</span></span>
<span data-ttu-id="ee381-110">Pode concluir tarefas Olá utilizando um dos Olá seguintes versões de interface de linha de comandos (CLI):</span><span class="sxs-lookup"><span data-stu-id="ee381-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="ee381-111">[Azure CLI 1.0](#quick-commands) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="ee381-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ee381-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="ee381-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ee381-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="ee381-113">Quick commands</span></span>
<span data-ttu-id="ee381-114">tarefas de Olá tooaccomplish rapidamente, siga os passos Olá nesta secção.</span><span class="sxs-lookup"><span data-stu-id="ee381-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="ee381-115">Para obter mais informações e contexto, início às Olá ["Instruções detalhadas"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) secção.</span><span class="sxs-lookup"><span data-stu-id="ee381-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ee381-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee381-116">Prerequisites</span></span>
* <span data-ttu-id="ee381-117">Um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ee381-117">A resource group</span></span>
* <span data-ttu-id="ee381-118">Uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="ee381-118">An Azure virtual network</span></span>
* <span data-ttu-id="ee381-119">Um grupo de segurança de rede com um SSH entrada</span><span class="sxs-lookup"><span data-stu-id="ee381-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="ee381-120">Uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="ee381-120">A subnet</span></span>
* <span data-ttu-id="ee381-121">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ee381-121">An Azure storage account</span></span>
* <span data-ttu-id="ee381-122">Chaves de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ee381-122">Azure storage account keys</span></span>
* <span data-ttu-id="ee381-123">Uma partilha de armazenamento de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="ee381-123">An Azure File storage share</span></span>
* <span data-ttu-id="ee381-124">Uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="ee381-124">A Linux VM</span></span>

<span data-ttu-id="ee381-125">Substitua qualquer exemplos as suas próprias definições.</span><span class="sxs-lookup"><span data-stu-id="ee381-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="ee381-126">Criar um diretório de montagem local Olá</span><span class="sxs-lookup"><span data-stu-id="ee381-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="ee381-127">Olá ficheiro armazenamento SMB partilha toohello montagem ponto de montagem</span><span class="sxs-lookup"><span data-stu-id="ee381-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="ee381-128">Manter Olá montagem após um reinício</span><span class="sxs-lookup"><span data-stu-id="ee381-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="ee381-129">Adicionar Olá seguinte linha demasiado`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="ee381-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ee381-130">Instruções detalhadas</span><span class="sxs-lookup"><span data-stu-id="ee381-130">Detailed walkthrough</span></span>

<span data-ttu-id="ee381-131">O File storage oferece partilhas de ficheiros na nuvem de Olá que utilizam o protocolo SMB padrão do Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="ee381-132">Com a versão mais recente Olá do armazenamento de ficheiros, também é possível montar uma partilha de ficheiros de qualquer sistema operativo que suporta o SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="ee381-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="ee381-133">Quando utiliza uma montagem SMB no Linux, obter cópias de segurança fácil tooa robusta, permanente arquivo local de armazenamento que é suportado por um SLA.</span><span class="sxs-lookup"><span data-stu-id="ee381-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="ee381-134">Mover os ficheiros de uma montagem SMB tooan VM que está alojada no armazenamento de ficheiros é que uma excelente forma toodebug registos.</span><span class="sxs-lookup"><span data-stu-id="ee381-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="ee381-135">Isto acontece porque Olá partilha do SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="ee381-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="ee381-136">SMB não é a melhor solução de Olá para transmissão em fluxo Linux ou os registos de aplicação em tempo real, porque não se encontra Olá protocolo SMB criada toohandle essas funções de registo pesada.</span><span class="sxs-lookup"><span data-stu-id="ee381-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="ee381-137">Uma ferramenta de camada de registo dedicado, unificada como Fluentd seria uma melhor opção que SMB para a recolha de Linux e aplicação de registo de saída.</span><span class="sxs-lookup"><span data-stu-id="ee381-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="ee381-138">Nestas instruções detalhadas, iremos criar pré-requisitos Olá necessário toofirst criar partilha de armazenamento de ficheiros de Olá e, em seguida, monte-lo através de SMB numa VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="ee381-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="ee381-139">Crie uma conta de armazenamento do Azure utilizando Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ee381-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="ee381-140">Mostra chaves de conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="ee381-141">Quando cria uma conta de armazenamento, chaves de conta Olá são criadas pares para que pode ser rotação sem qualquer interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="ee381-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="ee381-142">Quando mudar toohello segunda chave num par de Olá, crie um novo par de chaves.</span><span class="sxs-lookup"><span data-stu-id="ee381-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="ee381-143">Chaves de conta de armazenamento novas sempre são criadas pares, assegurando que tem sempre, pelo menos, um armazenamento não utilizadas chaves pronto tooswitch para.</span><span class="sxs-lookup"><span data-stu-id="ee381-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="ee381-144">chaves de conta de armazenamento de Olá tooshow, utilize Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ee381-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="ee381-145">Crie a partilha de armazenamento de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-145">Create hello File storage share.</span></span>

    <span data-ttu-id="ee381-146">partilha de ficheiros de armazenamento Olá contém partilha do SMB Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="ee381-147">quota de Olá sempre é expresso em gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="ee381-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="ee381-148">toocreate Olá partilha do File storage, utilize Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ee381-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="ee381-149">Crie o diretório de ponto de montagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="ee381-150">Tem de criar um diretório local as Olá de toomount ficheiros de Linux do Olá sistema partilha de SMB.</span><span class="sxs-lookup"><span data-stu-id="ee381-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="ee381-151">Nada escritas ou ler a partir do diretório de montagem local Olá é reencaminhado toohello partilha do SMB que está alojado no armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="ee381-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="ee381-152">diretório de Olá toocreate, Olá utilize seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ee381-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="ee381-153">Monte Olá partilha do SMB utilizando Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ee381-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="ee381-154">Manter Olá SMB montar através de reinícios.</span><span class="sxs-lookup"><span data-stu-id="ee381-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="ee381-155">Quando reiniciar Olá VM com Linux, hello partilha SMB montada é desmontada durante o encerramento.</span><span class="sxs-lookup"><span data-stu-id="ee381-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="ee381-156">tooremount Olá partilha SMB arranque, tem de adicionar uma linha de toohello Linux /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="ee381-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="ee381-157">Linux utiliza Olá fstab toolist Olá ficheiro sistemas de ficheiros que necessita de toomount durante o processo de arranque Olá.</span><span class="sxs-lookup"><span data-stu-id="ee381-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="ee381-158">Adicionar partilha SMB Olá garante que partilha do File storage Olá é um sistema de ficheiros permanentemente montado para Olá VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="ee381-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="ee381-159">Nova VM adicionar Olá ficheiro armazenamento SMB partilha tooa é possível ao utilizar init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ee381-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="ee381-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ee381-160">Next steps</span></span>

- [<span data-ttu-id="ee381-161">Nuvem init toocustomize uma VM com Linux a utilizar durante a criação</span><span class="sxs-lookup"><span data-stu-id="ee381-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="ee381-162">Adicionar um disco tooa VM com Linux</span><span class="sxs-lookup"><span data-stu-id="ee381-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="ee381-163">Encriptar discos uma VM com Linux utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ee381-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
