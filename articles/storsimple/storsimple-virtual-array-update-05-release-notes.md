---
title: "notas de versão 0.5 de atualização de matriz Virtual de aaaStorSimple | Microsoft Docs"
description: "Descreve open crítico problemas e resoluções para execução de matriz Virtual StorSimple Olá 0,5 de atualização."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>Notas de versão 0.5 de atualização de matriz Virtual StorSimple

## <a name="overview"></a>Descrição geral

Olá notas de versão seguintes identificam problemas abertos críticos de Olá e Olá resolver problemas de atualizações de matriz Virtual do Microsoft Azure StorSimple.

notas de versão Olá continuamente são atualizadas e à medida que são descobertos problemas críticos que requerem uma solução, estes são adicionados. Antes de implementar a matriz de Virtual StorSimple, reveja com atenção as informações de Olá contidas nas notas de versão Olá.

Atualização 0,5 corresponde à versão do software toohello **10.0.10290.0**.

> [!NOTE]
> As atualizações são acontece e reinicie o seu dispositivo. Se a e/s estão em curso, o dispositivo de Olá incorreu período de indisponibilidade. Para obter instruções detalhadas sobre como tooapply Olá atualização, visite demasiado[instalação atualização 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>Novidades no Olá atualização 0,5
Atualização 0,5 é principalmente uma compilação de correção de erro. melhoramentos de principais de Olá e correções de erros são os seguintes:

- **Melhoramentos de resiliência de cópia de segurança** -nesta versão tem de correções que melhoram a resiliência Olá de cópia de segurança. No Olá versões anteriores, as cópias de segurança foram repetidas apenas para determinadas exceções. Esta versão repete todas as exceções de cópia de segurança de Olá e torna Olá cópias de segurança mais resilientes.

- **Atualizações para a monitorização de utilização do armazenamento** -a partir de 30 de Junho de 2017, Olá a monitorização da utilização de armazenamento para a série de dispositivo Virtual StorSimple será descontinuado. Isto aplica-se toohello monitorização gráficos em todos os Olá virtual as matrizes de executar a atualização 0.4 ou inferior. Esta atualização contém alterações Olá necessárias para lhe toocontinue Olá utilização de utilização do armazenamento de monitorização no Olá portal do Azure. Instale esta atualização crítica antes de 30 de Junho de 2017 toocontinue utilizando Olá funcionalidade de monitorização.


## <a name="issues-fixed-in-hello-update-05"></a>Problemas fixos em Olá atualização 0,5

Olá tabela seguinte fornece um resumo dos problemas fixo nesta versão.

| Não. | Funcionalidade | Problema |
| --- | --- | --- |
| 1 |Resiliência de cópia de segurança| No Olá versões anteriores, as cópias de segurança foram repetidas apenas para determinadas exceções. Esta versão contém uma correção toomake cópias de segurança de mais resiliente repetindo todas as exceções de cópia de segurança de Olá.|
| 2 |Monitorização| Olá monitorização de utilização de armazenamento para a série de dispositivo Virtual StorSimple vai ser preterida a partir de 30 de Junho de 2017. Esta ação afeta Olá monitorização gráficos no serviço do Gestor de dispositivos do StorSimple Olá em execução em matrizes Virtual StorSimple (1200 modelo). Esta versão inclui atualizações que permitem Olá utilizador toocontinue Olá utilização de monitorização da utilização de armazenamento em matrizes de virtual Olá para além de 30 de Junho de 2017.|
| 3 |Servidor de ficheiros| No Olá versões anteriores, um utilizador por engano Copiar matriz virtual de toohello ficheiros encriptados. Esta versão contém uma correção que não lhe permita copiar da matriz de toovirtual ficheiros encriptados. Se o dispositivo tiver toohello anteriores existentes do ficheiros encriptados, atualizar, as cópias de segurança irão continuar toofail até que todos os ficheiros de Olá encriptado são eliminados do sistema de Olá. |


## <a name="known-issues-in-hello-update-05"></a>Problemas conhecidos no Olá atualização 0,5

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
| **8.** |Utilizar a capacidade de partilhas |Poderá ver partilhar consumo quando não existe nenhum dados numa partilha de Olá. Este consumo é porque a capacidade de Olá utilizado para partilhas inclui metadados. | |
| **9.** |Recuperação após desastre |Só pode efetuar a recuperação de desastre Olá de um toohello do servidor de ficheiros que o dispositivo de origem Olá mesmo domínio. Dispositivo de destino do desastre recuperação tooa noutro domínio não é suportado nesta versão. |Está implementado numa versão posterior. Para mais informações, visite demasiado[ativação pós-falha e recuperação após desastre para a matriz de Virtual StorSimple](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |dispositivos virtuais do StorSimple Olá não podem ser geridos através de Olá Azure PowerShell nesta versão. |Todos os Olá gestão de dispositivos virtuais Olá deve ser feito Olá Azure portal e Olá local IU da web. |
| **11.** |Alteração de palavra-passe |Olá consola de dispositivos de matriz virtual apenas aceita entrada no en-us formato de teclado. | |
| **12.** |CHAP |Não não possível remover as credenciais CHAP depois de criado. Além disso, se modificar as credenciais CHAP Olá, precisa de tootake volumes de Olá offline e, em seguida, colocá-los online para Olá alteração tootake produza efeitos. |Este problema é resolvido numa versão posterior. |
| **13.** |servidor de iSCSI |Olá 'Armazenamento utilizado' apresentado para um volume de iSCSI pode ser diferente no serviço do Gestor de dispositivos do StorSimple de Olá e anfitrião iSCSI de Olá. |anfitrião de iSCSI Olá tem uma vista de sistema de ficheiros de Olá.<br></br>dispositivo Olá vê os blocos de Olá atribuídos ao volume Olá estava no tamanho máximo de Olá. |
| **14.** |Servidor de ficheiros |Se um ficheiro numa pasta tem uma alternativa dados fluxo (anúncios) associados à mesma, Olá anúncios não é uma cópia de segurança ou restaurado através de recuperação após desastre, clone e recuperação ao nível do Item. | |
| **15.** |Servidor de ficheiros |As ligações simbólicas não são suportadas. | |
| **16.** |Servidor de ficheiros |Os ficheiros protegidos pelo Windows sistema EFS (Encrypting File) quando copiadas ou armazenado numa Olá resultado de servidor de ficheiros de matriz Virtual StorSimple uma configuração suportada.  | |

## <a name="next-step"></a>Passo seguinte
[Instalar a atualização 0,5](storsimple-virtual-array-install-update-05.md) na sua matriz de Virtual StorSimple.

## <a name="references"></a>Referências
Está à procura de uma nota de versão mais antiga? Vá para:

* [Notas de versão 0.4 de atualização de matriz Virtual StorSimple](storsimple-virtual-array-update-04-release-notes.md)
* [Notas de versão 0,3 de atualização de matriz Virtual StorSimple](storsimple-ova-update-03-release-notes.md)
* [Notas de versão de atualização de matriz Virtual StorSimple 0.1 e 0,2](storsimple-ova-update-01-release-notes.md)
* [Notas de lançamento de disponibilidade geral de matriz Virtual StorSimple](storsimple-ova-pp-release-notes.md)

