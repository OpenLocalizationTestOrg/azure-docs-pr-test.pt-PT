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
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="52c33-103">Carregar a conta de armazenamento de toolab ficheiro VHD utilizando o AzCopy</span><span class="sxs-lookup"><span data-stu-id="52c33-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="52c33-104">No Azure DevTest Labs, os ficheiros VHD podem ser imagens personalizadas toocreate utilizado, que são utilizados tooprovision máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="52c33-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="52c33-105">Olá, os seguintes passos guiá-lo utilizando tooupload de utilitário da linha de comandos do AzCopy Olá conta de armazenamento de um VHD ficheiro tooa laboratório.</span><span class="sxs-lookup"><span data-stu-id="52c33-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="52c33-106">Depois de carregar o ficheiro VHD, Olá [passos secção](#next-steps) lista alguns artigos que ilustram a forma como toocreate uma imagem personalizada do Olá carregado o ficheiro VHD.</span><span class="sxs-lookup"><span data-stu-id="52c33-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="52c33-107">Para obter mais informações sobre discos e VHDs no Azure, consulte [sobre discos e VHD para as máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="52c33-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="52c33-108">O AzCopy é um utilitário da linha de comandos só de Windows.</span><span class="sxs-lookup"><span data-stu-id="52c33-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="52c33-109">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="52c33-109">Step-by-step instructions</span></span>

<span data-ttu-id="52c33-110">Olá seguintes percurso de passos que através do carregar um VHD ficheiro tooAzure DevTest Labs utilizando [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="52c33-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="52c33-111">Obter o nome de Olá da conta de armazenamento do laboratório de Olá Olá portal do Azure a utilizar:</span><span class="sxs-lookup"><span data-stu-id="52c33-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="52c33-112">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="52c33-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="52c33-113">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="52c33-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="52c33-114">Na lista de Olá de laboratórios, selecione laboratório pretendido Olá.</span><span class="sxs-lookup"><span data-stu-id="52c33-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="52c33-115">No painel do laboratório de Olá, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="52c33-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="52c33-116">No laboratório Olá **configuração** painel, selecione **imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="52c33-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="52c33-117">No Olá **imagens personalizadas** painel, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="52c33-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="52c33-118">No Olá **imagem personalizada** painel, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="52c33-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="52c33-119">No Olá **VHD** painel, selecione **carregar um VHD com o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="52c33-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carregar o VHD com o PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="52c33-121">Olá **carregar uma imagem através do PowerShell** painel apresenta um toohello chamada **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="52c33-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="52c33-122">Olá primeiro parâmetro (*destino*) contém Olá URI para um contentor do blob (*carrega*) no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="52c33-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="52c33-123">Tome nota dos Olá completa URI porque é utilizado em passos posteriores.</span><span class="sxs-lookup"><span data-stu-id="52c33-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="52c33-124">Carregar ficheiro VHD Olá utilizando o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="52c33-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="52c33-125">[Transfira e instale Olá a versão mais recente do AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="52c33-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="52c33-126">Abra uma janela de comandos e navegue até o diretório de instalação do AzCopy toohello.</span><span class="sxs-lookup"><span data-stu-id="52c33-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="52c33-127">Opcionalmente, pode adicionar o caminho do sistema de tooyour instalação localização Olá AzCopy.</span><span class="sxs-lookup"><span data-stu-id="52c33-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="52c33-128">Por predefinição, o AzCopy é instalado toohello seguinte diretório:</span><span class="sxs-lookup"><span data-stu-id="52c33-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="52c33-129">Utilizar Olá conta chave e BLOBs de contentor de armazenamento URI, execute Olá seguinte comando na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="52c33-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="52c33-130">Olá *vhdFileName* . o valor tem toobe aspas.</span><span class="sxs-lookup"><span data-stu-id="52c33-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="52c33-131">processo de Olá de carregamento de um ficheiro VHD pode ser demorado, consoante o tamanho de ficheiro VHD Olá Olá e a velocidade da ligação.</span><span class="sxs-lookup"><span data-stu-id="52c33-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="52c33-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="52c33-132">Next steps</span></span>

- [<span data-ttu-id="52c33-133">Criar uma imagem personalizada no Azure DevTest Labs de um ficheiro VHD utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52c33-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="52c33-134">Criar uma imagem personalizada no Azure DevTest Labs de um ficheiro VHD utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="52c33-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)