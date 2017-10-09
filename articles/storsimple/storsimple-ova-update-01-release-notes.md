---
title: "notas de versão de atualizações de matriz Virtual aaaStorSimple | Microsoft Docs"
description: "Descreve resoluções para Olá matriz Virtual StorSimple e os problemas críticos de aberta atualização 0,2 e 0.1 a executar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Notas de versão de atualização de matriz Virtual 0,2 e 0.1 do StorSimple
## <a name="overview"></a>Descrição geral
Olá notas de versão seguintes identificam problemas abertos críticos de Olá e Olá resolver problemas de atualizações de matriz Virtual do Microsoft Azure StorSimple. (Matriz Virtual do Microsoft Azure StorSimple também é conhecido como Olá no local do dispositivo virtual StorSimple ou do dispositivo virtual StorSimple Olá.) 

notas de versão Olá continuamente são atualizadas e à medida que são descobertos problemas críticos que requerem uma solução, estes são adicionados. Antes de implementar o dispositivo virtual StorSimple, reveja com atenção as informações de Olá contidas nas notas de versão Olá.

Atualização 0,2 corresponde à versão do software toohello **10.0.10280.0**; Atualização 0.1 é versão **10.0.10279.0**. secções Olá abaixo listam as alterações de Olá para cada atualização. 

> [!NOTE]
> As atualizações são acontece e irão reiniciar o seu dispositivo. Se a e/s estão em curso, o dispositivo Olá será cobrado período de indisponibilidade.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problemas fixos em Olá atualização 0,2
Atualização 0,2 inclui todas as alterações da atualização 0.1 na adição toohello correção descrita no Olá a tabela seguinte:

| Funcionalidade | Problema |
| --- | --- |
| Atualizações |Na última versão Olá, as atualizações não foram detetadas automaticamente no Olá portal clássico do Azure, para que tinha toouse Olá locais atualizações de tooinstall IU da Web. Este problema ser corrigido nesta versão. Depois de instalar a atualização 0,2, pode instalar as atualizações futuras utilizando Olá portal clássico do Azure. |

## <a name="whats-new-in-hello-update-01"></a>Novidades no Olá atualização 0.1
Atualização 0.1 contém seguinte Olá correções de erros e melhoramentos. 

* **Resiliência melhorada para falhas de nuvem**: esta versão tem várias correções de erros em torno da recuperação após desastre, cópia de segurança, restaurar e criação de camadas no evento Olá de uma interrupção de conectividade de nuvem. 
* **Restauro desempenho melhorado**: esta versão foi correções de erros que significativamente ter diminuir o tempo de conclusão de Olá de tarefas de restauro Olá.
* **Automatizada otimização de recuperação de espaço**: quando os dados são eliminados em volumes de aprovisionamento dinâmico, hello blocos de armazenamento não utilizados necessário toobe recuperada. Nesta versão tem Olá melhorada espaço recuperação processo a partir da nuvem Olá, resultando em Olá não utilizada se tornar disponível mais rapidamente como em comparação com toohello versões anteriores do espaço.
* **Novas imagens de disco virtual**: VMDK, novo VHD e VHDX estão agora disponíveis através de Olá portal clássico do Azure. Pode transferir estas imagens tooprovision novos atualização 0.1 dispositivos.
* **Melhorar a precisão Olá do Estado de tarefas no portal de Olá**: na Olá versão anterior do software, o estado da tarefa de criação de relatórios no portal de Olá não foi granular. Este problema é resolvido nesta versão.
* **Experiência de associação de domínio**: correções de erros relacionados com a associar a toodomain e mudar o nome de dispositivo Olá.

## <a name="issues-fixed-in-hello-update-01"></a>Problemas fixos em Olá atualização 0.1
Olá tabela seguinte fornece um resumo dos problemas fixo nesta versão.

| Não. | Funcionalidade | Problema |
| --- | --- | --- |
| 1 |VMDK |Em algumas versões do VMware, o disco do SO Olá foi visto como dispersa fazendo com que alertas e perturbar as operações normais. Isto foi corrigido nesta versão. |
| 2 |servidor de iSCSI |Na última versão Olá, o utilizador Olá foi toospecify necessário um gateway para cada interface de rede ativada do dispositivo virtual StorSimple. Este comportamento é alterado nesta versão, para que hello utilizador tenha tooconfigure pelo menos um gateway para todas as interfaces de rede de Olá ativada. |
| 3 |Pacote de suporte |Na versão anterior do software de Olá, suporta a coleção de pacotes falhou ao tamanhos de pacote de Olá foram superiores a 1 GB. Este problema ser corrigido nesta versão. |
| 4 |Acesso à nuvem |Versão de último Olá, se Olá matriz Virtual StorSimple não tinha a conectividade de rede e foi reiniciado, hello IU local teria problemas de conectividade. Este problema esteja corrigido nesta versão. |
| 5 |Gráficos de monitorização |Na versão anterior de Olá, após uma ativação pós-falha do dispositivo, gráficos de utilização de capacidade de nuvem Olá apresentada valores incorretos no Olá portal clássico do Azure. Isto é corrigido na versão atual do Olá. |

## <a name="known-issues-in-hello-update-01"></a>Problemas conhecidos no Olá atualização 0.1
Olá tabela seguinte fornece um resumo dos problemas conhecidos para Olá matriz Virtual StorSimple e inclui problemas Olá indicado lançamento de versões anteriores do Olá. **Olá versão problemas indicação em contrário nesta versão estão marcados com um asterisco. Praticamente todos os problemas de Olá nesta lista tem transportados através de versão Olá GA da matriz Virtual StorSimple.**

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
| **14.** |Servidor de ficheiros * |Se um ficheiro numa pasta tem uma alternativa dados fluxo (anúncios) associados à mesma, Olá anúncios não é uma cópia de segurança ou restaurado através de recuperação após desastre, clone e recuperação ao nível do Item. | |

## <a name="next-step"></a>Passo seguinte
[Instalar atualizações](storsimple-ova-install-update-01.md) na sua matriz de Virtual StorSimple.

