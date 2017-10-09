---
title: aaaStorSimple componentes de hardware e Estado | Microsoft Docs
description: "Saiba como toomonitor Olá componentes de hardware do dispositivo StorSimple através de Olá serviço StorSimple Manager."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0d56a2ba-daf0-45ad-9610-8b8712dd5750
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 12a62c0ffc4a5b5e72a25e9e1d976009be03c598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-hardware-components-and-status"></a>Utilizar componentes de hardware de toomonitor de serviço StorSimple Manager Olá e o Estado
## <a name="overview"></a>Descrição geral
Este artigo descreve Olá vários componentes físicos e lógicos no dispositivo StorSimple no local. Também explica como toomonitor Olá estado do componente de dispositivo utilizando Olá **manutenção** página Olá serviço StorSimple Manager. 

Olá **manutenção** página mostra o estado do hardware Olá todos os componentes de dispositivo do StorSimple Olá. 

Na lista de Olá dos componentes 8100, existem três secções que descrevem:

* **Partilhado componentes** – estes não fazem parte dos controladores de Olá, tais como unidades de disco, bastidor, componentes PCM temperatura PCM, linha tensão e linha sensores atuais.
* **Componentes de controlador 0** – componentes Olá que se encontram no controlador 0, como o controlador, SAS expander e o conector, sensores de temperatura de controlador e Olá várias interfaces de rede.
* **Componentes de controlador 1** – Olá componentes que constituem toothose semelhante detalhada para o controlador 0 do controlador 1.

Um dispositivo 8600 tem componentes adicionais que correspondem toohello bastidor expandido Bunch de discos (EBOD). Na lista de Olá dos componentes, existem cinco secções. Deles, existem três secções que contêm componentes de Olá no bastidor primário Olá e são idêntico toohello aqueles descritos para 8100. Existem duas secções adicionais para Olá bastidor EBOD que descrevem:

* **EBOD bastidor partilhado componentes** – componentes Olá está presente na inclusão EBOD Olá e PCM que não fazem parte do controlador EBOD Olá.
* **Componentes de EBOD controlador 0** – Olá componentes que residem no bastidor EBOD 0, tais como controlador EBOD Olá, sensores de temperatura de expander e o conector e o controlador SAS.
* **Componentes de 1 de controlador EBOD** – Olá componentes que constituem a inclusão EBOD 1, toothose semelhante detalhadas para inclusão EBOD 0.

> [!NOTE]
> **secção de estado do hardware Olá não está presente na página de manutenção de Olá para um dispositivo virtual StorSimple (1100).**
> 
> 

## <a name="monitor-hello-hardware-status"></a>Monitorizar o estado do hardware Olá
Execute Olá seguir o estado do hardware passos tooview Olá de um componente de dispositivo:

1. Navegue demasiado**dispositivos**, selecione um dispositivo StorSimple específico. Clique em toogo no menu de nível de dispositivo Olá e, em seguida, clique em **manutenção**. 
2. Localizar Olá **estado do Hardware** secção e escolha entre os componentes de disponíveis Olá (conforme descrito acima). Basta clicar uma seta precedente Olá etiqueta tooexpand Olá lista e vista Olá estado do componente de Olá vários componentes do dispositivo. Consulte Olá [lista de componentes de detalhado para inclusão principal Olá](#component-list-for-primary-enclosure-of-storsimple-device) e Olá [lista de componentes de detalhado para Olá bastidor EBOD](#component-list-for-ebod-enclosure-of-storsimple-device).
3. Utilize Olá seguir o estado do componente de Olá de cor codificação toointerpret de esquema:
   
   * **Verde verificação** – Denotes um **bom estado de funcionamento** ou **OK** componente.
   * **Amarelo** – indica um componente na **aviso** estado.
   * **Exclamação vermelha** – Denotes um componente que tenha um **falha** ou **necessita de atenção** estado.
   * **Branco com texto preto** – indica um componente que não está presente.
4. Se tiver um componente que não esteja num **bom estado de funcionamento** de estado, contacte Support da Microsoft. Se os alertas são ativados no seu dispositivo, receberá um alerta por e-mail. Se precisar de tooreplace um componente de falha de hardware, consulte [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Lista de componentes para inclusão principal do dispositivo StorSimple
Olá seguinte tabela destaca Olá componentes físicos e lógicos contidos no bastidor primário do Olá do dispositivo StorSimple no local.

| Componente | Módulo | Tipo | Localização | Unidade de substituível em campo (FRU)? | Descrição |
| --- | --- | --- | --- | --- | --- |
| Unidade na ranhura [0-11] |Unidades de disco |Físico |Partilhado |Sim |É apresentada uma linha para cada um dos Olá SSD ou Olá HDD unidades no bastidor primário Olá. |
| Sensor de temperatura de ambiente |Inclusão |Físico |Partilhado |Não |Medidas Olá temperatura num chassis de Olá. |
| Sensor de temperatura média dimensão que plane |Inclusão |Físico |Partilhado |Não |Medidas Olá temperatura de plane intermédio Olá. |
| Audible alarme |Inclusão |Físico |Partilhado |Não |Indica se o subsistema de alarme audible Olá num chassis de Olá está funcional. |
| Inclusão |Inclusão |Físico |Partilhado |Sim |Indique a presença Olá um chassis. |
| Definições de inclusão |Inclusão |Físico |Partilhado |Não |Refere-se o painel frontal da toohello de chassis Olá. |
| Sensores de tensão de linha |PCM |Físico |Partilhado |Não |Várias sensores de tensão de linha tem o respetivo estado apresentado, que indica se Olá medido tensão respeitam a tolerância. |
| Sensores atuais de linha |PCM |Físico |Partilhado |Não |Várias sensores atual de linha tem o respetivo estado apresentado, que indica se hello atual medido respeitam a tolerância. |
| Sensores de temperatura no PCM |PCM |Físico |Partilhado |Não |Várias sensores de temperatura, tais como os sensores de entrada e de hotspots tem o respetivo estado apresentado, que indica se Olá medido temperatura é respeitam a tolerância. |
| Fonte de alimentação [0-1] |PCM |Físico |Partilhado |Sim |Uma linha é apresentada para cada uma das fontes de alimentação Olá no Olá dois PCMs localizados em Olá back of dispositivo Olá. |
| Arrefecimento [0-1] |PCM |Físico |Partilhado |Sim |Uma linha é apresentada para cada um dos Olá quatro ventoinhas de arrefecimento residentes nas Olá dois PCMs. |
| Bateria [0-1] |PCM |Físico |Partilhado |Sim |É apresentada uma linha para cada um dos módulos de cópia de segurança de bateria Olá que são seated no Olá PCM. |
| Metis |N/D |Lógica |Partilhado |N/D |Apresenta o estado de Olá de baterias Olá: tem de charging e estão a aproximar-se o fim-de-vida. |
| Cluster |N/D |Lógica |Partilhado |N/D |Apresenta Olá estado do cluster de Olá que é criado entre dois módulos de controlador integrado Olá. |
| Nó de cluster |N/D |Lógica |Partilhado |N/D |Indica o estado de Olá de controlador de Olá como parte do cluster de Olá. |
| Quórum de cluster |N/D |Lógica | |N/D |Indique a presença Olá Olá maioria disco a associação ao hello do agrupamento de armazenamento HDD. |
| Espaço de dados HDD |N/D |Lógica |Partilhado |N/D |espaço de armazenamento de Olá que é utilizado para dados no agrupamento de armazenamento de disco rígido (HDD) Olá. |
| Espaço de gestão de HDD |N/D |Lógica |Partilhado |N/D |espaço de Olá reservado no Olá agrupamento de armazenamento HDD para tarefas de gestão. |
| Espaço de quórum HDD |N/D |Lógica |Partilhado |N/D |espaço de Olá reservado no Olá agrupamento de armazenamento HDD para quórum de cluster. |
| Espaço de substituição de HDD |N/D |Lógica |Partilhado |N/D |espaço de Olá reservado no Olá agrupamento de armazenamento HDD para substituição de controlador. |
| Espaço de dados SSD |N/D |Lógica |Partilhado |N/D |espaço de armazenamento Olá utilizado para os dados na unidade de estado sólido Olá agrupamento de armazenamento (SSD). |
| Espaço de SSD NVRAM |N/D |Lógica |Partilhado |N/D |espaço de armazenamento de Olá no Olá agrupamento de armazenamento SSD que está dedicado para a lógica de NVRAM. |
| Agrupamento de armazenamento HDD |N/D |Lógica |Partilhado |N/D |Apresenta Olá Estado Olá lógicas do agrupamento de armazenamento criada a partir desse dispositivo HDDs. |
| Agrupamento de armazenamento SSD |N/D |Lógica |Partilhado |N/D |Apresenta Olá Estado Olá lógicas do agrupamento de armazenamento criada a partir desse dispositivo SSDs. |
| Controlador [0-1], [Estado] |E/S |Físico |Controlador |Sim |Apresenta o estado de Olá de controlador de Olá, e se está no modo de reserva dinâmica ou Active Directory dentro de chassis Olá. |
| Sensores de temperatura no controlador |E/S |Físico |Controlador |Não |Várias sensores de temperatura, tais como o módulo de e/s, temperatura de CPU, sensores DIMM e PCIe tem o respetivo estado apresentado, que indica se é ou não temperatura Olá encontrou respeitam a tolerância. |
| SAS expander |E/S |Físico |Controlador |Não |Indica o estado de Olá da Olá série anexado SCSI (SAS) expander, que é utilizado tooconnect Olá armazenamento integrada toohello controlador. |
| Conector SAS [0-1] |E/S |Físico |Controlador |Não |Indica o estado de Olá de cada conector SAS, que é utilizado tooconnect integrado armazenamento toohello SAS expander. |
| Interligação de média dimensão que plane SBB |E/S |Físico |Controlador |Não |Indica o estado de Olá do conector de média dimensão que plane Olá, que é utilizado tooconnect cada plane intermédio de toohello de controlador. |
| Núcleo do processador |E/S |Físico |Controlador |Não |Indica o estado de Olá Olá de núcleos de processador dentro de cada controlador. |
| Energia electronics de inclusão |E/S |Físico |Controlador |Não |Indica o estado de Olá do sistema de energia Olá utilizado por inclusão Olá. |
| Diagnóstico de electronics bastidor |E/S |Físico |Controlador |Não |Indica o estado de Olá da subsistemas de diagnóstico de Olá fornecido pelo controlador de Olá. |
| Controlador de gestão de placa base (BMC) |E/S |Físico |Controlador |Não |Indica o estado de Olá da Olá gestão controlador da placa base (BMC), que é um processador de serviço especializadas que monitoriza o dispositivo de hardware Olá através de sensores e comunica com o administrador de sistema Olá através de uma ligação independente. |
| Ethernet |E/S |Físico |Controlador |Não |Indica o estado de Olá de cada uma das interfaces de rede hello, ou seja, gestão de Olá e portas de dados fornecidas no controlador de Olá. |
| NVRAM |E/S |Físico |Controlador |Não |Indica o estado de Olá da NVRAM, uma memória de acesso aleatório não volátil cópia de segurança de bateria Olá que serve tooretain das informações críticas para a aplicação no evento Olá de falha de energia. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Lista de componentes para inclusão EBOD do dispositivo StorSimple
Olá seguinte tabela destaca Olá componentes físicos e lógicos contidos no Olá bastidor EBOD do dispositivo StorSimple no local.

| Componente | Módulo | Tipo | Localização | FRU? | Descrição |
| --- | --- | --- | --- | --- | --- |
| Unidade na ranhura [0-11] |Unidades de disco |Físico |Partilhado |Sim |É apresentada uma linha para cada um dos Olá que HDD unidades no início de Olá de Olá bastidor EBOD. |
| Sensor de temperatura de ambiente |Inclusão |Físico |Partilhado |Não |Medidas Olá temperatura num chassis de Olá. |
| Sensor de temperatura média dimensão que plane |Inclusão |Físico |Partilhado |Não |Medidas Olá temperatura de plane intermédio Olá. |
| Audible alarme |Inclusão |Físico |Partilhado |Não |Indica se o subsistema de alarme audible Olá num chassis de Olá está funcional. |
| Inclusão |Inclusão |Físico |Partilhado |Sim |Indique a presença Olá um chassis. |
| Definições de inclusão |Inclusão |Físico |Partilhado |Não |Refere-se de que toohello OPS ou o painel frontal da Olá de chassis Olá. |
| Sensores de tensão de linha |PCM |Físico |Partilhado |Não |Várias sensores de tensão de linha tem o respetivo estado apresentado, que indica se Olá medido tensão respeitam a tolerância. |
| Sensores atuais de linha |PCM |Físico |Partilhado |Não |Várias sensores atual de linha tem o respetivo estado apresentado, que indica se hello atual medido respeitam a tolerância. |
| Sensores de temperatura no PCM |PCM |Físico |Partilhado |Não |Várias sensores de temperatura, tais como os sensores de entrada e de hotspots tem o respetivo estado apresentado, que indica se Olá medido temperatura é respeitam a tolerância. |
| Fonte de alimentação [0-1] |PCM |Físico |Partilhado |Sim |Uma linha é apresentada para cada uma das fontes de alimentação Olá no Olá dois PCMs localizados em Olá back of dispositivo Olá. |
| Arrefecimento [0-1] |PCM |Físico |Partilhado |Sim |Uma linha é apresentada para cada um dos Olá quatro ventoinhas de arrefecimento residentes nas Olá dois PCMs. |
| Armazenamento local [HDD] |N/D |Lógica |Partilhado |N/D |Apresenta Olá Estado Olá lógicas do agrupamento de armazenamento criada a partir desse dispositivo HDDs. |
| Controlador [0-1], [Estado] |E/S |Físico |Controlador |Sim |Apresenta Olá estado dos controladores de Olá no módulo EBOD Olá. |
| Sensores de temperatura no EBOD |E/S |Físico |Controlador |Não |Várias sensores de temperatura de cada controlador de tem o respetivo estado apresentado, que indica se a temperatura Olá encontrou é respeitam a tolerância. |
| SAS expander |E/S |Físico |Controlador |Não |Indica o estado de Olá da expander SAS Olá, que é utilizado tooconnect Olá armazenamento integrada toohello controlador. |
| Conector SAS [0-2] |E/S |Físico |Controlador |Não |Indica o estado de Olá de cada conector SAS, que é utilizado tooconnect integrado armazenamento toohello SAS expander. |
| Interligação de média dimensão que plane SBB |E/S |Físico |Controlador |Não |Indica o estado de Olá do conector de média dimensão que plane Olá, que é utilizado tooconnect cada plane intermédio de toohello de controlador. |
| Energia electronics de inclusão |E/S |Físico |Controlador |Não |Indica o estado de Olá do sistema de energia Olá utilizado por inclusão Olá. |
| Diagnóstico de electronics bastidor |E/S |Físico |Controlador |Não |Indica o estado de Olá da subsistemas de diagnóstico de Olá fornecido pelo controlador de Olá. |
| Controlador de toodevice de ligação |E/S |Físico |Controlador |Não |Indica o estado de Olá da ligação de Olá entre o módulo de e/s de EBOD Olá e o controlador de dispositivo Olá. |

## <a name="next-steps"></a>Passos seguintes
* toouse Olá demasiado o dispositivo acedo de tooadminister de serviço StorSimple Manager[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).
* Se precisar de tootroubleshoot um componente de dispositivo que tem um Estado degradado ou falhado, consulte demasiado [StorSimple monitorização indicadores](storsimple-monitoring-indicators.md). 
* tooreplace um componente de falha de hardware, consulte [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).
* Se continuar tooexperience problemas com dispositivos, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md).

