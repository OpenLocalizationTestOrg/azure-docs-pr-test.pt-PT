---
title: "Máquinas virtuais do Azure no Explorador de servidores de aaaAccessing | Microsoft Docs"
description: "Obter uma descrição geral de como tooview criar e gerir máquinas virtuais do Azure (VMs) no Explorador de servidores no Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Aceder a máquinas virtuais do Azure no Explorador de servidores
Ao utilizar o Explorador de servidores no Visual Studio, pode apresentar informações sobre as máquinas virtuais alojadas pelo Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Aceder a máquinas virtuais no Explorador de servidores
Se tiver máquinas virtuais alojadas pelo Azure, pode aceder-os no Explorador de servidores. Tem primeiro de iniciar sessão tooview de subscrição do Azure tooyour sua dos mobile services. toosign, abra o menu de atalho Olá para Olá nó do Azure no Explorador de servidores e escolha **ligar tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget informações sobre as máquinas virtuais
1. No Explorador de servidores, escolha uma máquina virtual e, em seguida, escolha tooshow chave Olá F4 respetiva janela de propriedades.
   
    Olá, a tabela seguinte mostra as propriedades que estão disponíveis, mas estão todos os só de leitura. toochange-los, utilize Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Propriedade | Descrição |
   | --- | --- |
   | Nome DNS |URL de Olá com Olá endereço Internet da máquina virtual de Olá. |
   | Ambiente |Para uma máquina virtual, Olá o valor desta propriedade é sempre de produção. |
   | Nome |nome da máquina virtual de Olá Olá. |
   | Tamanho |tamanho de Olá da máquina virtual de Olá, que reflete a quantidade de Olá de memória e espaço em disco que está disponível. Para obter mais informações, consulte como: configurar os tamanhos de Máquina Virtual. |
   | Estado |Os valores incluem início, introdução, parar, parado e ao obter o estado. Se for apresentada a obter o estado, o estado atual do Olá é desconhecido. valores de Olá para esta propriedade é diferente do valores Olá que são utilizados em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |ID de subscrição de Olá para a sua conta do Azure. Pode mostrar estas informações no Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) visualizando as propriedades de Olá para uma subscrição. |
2. Escolha um nó de ponto final e, em seguida, ver Olá **propriedades** janela.
3. Olá tabela seguinte descreve Olá propriedades disponíveis de pontos finais, mas são só de leitura. pontos finais de Olá tooadd ou editar para uma máquina virtual, utilize Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Propriedade | Descrição |
   | --- | --- |
   | Nome |Um identificador para o ponto final de Olá. |
   | Porta privada |porta de Olá para aplicação de tooyour interno de acesso de rede. |
   | Protocolo |utiliza o protocolo de Olá Olá a camada de transporte para este ponto final, TCP ou UDP. |
   | Porta Pública |porta de Olá que é utilizada para acesso público tooyour aplicação. |

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a utilização de funções do Azure no Visual Studio, consulte [utilizando o ambiente de trabalho remoto com as funções do Azure](vs-azure-tools-remote-desktop-roles.md).

