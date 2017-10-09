---
title: "problemas comuns de tootroubleshoot aaaHow durante a criação do VHD | Microsoft Docs"
description: "Resolução de problemas de respostas toocommon questões e problemas durante a criação do VHD."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>Como tootroubleshoot de problemas comuns encontrados durante a criação do VHD
Este artigo é fornecido toohelp um publicador do Azure Marketplace e/ou coadministrador que pode ocorrer um problema ou tiver questões comuns ao publicar ou gerir os respetivos solution(s) de máquina virtual.

1. Como alterar o nome de Olá do anfitrião de Olá?
   
    Depois de criada a VM, os utilizadores não é possível atualizar o nome de Olá do anfitrião de Olá.
2. Como tooreset Olá serviço de ambiente de trabalho remoto ou a palavra-passe de início de sessão?
   
   * [Referência para a VM do Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Referência para a VM com Linux](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. Como toogenerate novo ssh certificados?
   
   Consulte a hiperligação de toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. Como tooconfigure um certificado VPN abra?
   
   Consulte a hiperligação de toohello: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. O que é a política de suporte de Olá para executar o software de servidor Microsoft no ambiente de máquina virtual do Microsoft Azure Olá (infraestrutura-como-um-serviço)?
   
   Consulte a hiperligação de toohello: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. Máquinas virtuais dispõem de qualquer identificador exclusivo?
   
   Azure codifica ID exclusivo de VM do Azure em cada VM. Consulte os detalhes neste blogue e a documentação.
7. Numa VM como posso gerir extensão de script personalizado Olá na tarefa de arranque Olá?
   
   Consulte a hiperligação de toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. Como toocreate uma VM a partir Olá utilizando o portal do Azure Olá VHD que é carregado toopremium armazenamento?
   
   Iremos ainda não suporta esta funcionalidade.
9. Uma aplicação de 32 bits é suportada no Olá Azure Marketplace?
   
   Consulte toohello ligação para obter detalhes sobre a política de suporte de Olá: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. Sempre que estou a tentar toocreate uma imagem do meu VHDs, posso obter Erro Olá ". VHD já está registado no repositório de imagens como recurso Olá"no PowerShell. Não foi possível a criar o qualquer imagem antes nem foi possível localizar qualquer imagem com este nome no Azure. Como resolver isto?
    
    Normalmente, isto acontecer se o utilizador Olá aprovisionado uma VM a partir deste VHD e não existe um bloqueio nessa VHD. Verifique que não há nenhuma VM alocado a partir deste VHD. Se o erro de Olá ainda manter, em seguida, volte a emitir um pedido de suporte utilizando a seguinte hiperligação ou a partir de Olá publicação portal relativamente a este (detalhes são fornecidos na resposta Olá da pergunta 11).
