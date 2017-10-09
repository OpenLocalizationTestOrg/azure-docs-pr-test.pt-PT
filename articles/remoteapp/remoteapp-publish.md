---
title: "aaaPublish uma aplicação no Azure RemoteApp | Microsoft Docs"
description: "Saiba como toopublish aplicações e recursos no Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Como toopublish uma aplicação no RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Depois de criar a coleção do RemoteApp, terá de toopublish Olá aplicações ou recursos que pretende que toomake disponível para os seus utilizadores. Olá imagens de modelo fornecidas com a sua subscrição apenas tem algumas aplicações publicadas por predefinição - tooshare Olá outras aplicações, terá de toopublish-los.

> [!NOTE]
> Precisa de tooupdate uma aplicação? Terá de demasiado[atualização Olá imagem](remoteapp-update.md) primeiro.
> 
> 

No Olá **publicação** separador no portal de Olá, clique em **publicar**. Ou pode adicionar uma aplicação a partir da imagem de modelo **iniciar** menu ou forneça Olá caminho toowhere Olá aplicação é instalada numa imagem de modelo de Olá. Se selecionar tooadd Olá **iniciar** menu, escolha Olá aplicação toopublish Olá lista. Se escolher tooprovide Olá caminho toohello aplicação, introduza um nome para a aplicação Olá e Olá caminho toohello aplicação. Utilizar variáveis no caminho de Olá - por exemplo, "% systemdrive %" em vez de "c:\".

> [!NOTE]
> Se quiser tooadd a aplicação da Olá **iniciar** menu, terá de toohave *adicionado toohello essa aplicação **iniciar** menu na imagem de modelo.* Caso contrário, RemoteApp apenas será apresentada que *é* no Olá **iniciar** menu e irá ser confundido. 
> 
> toomake se a aplicação fica no Olá **iniciar** menu, colocar um ficheiro de atalho - **.lnk** - Olá %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs pasta.
> 
> Caso se tenha esquecido tooadd Olá aplicação toohello **iniciar** menu quando criou o modelo de Olá, escolha tooadd Olá caminho toohello aplicação. (Ou recriar a imagem de modelo, mas é bastante um pouco mais trabalho).
> 
> 

