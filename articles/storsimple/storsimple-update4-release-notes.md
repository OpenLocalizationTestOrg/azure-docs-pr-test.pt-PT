---
title: "notas de versão 4 de atualização de série aaaStorSimple 8000 | Microsoft Docs"
description: "Descreve as novas funcionalidades Olá, problemas e soluções para StorSimple 8000 série atualização 4."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Notas de versão do StorSimple 8000 série atualização 4

## <a name="overview"></a>Descrição geral

Olá notas de versão seguintes descrevem as novas funcionalidades Olá e identificam problemas de abrir críticos Olá para StorSimple 8000 série atualização 4. Também contêm uma lista de atualizações de software Olá StorSimple incluído nesta versão. 

Atualização 4 pode ser aplicado tooany o dispositivo StorSimple com o lançamento (GA) ou atualização 0.1 através da atualização 3.1. versão do dispositivo Olá associada com a atualização 4 é 6.3.9600.17820.

Reveja as informações de Olá contidas na versão de Olá notas antes de implementar Olá atualizar na sua solução StorSimple.

> [!IMPORTANT]
> * Atualização 4 tem o software de dispositivos, USM de firmware, controladores de LSI e firmware, firmware de disco, Storport e Spaceport, segurança e outras atualizações do SO. Demora cerca de 4 horas tooinstall esta atualização. Atualização de firmware do disco é uma atualização acontece e resulta num tempo de inatividade para o seu dispositivo. Recomendamos que aplique a atualização 4 tookeep dispositivo atualizado. 
> * Para os novos lançamentos, poderá não ver atualizações imediatamente porque fazemos de uma implementação faseada de Olá atualizações. Aguarde alguns dias e, em seguida, análise de atualizações novamente como estes deixará de estar disponível em breve.

## <a name="whats-new-in-update-4"></a>Novidades na atualização 4

Olá seguintes melhoramentos essenciais e correções de erros foram efetuadas na atualização 4.

* **Mais inteligentes automatizada algoritmos de recuperação de espaço** – atualização 4, hello espaço automatizada recuperação algoritmos são recuperação de espaço de Olá tooadjust avançada ciclos com base no Olá esperado reclamada espaço disponível na nuvem de Olá. 

* **Melhoramentos de desempenho para volumes localmente afixados** – Update 4 melhorou desempenho Olá de volumes localmente afixados em cenários que têm a ingestão de dados de elevado (comparável toovolume tamanho dos dados).

* **Com base em Heatmap restauro** - na Olá anteriormente versões, após uma recuperação após desastre (DR), dados de Olá foi restauradas a partir de nuvem Olá com base nos padrões de acesso de Olá resultavam um desempenho lento. 

    Uma funcionalidade nova é implementada na atualização 4 que controla acedidos com frequência dados toocreate um heatmap quando o dispositivo de Olá está no tooDR anterior de utilização (segmentos de dados mais utilizados tem térmico elevado, enquanto a menor utilizada segmentos ter térmico baixo). Depois de DR, StorSimple utiliza Olá heatmap tooautomatically restauro e rehydrate dados Olá da nuvem Olá. 

    Todos os Olá restauros estão agora heatmap com base em restauros. Para obter mais informações sobre como heatmap tooquery e cancelar baseado em tarefas de restauro e rehydration, visite demasiado[do Windows PowerShell para StorSimple referência de cmdlet](https://technet.microsoft.com/library/dn688168.aspx).

* **Ferramenta de diagnóstico do StorSimple** – na atualização 4, um diagnóstico StorSimple ferramenta está a ser lançado tooallow para fácil diagnosticar e resolução de problemas relacionados com o estado de funcionamento de componente do toosystem, rede, desempenho e hardware. Esta ferramenta é executada através de Olá do Windows PowerShell para StorSimple. Para mais informações, visite demasiado[resolver problemas com a ferramenta de diagnóstico do StorSimple](storsimple-8000-diagnostics.md).

* **Ferramenta de migração do StorSimple baseadas na IU** -versão toothis anteriores, a migração dos dados da série de 5000 7000 necessário Olá utilizadores tooexecute parte do fluxo de trabalho de migração Olá utilizando a interface do PowerShell do Azure de Olá. Nesta versão, uma fácil de utilizar baseadas na IU StorSimple migração ferramenta é disponibilizada para suporte toofacilitate Olá mesmo fluxo de trabalho de migração. Esta ferramenta também permitirá para Olá na consolidação dos registos de recuperação. 

* **Alterações relacionadas com FIPS** - nesta versão em diante, FIPS está ativado por predefinição em todos os dispositivos de série de Olá 8000 do StorSimple para ambos Olá Microsoft Azure Government e contas de nuvem pública do Azure.

* **Atualizar as alterações** - nesta versão, tooupdate relacionados erros corrigir falhas.

* **Alerta de falhas de disco** -é adicionado um novo alerta que avisa o utilizador Olá de falhas de disco iminente nesta versão. Se encontrar este alerta, contacte a Microsoft Support tooship um disco de substituição. Para mais informações, visite demasiado[alertas de hardware no dispositivo StorSimple](storsimple-manage-alerts.md#hardware-alerts).

* **Alterações de substituição de controlador** -é adicionado um cmdlet que permite que o estado de Olá Olá utilizador tooquery do processo de substituição de controlador Olá nesta versão. Para mais informações, visite toohello [estado de substituição de controlador do cmdlet tooquery](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problemas fixos na atualização 4

Olá tabela seguinte fornece um resumo dos problemas que foram corrigidos na atualização 4.    

| Não | Funcionalidade | Problema | Aplica-se toophysical dispositivo | Aplica-se toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Ativação pós-falha |No Olá versão anterior, depois de Olá ativação pós-falha, não existe foi um problema relacionado com toocleanup observado no site do cliente Olá. Este problema ser corrigido nesta versão. |Sim |Sim |
| 2 |Volumes localmente afixados |Na versão anterior do Olá, Ocorreu uma problema toorelated volume a criação de volumes localmente afixados que resulta em falhas de criação do volume. Este problema foi causada de raiz e fixo nesta versão. |Sim |Não |
| 3 |Pacote de suporte |Na versão anterior, ocorreram o pacote de tooSupport relacionados problemas que resultaria numa exceção de System.OutOfMemory ou outros erros, causando uma falha de criação do pacote de suporte. Estes erros são fixo nesta versão. |Sim |Sim |
| 4 |Monitorização |Na versão anterior, não existe um problema relacionado com toomonitoring gráficos para volumes afixados localmente onde consumo é mostrado no EB. Este erro é resolvido nesta versão. |Sim |Sim |
| 5 |Migração |Na versão anterior, existem várias fiabilidade de toohello relacionados de problemas da migração a partir de dispositivos das séries 5000 7000 série too8000. Estes problemas tem sido resolvidos nesta versão. |Sim |Sim |
| 6 |Atualizar |Em versões anteriores, se tiver ocorrido uma falha de atualização, os controladores de Olá seriam entrar em modo de recuperação e, por conseguinte, Olá utilizador não foi possível continuar com a atualização Olá e teria toocontact Support da Microsoft. <br> Este comportamento foi alterado nesta versão. Se o utilizador Olá tem uma falha de atualização depois dos dois controladores de Olá em execução Olá a mesma versão (Update 4), Olá controladores não entrar em modo de recuperação. Se o utilizador Olá encontra desta falha, recomendamos que aguarde um bit e, em seguida, repita a atualização de Olá. repetição de Olá foi concluída com êxito. Se tentativas Olá falhar, em seguida, deve contactar o Support da Microsoft. |Sim |Sim |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Problemas conhecidos na atualização 4 a partir de versões anteriores

Existem não existem problemas conhecidos novo na atualização 4. Para obter uma lista dos problemas transportadas tooUpdate 4 a partir de versões anteriores, visite demasiado[notas de versão da atualização 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Série-attached SCSI (SAS) controlador e atualizações de firmware na atualização 4

Esta versão tem controlador SAS e atualizações de controladores e firmware LSI. Para mais informações sobre como tooinstall estas atualizações, consulte o artigo [instalar a atualização 4](storsimple-install-update-4.md) no dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-4"></a>Atualizações ao dispositivo virtual na atualização 4

Esta atualização não pode ser aplicado toohello dispositivo StorSimple de nuvem (também conhecido como dispositivo virtual Olá). Novos dispositivos virtuais terá toobe criado. 

## <a name="next-step"></a>Passo seguinte

Saiba como demasiado[instalar a atualização 4](storsimple-install-update-4.md) no dispositivo StorSimple.

