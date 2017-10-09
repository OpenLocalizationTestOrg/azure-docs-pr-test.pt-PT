---
title: aaaMonitor o dispositivo StorSimple | Microsoft Docs
description: "Descreve como toouse Olá desempenho toomonitor e/s do serviço StorSimple Manager, utilização da capacidade, débito de rede e desempenho do dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Utilizar toomonitor de serviço do StorSimple Manager Olá o dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Pode utilizar dispositivos específicos do Olá StorSimple Manager serviço toomonitor dentro da sua solução StorSimple. Pode criar gráficos personalizados com base no desempenho e/s, utilização da capacidade, débito de rede e métricas de desempenho do dispositivo. 

tooview Olá informações para um dispositivo específico, em Olá portal clássico do Azure, do serviço StorSimple Manager Olá selecione de monitorização. Clique em Olá **Monitor** separador e, em seguida, selecione de Olá lista de dispositivos. Olá **Monitor** página contém Olá informações a seguir.

## <a name="io-performance"></a>Desempenho de e/s
**Desempenho de e/s** controla métricas relacionadas com o número de toohello de leitura e escrita operações entre a iSCSI Olá interfaces de iniciador no servidor de anfitrião Olá e dispositivo Olá ou dispositivo Olá e nuvem Olá. Este desempenho pode ser medido para um volume específico, um contentor de volume específico ou todos os contentores de volume.

gráfico de Olá abaixo mostra Olá i / o para o dispositivo de tooyour iniciador Olá todos os volumes de Olá para um dispositivo de produção. métricas de Olá desenhadas são lidas e escrever bytes por segundo, ler e escrever operações de e/s por segundo e leem e escrevem latências.

![Desempenho de e/s de iniciador toodevice](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Para Olá mesmo dispositivo, as operações de e/s de Olá são desenhadas para dados Olá Olá dispositivo toohello nuvem para Olá todos os contentores de volume. Neste dispositivo, os dados de Olá são apenas na camada linear Olá e nada tem spilled toohello nuvem. Não existem não existem operações de leitura e escrita do dispositivo toohello nuvem a ocorrer. Por conseguinte, os picos de Olá no gráfico de Olá são um intervalo de 5 minutos, que corresponde a frequência de toohello em que o heartbeat Olá é verificado entre dispositivos de Olá e o serviço de Olá. 

![Desempenho de e/s de dispositivo toocloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Para hello mesmo dispositivo, um instantâneo na nuvem foi direcionado para os dados de volume começando 2:00 pm. Isto resultou em dados que fluem do Olá dispositivo toohello nuvem. Escritas de leituras foram servidas toohello nuvem esta duração. Olá gráfico de e/s mostra um horário de pico Olá várias métricas correspondente tempo toohello quando Olá instantâneo. 

![Desempenho de e/s de dispositivo toocloud após o instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Utilização de capacidade
**Utilização de capacidade** quantidade de toohello relacionados controla as métricas de espaço de armazenamento de dados que é utilizado por volumes Olá, contentores de volume ou dispositivo. Pode criar relatórios com base na utilização da capacidade de Olá do seu armazenamento primário, o seu armazenamento na nuvem ou o armazenamento do dispositivo. Utilização de capacidade pode ser medida em volume específico, um contentor de volume específico ou todos os contentores de volume.

Olá primário, de nuvem e de capacidade de armazenamento do dispositivo podem ser descritas da seguinte forma:

### <a name="primary-storage-capacity-utilization"></a>Utilização da capacidade de armazenamento primário
Estes gráficos mostram a quantidade de Olá de dados escritos tooStorSimple volumes antes dos dados de Olá é comprimidos e eliminação de duplicados. Pode ver a utilização de armazenamento primário Olá por todos os volumes ou de um único volume.

Ao ver gráficos utilização capacidade de volume de armazenamento primário de Olá para todos os volumes versus cada um dos volumes individuais Olá e soma dos dados primários Olá ambas nestes casos, poderão ocorrer um erro de correspondência entre dois números de Olá. Olá total primário de dados em todos os volumes não podem ser adicionados até toohello total da soma de dados primários de Olá de volumes individuais Olá. Isto pode ser devido tooone seguinte Olá:

* **Incluído em todos os volumes de dados de instantâneos**: Este comportamento é utilizado apenas se estiver a executar versão anterior ao Update 3. dados primários Olá apresentados para todos os volumes de Olá são a soma de Olá de dados principal do Olá para cada volume e dados de instantâneos de Olá. dados primários Olá mostrados para um determinado volume corresponde a quantidade de Olá tooonly de dados no volume de Olá (e não incluem dados de instantâneos de volume correspondente Olá).
  
    Também pode ser explicado por Olá equação os seguintes:
  
    *(Todos os volumes) de dados principal = soma de (dados primários (volume i) + tamanho dos dados de instantâneos (volume i))*
  
    *WHERE, dados primários (volume i) = tamanho de dados principal atribuídos toovolume i*
  
    Se os instantâneos de Olá são eliminados através do serviço de Olá, eliminação Olá é feita no modo assíncrono em segundo plano de Olá. Pode demorar algum tempo para Olá volume dados tamanho toobe atualizado seguintes Olá a eliminação do instantâneo. 
  
    Se executar a atualização 3 ou posterior, dados de instantâneos de Olá não estão incluídos nos dados do volume de Olá. E utilização primário Olá é calculada da seguinte forma:
  
    * Dados principal (todos os volumes) = soma de (dados primários (volume i)
  
    *WHERE, dados primários (volume i) = tamanho de dados principal atribuídos toovolume i*
* **Volumes com a monitorização desativada incluídos em todos os volumes**: Se tiver de volumes no seu dispositivo para o qual monitorização está desativada, Olá dados para estes volumes individuais de monitorização não estará disponível em gráficos de Olá. No entanto, os dados Olá para todos os volumes no gráfico de Olá incluem volumes Olá para o qual monitorização está desativada. 
* **Eliminar os volumes com em direto cópias de segurança associadas incluídas para todos os volumes**: se volumes que contêm dados de instantâneos são eliminados, mas ainda existem instantâneos Olá associado, em seguida, poderá ver um erro de correspondência.
* **Eliminar os volumes incluídos em todos os volumes**: em alguns casos, os volumes antigos poderão existir, apesar de estes foram eliminados. Não é utilizado o efeito de Olá da eliminação e dispositivo Olá pode mostrar inferior capacidade disponível. É necessário toocontact Microsoft Support tooremove estes volumes.

Olá gráficos seguintes mostram utilização da capacidade de armazenamento primário Olá de um dispositivo StorSimple antes e depois foi obtido um instantâneo de nuvem. Como esta é apenas os dados de volume, um instantâneo na nuvem não deve alterar armazenamento primário Olá. Como pode ver, o gráfico de Olá não mostra nenhuma diferença na utilização de capacidade primário Olá como resultado de um instantâneo de nuvem. instantâneo de nuvem Olá foi iniciado no aproximadamente 2:00 pm nesse dispositivo.

![Utilização da capacidade primário antes de instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Utilização da capacidade primário depois do instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Se estiver a executar a atualização 2 ou superior, pode dividir utilização da capacidade de armazenamento primário Olá por um volume individuais, todos os volumes, todos os volumes em camadas e todos os volumes localmente afixados conforme mostrado abaixo. Interrompendo para baixo por todos os localmente volumes afixados irão permitir tooquickly ascertain quantidade de escalão local Olá se esgotar.

![Utilização da capacidade de principal para todos os volumes localmente afixados](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Utilização da capacidade de armazenamento na nuvem
Estes gráficos mostram a quantidade de Olá de armazenamento em nuvem utilizado. Estes dados é de eliminação de duplicados e comprimidos. Esta quantidade inclui os instantâneos de nuvem que podem conter dados não serão refletidos na qualquer volume primário e são mantidos por motivos de retenção de legado ou necessário. Pode comparar Olá primário e nuvem armazenamento consumo figuras tooget uma ideia dos redução de dados de Olá classificar, apesar do número de Olá será não ser exato. Olá gráficos seguintes mostram Olá cloud storage utilização da capacidade de um dispositivo StorSimple antes e depois foi obtido um instantâneo de nuvem. Olá instantâneo na nuvem foi iniciado no aproximadamente 2:00 pm nesse dispositivo e pode ver a utilização da capacidade de nuvem Olá captura cópias de segurança em Olá mesmo tempo, o aumento de 5.73 MB too4.04 GB.

![Utilização da capacidade de nuvem antes de instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Utilização da capacidade de nuvem após o instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Utilização de capacidade de armazenamento do dispositivo
Estes gráficos mostram a utilização total de Olá para o dispositivo Olá, que poderá ser superior a utilização de armazenamento primário pois inclui camada linear do Olá SSD. Esta camada contém uma quantidade de dados também existe na Olá outros escalões do dispositivo. capacidade de Olá na camada de linear Olá SSD é cycled, para que quando novos dados é apresentada no, Olá antigo dados camada HDD de toohello movido (em que momento é eliminação de duplicados e comprimido) e, subsequentemente, toohello nuvem.

Ao longo do tempo, utilização da capacidade primário e de utilização da capacidade de dispositivo irão provavelmente aumentar em conjunto até que o início dos dados de Olá toobe camadas toohello nuvem. Nessa altura, utilização da capacidade de dispositivo Olá provavelmente começará tooplateau, mas a utilização da capacidade de principal de Olá irá aumentar à medida que são escritos mais dados.

Olá gráficos seguintes mostram utilização da capacidade de armazenamento primário Olá de um dispositivo StorSimple antes e depois foi obtido um instantâneo de nuvem. instantâneo de nuvem Olá iniciada às 2:00 pm e utilização da capacidade de dispositivo Olá iniciado diminuição nessa altura. utilização da capacidade de armazenamento dispositivo Olá correu para baixo de 11.58 GB too7.48 GB. Isto indica que provavelmente hello descomprimidos dados na camada SSD linear Olá foi eliminação de duplicados, comprimidos e movidos para a camada HDD de Olá. Tenha em atenção que, se o dispositivo de Olá já tem uma grande quantidade de dados no Olá SSD e camadas HDD, não poderá ver este diminuir. Neste exemplo, o dispositivo de Olá tem uma pequena quantidade de dados.

![Utilização da capacidade de dispositivo antes de instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Utilização da capacidade de dispositivo depois de instantâneo na nuvem](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Débito de rede
**Débito de rede** quantidade de toohello relacionados controla as métricas de dados transferidos de interfaces de rede de iniciador do Olá iSCSI no servidor de anfitrião de Olá e dispositivo Olá e entre o dispositivo de Olá e nuvem Olá. Pode monitorizar esta métrica para cada uma das interfaces de rede iSCSI Olá no seu dispositivo.

Olá seguir gráficos Mostrar Olá débito de rede para Olá dados 0 e 4 de dados, ambas as interfaces de rede GbE 1 no seu dispositivo. Neste caso, dados 0 foi ativado para a nuvem enquanto 4 de dados foi preparada para iSCSI. Pode ver os dois Olá de entrada e Olá tráfego de saída para o dispositivo StorSimple. linha simples de Olá no gráfico de Olá começando às 15:24 é owing toohello facto que iremos recolher dados a cada 5 minutos e deve ser ignorados. 

![Débito de rede para Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Débito de rede para Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Desempenho de dispositivo
**Desempenho de dispositivo** controla métricas relacionadas com toohello desempenho do seu dispositivo. Olá gráfico a seguir mostra estatísticas de utilização de CPU Olá para um dispositivo em produção.

![Utilização da CPU de dispositivo](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[utilizar o dashboard de dispositivo de serviço Olá StorSimple Manager](storsimple-device-dashboard.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

