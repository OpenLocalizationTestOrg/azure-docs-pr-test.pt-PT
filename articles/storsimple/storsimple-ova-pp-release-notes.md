---
title: "notas de versão de matriz Virtual aaaStorSimple | Microsoft Docs"
description: "Descreve problemas abertos críticos e resoluções para Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>Notas de versão de matriz Virtual StorSimple
## <a name="overview"></a>Descrição geral
Olá notas de versão seguintes identificam problemas abertos críticos Olá para versão de disponibilidade geral (DG) de Março de 2016 Olá do Olá Microsoft Azure StorSimple Virtual matriz (também conhecido como dispositivo virtual StorSimple no local de Olá ou Olá StorSimple virtual dispositivo). Esta versão corresponde à versão toosoftware 10.0.10271.0.

notas de versão Olá continuamente são atualizadas e à medida que são descobertos problemas críticos que requerem uma solução, estes são adicionados. Antes de implementar o dispositivo virtual StorSimple, reveja com atenção as informações de Olá contidas nas notas de versão Olá. 

Olá, a tabela seguinte fornece um resumo dos problemas conhecidos desta versão.

| Não. | Funcionalidade | Problema | Solução/comentários |
| --- | --- | --- | --- |
| **1.** |Atualizações |dispositivos virtuais Olá criados numa versão de pré-visualização Olá não podem ser atualizada tooa suportado versão de disponibilidade geral. |Estes dispositivos virtuais tem a ativação pós-falha para Olá utilizando um fluxo de trabalho do após desastre (DR) de recuperação de lançamento de disponibilidade geral. |
| **2.** |Disco de dados de aprovisionamento |Uma vez aprovisionou um disco de dados de um determinado tamanho especificado e criado Olá correspondente do dispositivo virtual StorSimple, tem não expandir ou reduzir o disco de dados de Olá. Tentar toodo, por isso, resultará na perda de todos os dados de Olá nas camadas locais do Olá do dispositivo Olá. | |
| **3.** |Política de grupo |Quando um dispositivo está associado a um domínio, aplicar uma política de grupo que pode afetar negativamente operação de dispositivo Olá. |Certifique-se de que a matriz de virtual está no seu próprio unidade organizacional (UO) do Active Directory e não existem objetos de política de grupo (GPO) são tooit aplicado. |
| **4.** |IU da web do local |Se as funcionalidades de segurança avançada estiverem ativadas no Internet Explorer (IE ESC), algumas páginas de IU da web de locais como resolução de problemas ou a manutenção poderão não funcionar corretamente. Botões nestas páginas também poderão não funcionar. |Desative funcionalidades de segurança avançada do Internet Explorer. |
| **5.** |IU da web do local |Numa máquina virtual de Hyper-V, Olá interfaces de rede na web Olá IU são apresentadas como 10 Gbps interfaces. |Este comportamento é um reflexão do Hyper-V. Hyper-V Mostra sempre a 10 Gbps para adaptadores de rede virtual. |
| **6.** |Volumes em camadas ou partilhas |Intervalo de byte bloqueio para aplicações que funcionam com Olá StorSimple volumes em camadas não é suportado. Se o bloqueio de intervalo de byte estiver ativado, a criação de camadas do StorSimple não irá funcionar. |Medidas recomendadas incluem: <br></br>Desative o intervalo de byte bloquear na lógica da sua aplicação.<br></br>Escolha tooput dados para esta aplicação em volumes localmente afixados por oposição ao tootiered volumes.<br></br>*Advertência*: Se utilizar localmente afixado volumes e o bloqueio de intervalo de byte está ativado, lembre-se de que o volume de Olá afixado localmente pode ficar online, mesmo antes de Olá restauro foi concluído. Nessas instâncias, se for um restauro em curso, em seguida, tem de aguardar Olá toocomplete de restauro. |
| **7.** |Partilhas em camadas |Trabalhar com ficheiros grandes pode resultar em camada lenta. |Ao trabalhar com ficheiros grandes, recomendamos que esse ficheiro maior Olá é inferior a 3 de % do tamanho da partilha de Olá. |
| **8.** |Utilizar a capacidade de partilhas |Poderá ver partilhar consumo na ausência de Olá de quaisquer dados na partilha de Olá. Isto acontece porque a capacidade de Olá utilizado para partilhas inclui metadados. | |
| **9.** |Recuperação após desastre |Só pode efetuar a recuperação de desastre Olá de um toohello do servidor de ficheiros que o dispositivo de origem Olá mesmo domínio. Dispositivo de destino do desastre recuperação tooa noutro domínio não é suportado nesta versão. |Isto irá ser implementado uma versão posterior. |
| **10.** |Azure PowerShell |dispositivos virtuais do StorSimple Olá não podem ser geridos através de Olá Azure PowerShell nesta versão. |Todos os Olá gestão de dispositivos virtuais Olá deve ser feito Olá portal clássico do Azure e IU da web local Olá. |
| **11.** |Alteração de palavra-passe |consola de dispositivo Olá matriz virtual apenas aceita entrada no formato de teclado en-US. | |
| **12.** |CHAP |Não não possível remover as credenciais CHAP depois de criado. Além disso, se modificar as credenciais CHAP Olá, será necessário tootake volumes de Olá offline e, em seguida, colocá-los online para Olá alteração tootake produza efeitos. |Estes serão resolvidos numa versão posterior. |
| **13.** |servidor de iSCSI |Olá 'Armazenamento utilizado' apresentado para um volume de iSCSI pode ser diferente no serviço do StorSimple Manager Olá e o anfitrião de iSCSI Olá. |anfitrião de iSCSI Olá tem uma vista de sistema de ficheiros de Olá.<br></br>dispositivo Olá vê os blocos de Olá atribuídos ao volume Olá estava no tamanho máximo de Olá. |

