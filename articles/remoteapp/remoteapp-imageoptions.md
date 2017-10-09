---
title: aaaCreate uma imagem do Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as opções de Olá disponíveis para a criação de imagens para o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="bf332-103">Criar uma imagem do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bf332-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bf332-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="bf332-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bf332-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="bf332-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bf332-106">O Azure RemoteApp utiliza imagens toohold Olá as aplicações que partilha com os seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="bf332-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="bf332-107">(Iremos assumir a imagem e utilizá-lo toocreate VMs - que do que os utilizadores de Olá aceder quando iniciam sessão no Azure RemoteApp.) toocreate uma coleção do Azure RemoteApp com a sua seleção de aplicações, se se trata de nuvem ou híbrida, que comece por criar uma imagem com essas aplicações instaladas.</span><span class="sxs-lookup"><span data-stu-id="bf332-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="bf332-108">Em seguida, crie uma coleção que utilize essa imagem, atribuir utilizadores toohello coleção e publicar os utilizadores toothose de aplicações.</span><span class="sxs-lookup"><span data-stu-id="bf332-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="bf332-109">Tem várias opções para criar ou utilizar imagens.</span><span class="sxs-lookup"><span data-stu-id="bf332-109">You have several options for creating or using images.</span></span> <span data-ttu-id="bf332-110">básico Olá [requisito](remoteapp-imagereqs.md) para uma imagem é que executam o Windows Server 2012 R2 e ter a função de anfitrião de sessões de ambiente de trabalho remoto (RDSH) Olá instalada.</span><span class="sxs-lookup"><span data-stu-id="bf332-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="bf332-111">Como obter que é onde obter interessantes coisas.</span><span class="sxs-lookup"><span data-stu-id="bf332-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="bf332-112">Tem Olá seguintes opções quando se trata tooimages:</span><span class="sxs-lookup"><span data-stu-id="bf332-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="bf332-113">Pode importar e utilizar um [baseada em imagem numa máquina virtual do Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="bf332-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="bf332-114">Este é boa para aplicações de linha de negócio que necessitam de definições personalizadas.</span><span class="sxs-lookup"><span data-stu-id="bf332-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="bf332-115">Pode personalizar Olá toowork de imagem para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="bf332-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="bf332-116">Pode [criar e carregar uma imagem personalizada](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="bf332-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="bf332-117">Este é boa se já tiver uma imagem que utilizar para a implementação de serviços de ambiente de trabalho remoto no local.</span><span class="sxs-lookup"><span data-stu-id="bf332-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="bf332-118">Pode utilizar um Olá [imagens de modelo](remoteapp-images.md) incluídos na sua subscrição do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bf332-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="bf332-119">Estas imagens são criadas e mantido pela equipa do RemoteApp Olá e contenham algumas aplicações (como Olá Office suite) padrão que pode tornar disponível tooyour utilizadores.</span><span class="sxs-lookup"><span data-stu-id="bf332-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="bf332-120">Tenha em atenção que imagem do Office 365 Pro Plus Olá só pode ser utilizada numa definição de produção.</span><span class="sxs-lookup"><span data-stu-id="bf332-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="bf332-121">Independentemente de onde pode obter a imagem ou como criar, poderá ser útil se compreende Olá toomake [requisitos da aplicação](remoteapp-appreqs.md) tooensure que a aplicação funciona bem em RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bf332-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="bf332-122">Em seguida, o passo seguinte Olá é toocreate um [nuvem](remoteapp-create-cloud-deployment.md) ou [híbrida](remoteapp-create-hybrid-deployment.md) coleção.</span><span class="sxs-lookup"><span data-stu-id="bf332-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

