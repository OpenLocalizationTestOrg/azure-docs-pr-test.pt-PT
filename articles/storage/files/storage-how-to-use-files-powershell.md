---
title: aaaHow toouse PowerShell toomanage File storage do Azure | Microsoft Docs
description: Saiba toouse PowerShell toomanage File storage do Azure.
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Como toouse PowerShell toomanage File storage do Azure
Pode utilizar o Azure PowerShell toocreate e gerir partilhas de ficheiros.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Instalar os cmdlets do PowerShell Olá para o Storage do Azure
tooprepare toouse PowerShell, transfira e instale os cmdlets do PowerShell do Azure de Olá. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para Olá instalar instruções de instalação e do ponto.

> [!NOTE]
> Recomenda-se transferir e instalar ou atualizar o módulo Azure PowerShell mais recente do toohello.
> 
> 

Abra uma janela do Azure PowerShell ao clicar em **Iniciar** e escrever **Windows PowerShell**. janela do PowerShell Olá carrega o módulo do Azure Powershell Olá por si.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Criar um contexto para a conta de armazenamento e a chave
Crie um contexto de conta de armazenamento Olá. contexto de Olá encapsula Olá chave conta do storage nome e a conta. Para obter instruções sobre a cópia da sua chave de conta de Olá [portal do Azure](https://portal.azure.com), consulte [ver e copiar chaves de acesso de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Substitua `storage-account-name` e `storage-account-key` com o nome da conta de armazenamento e a chave no seguinte exemplo de Olá.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Criar uma nova partilha de ficheiros
Criar Olá nova partilha, com o nome `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

Tem agora uma partilha de ficheiros no Armazenamento de ficheiros. Em seguida, vamos adicionar um diretório e um ficheiro.

> [!IMPORTANT]
> Olá nome da partilha de ficheiros tem de ser todo em minúsculas. Para obter detalhes completos sobre a nomenclatura de partilhas de ficheiros e ficheiros, veja [Naming and Referencing Shares, Directories, Files, and Metadata (Nomenclatura e Referência de Partilhas, Diretórios, Ficheiros e Metadados)](https://msdn.microsoft.com/library/azure/dn167011.aspx).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Crie um diretório na partilha de ficheiros de Olá
Crie um diretório na partilha de Olá. Diretório de Olá com o nome no seguinte exemplo de Olá, `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Carregar um diretório do ficheiro local toohello
Agora carregue um diretório do ficheiro local toohello. Olá exemplo seguinte carrega um ficheiro de `C:\temp\Log1.txt`. Edite o caminho do ficheiro Olá para que aponte tooa ficheiro válido no seu computador local.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Listar Olá ficheiros no diretório de Olá
ficheiro de Olá toosee no diretório de Olá, pode listar todos os ficheiros do diretório de Olá. Este comando devolve Olá ficheiros e subdiretórios (se existir alguma) no diretório do Olá CustomLogs.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile devolve uma lista de ficheiros e diretórios para qualquer diretório no qual o objeto passa. "Get-AzureStorageFile-partilhar $s" devolve uma lista de ficheiros e diretórios no diretório de raiz de Olá. tooget uma lista de ficheiros num subdiretório, tem de toopass Olá subdiretório tooGet-AzureStorageFile. Que é que isto faz – Olá primeira parte comando Olá segurança toohello pipe devolve uma instância de diretório do subdiretório Olá CustomLogs. Em seguida, é passado para o Get-AzureStorageFile, que devolve Olá ficheiros e diretórios no CustomLogs.

## <a name="copy-files"></a>Copiar ficheiros
A partir da versão 0.9.7 do Azure PowerShell, pode copiar um ficheiro do ficheiro tooanother, um ficheiro tooa blob ou um ficheiro de tooa de blob. Abaixo, demonstramos como tooperform estes copiar operações utilizando os cmdlets do PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Passos seguintes
Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.

* [FAQ](../storage-files-faq.md)
* [Resolução de Problemas no Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Resolução de Problemas no Linux](storage-troubleshoot-linux-file-connection-problems.md)    