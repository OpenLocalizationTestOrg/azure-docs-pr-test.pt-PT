---
title: "aaaUpdate a coleção do Azure RemoteApp | Microsoft Docs"
description: "Saiba como tooupdate a coleção do Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Atualizar uma coleção no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Ficará uma hora, inevitavelmente, quando precisa de imagem ou tooupdate Olá aplicações na sua coleção do Azure RemoteApp. Se estiver a utilizar uma das imagens de Olá incluídas na sua subscrição do Azure RemoteApp, numa coleção de uma nuvem ou híbrida, atualizações de todos as são processadas pelo Azure RemoteApp, pelo que pode rest fácil.

No entanto, se estiver a utilizar uma imagem personalizada (que criou a partir do zero ou que criou ao modificar uma das nossas imagens), é responsável pela manutenção Olá imagem e das aplicações. Se precisar de tooupdate imagem ou qualquer uma das aplicações Olá dentro-lo, terá de toocreate uma versão nova e atualizada da imagem de Olá e, em seguida, substituir Olá existente imagem na sua coleção com esta nova imagem atualizada.

Por isso, como deve proceder atualizar a sua coleção? É bastante simples:

1. Atualize imagem de Olá que utilizou na sua coleção. Aplicar qualquer ou as atualizações necessárias e, em seguida, guarde-o com um novo nome.
2. [Carregar](remoteapp-uploadimage.md) ou [importar](remoteapp-image-on-azurevm.md) tooRemoteApp essa imagem.
3. Agora, na página de coleção de Olá, clique em **atualização**.
4. Escolher imagem novo Olá Olá **imagem de modelo** lista.
5. Segue-se parte tricky Olá - terá toodecide como toodeal com todos os utilizadores que estão atualmente a utilizar uma aplicação na coleção de Olá. Tem Olá seguintes opções:
   
   * **Dê 60 minutos após a atualização de Olá aos utilizadores**. Assim que a atualização de Olá estiver concluída, o Azure RemoteApp apresentará uma mensagem tooany os utilizadores ativos informar toosave respetivo trabalho registo desativado e volte a iniciar sessão. Após 60 minutos, os utilizadores ativos que não tenham sessão terminada automaticamente a sessão serão terminada. Os utilizadores podem imediatamente iniciar sessão novamente.
   * **Terminar sessão dos utilizadores imediatamente**. Assim que a atualização de Olá estiver concluída, terminar sessão todos os utilizadores automaticamente, sem qualquer aviso. Se escolher esta opção, os utilizadores poderão perder dados. No entanto, estes podem voltar a ligar aplicação toohello imediatamente.
6. Clique em Olá marca de verificação toostart Olá atualizar.

