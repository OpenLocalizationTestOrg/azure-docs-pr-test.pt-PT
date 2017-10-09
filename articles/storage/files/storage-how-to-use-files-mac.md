---
title: "partilha de ficheiros do Azure aaaMount através de SMB com macOS | Microsoft Docs"
description: "Saiba como partilhar toomount um ficheiro do Azure através de SMB com macOS."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Montar uma partilha de Ficheiros do Azure através de SMB com macOS
[File storage do Azure](../storage-dotnet-how-to-use-files.md) é serviço da Microsoft que lhe permite toocreate e utilizar partilhas de ficheiros de rede no Olá do Azure utilizando o padrão da indústria de Olá. As partilhas de Ficheiros do Azure podem ser montadas no macOS Sierra (10.12) e El Capitan (10.11). Este artigo mostra duas formas diferentes toomount uma partilha de ficheiros do Azure no macOS com Olá LCA IU e utilizando Olá Terminal.

> [!Note]  
> Antes de montar uma partilha de Ficheiros do Azure através de SMB, recomendamos desativar a assinatura de pacotes SMB. Não se o fizer, poderá produzir fraco desempenho quando aceder à partilha de ficheiros do Azure Olá partir macOS. A ligação de SMB será encriptada, pelo que isto não afeta a segurança de Olá da sua ligação. De Olá terminal, Olá comandos seguintes irão desativar a assinatura do pacote SMB, conforme descrito por este [artigo de suporte da Apple no desativar a assinatura do pacote SMB](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Pré-requisitos para montar uma partilha de Ficheiros do Azure em macOS
* **Nome da conta de armazenamento**: toomount partilha de um ficheiro do Azure, será necessário Olá nome Olá da conta de armazenamento.

* **Chave de conta de armazenamento**: a partilha de um ficheiro de Azure toomount, será necessário Olá chave de armazenamento () principais ou secundários. Atualmente, não são suportadas chaves SAS para a montagem.

* **Confirme que a porta 445 está aberta**: o SMB comunica através da porta TCP 445. No computador de cliente (Olá Mac), verifique se que a firewall não está a bloquear a porta TCP 445 toomake.

## <a name="mount-an-azure-file-share-via-finder"></a>Montar uma partilha de Ficheiros do Azure através do Finder
1. **Abrir LCA**: LCA está aberta no macOS por predefinição, mas pode garantir é Olá selecionado atualmente no Olá ancoragem aplicação clicando Olá "o macOS enfrentam ícone":  
    ![Olá macOS enfrentam ícone](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Selecione "Ligar tooServer" Olá "Ir" Menu**: utilizando o caminho UNC Olá de Olá [pré-requisitos](#preq), converter barra invertida duplo do Olá início (`\\`) demasiado`smb://` e todos os outras barras invertidas (`\`) barras tooforwards (`/`). A ligação deverá ter um aspeto semelhante Olá: ![caixa de diálogo de "Ligar tooServer" Olá](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Utilize Olá partilha de armazenamento e de nome de chave de conta quando lhe for pedido um nome de utilizador e palavra-passe**: quando clicar em "Ligar" da caixa de diálogo de "Ligar tooServer" Olá, será solicitado para Olá nome de utilizador e palavra-passe (tal será autopopulated com seu macOS nome de utilizador). Tem a opção Olá de colocar a chave de conta de armazenamento/nome de partilha de Olá no seu macOS Keychain.

4. **Partilha de ficheiros do Azure Olá utilização conforme o desejado**: após substituindo Olá partilha de armazenamento e o nome da chave de conta no Olá nome de utilizador e palavra-passe, será possível montar a partilha de Olá. Pode utilizar este que normalmente utilizaria uma partilha de pasta/ficheiro local, incluindo, arrastar e largar os ficheiros numa partilha de ficheiros de Olá:

    ![Instantâneo de uma partilha de Ficheiros do Azure montada](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Montar uma partilha de Ficheiros do Azure através do Terminal
1. Substitua `<storage-account-name>` com o nome de Olá da sua conta de armazenamento. Indique a Chave da Conta de Armazenamento como a palavra-passe, quando lhe for pedido. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Partilha de ficheiros do Azure Olá utilização conforme o desejado**: partilha de ficheiros do Azure Olá será montada no ponto de montagem Olá especificado pelo comando anterior Olá.  

    ![Um instantâneo de Olá montar a partilha de ficheiros do Azure](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Passos seguintes
Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.

* [Artigo de suporte de Apple - como tooconnect com partilha de ficheiros no Mac](https://support.apple.com/HT204445)
* [FAQ](../storage-files-faq.md)
* [Resolução de Problemas no Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Resolução de Problemas no Linux](storage-troubleshoot-linux-file-connection-problems.md)    