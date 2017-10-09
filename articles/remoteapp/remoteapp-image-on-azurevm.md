---
title: aaaCreate uma imagem do Azure RemoteApp com base numa VM do Azure | Microsoft Docs
description: "Saiba como toocreate uma imagem para o Azure RemoteApp, começando por uma máquina virtual do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="50736-103">Criar uma imagem do Azure RemoteApp com base numa máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="50736-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="50736-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="50736-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="50736-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="50736-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="50736-106">Pode criar imagens do Azure RemoteApp (que contêm aplicações Olá que partilhar na sua coleção) a partir de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="50736-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="50736-107">Pode também optar por toouse uma imagem de máquina virtual adicionámos Galeria de imagem de VM do Azure toohello que cumpra todos os requisitos de imagem do Azure RemoteApp Olá - pode utilizar essa imagem da VM como um ponto de partida para a própria VM, se pretender.</span><span class="sxs-lookup"><span data-stu-id="50736-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="50736-108">Procure apenas imagem de "Windows Server ambiente de trabalho anfitrião de sessões remoto" Olá na biblioteca de Olá.</span><span class="sxs-lookup"><span data-stu-id="50736-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="50736-109">Existem dois toocreate passos a sua própria imagem com base numa VM do Azure - criar Olá imagem e, em seguida, carregue-o partir tooAzure de biblioteca Olá VM do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="50736-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="50736-110">Criar uma imagem personalizada com base numa VM do Azure</span><span class="sxs-lookup"><span data-stu-id="50736-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="50736-111">Utilize estes passos toocreate uma imagem com base numa VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="50736-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="50736-112">Crie uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="50736-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="50736-113">Pode utilizar Olá "Windows Server ambiente de trabalho anfitrião de sessões remoto" ou imagem "Windows Server remoto ambiente de trabalho sessão anfitrião com o Microsoft Office 365 ProPlus" Olá da Galeria de imagem de máquina virtual do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="50736-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="50736-114">Esta imagem satisfaz todos os requisitos de imagem de modelo do Olá Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="50736-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="50736-115">Para obter mais informações, consulte [criar uma VM com o Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50736-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="50736-116">Ligar toohello VM e instalar e configurar aplicações Olá que pretende que o tooshare através do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="50736-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="50736-117">Certifique-se de que tooperform quaisquer configurações adicionais do Windows necessárias para as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="50736-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="50736-118">Para obter mais informações, consulte [como tooLog no tooa Máquina Virtual a executar o Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50736-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="50736-119">Se estiver a utilizar uma das imagens de anfitrião de sessões de ambiente de trabalho remoto do Windows Server Olá, há um script de validação incluídos irá garantir que a VM cumpre Olá RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="50736-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="50736-120">script de toorun, faça duplo clique em **ValidateRemoteAppImage** no ambiente de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="50736-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="50736-121">Certifique-se de que todos os erros comunicados pelo script de Olá sejam corrigidos antes do passo seguinte do toohello continuar.</span><span class="sxs-lookup"><span data-stu-id="50736-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="50736-122">SYSPREP generalize e capture a imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="50736-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="50736-123">Consulte [como tooCapture tooUse uma Máquina Virtual do Windows como um modelo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="50736-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="50736-124">Importar imagem Olá para a biblioteca de imagens do Azure RemoteApp Olá</span><span class="sxs-lookup"><span data-stu-id="50736-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="50736-125">Utilize estes passos tooimport Olá nova imagem para o Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="50736-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="50736-126">No Olá **imagens de modelo** separador:</span><span class="sxs-lookup"><span data-stu-id="50736-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="50736-127">Se tiver não imagens existentes, clique em **carregar ou importar uma imagem de modelo**.</span><span class="sxs-lookup"><span data-stu-id="50736-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="50736-128">Se já tiver, pelo menos, uma imagem, clique em  **+**  tooadd uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="50736-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="50736-129">Selecione **importar uma imagem das suas máquinas virtuais** biblioteca e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="50736-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="50736-130">Na página seguinte do Olá, selecione a sua imagem personalizada da lista de Olá e confirme que seguiu os passos de Olá apresentados quando criou a imagem.</span><span class="sxs-lookup"><span data-stu-id="50736-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="50736-131">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="50736-131">Click **Next**.</span></span>
4. <span data-ttu-id="50736-132">Introduza um nome para a nova imagem do RemoteApp Olá e escolha a localização de Olá e, em seguida, clique em processo de importação do Olá marca de verificação toostart Olá.</span><span class="sxs-lookup"><span data-stu-id="50736-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="50736-133">Pode importar imagens a partir de qualquer localização do Azure suportada pelo Virtual Machines do Azure tooany localização do Azure suportada pelo Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="50736-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="50736-134">Dependendo das localizações de Olá importação Olá pode demorar até too25 minutos.</span><span class="sxs-lookup"><span data-stu-id="50736-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="50736-135">Agora, está pronto toocreate sua nova coleção, se um [nuvem](remoteapp-create-cloud-deployment.md) coleção ou [híbrida](remoteapp-create-hybrid-deployment.md), dependendo das suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="50736-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

