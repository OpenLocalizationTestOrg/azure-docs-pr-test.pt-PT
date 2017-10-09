---
title: "aaaTroubleshoot RemoteApp as coleções na nuvem - criação | Microsoft Docs"
description: "Saiba como tootroubleshoot RemoteApp cloud falhas na criação de coleção"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Criar coleções do RemoteApp na nuvem de resolução de problemas
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Se estiver a ter problemas ao criar uma coleção na nuvem, consulte Olá informações a seguir.

## <a name="your-image-is-invalid"></a>A imagem é inválida
Se vir uma mensagem como "GoldImageInvalid" quando que está a aguardar tooprovision do Azure a coleção, significa que a imagem de modelo não cumpre os Olá [definido requisitos de imagem](remoteapp-imagereqs.md). Por isso, aceda a ler os [requisitos](remoteapp-imagereqs.md), corrija a imagem e tente toocreate a coleção novamente.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Erros comuns vistos no portal de gestão do Azure Olá
    DNS server could not be reached
    ProvisioningTimeout

Coleções de nuvem, muitas vezes, falhar durante a criação devido a está a utilizar imagens personalizadas.  Se vir um Olá acima erros e estiver a utilizar uma coleção de Olá toocreate imagem personalizada, verifique Olá os seguintes aspetos:

* Certifique-se de que essa imagem personalizada de Olá carregou cumpre os requisitos de imagem.
* Mais frequentemente Olá problema comum é que dessa imagem Olá não foi corretamente syspreped.  
* Certifique-se de imagem de Olá pode efetuar o arranque no Hyper-V ou tente criar uma VM do IAAS diretamente na sua subscrição do Azure utilizando a imagem de Olá. Se Olá VM falhar tooboot e não iniciar, em seguida, normalmente, isto indica que dessa imagem personalizada Olá não foi preparada corretamente.  Certifique-se de que foi compilada imagem personalizada Olá seguintes Olá como toocreate um modelo personalizado de imagem do RemoteApp

Se estiver a utilizar uma das imagens de Microsoft Olá incluídas na sua subscrição, tente toocreate Olá coleção. Se Olá problema persistir, contacte o suporte da Microsoft.

    PlatformImageTrialModeOnly

Se vir este erro isto normalmente significa que foram atualizados tooa paga conta, mas que está a tentar toouse uma imagem de Microsoft fornecido é válida apenas durante o modo de avaliação de Olá do serviço de Olá. Neste caso, tente toocreate novamente a coleção de nuvem, mas ser toospecify se Olá correto imagem.

