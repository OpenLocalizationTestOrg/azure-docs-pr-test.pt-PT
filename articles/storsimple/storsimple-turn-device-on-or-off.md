---
title: "aaaTurn o dispositivo de série 8000 do StorSimple ou desativar | Microsoft Docs"
description: "Explica como ativar o num dispositivo que foi encerrado ou perdido de energia tooturn num novo dispositivo StorSimple e desativar um dispositivo em execução."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Ativar ou desativar o dispositivo de série 8000 do StorSimple
## <a name="overview"></a>Descrição geral
Não é necessário como parte da operação do sistema normal encerrar um dispositivo de Microsoft Azure StorSimple. No entanto, poderá ser necessário tooturn num novo dispositivo ou num dispositivo que tinha toobe encerrado. Geralmente, é necessário um encerramento nos casos em que deve substituir o hardware falhada, fisicamente mover uma unidade ou demorar um dispositivo de serviço fora de. Este tutorial descreve o procedimento de Olá necessário para ativar e encerrar o dispositivo StorSimple em cenários diferentes.

## <a name="turn-on-a-new-device"></a>Ativar um novo dispositivo
Olá passos para ativar um dispositivo StorSimple para Olá pela primeira vez diferem consoante se o dispositivo de Olá é um 8100 ou um modelo de 8600. Olá 8100 tem um bastidor primário único, enquanto Olá 8600 é um dispositivo de inclusão de dupla com um bastidor primário e um bastidor EBOD. Olá os passos detalhados para ambos os modelos são abordados em Olá secções a seguir.

* [Novo dispositivo com apenas a inclusão principal](#new-device-with-primary-enclosure-only)
* [Novo dispositivo com a inclusão EBOD](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Novo dispositivo com apenas a inclusão principal
modelo de Olá StorSimple 8100 é um dispositivo de inclusão único. O dispositivo inclui redundante energia e arrefecimento módulos (PCMs). Tanto PCMs tem de estar instalados e ligado toodifferent energia origens tooensure elevada disponibilidade.

Efetue Olá toocable passos a seguir o dispositivo de energia.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Para a configuração do dispositivo e de cabos de instruções, visite demasiado[instalar o seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md). Certifique-se que siga as instruções de Olá exatamente.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Novo dispositivo com a inclusão EBOD
modelo de Olá StorSimple 8600 tem um bastidor primário e um bastidor EBOD. Isto requer Olá unidades toobe instalou os cabos em conjunto para conectividade Serial Attached SCSI (SAS) e de energia.

Quando configurar este dispositivo para Olá pela primeira vez, execute os passos de Olá para SAS cablagem pela primeira vez e Olá, em seguida, concluir os passos para power cablagem.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Para a configuração do dispositivo e de cabos de instruções, visite demasiado[instalar o seu dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md). Certifique-se que siga as instruções de Olá exatamente.

## <a name="turn-on-a-device-after-shutdown"></a>Ativar um dispositivo após encerramento
são diferentes dependendo se o dispositivo de Olá é um 8100 ou um modelo de 8600 Olá os passos para ativar um dispositivo StorSimple depois de ter sido encerrado. Olá 8100 tem um bastidor primário único, enquanto Olá 8600 é um dispositivo de inclusão de dupla com um bastidor primário e um bastidor EBOD.

* [Dispositivos com apenas a inclusão principal](#device-with-primary-enclosure-only)
* [Dispositivo com a inclusão EBOD](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Dispositivos com apenas a inclusão principal
Após um encerramento, utilize Olá seguir o procedimento tooturn num dispositivo StorSimple com um bastidor primário e não bastidor EBOD.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn num dispositivo com apenas um bastidor primário
1. Certifique-se de que o power Olá muda em ambos os energia e arrefecimento módulos (PCMs) estão na posição de OFF Olá. Se Olá comutadores não estiverem na posição de OFF Olá, em seguida, inverte-los toohello OFF posição e aguarde Olá lights toogo desativado.
2. Ative dispositivos Olá por indicar Olá comutadores de energia em ambos os posição do PCMs toohello ON. dispositivo Olá deve ativar.
3. Olá de verificação seguintes tooverify Olá dispositivos é completamente no:
   
   1. Olá OK LEDs em ambos os módulos PCM são verde.
   2. o estado de Olá LEDs em ambos os controladores são verde sólida.
   3. Olá blinking o LED azul dos controladores de Olá, que indica que esse controlador Olá está ativo.
      
      Se qualquer uma das seguintes condições não forem cumpridas, o dispositivo não está em bom estado. . [Contacte a Microsoft Support](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Dispositivo com a inclusão EBOD
Após um encerramento, utilize Olá seguir o procedimento tooturn num dispositivo StorSimple com um bastidor primário e um bastidor EBOD. Execute cada passo na sequência exatamente tal como descrito. Falha toodo, por isso, pode resultar em perda de dados.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn num dispositivo com um site primário e um bastidor EBOD
1. Certifique-se que Olá bastidor EBOD inclusão principal toohello ligado. Para obter mais informações, consulte [instalar o seu dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Certifique-se de que hello, energia e arrefecimento módulos (PCMs) no Olá EBOD e inclusões primários estão na posição do Olá OFF. Se Olá comutadores não estiverem na posição de OFF Olá, em seguida, inverte-los toohello OFF posição e aguarde Olá lights toogo desativado.
3. Ative Olá bastidor EBOD primeiro por indicar Olá comutadores de energia em ambos os posição do PCMs toohello ON. Olá PCM LEDs deve estar verde. Um controlador EBOD LED verde esta unidade indica que a inclusão EBOD Olá está ativada.
4. Ative a inclusão principal Olá por indicar Olá comutadores de energia em ambos os posição do PCMs toohello ON. sistema completo Olá agora deve estar no.
5. Verifique se Olá SAS LEDs são verdes, assegura que essa ligação Olá entre Olá bastidor EBOD e inclusão principal Olá é bom.

## <a name="turn-on-a-device-after-a-power-loss"></a>Ativar um dispositivo após uma falha de energia
Uma falha de energia ou uma interrupção, pode encerrar um dispositivo StorSimple. Falha de energia Olá pode acontecer num de fontes de alimentação Olá ou ambas as fontes de alimentação. passos de recuperação Olá são diferentes dependendo se o dispositivo de Olá é um 8100 ou um modelo de 8600. Olá 8100 tem um bastidor primário único, enquanto Olá 8600 é um dispositivo de inclusão de dupla com um bastidor primário e um bastidor EBOD. Esta secção descreve o procedimento de recuperação de Olá para cada cenário.

* [Dispositivos com apenas a inclusão principal](#8100)
* [Dispositivo com a inclusão EBOD](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Dispositivos com apenas a inclusão principal<a name="8100">
sistema Olá pode continuar a conclusão da operação normal, se houver perda de energia tooone do respetivos fontes de alimentação. No entanto, tooensure elevada disponibilidade do dispositivo Olá, restauro energia toohello fonte de alimentação logo que possível.

Se existir uma falha de energia ou uma interrupção de energia em ambas as fontes de alimentação, Olá sistema será encerrado de forma ordenada e controlada. Quando é restaurada energia Olá, sistema Olá irão ligar automaticamente.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Dispositivo com a inclusão EBOD<a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Falha de energia no um power fornecer
sistema Olá pode continuar a conclusão da operação normal, se houver perda de energia tooone do respetivos fontes de alimentação no bastidor primário Olá ou a inclusão EBOD Olá. No entanto, tooensure elevada disponibilidade do dispositivo Olá, restaure energia toohello fonte de alimentação logo que possível.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Falha de energia em ambas as fontes de alimentação no site primário e inclusões EBOD
Se existir uma interrupção de energia ou falha de energia em ambas as fontes de alimentação, Olá bastidor EBOD irá encerrar imediatamente e inclusão principal Olá será encerrado de forma ordenada e controlada. Quando é restaurada energia, a aplicação Olá será iniciada automaticamente.

Se energia Olá é desligada manualmente, em seguida, tirar Olá sistema de toohello de energia de toorestore passos a seguir.

1. Ative Olá bastidor EBOD.
2. Depois de Olá bastidor EBOD no, ative a inclusão principal Olá.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Falha de energia em ambas as fontes de alimentação no bastidor EBOD
Quando configurar o seu cabos, tem de se certificar que Olá EBOD nunca é ligado tooa individualmente separar PDU. Se Olá EBOD e inclusão principal falharem Olá mesmo tempo, o sistema de Olá será recuperada.

Se apenas Olá bastidor EBOD falha em ambas as fontes de alimentação, o sistema de Olá não será recuperada automaticamente. Tome Olá tooturn passos a seguir no sistema de Olá e restaurá-lo bom estado de funcionamento tooa:

1. Se o bastidor primário Olá estiver ativada, desactivar energia e arrefecimento módulos (PCMs).
2. Aguarde alguns minutos para Olá tooshut de sistema pendente.
3. Ative Olá bastidor EBOD.
4. Depois de Olá bastidor EBOD no, ative a inclusão principal Olá.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Ativar um dispositivo após Olá primário e EBOD bastidor ligação
Se Olá ligação entre o controlador de reserva dinâmica Olá e controlador EBOD correspondente de Olá, o dispositivo de Olá continua toowork. Se Olá ligação entre o controlador de Active Directory do sistema de Olá e controlador EBOD correspondente de Olá, deve ocorrer a ativação pós-falha e dispositivo Olá deve continuar toowork como habitualmente.

Quando ambos os cabos de Serial Attached SCSI (SAS) são removidos ou ligação Olá entre Olá bastidor EBOD e inclusão principal Olá é severed, o dispositivo de Olá deixa de funcionar. Neste momento, efetue Olá os seguintes passos.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn no dispositivo Olá depois de perder a ligação
1. Olá acesso back of dispositivo Olá.
2. Se Olá ligação de cabo SAS entre bastidor EBOD Olá e inclusão principal Olá for interrompida, todos os fila SAS LEDs no Olá bastidor EBOD será desativada.
3. Encerre energia e arrefecimento módulos (PCMs) no bastidor EBOD Olá e inclusão principal Olá.
4. Aguarde até que todos os lights Olá no Olá back of ambas as caixas de Olá desativar.
5. Reinsert cabos SAS de Olá e certifique-se de que existe uma ligação boa entre bastidor EBOD Olá e inclusão principal Olá.
6. Ative Olá bastidor EBOD primeiro por indicar ambas PCM comutadores toohello no posição.
7. Certifique-se de que o bastidor EBOD Olá está ativada por a verificar se o LED de Olá verde está ON.
8. Ative a inclusão principal Olá.
9. Certifique-se de que o bastidor primário Olá está ativada por a verificar se o LED de controlador verde Olá está no.
10. Certifique-se de que Olá ligação de inclusão EBOD com inclusão principal Olá é boa ao verificar a fila SAS que Olá LEDs (quatro por controlador EBOD) estão todos em.

> [!IMPORTANT]
> Se os cabos SAS de Olá danificados ou de ligação Olá entre Olá bastidor EBOD e inclusão principal Olá está não boa, quando ativar o sistema de Olá, entra em modo de recuperação. . [Contacte a Microsoft Support](storsimple-8000-contact-microsoft-support.md) se isto acontecer.


## <a name="turn-off-a-running-device"></a>Desativar um dispositivo em execução
Um dispositivo StorSimple em execução poderá ter toobe encerrar se está a ser movido, retirada do serviço, ou um componente malfunctioning que necessita de toobe substituído. passos de Olá são diferentes dependendo se o dispositivo StorSimple Olá é um 8100 ou um modelo de 8600. Olá 8100 tem um bastidor primário único, enquanto Olá 8600 é um dispositivo de inclusão de dupla com um bastidor primário e um bastidor EBOD. Esta secção descreve em detalhe Olá passos tooshut para baixo de um dispositivo em execução.

* [Dispositivo com a inclusão principal](#8100a)
* [Dispositivo com a inclusão EBOD](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Dispositivo com a inclusão principal<a name="8100a">
tooshut baixo dispositivo Olá de forma controlada e ordenada, pode fazê-lo através de Olá portal clássico do Azure ou através de Olá do Windows PowerShell para StorSimple. 

> [!IMPORTANT]
> Não encerre um dispositivo em execução com o botão de energia Olá Olá back of dispositivo Olá.
> 
> Antes de encerrar o dispositivo de Olá, certifique-se de que todos os componentes de dispositivo Olá estão em bom Estados. No portal clássico do Azure de Olá, navegue demasiado**dispositivos** > **manutenção** > **estado do Hardware**e verifique o estado de todos os Olá componentes for verde. Isto acontece apenas para um sistema de bom estado de funcionamento. Se o sistema Olá está a ser encerrado tooreplace um componente malfunctioning, verá um falha (vermelho) ou degradado Estado (amarelo) para o componente de respetivos Olá no Olá **estado do Hardware**.
> 
> 

Depois de aceder ao hello do Windows PowerShell para StorSimple ou Olá portal clássico do Azure, siga os passos de Olá no [encerrar um dispositivo StorSimple](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Dispositivo com a inclusão EBOD<a name="8600a">
> [!IMPORTANT]
> Antes de encerrar inclusão principal Olá e inclusão EBOD Olá, certifique-se de que todos os componentes de dispositivo Olá estão em bom Estados. No portal do Azure de Olá, navegue demasiado**dispositivos** > **Monitor** > **estado de funcionamento do Hardware**e certifique-se de que todos os componentes de Olá estão em bom Estados.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut para baixo de um dispositivo em execução com a inclusão EBOD
1. Siga todos os passos de Olá apresentados na [encerrar um dispositivo StorSimple](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) para inclusão principal Olá.
2. Depois de Olá inclusão principal é encerrado, encerrado Olá EBOD pela indicar desativar comutadores de energia e arrefecimento módulo (PCM).
3. tooverify Olá EBOD foi encerrado, verifique se todos os acende-no Olá back of bastidor EBOD Olá estão desativadas.

> [!NOTE]
> não devem ser removidos cabos SAS Olá que são utilizados tooconnect Olá EBOD bastidor toohello primário bastidor até após o encerramento do sistema de Olá.

## <a name="next-steps"></a>Passos seguintes
[Contacte o Support Microsoft](storsimple-8000-contact-microsoft-support.md) se ocorrerem problemas ao ativar ou encerrar um dispositivo StorSimple.

