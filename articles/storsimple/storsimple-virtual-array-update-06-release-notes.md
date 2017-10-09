---
title: "notas de versão 0,6 de atualização de matriz Virtual de aaaStorSimple | Microsoft Docs"
description: "Descreve open crítico problemas e resoluções para execução de matriz Virtual StorSimple Olá 0,6 de atualização."
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
ms.date: 05/24/2017
ms.author: alkohli
ms.openlocfilehash: 7b573457dc07ce41e95d49d66ccc174045f31a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-06-release-notes"></a>Notas de versão 0,6 de atualização de matriz Virtual StorSimple

## <a name="overview"></a>Descrição geral

Olá notas de versão seguintes identificam problemas abertos críticos de Olá e Olá resolver problemas de atualizações de matriz Virtual do Microsoft Azure StorSimple.

notas de versão Olá continuamente são atualizadas e à medida que são descobertos problemas críticos que requerem uma solução, estes são adicionados. Antes de implementar a matriz de Virtual StorSimple, reveja com atenção as informações de Olá contidas nas notas de versão Olá.

Atualização 0,6 corresponde à versão do software toohello **10.0.10293.0**.

> [!IMPORTANT]
> - As atualizações são acontece e reinicie o seu dispositivo. Se a e/s estão em curso, o dispositivo de Olá incorreu período de indisponibilidade. Para obter instruções detalhadas sobre como tooapply Olá atualização, visite demasiado[instalação atualização 0,6](storsimple-virtual-array-install-update-06.md).
>
> - Recomendamos vivamente que instale a atualização 0,6 imediatamente porque esta contém correções de segurança críticas.


## <a name="whats-new-in-hello-update-06"></a>Novidades no Olá atualização 0,6
Atualização 0,6 é uma atualização crítica e deve ser implementada imediatamente. Esta atualização contém Olá seguintes correções: 

- **Correções de segurança do Windows** -com esta versão **correções de segurança críticas do Windows**. Reveja Olá seguintes atualizações de segurança para obter mais informações sobre problemas de segurança de Olá e Olá correções associadas:
    - [Dezembro de 2016 qualidade apenas de segurança de atualização para Windows 8.1 e Windows Server 2012 R2](https://support.microsoft.com/help/3205400/december-2016-security-only-quality-update-for-windows-8.1-and-windows-server-2012-r2)
    - [Março de 2017 qualidade apenas de segurança de atualização para Windows 8.1 e Windows Server 2012 R2](https://support.microsoft.com/help/4012213/march-2017-security-only-quality-update-for-windows-8-1-and-windows-server-2012-r23)
    - [9 de Maio de 2017 — KB4019213 (atualização só de segurança)](https://support.microsoft.com/help/4019213/windows-8-update-kb4019213)

- **Restaurar a correção** -nas versões anteriores, Ocorreu um erro que possam impedir o restauro de Olá conclusão. Corrigir este erro nesta versão.


## <a name="issues-fixed-in-hello-update-06"></a>Problemas fixos em Olá atualização 0,6

Olá tabela seguinte fornece um resumo dos problemas fixo nesta versão.

| Não. | Funcionalidade | Problema |
| --- | --- | --- |
| 1 |Segurança| Esta versão contém atualizações de segurança do Windows críticas. Sugerimos que instalar esta atualização imediatamente.|
| 2 |Restauro| Durante um restauro, Ocorreu uma condição provável de antecipação que seria impeçam a conclusão da tarefa de restauro Olá. correção de erros de Olá corrige esta condição provável de antecipação.|


## <a name="known-issues-in-hello-update-06"></a>Problemas conhecidos no Olá atualização 0,6

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
| **17.** |Atualizações |Se vir o erro código: 2359302 (hex 0x240006) quando tenta tooinstall uma correção através de Olá IU local, em seguida, isto implica que correção Olá já está instalada no seu dispositivo.   | |

## <a name="next-step"></a>Passo seguinte
[Instalar a atualização 0,6](storsimple-virtual-array-install-update-06.md) na sua matriz de Virtual StorSimple.

## <a name="references"></a>Referências
Está à procura de uma nota de versão mais antiga? Vá para:

* [Notas de versão 0.5 de atualização de matriz Virtual StorSimple](storsimple-virtual-array-update-05-release-notes.md)
* [Notas de versão 0.4 de atualização de matriz Virtual StorSimple](storsimple-virtual-array-update-04-release-notes.md)
* [Notas de versão 0,3 de atualização de matriz Virtual StorSimple](storsimple-ova-update-03-release-notes.md)
* [Notas de versão de atualização de matriz Virtual StorSimple 0.1 e 0,2](storsimple-ova-update-01-release-notes.md)
* [Notas de lançamento de disponibilidade geral de matriz Virtual StorSimple](storsimple-ova-pp-release-notes.md)

