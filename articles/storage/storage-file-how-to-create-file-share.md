---
title: aaaHow toocreate uma partilha de ficheiros do Azure | Microsoft Docs
description: "Como toocreate um Azure partilha de ficheiros no File storage do Azure utilizando Olá portal do Azure, PowerShell e Olá CLI do Azure."
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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Criar uma Partilha de Ficheiros no armazenamento de Ficheiros do Azure
Pode criar partilhas de ficheiros do Azure utilizando [portal do Azure](https://portal.azure.com/), Olá cmdlets do PowerShell de armazenamento do Azure, Olá bibliotecas de cliente do Storage do Azure ou Olá API de REST do Storage do Azure. Neste tutorial, irá aprender:
* [Como toocreate um ficheiro de Azure partilhar utilizando Olá portal do Azure](#Create file share through hello Portal)
* [Como toocreate um Azure partilha de ficheiros com o Powershell](#Create file share using PowerShell)
* [Como toocreate um Azure partilha de ficheiros ao utilizar a CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Pré-requisitos
toocreate uma partilha de ficheiros do Azure, pode utilizar uma conta de armazenamento que já exista, ou [criar uma nova conta de armazenamento do Azure](storage-create-storage-account.md). toocreate uma partilha de ficheiros do Azure com o PowerShell, terá de chave de conta de Olá e o nome da conta de armazenamento... Precisa de chave de conta de armazenamento se planear toouse Powershell ou a CLI.

## <a name="create-file-share-through-hello-portal"></a>Criar partilha de ficheiros através de Olá Portal
1. **Aceda tooStorage painel de conta no Portal do Azure**:    
    ![Painel da Conta de Armazenamento](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **Clique no botão Adicionar Partilha de Ficheiros**:    
    ![Clique em Olá adicionar botão de partilha de ficheiros](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **Indique o Nome e a Quota. Atualmente, a quota pode ter um máximo de 5 TB**:    
    ![Forneça um nome e uma quota pretendida para a nova partilha de ficheiros Olá](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **Veja a partilha de ficheiros nova**: ![Veja a partilha de ficheiros nova](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **Carregue um ficheiro**: ![Carregue um ficheiro](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **Navegue para a partilha de ficheiros e faça a gestão dos seus diretórios e ficheiros**: ![Navegar para a partilha de ficheiros](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Criar a partilha de Ficheiros através do PowerShell
tooprepare toouse PowerShell, transfira e instale os cmdlets do PowerShell do Azure de Olá. Consulte [como tooinstall e configurar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para Olá instalar instruções de instalação e do ponto.

> [!Note]  
> Recomenda-se transferir e instalar ou atualizar o módulo Azure PowerShell mais recente do toohello.

1. **Criar um contexto para a conta de armazenamento e a chave** contexto Olá encapsula Olá chave conta do storage nome e a conta. Para obter instruções sobre a cópia da chave de conta a partir do [portal do Azure](https://portal.azure.com/), veja [View and copy storage access keys (Ver e copiar chaves de acesso de armazenamento)](storage-create-storage-account.md#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Criar uma partilha de ficheiros nova**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> Olá nome da partilha de ficheiros tem de ser todo em minúsculas. Para obter detalhes completos sobre a nomenclatura de partilhas de ficheiros e ficheiros, veja [Naming and Referencing Shares, Directories, Files, and Metadata (Nomenclatura e Referência de Partilhas, Diretórios, Ficheiros e Metadados)](https://msdn.microsoft.com/library/azure/dn167011.aspx).

## <a name="create-file-share-through-command-line-interface-cli"></a>Criar a partilha de Ficheiros através da Interface de Linha de Comandos (CLI)
1. **tooprepare toouse uma Interface de linha de comandos (CLI), transfira e instale Olá CLI do Azure.**  
    Veja [Instalar a CLI 2.0 do Azure](/cli/azure/install-az-cli2.md) e [Introdução à CLI 2.0 do Azure](/cli/azure/get-started-with-azure-cli.md).

2. **Crie uma ligação cadeia toohello armazenamento onde pretende que a partilha de Olá toocreate.**  
    Substitua ```<storage-account>``` e ```<resource_group>``` com o grupo de recursos e nome de conta de armazenamento no seguinte exemplo de Olá.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Criar partilha de ficheiros**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Passos seguintes
* [Connect and Mount File Share - Windows](storage-file-how-to-use-files-windows.md) (Ligar e Montar Partilha de Ficheiros - Windows)
* [Connect and Mount File Share - Linux](storage-how-to-use-files-linux.md) (Ligar e Montar Partilha de Ficheiros - Linux)
* [Connect and Mount File Share - macOS](storage-file-how-to-use-files-mac.md) (Ligar e Montar Partilha de Ficheiros - macOS)

Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.

* [FAQ](storage-files-faq.md)
* [Resolução de problemas](storage-troubleshoot-file-connection-problems.md)