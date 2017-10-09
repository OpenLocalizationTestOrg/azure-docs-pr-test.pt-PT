---
title: Certifique-se de aaaIntroduction tooIP fluxo no observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma descrição geral de Olá IP de observador de rede fluxo Certifique-se de capacidade"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Certifique-se de fluxo de tooIP de introdução no observador de rede do Azure

Fluxo IP Certifique-se verifica se um pacote é permitido ou negado tooor a partir de uma máquina virtual com base nas informações de 5 cadeias de identificação. Esta informação é constituído por direção, protocolo, local IP, remoto IP, porta local e porta remota. Se pacotes hello é negado por um grupo de segurança, é devolvido o nome de Olá da regra Olá negado pacotes hello de. Enquanto qualquer IP de origem ou de destino pode ser selecionado, esta funcionalidade ajuda os administradores Diagnostique rapidamente problemas de conectividade do ou toohello internet e da ou toohello num ambiente no local.

Fluxo IP verificar destina-se uma interface de rede de uma máquina virtual. Fluxo de tráfego, em seguida, é verificado com base nas definições de Olá configurado tooor dessa interface de rede. Esta funcionalidade é útil para confirmar se uma regra num grupo de segurança de rede está a bloquear tooor de tráfego de entrada ou saída de uma máquina virtual.

Certifique-se de uma instância do observador de rede necessidades toobe criada em todas as regiões que planeia toorun fluxo IP. Observador de rede é um serviço regional e só pode ser executada relativamente aos recursos na Olá mesma região. Isto não afeta Olá resultados do fluxo IP, certifique-se como rota Olá associada Olá que NIC ainda vai ser devolvido.

![1][1]

## <a name="next-steps"></a>Passos seguintes

Visite Olá seguinte artigo toolearn se um pacote é permitido ou negado para uma máquina virtual específica através do portal Olá. [Verifique se o tráfego é permitido numa VM com o IP fluxo verificar através do portal Olá](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












