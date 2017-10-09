---
title: "notas de versão 0.4 de atualização de matriz Virtual de aaaStorSimple | Microsoft Docs"
description: "Descreve open crítico problemas e resoluções para execução de matriz Virtual StorSimple Olá 0.4 de atualização."
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
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>Notas de versão 0.4 de atualização de matriz Virtual StorSimple

## <a name="overview"></a>Descrição geral

Olá notas de versão seguintes identificam problemas abertos críticos de Olá e Olá resolver problemas de atualizações de matriz Virtual do Microsoft Azure StorSimple.

notas de versão Olá continuamente são atualizadas e à medida que são descobertos problemas críticos que requerem uma solução, estes são adicionados. Antes de implementar a matriz de Virtual StorSimple, reveja com atenção as informações de Olá contidas nas notas de versão Olá.

Atualização 0.4 corresponde à versão do software toohello **10.0.10289.0**.

> [!NOTE]
> As atualizações são acontece e reinicie o seu dispositivo. Se a e/s estão em curso, o dispositivo de Olá incorreu período de indisponibilidade.


## <a name="whats-new-in-hello-update-04"></a>Novidades no Olá atualização 0.4
Atualização 0.4 é principalmente uma compilação de correção de erro conjugada com alguns melhoramentos. Nesta versão, vários erros, resultando em falhas de cópia de segurança na versão anterior do Olá tem sido resolvidos. melhoramentos de principais de Olá e correções de erros são os seguintes:

- **Melhoramentos de desempenho de cópia de segurança** -nesta versão efetuou vários melhoramentos de chaves tooimprove Olá desempenho. Como resultado, as cópias de segurança de Olá que envolvem um grande número de ficheiros Consulte uma redução significativa da Olá toocomplete de tempo, para cópias de segurança completas e incrementais.

- **Avançada de desempenho de restauro** -esta versão contém melhoramentos significativamente melhorar o desempenho de restauro de Olá ao utilizar o elevado número de ficheiros. Se utilizar 2-4 milhões de ficheiros, é recomendável que Aprovisiona uma matriz de virtual com as melhorias de Olá toosee do 16 GB de RAM. Quando utilizar inferior a 2 milhões de ficheiros, requisitos mínimos de Olá para a máquina virtual de Olá continua toobe 8 GB de RAM.

- **Pacote de tooSupport melhoramentos** -os melhoramentos de Olá incluem a iniciar sessão Olá as estatísticas de disco, da CPU, memória, rede e na nuvem para o pacote de suporte de Olá, deste modo, melhorar o processo de Olá de diagnosticar/depuração problemas de dispositivos.

- **Limite localmente afixado iSCSI volumes too200 GB** -para volumes afixados localmente, recomendamos que limite tooa 200 GB iSCSI volume na sua matriz de Virtual StorSimple. reserva de local de Olá para volumes em camadas continua toobe 10% do Olá aprovisionado o tamanho do volume, mas está limitado a 200 GB. 

- **Correções de erros relacionados com a cópia de segurança** -em versões anteriores do software, ocorreram problemas toobackups relacionados que possam causar falhas de cópia de segurança. Estes erros têm sido resolvidos nesta versão.


## <a name="issues-fixed-in-hello-update-04"></a>Problemas fixos em Olá atualização 0.4

Olá tabela seguinte fornece um resumo dos problemas fixo nesta versão.

| Não. | Funcionalidade | Problema |
| --- | --- | --- |
| 1 |Desempenho de cópia de segurança|No Olá versões anteriores, as cópias de segurança de Olá que envolve um grande número de ficheiros demoraria um toocomplete muito tempo (por ordem de Olá de dias). Nesta versão, Olá completa e incrementais Consulte uma redução significativa da Olá toocompletion de tempo. |
| 2 |Pacote de suporte|Disco, da CPU, memória, rede e estatísticas de nuvem agora são registadas nos registos de suporte de toohello efetuar pacotes de suporte de Olá muito eficaz na resolução de problemas do dispositivo.|
| 3 |Cópia de segurança |Nas versões anteriores, as cópias de segurança de execução longa pode resultar num crunch de espaço no dispositivo Olá, resultando em falhas de cópia de segurança. Este erro é abordado nesta versão, permitindo tooqueue não mais de 5 cópias de segurança de uma só vez.|
| 4 |iSCSI | Nas versões anteriores, reserva local do Olá para volumes em camadas ou localmente afixados foi 10% do tamanho do volume Olá aprovisionado. Nesta versão, reserva local do Olá para todos os volumes do iSCSI (localmente afixado ou em camadas) está % too10 limitada com um máximo de até 200 GB (para os volumes em camadas maiores do que 2 TB) deste modo, libertar mais espaço no disco local Olá. Recomendamos que os volumes de Olá afixado localmente nesta versão estar limitado too200 GB.|


## <a name="known-issues-in-hello-update-04"></a>Problemas conhecidos no Olá atualização 0.4

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
| **15.** |Servidor de ficheiros |As ligações simbólicas não são suportadas. | |
| **16.** |Servidor de ficheiros |Os ficheiros protegidos pelo Windows sistema EFS (Encrypting File) quando copiadas ou armazenado numa Olá resultado de servidor de ficheiros de matriz Virtual StorSimple uma configuração suportada.  | |

## <a name="next-step"></a>Passo seguinte
[Instalar a atualização 0.4](storsimple-virtual-array-install-update-04.md) na sua matriz de Virtual StorSimple.

## <a name="references"></a>Referências
Está à procura de uma nota de versão mais antiga? Vá para: 

* [Notas de versão 0,3 de atualização de matriz Virtual StorSimple](storsimple-ova-update-03-release-notes.md)
* [Notas de versão de atualização de matriz Virtual StorSimple 0.1 e 0,2](storsimple-ova-update-01-release-notes.md)
* [Notas de lançamento de disponibilidade geral de matriz Virtual StorSimple](storsimple-ova-pp-release-notes.md)

