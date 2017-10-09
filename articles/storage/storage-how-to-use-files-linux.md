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
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Utilizar o File storage do Azure com o Linux
[File storage do Azure](storage-dotnet-how-to-use-files.md) sistema de ficheiros de nuvem de fácil toouse da Microsoft. Partilhas de ficheiros do Azure podem ser montadas nas distribuições do Linux utilizando Olá [cifs utils pacote](https://wiki.samba.org/index.php/LinuxCIFS_utils) de Olá [projeto Samba](https://www.samba.org/). Este artigo mostra duas formas toomount uma partilha de ficheiros do Azure: a pedido com Olá `mount` comando e de arranque através da criação de uma entrada no `/etc/fstab`.

> [!NOTE]  
> Na ordem toomount uma partilha de ficheiros de Azure fora Olá região do Azure que está alojado, tal como no local ou numa região diferente do Azure, Olá SO deve suportar a funcionalidade de encriptação de Olá do SMB 3.0. Funcionalidade de encriptação para SMB 3.0 para Linux foi introduzida no 4.11 kernel. Esta funcionalidade permite a montagem do Azure da partilha de ficheiros no local ou uma região do Azure diferente. Momento Olá da publicação, esta funcionalidade foi backported tooUbuntu 16.04 e superior.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Prerequisities para montar uma partilha de ficheiros do Azure com o Linux e Olá pacote cifs utils
* **Escolha uma distribuição de Linux que pode ter o pacote de cifs utils Olá instalado**: a Microsoft recomenda Olá as distribuições do Linux na Galeria de imagem do Azure Olá os seguintes:

    * Ubuntu Server 14.04 +
    * RHEL 7 +
    * CentOS 7 +
    * Debian 8
    * openSUSE 13.2 +
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Olá cifs utils pacote está instalado**: Olá cifs-utils pode ser instalado utilizando o Gestor de pacotes de Olá na distribuição de Linux Olá à sua escolha. 

    No **Ubuntu** e **baseado em Debian** distribuições, utilize Olá `apt-get` Gestor de pacotes:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    No **RHEL** e **CentOS**, utilize Olá `yum` Gestor de pacotes:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    No **openSUSE**, utilize Olá `zypper` Gestor de pacotes:

    ```
    sudo zypper install samba*
    ```

    Em outras distribuições, utilize o Gestor de pacote adequado Olá ou [compilar a partir da origem](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Opte por utilizar permissões de diretório/ficheiro Olá de partilha montada Olá**: exemplos de Olá abaixo, utilizamos 0777, toogive ler, escrever e executar os utilizadores tooall de permissões. Pode ser substituído com outros [chmod permissões](https://en.wikipedia.org/wiki/Chmod) conforme pretendido. 

* **Nome da conta de armazenamento**: toomount partilha de um ficheiro do Azure, será necessário Olá nome Olá da conta de armazenamento.

* **Chave de conta de armazenamento**: a partilha de um ficheiro de Azure toomount, será necessário Olá chave de armazenamento () principais ou secundários. Atualmente, não são suportadas chaves SAS para a montagem.

* **Certifique-se de que a porta 445 está aberta**: SMB comunica através da porta TCP 445 - verifique toosee se a firewall não está a bloquear TCP portas 445 do computador cliente.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Montar Olá a pedido com partilha de ficheiros do Azure`mount`
1. **[Instalar o pacote de cifs utils Olá para a distribuição de Linux](#install-cifs-utils)**.

2. **Crie uma pasta para o ponto de montagem Olá**: Isto pode ser efetuado em qualquer local no sistema de ficheiros de Olá.

    ```
    mkdir mymountpoint
    ```

3. **Partilha de ficheiros de Azure ao hello do toomount de comando utilize Olá montagem**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações adequadas Olá.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Quando tiver terminado utilizando Olá a partilha de ficheiros do Azure, pode utilizar `sudo umount ./mymountpoint` partilha de Olá toounmount.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Criar um ponto de montagem persistente para partilha de ficheiros do Azure Olá com`/etc/fstab`
1. **[Instalar o pacote de cifs utils Olá para a distribuição de Linux](#install-cifs-utils)**.

2. **Crie uma pasta para o ponto de montagem Olá**: Isto pode ser efetuado em qualquer local no sistema de ficheiros de Olá, mas tem toonote Olá um caminho absoluto da pasta de Olá. Olá seguinte exemplo cria uma pasta na raiz.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Olá tooappend demasiado a seguinte linha de comandos seguinte Olá de utilização`/etc/fstab`**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações adequadas Olá.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Pode utilizar `sudo mount -a` partilha de ficheiros do Azure Olá toomount após editar `/etc/fstab` em vez de ser reiniciado.

## <a name="feedback"></a>Comentários
Utilizadores do Linux, queremos toohear da!

Olá File storage do Azure para o grupo de utilizadores do Linux fornece um fórum para si tooshare comentários à medida que avalia e que adotar o armazenamento de ficheiros no Linux. E-mail [File storage do Azure Linux utilizadores](mailto:azurefileslinuxusers@microsoft.com) grupo toojoin Olá dos utilizadores.

## <a name="next-steps"></a>Passos seguintes
Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.
* [File Service REST API reference (Referência da API REST do Serviço do Ficheiros)](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Com o Azure PowerShell com o storage do Azure](storage-powershell-guide-full.md)
* [Como toouse AzCopy com o storage do Microsoft Azure](storage-use-azcopy.md)
* [Utilizar Olá CLI do Azure com o storage do Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [FAQ](storage-files-faq.md)
* [Resolução de problemas](storage-troubleshoot-file-connection-problems.md)
