---
title: "janela do aaaUsing Olá Shell de nuvem do Azure (pré-visualização) | Microsoft Docs"
description: "Janela de Shell de nuvem do Azure Olá de instruções."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a>Utilizando Olá janela da Shell de nuvem do Azure

Este documento explica como toouse Olá janela da Shell de nuvem.

## <a name="concurrent-sessions"></a>Sessões simultâneas
Shell de nuvem permite várias sessões em simultâneo em separadores de browser, permitindo tooexist cada sessão como um processo de Bash separado.
Se sair com uma sessão, não se esqueça de tooexit cada janela de sessão como cada processo é executado independentemente embora são executadas em Olá mesma máquina.

## <a name="restart-cloud-shell"></a>Reiniciar o Shell de nuvem
![](media/recycle.png)
> [!WARNING]
> Reiniciar o Shell de nuvem irá repor o estado da máquina e todos os ficheiros não persistentes ao seu ficheiro partilha serão perdida.

* Clique Olá reinício ícone na barra de ferramentas de Olá tooreceive um novo ambiente de nuvem Shell.

## <a name="minimize--maximize-cloud-shell-window"></a>Minimizar & maximize a janela da Shell de nuvem
![](media/minmax.png)
* Clique em Olá minimizar ícone na Olá principais direita da Olá janela toohide-lo. Clique novamente Olá ícone de nuvem Shell toounhide.
* Clique em Olá maximizar a altura do ícone tooset janela toomax. toorestore janela tooprevious tamanho, clique em restaurar.

## <a name="copy-and-paste"></a>Copiar e colar
* Windows: `Ctrl-insert` toocopy e `Shift-insert` toopaste. Contexto pendente, também pode ativar copiar/colar.
  * FireFox/IE podem não suportar corretamente as permissões da área de transferência.
* Mac OS: `Cmd-c` toocopy e `Cmd-v` toopaste. Contexto pendente, também pode ativar copiar/colar.

## <a name="resize-cloud-shell-window"></a>Redimensionar a janela da Shell de nuvem
* Clique e arraste o limite superior de Olá da barra de ferramentas Olá ou reduzir verticalmente a janela do tooresize Olá Shell da nuvem.

## <a name="scrolling-text-display"></a>Deslocamento apresentação de texto
* Desloque-se com o rato ou touchpad toomove terminal texto a.

## <a name="exit-command"></a>Comando de saída
Executar `exit` termina a sessão ativa de Olá. Este comportamento ocorre por predefinição, passados 20 minutos, sem interação do.

## <a name="next-steps"></a>Passos seguintes
[Início rápido de Shell de nuvem](quickstart.md)
