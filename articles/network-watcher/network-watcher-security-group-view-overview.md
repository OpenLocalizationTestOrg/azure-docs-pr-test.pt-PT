---
title: Vista de grupo toosecurity aaaIntroduction no observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma descrição geral de Olá capacidade de vista de segurança do observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Vista do grupo de segurança do introdução toonetwork no observador de rede do Azure

Grupos de segurança de rede estão associados a um nível de sub-rede ou um nível de NIC. Quando associados a um nível de sub-rede, aplica-se as instâncias VM de Olá tooall na sub-rede Olá. Vista de grupo de segurança de rede devolve todos os NSGs Olá configurado e regras que estão associadas a um nível NIC e a sub-rede para uma máquina virtual que fornecem informações sobre a configuração de Olá. Além disso, as regras de segurança eficaz Olá são devolvidas para cada um dos Olá NICs numa VM. Vista de grupo de segurança de rede a utilizar, pode avaliar uma VM para vulnerabilidades de rede, tais como portas abertas. Também pode validar se o grupo de segurança de rede está a funcionar conforme esperado com base num [comparação entre Olá configurado e Olá regras de segurança eficaz](network-watcher-nsg-auditing-powershell.md).

Um caso de utilização expandido mais está em conformidade de segurança e de auditoria. Pode definir um conjunto de regras de segurança prescritiva como um modelo para a governação de segurança na sua organização. Uma auditoria periódica de compatibilidade pode ser implementada de forma programática através da comparação regras de prescritiva Olá com regras Efetivo Olá para cada uma das VMs Olá na sua rede.

Olá regras portais são divididas por eficaz, sub-rede, Interface de rede e predefinido. Isto proporciona uma vista simple numa máquina virtual do Olá regras aplicadas tooa. Um botão de transferência é fornecida tooeasily transferir todas as regras de segurança de Olá, independentemente do separador Olá para um ficheiro CSV.

![vista do grupo de segurança][1]

As regras podem ser selecionadas e um novo painel abre-se as prefixos tooshow Olá grupo de segurança de rede e de origem e de destino. A partir deste painel pode navegar diretamente toohello recursos de grupo de segurança de rede.

![pesquisa][2]

### <a name="next-steps"></a>Passos seguintes

Saiba como tooaudit a segurança de rede de grupo de definições, visitando [definições do grupo de segurança de rede de auditoria com o PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









