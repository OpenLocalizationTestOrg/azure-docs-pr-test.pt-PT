---
title: "aaaStorSimple monitorização indicadores | Microsoft Docs"
description: "Descreve Olá leve - emitting diodes (LEDs) e alarmes audible utilizados toomonitor Olá estado do dispositivo do StorSimple Olá."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Utilizar o seu dispositivo StorSimple toomanage indicadores de monitorização
## <a name="overview"></a>Descrição geral
O dispositivo StorSimple inclui leve - emitting diodes (LEDs) e alarmes que pode utilizar toomonitor Olá módulos e o estado geral de dispositivo do StorSimple Olá. Olá indicadores de monitorização pode ser encontrado nos componentes de hardware Olá de inclusão principal do dispositivo Olá e inclusão EBOD Olá. Olá monitorização indicadores pode ser LEDs ou audible alarmes.

Existem três LED Estados utilizados tooindicate Olá estado de um módulo: verde, flashing toored verde-amber, ou amber vermelho.  

* Verde LEDs representam um bom estado de funcionamento.  
* Flashing verde toored-amber LEDs representam a presença de Olá das condições não críticos que poderão necessitar de intervenção do utilizador.  
* Vermelho amber LEDs indicarem que existe uma falha crítica presente no módulo Olá.  

Olá resto deste artigo descreve Olá vários monitorização indicador LEDs, as respetivas localizações no dispositivo do StorSimple Olá, estado do dispositivo Olá com base no Olá LED Estados e quaisquer associados alarmes audible.

## <a name="front-panel-indicator-leds"></a>Indicador de painel frontal LEDs
painel frontal Olá, também conhecido como Olá *painel operações* ou *painel ops*, apresenta o estado de todos os módulos de Olá agregado Olá no sistema de Olá. painel frontal Olá é idêntico no Olá StorSimple primário e Olá bastidor EBOD e é ilustrado abaixo.  

   ![Painel frontal do dispositivo][1]

painel frontal Olá contém Olá indicadores os seguintes:  

1. Botão Mute
2. Indicador de energia LED (vermelho/verde-amber)
3. Indicador de falhas de módulo GUIADO (no red-amber/DESATIVADA)
4. Indicador de falhas lógica GUIADO (no red-amber/OFF
5. Apresentação de ID de unidade  

Olá principal diferença entre o painel frontal Olá LEDs para dispositivo Olá e os do Olá bastidor EBOD é Olá **o número de identificação de unidade de sistema** mostrado no ecrã de Olá LED. unidade de predefinição Olá ID apresentado no dispositivo Olá é **00**, enquanto que é apresentado no Olá bastidor EBOD de ID de unidade de predefinição de Olá **01**. Isto permite-lhe tooquickly diferenciar entre o dispositivo de Olá e inclusão EBOD Olá quando Olá dispositivo for ligado. Se o dispositivo está desativado, utilize as informações de Olá fornecidas [ativar um novo dispositivo](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) dispositivo de Olá toodifferentiate de Olá bastidor EBOD.  

## <a name="front-panel-led-status"></a>Painel frontal LED Estado
Utilize Olá Estado Olá tooidentify de tabela indicado pelo Olá LEDs no painel frontal da Olá para dispositivo Olá ou a inclusão EBOD Olá a seguir.  

| Energia do sistema | Falha do módulo | Índice de falhas lógica | Alarme | Estado |
| --- | --- | --- | --- | --- |
| Amber vermelho |OFF |OFF |N/D |Perda de energia de AC, a utilizar na cópia de segurança energia, ou de energia de AC e módulos de controlador Olá foram removidos. |
| Verde |ON |ON |N/D |Estado de teste de ativação painel OPS (5s) |
| Verde |OFF |OFF |N/D |Ligar, todas as funções de boas |
| Verde |ON |N/D |Falhas PCM LEDs, falhas de ventoinha LEDs |Quaisquer falhas PCM, falhas de ventoinha, ativação pós-falha ou em temperatura |
| Verde |ON |N/D |Módulo de e/s LEDs |Quaisquer falhas de módulo de controlador |
| Verde |ON |N/D |N/D |Falhas de lógica de inclusão |
| Verde |Flash |N/D |Estado do módulo LED no módulo de controlador. Falhas PCM LEDs, falhas de ventoinha LEDs |Tipo de módulo de controlador desconhecido instalado, I2C bus falha, o erro de configuração do controlador módulo vital produto dados (VPD) |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Indicador de módulo (PCM) arrefecimento LEDs de energia
O indicador arrefecimento de módulo (PCM) LEDs de energia pode ser encontrado no Olá back of inclusão principal Olá ou bastidor EBOD em cada módulo PCM. Este tópico descreve como Olá toouse seguir o estado de Olá toomonitor LEDs do dispositivo StorSimple.  

* PCM LEDs para inclusão principal Olá
* PCM LEDs para Olá bastidor EBOD

## <a name="pcm-leds-for-hello-primary-enclosure"></a>PCM LEDs para inclusão principal Olá
o dispositivo StorSimple Olá tem um módulo PCM 764W com um bateria adicional. Olá ilustração seguinte mostra painel LED de Olá para dispositivo Olá.  

   ![PCM LEDs no bastidor primário Olá][2]

Legenda de LED:

1. Falha de energia de AC
2. Falha de ventoinha
3. Falhas de bateria
4. PCM OK
5. Falha de DC
6. Bateria boa  

Estado de Olá de Olá que PCM indicado no Olá GUIADO painel. Painel de PCM LED de dispositivo Olá tem seis LEDs. Quatro estes LEDs apresentar o estado de Olá de fonte de alimentação Olá e ventoinha Olá. Olá restantes dois LEDs indica o estado de Olá do módulo de cópia de segurança de bateria Olá no Olá PCM. Pode utilizar Olá seguintes tabelas toodetermine Olá Estado Olá PCM.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Indicador PCM LEDs de fonte de alimentação e ventoinha
| Estado | PCM OK (verde) | Falha de AC (amber) | Ventoinha falhar (amber) | Falha de DC (amber) |
| --- | --- | --- | --- | --- |
| Sem energia de AC (tooenclosure) |OFF |OFF |OFF |OFF |
| Sem energia de AC (apenas para este PCM) |OFF |ON |OFF |ON |
| AC está presente no PCM - OK |ON |OFF |OFF |OFF |
| Falha PCM (ventoinha falhar) |OFF |OFF |ON |N/D |
| Falhas PCM (através de amp, através de tensão, através de atual) |OFF |ON |ON |ON |
| PCM (ventoinha fora tolerância) |ON |OFF |OFF |ON |
| Modo de reserva dinâmica |Flashing |OFF |OFF |OFF |
| Transferência de firmware PCM |OFF |Flashing |Flashing |Flashing |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Indicador PCM LEDs para bateria Olá de cópia de segurança
| Estado | Bateria bom (verde) | Falhas de bateria (amber) |
| --- | --- | --- |
| Bateria não está presente |OFF |OFF |
| Bateria presente e cobrada |ON |OFF |
| Discharge charging ou a manutenção de bateria |Flashing |OFF |
| Falhas de "de forma recuperável" da bateria (recuperáveis) |OFF |Flashing |
| Falhas de "disco rígida" da bateria (não recuperável) |OFF |ON |
| Bateria disarmed |Flashing |OFF |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>PCM LEDs para Olá bastidor EBOD
Olá bastidor EBOD tem um PCM 580W e nenhum bateria adicional. Painel PCM Olá para Olá bastidor EBOD tem indicador LEDs apenas para fontes de alimentação Olá e ventoinha Olá. Olá ilustração seguinte mostra estes LEDs.

   ![PCM LEDs no Olá bastidor EBOD][3] 

Pode utilizar Olá seguinte tabela toodetermine Olá Estado Olá PCM.  

| Estado | PCM OK (verde) | Falha de AC (amber) | Ventoinha falhar (amber) | Falha de DC (amber) |
| --- | --- | --- | --- | --- |
| Sem energia de AC (tooenclosure) |OFF |OFF |OFF |OFF |
| Sem energia de AC (apenas para este PCM) |OFF |ON |OFF |ON |
| AC está presente no PCM – OK |ON |OFF |OFF |OFF |
| Falha PCM (ventoinha falhar) |OFF |OFF |ON |X |
| Falhas PCM (através de amp, através de tensão, através de atual |OFF |ON |ON |ON |
| PCM (ventoinha fora tolerância) |ON |OFF |OFF |ON |
| Modelo de reserva dinâmica |Flashing |OFF |OFF |OFF |
| Transferência de firmware PCM |OFF |Flashing |Flashing |Flashing |

## <a name="controller-module-indicator-leds"></a>Indicador de módulo de controlador LEDs
o dispositivo StorSimple Olá contém LEDs para o controlador principal de Olá e módulos de controlador Olá EBOD.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>Monitorização LEDs para o controlador principal de Olá
Olá ilustração seguinte ajuda-o a identificar Olá LEDs no controlador principal de Olá. (Todos os componentes de Olá estão listada tooaid no orientação).  

   ![LEDs - controlador principal de monitorização][4]

A tabela de utilização Olá seguinte toodetermine se o módulo de controlador Olá está a funcionar corretamente.  

### <a name="controller-indicator-leds"></a>Indicador de controlador LEDs
| LED | Descrição |
| --- | --- |
| ID LED (azul) |Indica que esse módulo Olá está a ser identificado. Se hello LED azul é blinking num controlador de execução, em seguida, hello controlador é Olá Active Directory controlador e Olá outro Olá espera controlador de. Para obter mais informações, consulte [identificar controlador ativo do Olá no seu dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| Falhas LED (amber) |Indica uma falha no controlador de Olá. |
| LED OK (verde) |Gradual verde indica que desse controlador Olá está OK. Flashing verde indica um erro de configuração VPD de controlador. |
| Atividade SAS LEDs (verde) |Gradual verde indica uma ligação com nenhuma atividade atual. Flashing verde indica a ligação de Olá tem actividade em curso. |
| Estado de Ethernet LEDs |Lado direito indicar atividade de ligação/rede: Active Directory, (flashing verde) de ligação (verde gradual) atividade de rede. Lado esquerdo indica a velocidade da rede: (amarelo) 1000 Mb/s, (OFF) e (verde) 100 Mb/s, 10 Mb/s. Dependendo do modelo de componente de Olá, este leve poderá blink, mesmo que a interface de rede Olá não está ativada. |
| POST LEDs |Indica o progresso de arranque Olá quando o controlador de Olá está ativado. Se o dispositivo StorSimple Olá falhar tooboot, este LED ajudará a identificar o ponto de Olá no processo de arranque Olá em que ocorreu a falha de Olá Support da Microsoft. |

> [!IMPORTANT]
> Se a falhas de Olá LED é lit, há um problema com o módulo de controlador Olá que poderá ser resolvido reiniciando controlador Olá. Contacte Support da Microsoft se o controlador de Olá reiniciar não resolver este problema.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>Monitorização LEDs para Olá EBOD (bastidor EBOD)
Cada um dos Olá 6 Gb/controladores de SAS EBOD s tem LEDs indicam o respetivo estado conforme mostrado na seguinte ilustração de Olá.  

  ![Monitorização LEDs - bastidor EBOD][5]

A tabela de utilização Olá seguinte toodetermine se Olá módulo de controlador EBOD está a funcionar normalmente.  

### <a name="ebod-controller-module-indicator-leds"></a>Indicador de módulo de controlador EBOD LEDs
| Estado | Módulo de e/s OK (verde) | Falhas de módulo de e/s (amber) | Atividade de porta de anfitrião (verde) |
| --- | --- | --- | --- |
| Módulo de controlador OK |ON |OFF |- |
| Falha do módulo de controlador |OFF |ON |- |
| Nenhuma ligação de porta de anfitrião externo |- |- |OFF |
| Ligação de porta de anfitrião externo – nenhuma atividade |- |- |ON |
| Ligação de porta de anfitrião externo - atividade |- |- |Flashing |
| Erro de metadados do módulo de controlador |Flashing |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Indicador de unidade de disco LEDs para inclusão principal Olá e inclusão EBOD
o dispositivo StorSimple Olá tem unidades de disco localizadas no bastidor primário Olá e inclusão EBOD Olá. Cada unidade de disco contém monitorização indicador LEDs, conforme descrito nesta secção. 

Para unidades de disco Olá, o estado da unidade de Olá é indicado por uma verde LED e um LED red amber montado em frente Olá do módulo de carrier cada unidade. Olá ilustração seguinte mostra estes LEDs.

  ![Unidade de disco LEDs][6]

Utilize Olá tabela toodetermine Olá Estado cada unidade de disco, o que por sua vez afeta Olá Estado painel global frontal LED a seguir.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Indicador de unidade de disco LEDs para Olá bastidor EBOD
| Estado | Atividade LED de OK (verde) | Falhas LED (amber vermelho) | Painel de ops LED de associados |
| --- | --- | --- | --- |
| Nenhuma unidade instalado |OFF |OFF |Nenhuma |
| Unidade instalada e operacional |Flashing / com atividade |X |Nenhuma |
| Conjunto de identidade de dispositivo de serviços de bastidor SCSI (SES) |ON |Flashing 1 segundo em/1 segundo desativado |Nenhuma |
| Conjunto de bits de falhas de dispositivo SES |ON |ON |Lógica falha (vermelho) |
| Falha de circuito de controlo de energia |OFF |ON |Falha do módulo (vermelho) |

## <a name="audible-alarms"></a>Alarmes audible
Um dispositivo StorSimple contém alarmes audible associados ao bastidor primário Olá e inclusão EBOD Olá. Um alarme audible está localizado no painel frontal Olá (também conhecido como painel de ops Olá) de ambas as caixas. alarme audible Olá indica quando está presente uma condição de falha. Olá seguintes condições serão ativados alarme Olá:  

* Falhas de ventoinha ou falha
* Tensão fora do intervalo
* Ativação pós-falha ou com a condição de temperatura
* Thermal overrun
* Falhas de sistema
* Índice de falhas lógica
* Falha de alimentação de energia
* Remoção de uma potência arrefecimento módulo (PCM)  

Olá tabela seguinte descreve Olá várias alarme Estados.  

### <a name="alarm-states"></a>Estados de alarme
| Estado de alarme | Ação | Acção conjunta mute botão premido |
| --- | --- | --- |
| S0 |Modo normal: automática |Aviso sonoro duas vezes |
| S1 |Modo de falhas: 1 segundo em/1 segundo desativado |Transição tooS2 ou S3 (consulte as notas de) |
| S2 |Modo de lembrar: beep intermitente |Nenhuma |
| S3 |Modo muted: automática |Nenhuma |
| S4 |Modo de falhas crítico: alarme contínua |Não está disponível: desativar som não Active Directory |

> [!NOTE]
> * Estado de alarme S1, se não premir mute em dois minutos, o estado de Olá transita automaticamente tooS2 ou S3.  
> * Estados de alarme S1 tooS4 devolver tooS0 depois de condição de falha de Olá está desmarcada.  
> * Estado de falha crítica S4 pode ser introduzido a partir de qualquer outro Estado.  


Pode mute alarme audible Olá, premindo o botão mute Olá no painel de ops Olá. Muting automática irá ocorrer depois de dois minutos se comutador mute Olá não é operada manualmente. Quando é muted alarme Olá, continuará toosound com tooindicate beeps intermitente curto que continua a existir um problema. alarme Olá será automática quando todos os problemas de Olá são eliminados.

Olá tabela seguinte descreve Olá alarme de várias condições.

### <a name="alarm-conditions"></a>Condições de alarme
| Estado | Gravidade | Alarme | OPS painel LED |
| --- | --- | --- | --- |
| Alerta PCM – perda de energia de DC de um único PCM |Falhas – sem perda de redundância |S1 |Falha do módulo |
| Alerta PCM – perda de energia de DC de um único PCM |Falhas – perda de redundância |S1 |Falha do módulo |
| Falha de ventoinha PCM |Falhas – perda de redundância |S1 |Falha do módulo |
| O módulo SBB detetou falhas PCM |Índice de falhas |S1 |Falha do módulo |
| PCM removido |Erro de configuração |Nenhuma |Falha do módulo |
| Erro de configuração de inclusão |Índice de falhas – crítico |S1 |Falha do módulo |
| Alerta de aviso de temperatura baixa |Aviso |S1 |Falha do módulo |
| Alerta de aviso de temperatura elevada |Aviso |S1 |Falha do módulo |
| Ao longo de alarme de temperatura |Índice de falhas – crítico |S1 |Falha do módulo |
| Falha de barramento I2C |Falhas – perda de redundância |S1 |Falha do módulo |
| Erro de comunicação (I2C) de painel do OPS Manager |Índice de falhas – crítico |S1 |Falha do módulo |
| Erro de controlador |Índice de falhas – crítico |S1 |Falha do módulo |
| Falhas de módulo de interface SBB |Índice de falhas – crítico |S1 |Falha do módulo |
| Falha no módulo de interface SBB – não funcionar módulos restante |Índice de falhas – crítico |S4 |Falha do módulo |
| Módulo de interface SBB removido |Aviso |Nenhuma |Falha do módulo |
| Falha de controlo de energia de unidade |Aviso – sem perda de energia de unidade |S1 |Falha do módulo |
| Falha de controlo de energia de unidade |Índice de falhas – crítico; Falha de energia de unidade |S1 |Falha do módulo |
| Unidade removida |Aviso |Nenhuma |Falha do módulo |
| Energia suficiente disponível |Aviso |Nenhum |Falha do módulo |

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [StorSimple componentes de hardware e estado](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


