---
title: aaaReplace um controlador de StorSimple EBOD | Microsoft Docs
description: Explica como tooremove e substitua um ou ambos os controladores EBOD num dispositivo StorSimple 8600.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Substituir um controlador EBOD no dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Este tutorial explica como tooreplace um módulo de controlador EBOD defeituoso no seu dispositivo do Microsoft Azure StorSimple. um módulo de controlador EBOD tooreplace, tem de:

* Remover Olá defeituoso EBOD controlador
* Instalar um novo controlador EBOD

Considere Olá seguintes informações antes de começar:

* Módulos EBOD em branco tem de ser inseridos em todas as ranhuras de não utilizadas. inclusão de Olá não será esporádico corretamente se uma ranhura é deixada aberta.
* controlador EBOD Olá é frequente-swappable e pode ser removido ou substituído. Não remova um módulo falhado até ter uma substituição. Quando inicia o processo de substituição de Olá, deve ser concluído dentro de 10 minutos.

> [!IMPORTANT]
> Antes de tentar tooremove ou substituir qualquer componente do StorSimple, certifique-se de que revê Olá [convenções de ícone de segurança](storsimple-safety.md#safety-icon-conventions) e outros [precauções de segurança](storsimple-safety.md).
> 
> 

## <a name="remove-an-ebod-controller"></a>Remover um controlador EBOD
Antes de Olá Falha ao substituir o módulo de controlador EBOD no dispositivo StorSimple, certifique-se de que Olá outro módulo de controlador EBOD está ativa e em execução. Olá procedimento e tabela seguintes explicam como tooremove Olá módulo de controlador EBOD.

#### <a name="tooremove-an-ebod-module"></a>tooremove um módulo EBOD
1. Abra Olá portal clássico do Azure.
2. Navegue demasiado**dispositivos** > **manutenção** > **estado do Hardware**e certifique-se de que o estado de Olá de Olá GUIADO para Olá EBOD Active Directory módulo de controlador é verde e Olá LED para o módulo de controlador EBOD Olá falhada é vermelho.
3. Localize o módulo de controlador EBOD Olá falhada Olá back of dispositivo Olá.
4. Remova os cabos de Olá ligar o controlador de toohello Olá EBOD controlador módulo antes de tirar o módulo EBOD Olá fora do sistema de Olá.
5. Tome nota da porta SAS exata de Olá da Olá EBOD controlador módulo que foi ligado toohello controlador. Será necessário toorestore de configuração Olá system toothis depois de as substituir o módulo EBOD Olá. 
   
   > [!NOTE]
   > Normalmente, esta será a porta A, que é denominada como **alojar na** no Olá diagrama a seguir.
   > 
   > 
   
    ![Controlador Backplane de EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Figura 1** módulo do Back EBOD
   
   | Etiqueta | Descrição |
   |:--- |:--- |
   | 1 |Falhas LED |
   | 2 |Energia LED |
   | 3 |Conectores SAS |
   | 4 |SAS LEDs |
   | 5 |Portas série fábrica apenas para utilização |
   | 6 |Porta (anfitrião do) |
   | 7 |Porta B (anfitrião de saída) |
   | 8 |Porta C (apenas para utilização de fábrica) |

## <a name="install-a-new-ebod-controller"></a>Instalar um novo controlador EBOD
Olá procedimento e tabela seguintes explicam como tooinstall um módulo de controlador EBOD no dispositivo StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall um controlador EBOD
1. Verifique o dispositivo EBOD Olá para danos, especialmente toohello conector de interface. Não instale o novo controlador de EBOD Olá se qualquer pins são bent.
2. Com as bloqueios simultâneos de Olá no Olá abra posição, o módulo de Olá gradualmente no bastidor Olá até os bloqueios simultâneos de Olá envolvimento.
   
    ![Instalar o controlador de EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Figura 2** módulo de controlador instalar Olá EBOD
3. Bloqueio temporário de Olá fechar. Deve ouvir um clique como bloqueio temporário de Olá envolva.
   
    ![Ao libertar o bloqueio temporário EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Figura 3** fechar bloqueio temporário do módulo EBOD Olá
4. Restabeleça a ligação de cabos de Olá. Utilize a configuração exata de Olá que estava presente antes de substituição de Olá. Consulte Olá diagrama a seguir e na tabela para obter detalhes sobre como os cabos de Olá tooconnect.
   
    ![Instalar os cabos do dispositivo 4U de energia](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Figura 4**. Cabos de restabelecer a ligação
   
   | Etiqueta | Descrição |
   |:--- |:--- |
   | 1 |Inclusão principal |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Controlador 0 |
   | 5 |Controlador 1 |
   | 6 |Controlador EBOD 0 |
   | 7 |Controlador EBOD 1 |
   | 8 |Inclusão EBOD |
   | 9 |Unidades de distribuição de energia |

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).

