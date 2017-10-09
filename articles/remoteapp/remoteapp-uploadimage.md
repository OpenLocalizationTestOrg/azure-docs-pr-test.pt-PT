---
title: aaaUpload uma imagem personalizada para o Azure RemoteApp | Microsoft Docs
description: Saiba como tooupload personalizadas de imagem para o Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="bbf14-103">Carregar uma imagem personalizada para o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bbf14-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bbf14-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="bbf14-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bbf14-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="bbf14-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bbf14-106">Agora que criou a imagem de modelo personalizado ou Atualizou com as alterações, terá de tooupload biblioteca de imagens essa imagem tooyour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bbf14-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="bbf14-107">Utilize estes passos.</span><span class="sxs-lookup"><span data-stu-id="bbf14-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="bbf14-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bbf14-108">Before you start</span></span>
1. <span data-ttu-id="bbf14-109">Verificar a sua imagem personalizada cumpre Olá [requisitos de imagem](remoteapp-imagereqs.md) e [os requisitos da aplicação](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="bbf14-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="bbf14-110">Instalar Olá [módulo Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bbf14-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="bbf14-111">Passo a passo sobre como imagem personalizada tooupload</span><span class="sxs-lookup"><span data-stu-id="bbf14-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="bbf14-112">Abra o Portal de gestão do Azure e navegue toohello RemoteApp página.</span><span class="sxs-lookup"><span data-stu-id="bbf14-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="bbf14-113">No Olá **imagens de modelo** separador, clique em **carregar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="bbf14-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="bbf14-114">Introduza um nome amigável para a imagem e especifique a localização de conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="bbf14-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="bbf14-115">Certifique-se de localização de Olá Olá mesma localização que a coleção do RemoteApp ou para uma localização onde pretende toocreate um.</span><span class="sxs-lookup"><span data-stu-id="bbf14-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="bbf14-116">Quando lhe for pedido, transferir Olá script tooyour local PC.</span><span class="sxs-lookup"><span data-stu-id="bbf14-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="bbf14-117">Copie os parâmetros de comando de Olá na área de transferência do Olá texto caixa tooyour.</span><span class="sxs-lookup"><span data-stu-id="bbf14-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="bbf14-118">Abra uma janela elevada do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbf14-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="bbf14-119">De Olá elevados janela do Windows PowerShell, navegue até toohello mesmo diretório onde transferiu o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="bbf14-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="bbf14-120">Olá colar copiados comandos e prima **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bbf14-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="bbf14-121">processo de carregamento de Olá começará e duração pode depender de vários fatores, incluindo a velocidade da rede e o tamanho da imagem de Olá</span><span class="sxs-lookup"><span data-stu-id="bbf14-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="bbf14-122">Se o seu carregamento falhar devido a interrupção de rede ou coisas como ou, pode sempre retomar o processo de carregamento de Olá que começou.</span><span class="sxs-lookup"><span data-stu-id="bbf14-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="bbf14-123">tooresume um carregamento, executar script de Olá novamente utilizando Olá a mesma linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="bbf14-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="bbf14-124">Nunca modificar o script de carregamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="bbf14-124">Never modify hello upload script.</span></span> <span data-ttu-id="bbf14-125">Verificações específicos tem sido implementado tooensure que Olá imagem cumpre os requisitos de imagem Olá e os requisitos da aplicação.</span><span class="sxs-lookup"><span data-stu-id="bbf14-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="bbf14-126">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="bbf14-126">Common problems</span></span>
* <span data-ttu-id="bbf14-127">Certifique-se de que utilizar o Windows PowerShell, não o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbf14-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="bbf14-128">Terá de módulo de Azure PowerShell tooinstall Olá porque determinados módulos são necessários durante o processo de carregamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="bbf14-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="bbf14-129">Nunca alter script Olá, validações existem para sua comodidade.</span><span class="sxs-lookup"><span data-stu-id="bbf14-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="bbf14-130">Se o ficheiro de vhd Olá obtém bloqueado durante o carregamento, copie o ficheiro de Olá ou movê-la tooa nova localização e a tentativa de carregamento novamente.</span><span class="sxs-lookup"><span data-stu-id="bbf14-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="bbf14-131">Poderão existir alguns processo do Windows que está a impedir o carregamento.</span><span class="sxs-lookup"><span data-stu-id="bbf14-131">There might be some Windows process that is preventing upload.</span></span>  

