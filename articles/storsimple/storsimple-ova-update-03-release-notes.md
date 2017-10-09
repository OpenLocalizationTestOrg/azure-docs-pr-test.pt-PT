---
title: "notas de versão de atualizações de matriz Virtual aaaStorSimple | Microsoft Docs"
description: "Descreve open crítico problemas e resoluções para execução de matriz Virtual StorSimple Olá atualização 0.3."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>Notas de versão 0,3 de atualização de matriz Virtual StorSimple
## <a name="overview"></a>Descrição geral
Olá notas de versão seguintes identificam problemas abertos críticos de Olá e Olá resolver problemas de atualizações de matriz Virtual do Microsoft Azure StorSimple.

notas de versão Olá continuamente são atualizadas e à medida que são descobertos problemas críticos que requerem uma solução, estes são adicionados. Antes de implementar a matriz de Virtual StorSimple, reveja com atenção as informações de Olá contidas nas notas de versão Olá.

Atualização 0.3 corresponde à versão do software toohello **10.0.10288.0**.

> [!NOTE]
> As atualizações são acontece e reinicie o seu dispositivo. Se a e/s estão em curso, o dispositivo de Olá incorreu período de indisponibilidade.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Novidades no Olá atualização 0.3
Atualização 0.3 é principalmente uma compilação de correção de erro. Nesta versão, vários erros, resultando em falhas de cópia de segurança na versão anterior do Olá tem sido resolvidos.

## <a name="issues-fixed-in-hello-update-03"></a>Problemas fixos em Olá atualização 0.3
Olá tabela seguinte fornece um resumo dos problemas fixo nesta versão.

| Não. | Funcionalidade | Problema |
| --- | --- | --- |
| 1 |Cópias de segurança |Um problema foi visto na Olá versão anterior, onde as cópias de segurança Olá falharão toocomplete para uma partilha de ficheiros. Se o problema ocorreu, provocaria a falha de tarefa de cópia de segurança de Olá e foi gerado um alerta crítico em Olá StorSimple Manager serviço toonotify Olá utilizador. Este problema não afetam Olá dados em partilhas de Olá ou aceder a dados toohello. causa de raiz de Olá foi identificada e resolvida nesta versão. <br></br> correção de Olá não se aplica retroactively tooshares que já está a ver este problema. Os clientes que estão a ver este problema devem primeiro aplicar atualização 0.3, em seguida, contacte a Microsoft Support tooperform um problema de Olá toofix cópia de segurança completa do sistema. Em vez de contactar a Microsoft Support, os clientes também podem restaurar tooa nova partilha de uma cópia de segurança de bom estado de funcionamento para partilhas de Olá afetado. |
| 2 |iSCSI |Um problema foi visto na Olá versão anterior, onde os volumes de Olá seriam desaparecem quando copiar o volume de tooa de dados no Olá matriz Virtual StorSimple. Este problema foi corrigido nesta versão. <br></br> Correções de Olá entram em vigor apenas no recém-criado volumes. Correções de Olá não aplicam retroactively toovolumes que já está a ver este problema. Os clientes aconselhados toobring Olá afetado volumes online através do portal clássico do Azure Olá, efetuar uma cópia de segurança para estes volumes e, em seguida, restaurar estes volumes toonew de volumes. |

## <a name="known-issues-in-hello-update-03"></a>Problemas conhecidos no Olá atualização 0.3
Olá tabela seguinte fornece um resumo dos problemas conhecidos para Olá matriz Virtual StorSimple e inclui problemas Olá indicado lançamento de versões anteriores do Olá. 

| Não. | Funcionalidade | Problema | Solução/comentários |
| --- | --- | --- | --- |
| **1.** |Atualizações |dispositivos virtuais Olá criados numa versão de pré-visualização Olá não podem ser atualizada tooa suportado versão de disponibilidade geral. |Estes dispositivos virtuais tem a ativação pós-falha para Olá utilizando um fluxo de trabalho do após desastre (DR) de recuperação de lançamento de disponibilidade geral. |
| **2.** |Disco de dados de aprovisionamento |Uma vez aprovisionou um disco de dados de um determinado tamanho especificado e criado Olá correspondente do dispositivo virtual StorSimple, tem não expandir ou reduzir o disco de dados de Olá. Tentativa de resultados de toodo uma perda de todos os dados de Olá nas camadas locais do Olá do dispositivo Olá. | |
| **3.** |Política de grupo |Quando um dispositivo está associado a um domínio, aplicar uma política de grupo que pode afetar negativamente operação de dispositivo Olá. |Certifique-se de que a matriz de virtual está no seu próprio unidade organizacional (UO) do Active Directory e não existem objetos de política de grupo (GPO) são tooit aplicado. |
| **4.** |IU da web do local |Se as funcionalidades de segurança avançada estiverem ativadas no Internet Explorer (IE ESC), algumas páginas de IU da web de locais como resolução de problemas ou a manutenção poderão não funcionar corretamente. Botões nestas páginas também poderão não funcionar. |Desative funcionalidades de segurança avançada do Internet Explorer. |
| **5.** |IU da web do local |Numa máquina virtual de Hyper-V, Olá interfaces de rede na web Olá IU são apresentadas como 10 Gbps interfaces. |Este comportamento é um reflexão do Hyper-V. Hyper-V Mostra sempre a 10 Gbps para adaptadores de rede virtual. |
| **6.** |Volumes em camadas ou partilhas |Intervalo de byte bloqueio para aplicações que funcionam com Olá StorSimple volumes em camadas não é suportado. Se o bloqueio de intervalo de byte estiver ativado, criação de camadas do StorSimple não funciona. |Medidas recomendadas incluem: <br></br>Desative o intervalo de byte bloquear na lógica da sua aplicação.<br></br>Escolha tooput dados para esta aplicação em volumes localmente afixados por oposição ao tootiered volumes.<br></br>*Advertência*: quando utilizar localmente afixado volumes e o bloqueio de intervalo de byte está ativado, volume localmente afixado de Olá pode ficar online, mesmo antes de Olá restauro foi concluído. Nessas instâncias, se for um restauro em curso, em seguida, tem de aguardar Olá toocomplete de restauro. |
| **7.** |Partilhas em camadas |Trabalhar com ficheiros grandes pode resultar em camada lenta. |Ao trabalhar com ficheiros grandes, recomendamos que esse ficheiro maior Olá é inferior a 3 de % do tamanho da partilha de Olá. |
| **8.** |Utilizar a capacidade de partilhas |Poderá ver partilhar consumo quando não existe nenhum dados numa partilha de Olá. Isto acontece porque a capacidade de Olá utilizado para partilhas inclui metadados. | |
| **9.** |Recuperação após desastre |Só pode efetuar a recuperação de desastre Olá de um toohello do servidor de ficheiros que o dispositivo de origem Olá mesmo domínio. Dispositivo de destino do desastre recuperação tooa noutro domínio não é suportado nesta versão. |Está implementado numa versão posterior. |
| **10.** |Azure PowerShell |dispositivos virtuais do StorSimple Olá não podem ser geridos através de Olá Azure PowerShell nesta versão. |Todos os Olá gestão de dispositivos virtuais Olá deve ser feito Olá portal clássico do Azure e IU da web local Olá. |
| **11.** |Alteração de palavra-passe |consola de dispositivo Olá matriz virtual apenas aceita entrada no formato de teclado en-US. | |
| **12.** |CHAP |Não não possível remover as credenciais CHAP depois de criado. Além disso, se modificar as credenciais CHAP Olá, precisa de tootake volumes de Olá offline e, em seguida, colocá-los online para Olá alteração tootake produza efeitos. |Este problema é resolvido numa versão posterior. |
| **13.** |servidor de iSCSI |Olá 'Armazenamento utilizado' apresentado para um volume de iSCSI pode ser diferente no serviço do StorSimple Manager Olá e o anfitrião de iSCSI Olá. |anfitrião de iSCSI Olá tem uma vista de sistema de ficheiros de Olá.<br></br>dispositivo Olá vê os blocos de Olá atribuídos ao volume Olá estava no tamanho máximo de Olá. |
| **14.** |Servidor de ficheiros |Se um ficheiro numa pasta tem uma alternativa dados fluxo (anúncios) associados à mesma, Olá anúncios não é uma cópia de segurança ou restaurado através de recuperação após desastre, clone e recuperação ao nível do Item. | |

## <a name="next-step"></a>Passo seguinte
[Instalar a atualização 0.3](storsimple-ova-install-update-01.md) na sua matriz de Virtual StorSimple.

## <a name="references"></a>Referências
Está à procura de uma nota de versão mais antiga? Vá para: 

* [Notas de versão de atualização de matriz Virtual StorSimple 0.1 e 0,2](storsimple-ova-update-01-release-notes.md)
* [Notas de lançamento de disponibilidade geral de matriz Virtual StorSimple](storsimple-ova-pp-release-notes.md)

