---
title: "partilham de aaaMount uma partilha de ficheiros do Azure e Olá de acesso no Windows | Microsoft Docs"
description: "Monte uma partilha de ficheiros do Azure e a partilha de Olá de acesso no Windows."
services: storage
documentationcenter: na
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
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Montar uma partilha de ficheiros do Azure e a partilha de Olá de acesso no Windows
[File storage do Azure](../storage-dotnet-how-to-use-files.md) sistema de ficheiros de nuvem de fácil toouse da Microsoft. As partilhas de Ficheiros do Azure podem ser montadas no Windows e no Windows Server. Este artigo mostra três formas diferentes toomount uma partilha de ficheiros do Azure no Windows: com Olá IU do Explorador de ficheiros, através do PowerShell e através de Olá linha de comandos. 

Na ordem toomount um Azure de partilha de ficheiros fora Olá região do Azure está alojado no, tal como no local ou numa região diferente do Azure, Olá SO tem de suportar SMB 3.0. 

A partilha de Ficheiros do Azure pode ser montada num computador Windows no local ou numa VM do Azure, dependendo da versão do SO. Tabela abaixo ilustra Olá 

| Versão do Windows        | Versão do SMB |Montável em VM do Azure|Montável no Local|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Sim                 | Não                  |
| Windows Server 2008 R2 | SMB 2.1     | Sim                 | Não                  |
| Windows 8              | SMB 3.0     | Sim                 | Sim                 |
| Windows Server 2012    | SMB 3.0     | Sim                 | Sim                 |
| Windows Server 2012 R2 | SMB 3.0     | Sim                 | Sim                 |
| Windows 10             | SMB 3.0     | Sim                 | Sim                 |

> [!Note]  
> Recomendamos sempre tendo hello mais recente KB para a sua versão do Windows.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Pré-requisitos para Montar a Partilha de Ficheiros do Azure com o Windows 
* **Nome da conta de armazenamento**: toomount partilha de um ficheiro do Azure, será necessário Olá nome Olá da conta de armazenamento.

* **Chave de conta de armazenamento**: a partilha de um ficheiro de Azure toomount, será necessário Olá chave de armazenamento () principais ou secundários. Atualmente, não são suportadas chaves SAS para a montagem.

* **Confirme que a porta 445 está aberta**: o armazenamento de Ficheiros do Azure utiliza o protocolo SMB. SMB comunica através da porta TCP 445 - Verifique o toosee se a firewall não está a bloquear as portas TCP 445 do computador cliente.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Montar a partilha de ficheiros do Azure Olá com o Explorador de ficheiros
> [!Note]  
> Tenha em atenção que Olá instruções a seguir são apresentadas no Windows 10 e poderão ser algo diferentes em versões mais antigas. 

1. **Abra o Explorador de ficheiros**: Isto pode ser feito através da abertura de Olá Menu Iniciar ou premindo atalho Win + I.

2. **Navegue até o item de "Este PC" toohello no lado esquerdo Olá da janela de Olá. Isto vai alterar menus Olá disponíveis no Friso de Olá. No menu de computador Olá, selecione "Unidade de rede de mapa"**.
    
    ![Uma captura de ecrã de Olá "Unidade de rede de mapa" menu pendente](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Caminho UNC Olá cópia a partir do painel de "Ligar" Olá no portal do Azure de Olá**: uma descrição detalhada do como toofind estas informações podem ser encontradas [aqui](storage-how-to-use-files-portal.md#connect-to-file-share).

    ![caminho UNC Olá a partir do painel de ligação de armazenamento de ficheiros do Azure Olá](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. **Selecione a letra de unidade de Olá e introduza o caminho UNC Olá.** 
    
    ![Uma captura de ecrã da caixa de diálogo de "Unidade de rede de mapa" Olá](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Olá utilize prepended com o nome da conta de armazenamento `Azure\` como Olá nome de utilizador e uma chave de conta de armazenamento como palavra-passe de Olá.**
    
    ![Uma captura de ecrã da caixa de diálogo de credenciais de rede Olá](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Utilize a patilha de Ficheiros do Azure como pretendido**.
    
    ![A partilha de Ficheiros do Azure está agora montada](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Quando está pronto toodismount (a ou desligar) partilha de ficheiros do Azure Olá, pode fazer com o botão direito clicando na entrada de Olá para partilha de Olá Olá "localizações de rede" no Explorador de ficheiros e selecionando "Desligar"**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Montar a partilha de ficheiros do Azure Olá com o PowerShell
1. **Seguinte de Olá utilize comando partilha de ficheiros do Azure de Olá toomount**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações adequadas Olá.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Partilha de ficheiros do Azure Olá utilização conforme o desejado**.

3. **Quando tiver terminado, desmontar a partilha de ficheiros do Azure de Olá utilizando Olá os seguintes comandos**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Pode utilizar Olá `-Persist` parâmetro no `New-PSDrive` toomake Olá ficheiros do Azure partilha toohello visível restante Olá SO enquanto montada.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Montar a partilha de ficheiros do Azure Olá com linha de comandos
1. **Seguinte de Olá utilize comando partilha de ficheiros do Azure de Olá toomount**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações adequadas Olá.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Partilha de ficheiros do Azure Olá utilização conforme o desejado**.

3. **Quando tiver terminado, desmontar a partilha de ficheiros do Azure de Olá utilizando Olá os seguintes comandos**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Pode configurar Olá ficheiros do Azure partilha tooautomatically restabelecer a ligação em reinício por persistentes Olá credenciais no Windows. Olá seguir comando serão mantidas credenciais Olá:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Passos seguintes
Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.

* [FAQ](../storage-files-faq.md)
* [Resolução de Problemas no Windows](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos concetuais
* [Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Armazenamento de Ficheiros do Azure: um prático sistema de ficheiros SMB na cloud para Windows e Linux)
* [Como toouse File storage do Azure com o Linux](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Suporte de ferramentas para o armazenamento de Ficheiros do Azure
* [Como toouse AzCopy com armazenamento do Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Utilizar Olá CLI do Azure com o Storage do Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Resolução de problemas do armazenamento de Ficheiros do Azure - Windows](storage-troubleshoot-windows-file-connection-problems.md)
* [Resolução de problemas do armazenamento de Ficheiros do Azure - Linux](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Publicações no blogue
* [Azure File storage is now generally available (O Armazenamento de Ficheiros do Azure está agora disponível normalmente)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Por dentro do armazenamento de Ficheiros do Azure)
* [Introducing Microsoft Azure File Service (Introdução ao Serviço de Ficheiros do Microsoft Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrar dados tooAzure ficheiro](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referência
* [Storage Client Library for .NET reference (Referência da Biblioteca de Clientes do Armazenamento para .NET)](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [File Service REST API reference (Referência da API REST do Serviço do Ficheiros)](http://msdn.microsoft.com/library/azure/dn167006.aspx)
