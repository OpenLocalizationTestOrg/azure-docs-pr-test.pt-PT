---
title: aaaUse File storage do Azure com o Linux | Microsoft Docs
description: Saiba como toomount um ficheiro de Azure partilha SMB no Linux.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="025e4-103">Utilizar o File storage do Azure com o Linux</span><span class="sxs-lookup"><span data-stu-id="025e4-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="025e4-104">[File storage do Azure](../storage-dotnet-how-to-use-files.md) sistema de ficheiros de nuvem de fácil toouse da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="025e4-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="025e4-105">Partilhas de ficheiros do Azure podem ser montadas nas distribuições do Linux utilizando Olá [cifs utils pacote](https://wiki.samba.org/index.php/LinuxCIFS_utils) de Olá [projeto Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="025e4-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="025e4-106">Este artigo mostra duas formas toomount uma partilha de ficheiros do Azure: a pedido com Olá `mount` comando e de arranque através da criação de uma entrada no `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="025e4-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="025e4-107">Na ordem toomount uma partilha de ficheiros de Azure fora Olá região do Azure que está alojado, tal como no local ou numa região diferente do Azure, Olá SO deve suportar a funcionalidade de encriptação de Olá do SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="025e4-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="025e4-108">Funcionalidade de encriptação para SMB 3.0 para Linux foi introduzida no 4.11 kernel.</span><span class="sxs-lookup"><span data-stu-id="025e4-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="025e4-109">Esta funcionalidade permite a montagem do Azure da partilha de ficheiros no local ou uma região do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="025e4-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="025e4-110">Momento Olá da publicação, esta funcionalidade foi backported tooUbuntu 16.04 e superior.</span><span class="sxs-lookup"><span data-stu-id="025e4-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="025e4-111">Prerequisities para montar uma partilha de ficheiros do Azure com o Linux e Olá pacote cifs utils</span><span class="sxs-lookup"><span data-stu-id="025e4-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="025e4-112">**Escolha uma distribuição de Linux que pode ter o pacote de cifs utils Olá instalado**: a Microsoft recomenda Olá as distribuições do Linux na Galeria de imagem do Azure Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="025e4-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="025e4-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="025e4-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="025e4-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="025e4-114">RHEL 7+</span></span>
    * <span data-ttu-id="025e4-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="025e4-115">CentOS 7+</span></span>
    * <span data-ttu-id="025e4-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="025e4-116">Debian 8</span></span>
    * <span data-ttu-id="025e4-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="025e4-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="025e4-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="025e4-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="025e4-119"><a id="install-cifs-utils"></a>**Olá cifs utils pacote está instalado**: Olá cifs-utils pode ser instalado utilizando o Gestor de pacotes de Olá na distribuição de Linux Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="025e4-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="025e4-120">No **Ubuntu** e **baseado em Debian** distribuições, utilize Olá `apt-get` Gestor de pacotes:</span><span class="sxs-lookup"><span data-stu-id="025e4-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="025e4-121">No **RHEL** e **CentOS**, utilize Olá `yum` Gestor de pacotes:</span><span class="sxs-lookup"><span data-stu-id="025e4-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="025e4-122">No **openSUSE**, utilize Olá `zypper` Gestor de pacotes:</span><span class="sxs-lookup"><span data-stu-id="025e4-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="025e4-123">Em outras distribuições, utilize o Gestor de pacote adequado Olá ou [compilar a partir da origem](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="025e4-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="025e4-124">**Opte por utilizar permissões de diretório/ficheiro Olá de partilha montada Olá**: exemplos de Olá abaixo, utilizamos 0777, toogive ler, escrever e executar os utilizadores tooall de permissões.</span><span class="sxs-lookup"><span data-stu-id="025e4-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="025e4-125">Pode ser substituído com outros [chmod permissões](https://en.wikipedia.org/wiki/Chmod) conforme pretendido.</span><span class="sxs-lookup"><span data-stu-id="025e4-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="025e4-126">**Nome da conta de armazenamento**: toomount partilha de um ficheiro do Azure, será necessário Olá nome Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="025e4-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="025e4-127">**Chave de conta de armazenamento**: a partilha de um ficheiro de Azure toomount, será necessário Olá chave de armazenamento () principais ou secundários.</span><span class="sxs-lookup"><span data-stu-id="025e4-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="025e4-128">Atualmente, não são suportadas chaves SAS para a montagem.</span><span class="sxs-lookup"><span data-stu-id="025e4-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="025e4-129">**Certifique-se de que a porta 445 está aberta**: SMB comunica através da porta TCP 445 - verifique toosee se a firewall não está a bloquear TCP portas 445 do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="025e4-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="025e4-130">Montar Olá a pedido com partilha de ficheiros do Azure`mount`</span><span class="sxs-lookup"><span data-stu-id="025e4-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="025e4-131">**[Instalar o pacote de cifs utils Olá para a distribuição de Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="025e4-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="025e4-132">**Crie uma pasta para o ponto de montagem Olá**: Isto pode ser efetuado em qualquer local no sistema de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e4-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="025e4-133">**Partilha de ficheiros de Azure ao hello do toomount de comando utilize Olá montagem**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="025e4-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="025e4-134">Quando tiver terminado utilizando Olá a partilha de ficheiros do Azure, pode utilizar `sudo umount ./mymountpoint` partilha de Olá toounmount.</span><span class="sxs-lookup"><span data-stu-id="025e4-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="025e4-135">Criar um ponto de montagem persistente para partilha de ficheiros do Azure Olá com`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="025e4-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="025e4-136">**[Instalar o pacote de cifs utils Olá para a distribuição de Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="025e4-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="025e4-137">**Crie uma pasta para o ponto de montagem Olá**: Isto pode ser efetuado em qualquer local no sistema de ficheiros de Olá, mas tem toonote Olá um caminho absoluto da pasta de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e4-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="025e4-138">Olá seguinte exemplo cria uma pasta na raiz.</span><span class="sxs-lookup"><span data-stu-id="025e4-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="025e4-139">**Olá tooappend demasiado a seguinte linha de comandos seguinte Olá de utilização`/etc/fstab`**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="025e4-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="025e4-140">Pode utilizar `sudo mount -a` partilha de ficheiros do Azure Olá toomount após editar `/etc/fstab` em vez de ser reiniciado.</span><span class="sxs-lookup"><span data-stu-id="025e4-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="025e4-141">Comentários</span><span class="sxs-lookup"><span data-stu-id="025e4-141">Feedback</span></span>
<span data-ttu-id="025e4-142">Utilizadores do Linux, queremos toohear da!</span><span class="sxs-lookup"><span data-stu-id="025e4-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="025e4-143">Olá File storage do Azure para o grupo de utilizadores do Linux fornece um fórum para si tooshare comentários à medida que avalia e que adotar o armazenamento de ficheiros no Linux.</span><span class="sxs-lookup"><span data-stu-id="025e4-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="025e4-144">E-mail [File storage do Azure Linux utilizadores](mailto:azurefileslinuxusers@microsoft.com) grupo toojoin Olá dos utilizadores.</span><span class="sxs-lookup"><span data-stu-id="025e4-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="025e4-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="025e4-145">Next steps</span></span>
<span data-ttu-id="025e4-146">Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e4-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="025e4-147">File Service REST API reference (Referência da API REST do Serviço do Ficheiros)</span><span class="sxs-lookup"><span data-stu-id="025e4-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="025e4-148">Como toouse AzCopy com o storage do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="025e4-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="025e4-149">Utilizar Olá CLI do Azure com o storage do Azure</span><span class="sxs-lookup"><span data-stu-id="025e4-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="025e4-150">FAQ</span><span class="sxs-lookup"><span data-stu-id="025e4-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="025e4-151">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="025e4-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
