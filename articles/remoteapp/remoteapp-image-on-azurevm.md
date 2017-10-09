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
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Criar uma imagem do Azure RemoteApp com base numa máquina virtual do Azure
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Pode criar imagens do Azure RemoteApp (que contêm aplicações Olá que partilhar na sua coleção) a partir de uma máquina virtual do Azure. Pode também optar por toouse uma imagem de máquina virtual adicionámos Galeria de imagem de VM do Azure toohello que cumpra todos os requisitos de imagem do Azure RemoteApp Olá - pode utilizar essa imagem da VM como um ponto de partida para a própria VM, se pretender. Procure apenas imagem de "Windows Server ambiente de trabalho anfitrião de sessões remoto" Olá na biblioteca de Olá.

Existem dois toocreate passos a sua própria imagem com base numa VM do Azure - criar Olá imagem e, em seguida, carregue-o partir tooAzure de biblioteca Olá VM do Azure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Criar uma imagem personalizada com base numa VM do Azure
Utilize estes passos toocreate uma imagem com base numa VM do Azure.

1. Crie uma máquina virtual do Azure. Pode utilizar Olá "Windows Server ambiente de trabalho anfitrião de sessões remoto" ou imagem "Windows Server remoto ambiente de trabalho sessão anfitrião com o Microsoft Office 365 ProPlus" Olá da Galeria de imagem de máquina virtual do Azure Olá. Esta imagem satisfaz todos os requisitos de imagem de modelo do Olá Azure RemoteApp.
   
    Para obter mais informações, consulte [criar uma VM com o Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Ligar toohello VM e instalar e configurar aplicações Olá que pretende que o tooshare através do RemoteApp. Certifique-se de que tooperform quaisquer configurações adicionais do Windows necessárias para as suas aplicações.
   
    Para obter mais informações, consulte [como tooLog no tooa Máquina Virtual a executar o Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Se estiver a utilizar uma das imagens de anfitrião de sessões de ambiente de trabalho remoto do Windows Server Olá, há um script de validação incluídos irá garantir que a VM cumpre Olá RemoteApp pre-reqs. script de toorun, faça duplo clique em **ValidateRemoteAppImage** no ambiente de trabalho Olá. Certifique-se de que todos os erros comunicados pelo script de Olá sejam corrigidos antes do passo seguinte do toohello continuar.
4. SYSPREP generalize e capture a imagem de Olá. Consulte [como tooCapture tooUse uma Máquina Virtual do Windows como um modelo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obter instruções.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Importar imagem Olá para a biblioteca de imagens do Azure RemoteApp Olá
Utilize estes passos tooimport Olá nova imagem para o Azure RemoteApp:

1. No Olá **imagens de modelo** separador:
   
   * Se tiver não imagens existentes, clique em **carregar ou importar uma imagem de modelo**.
   * Se já tiver, pelo menos, uma imagem, clique em  **+**  tooadd uma nova imagem.
2. Selecione **importar uma imagem das suas máquinas virtuais** biblioteca e, em seguida, clique em **seguinte**.
3. Na página seguinte do Olá, selecione a sua imagem personalizada da lista de Olá e confirme que seguiu os passos de Olá apresentados quando criou a imagem. Clique em **Seguinte**.
4. Introduza um nome para a nova imagem do RemoteApp Olá e escolha a localização de Olá e, em seguida, clique em processo de importação do Olá marca de verificação toostart Olá.

> [!NOTE]
> Pode importar imagens a partir de qualquer localização do Azure suportada pelo Virtual Machines do Azure tooany localização do Azure suportada pelo Azure RemoteApp. Dependendo das localizações de Olá importação Olá pode demorar até too25 minutos.
> 
> 

Agora, está pronto toocreate sua nova coleção, se um [nuvem](remoteapp-create-cloud-deployment.md) coleção ou [híbrida](remoteapp-create-hybrid-deployment.md), dependendo das suas necessidades.

