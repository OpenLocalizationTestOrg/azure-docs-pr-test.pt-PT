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
# <a name="create-an-azure-remoteapp-image"></a>Criar uma imagem do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

O Azure RemoteApp utiliza imagens toohold Olá as aplicações que partilha com os seus utilizadores. (Iremos assumir a imagem e utilizá-lo toocreate VMs - que do que os utilizadores de Olá aceder quando iniciam sessão no Azure RemoteApp.) toocreate uma coleção do Azure RemoteApp com a sua seleção de aplicações, se se trata de nuvem ou híbrida, que comece por criar uma imagem com essas aplicações instaladas. Em seguida, crie uma coleção que utilize essa imagem, atribuir utilizadores toohello coleção e publicar os utilizadores toothose de aplicações.

Tem várias opções para criar ou utilizar imagens. básico Olá [requisito](remoteapp-imagereqs.md) para uma imagem é que executam o Windows Server 2012 R2 e ter a função de anfitrião de sessões de ambiente de trabalho remoto (RDSH) Olá instalada. Como obter que é onde obter interessantes coisas.

Tem Olá seguintes opções quando se trata tooimages:

* Pode importar e utilizar um [baseada em imagem numa máquina virtual do Azure](remoteapp-image-on-azurevm.md). Este é boa para aplicações de linha de negócio que necessitam de definições personalizadas. Pode personalizar Olá toowork de imagem para a aplicação Olá.
* Pode [criar e carregar uma imagem personalizada](remoteapp-create-custom-image.md). Este é boa se já tiver uma imagem que utilizar para a implementação de serviços de ambiente de trabalho remoto no local.
* Pode utilizar um Olá [imagens de modelo](remoteapp-images.md) incluídos na sua subscrição do RemoteApp. Estas imagens são criadas e mantido pela equipa do RemoteApp Olá e contenham algumas aplicações (como Olá Office suite) padrão que pode tornar disponível tooyour utilizadores. Tenha em atenção que imagem do Office 365 Pro Plus Olá só pode ser utilizada numa definição de produção.

Independentemente de onde pode obter a imagem ou como criar, poderá ser útil se compreende Olá toomake [requisitos da aplicação](remoteapp-appreqs.md) tooensure que a aplicação funciona bem em RemoteApp. Em seguida, o passo seguinte Olá é toocreate um [nuvem](remoteapp-create-cloud-deployment.md) ou [híbrida](remoteapp-create-hybrid-deployment.md) coleção.

