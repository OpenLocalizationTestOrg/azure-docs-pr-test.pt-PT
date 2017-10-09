---
title: aaaUpload VHD ficheiro tooAzure DevTest Labs utilizando o AzCopy | Microsoft Docs
description: Carregar a conta de armazenamento de toolab ficheiro VHD utilizando o AzCopy
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Carregar a conta de armazenamento de toolab ficheiro VHD utilizando o AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

No Azure DevTest Labs, os ficheiros VHD podem ser imagens personalizadas toocreate utilizado, que são utilizados tooprovision máquinas de virtuais. Olá, os seguintes passos guiá-lo utilizando tooupload de utilitário da linha de comandos do AzCopy Olá conta de armazenamento de um VHD ficheiro tooa laboratório. Depois de carregar o ficheiro VHD, Olá [passos secção](#next-steps) lista alguns artigos que ilustram a forma como toocreate uma imagem personalizada do Olá carregado o ficheiro VHD. Para obter mais informações sobre discos e VHDs no Azure, consulte [sobre discos e VHD para as máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> O AzCopy é um utilitário da linha de comandos só de Windows.

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Olá seguintes percurso de passos que através do carregar um VHD ficheiro tooAzure DevTest Labs utilizando [AzCopy](http://aka.ms/downloadazcopy). 

1. Obter o nome de Olá da conta de armazenamento do laboratório de Olá Olá portal do Azure a utilizar:

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de Olá.

1. Na lista de Olá de laboratórios, selecione laboratório pretendido Olá.  

1. No painel do laboratório de Olá, selecione **configuração**. 

1. No laboratório Olá **configuração** painel, selecione **imagens personalizadas (VHDs)**.

1. No Olá **imagens personalizadas** painel, selecione **+ adicionar**. 

1. No Olá **imagem personalizada** painel, selecione **VHD**.

1. No Olá **VHD** painel, selecione **carregar um VHD com o PowerShell**.

    ![Carregar o VHD com o PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Olá **carregar uma imagem através do PowerShell** painel apresenta um toohello chamada **Add-AzureVhd** cmdlet. Olá primeiro parâmetro (*destino*) contém Olá URI para um contentor do blob (*carrega*) no Olá seguinte formato:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Tome nota dos Olá completa URI porque é utilizado em passos posteriores.

1. Carregar ficheiro VHD Olá utilizando o AzCopy:
 
1. [Transfira e instale Olá a versão mais recente do AzCopy](http://aka.ms/downloadazcopy).

1. Abra uma janela de comandos e navegue até o diretório de instalação do AzCopy toohello. Opcionalmente, pode adicionar o caminho do sistema de tooyour instalação localização Olá AzCopy. Por predefinição, o AzCopy é instalado toohello seguinte diretório:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Utilizar Olá conta chave e BLOBs de contentor de armazenamento URI, execute Olá seguinte comando na linha de comandos Olá. Olá *vhdFileName* . o valor tem toobe aspas. processo de Olá de carregamento de um ficheiro VHD pode ser demorado, consoante o tamanho de ficheiro VHD Olá Olá e a velocidade da ligação.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Passos seguintes

- [Criar uma imagem personalizada no Azure DevTest Labs de um ficheiro VHD utilizando Olá portal do Azure](devtest-lab-create-template.md)
- [Criar uma imagem personalizada no Azure DevTest Labs de um ficheiro VHD utilizando o PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)