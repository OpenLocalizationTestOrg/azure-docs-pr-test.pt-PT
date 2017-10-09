---
title: aaaMount File storage do Azure em VMs do Linux utilizando o SMB | Microsoft Docs
description: "Como toomount File storage do Azure em VMs do Linux utilizando o SMB com Olá Azure CLI 2.0"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="98211-103">Armazenamento de ficheiros do Azure de montagem em VMs do Linux utilizando o SMB</span><span class="sxs-lookup"><span data-stu-id="98211-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="98211-104">Este artigo mostra como tooutilize Olá serviço de armazenamento de ficheiros do Azure numa VM com Linux através de SMB montagem com Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="98211-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="98211-105">File storage do Azure oferece partilhas de ficheiros na nuvem de Olá utilizando o protocolo SMB padrão do Olá.</span><span class="sxs-lookup"><span data-stu-id="98211-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="98211-106">Também pode executar estes passos com Olá [CLI do Azure 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98211-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="98211-107">requisitos de Olá são:</span><span class="sxs-lookup"><span data-stu-id="98211-107">hello requirements are:</span></span>

- [<span data-ttu-id="98211-108">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="98211-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="98211-109">Ficheiros de chaves públicas e privadas SSH</span><span class="sxs-lookup"><span data-stu-id="98211-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="98211-110">Comandos Rápidos</span><span class="sxs-lookup"><span data-stu-id="98211-110">Quick Commands</span></span>

* <span data-ttu-id="98211-111">Um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="98211-111">A resource group</span></span>
* <span data-ttu-id="98211-112">Uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="98211-112">An Azure virtual network</span></span>
* <span data-ttu-id="98211-113">Um grupo de segurança de rede com um SSH entrada</span><span class="sxs-lookup"><span data-stu-id="98211-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="98211-114">Uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="98211-114">A subnet</span></span>
* <span data-ttu-id="98211-115">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="98211-115">An Azure storage account</span></span>
* <span data-ttu-id="98211-116">Chaves de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="98211-116">Azure storage account keys</span></span>
* <span data-ttu-id="98211-117">Uma partilha de armazenamento de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="98211-117">An Azure File storage share</span></span>
* <span data-ttu-id="98211-118">Uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="98211-118">A Linux VM</span></span>

<span data-ttu-id="98211-119">Substitua qualquer exemplos as suas próprias definições.</span><span class="sxs-lookup"><span data-stu-id="98211-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="98211-120">Criar um diretório de montagem local Olá</span><span class="sxs-lookup"><span data-stu-id="98211-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="98211-121">Olá ficheiro armazenamento SMB partilha toohello montagem ponto de montagem</span><span class="sxs-lookup"><span data-stu-id="98211-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="98211-122">Manter Olá montagem após um reinício</span><span class="sxs-lookup"><span data-stu-id="98211-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="98211-123">toodo por isso, adicionar Olá seguinte linha toohello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="98211-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="98211-124">Instruções detalhadas</span><span class="sxs-lookup"><span data-stu-id="98211-124">Detailed walkthrough</span></span>

<span data-ttu-id="98211-125">O File storage oferece partilhas de ficheiros na nuvem de Olá que utilizam o protocolo SMB padrão do Olá.</span><span class="sxs-lookup"><span data-stu-id="98211-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="98211-126">Com a versão mais recente Olá do armazenamento de ficheiros, também é possível montar uma partilha de ficheiros de qualquer sistema operativo que suporta o SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="98211-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="98211-127">Quando utiliza uma montagem SMB no Linux, obter cópias de segurança fácil tooa robusta, permanente arquivo local de armazenamento que é suportado por um SLA.</span><span class="sxs-lookup"><span data-stu-id="98211-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="98211-128">Mover os ficheiros de uma montagem SMB tooan VM que está alojada no armazenamento de ficheiros é que uma excelente forma toodebug registos.</span><span class="sxs-lookup"><span data-stu-id="98211-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="98211-129">Isto acontece porque Olá partilha do SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="98211-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="98211-130">SMB não é a melhor solução de Olá para transmissão em fluxo Linux ou os registos de aplicação em tempo real, porque não se encontra Olá protocolo SMB criada toohandle essas funções de registo pesada.</span><span class="sxs-lookup"><span data-stu-id="98211-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="98211-131">Uma ferramenta de camada de registo dedicado, unificada como Fluentd seria uma melhor opção que SMB para a recolha de Linux e aplicação de registo de saída.</span><span class="sxs-lookup"><span data-stu-id="98211-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="98211-132">Nestas instruções detalhadas, iremos criar pré-requisitos Olá necessário toofirst criar partilha de armazenamento de ficheiros de Olá e, em seguida, monte-lo através de SMB numa VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="98211-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="98211-133">Criar um grupo de recursos com [criar grupo az](/cli/azure/group#create) partilha de ficheiros de Olá toohold.</span><span class="sxs-lookup"><span data-stu-id="98211-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="98211-134">com o nome de um grupo de recursos de toocreate `myResourceGroup` na localização "EUA Oeste" Olá, utilize o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="98211-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="98211-135">Criar uma conta de armazenamento do Azure com [criar conta de armazenamento az](/cli/azure/storage/account#create) toostore Olá ficheiros concretos.</span><span class="sxs-lookup"><span data-stu-id="98211-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="98211-136">toocreate uma conta de armazenamento com o nome mystorageaccount utilizando o armazenamento de Standard_LRS Olá SKU, seguinte o exemplo de Olá de utilização:</span><span class="sxs-lookup"><span data-stu-id="98211-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="98211-137">Mostra chaves de conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="98211-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="98211-138">Quando cria uma conta de armazenamento, chaves de conta Olá são criadas pares para que pode ser rotação sem qualquer interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="98211-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="98211-139">Quando mudar toohello segunda chave num par de Olá, crie um novo par de chaves.</span><span class="sxs-lookup"><span data-stu-id="98211-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="98211-140">Chaves de conta de armazenamento novas sempre são criadas pares, assegurando que tem sempre, pelo menos, um armazenamento utilizado conta chave pronto tooswitch para.</span><span class="sxs-lookup"><span data-stu-id="98211-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="98211-141">Visualizar chaves de conta de armazenamento Olá com Olá [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="98211-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="98211-142">Olá, chaves de conta de armazenamento para Olá denominado `mystorageaccount` estão listados na seguinte o exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="98211-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="98211-143">tooextract uma chave única, utilize Olá `--query` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="98211-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="98211-144">Olá exemplo seguinte extrai primeira chave de Olá (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="98211-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="98211-145">Crie a partilha de armazenamento de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="98211-145">Create hello File storage share.</span></span>

    <span data-ttu-id="98211-146">partilha de ficheiros de armazenamento Olá contém Olá partilha do SMB com [criar partilha de armazenamento az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="98211-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="98211-147">quota de Olá sempre é expresso em gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="98211-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="98211-148">Uma das chaves de Olá passar de Olá anterior `az storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="98211-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="98211-149">Crie uma partilha denominada mystorageshare com uma quota de 10 GB ao utilizar o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="98211-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="98211-150">Crie um diretório do ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="98211-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="98211-151">Crie um diretório local nas Olá de toomount ficheiros de Linux do Olá sistema partilha de SMB.</span><span class="sxs-lookup"><span data-stu-id="98211-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="98211-152">Nada escritas ou ler a partir do diretório de montagem local Olá é reencaminhado toohello partilha do SMB que está alojado no armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="98211-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="98211-153">toocreate um diretório local em/mnt/mymountdirectory, seguinte o exemplo de Olá de utilização:</span><span class="sxs-lookup"><span data-stu-id="98211-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="98211-154">Olá SMB partilha toohello local diretório de montagem.</span><span class="sxs-lookup"><span data-stu-id="98211-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="98211-155">Forneça o seu próprio nome de utilizador de conta de armazenamento e a chave de conta de armazenamento para as credenciais de montagem Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="98211-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="98211-156">Manter Olá SMB montar através de reinícios.</span><span class="sxs-lookup"><span data-stu-id="98211-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="98211-157">Quando reiniciar Olá VM com Linux, hello partilha SMB montada é desmontada durante o encerramento.</span><span class="sxs-lookup"><span data-stu-id="98211-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="98211-158">Olá tooremount partilha do SMB no arranque, adicionar uma linha de toohello Linux /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="98211-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="98211-159">Linux utiliza Olá fstab toolist Olá ficheiro sistemas de ficheiros que necessita de toomount durante o processo de arranque Olá.</span><span class="sxs-lookup"><span data-stu-id="98211-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="98211-160">Adicionar partilha SMB Olá garante que partilha do File storage Olá é um sistema de ficheiros permanentemente montado para Olá VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="98211-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="98211-161">Nova VM adicionar Olá ficheiro armazenamento SMB partilha tooa é possível ao utilizar init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="98211-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="98211-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="98211-162">Next steps</span></span>

- [<span data-ttu-id="98211-163">Nuvem init toocustomize uma VM com Linux a utilizar durante a criação</span><span class="sxs-lookup"><span data-stu-id="98211-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="98211-164">Adicionar um disco tooa VM com Linux</span><span class="sxs-lookup"><span data-stu-id="98211-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="98211-165">Encriptar discos uma VM com Linux utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="98211-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
