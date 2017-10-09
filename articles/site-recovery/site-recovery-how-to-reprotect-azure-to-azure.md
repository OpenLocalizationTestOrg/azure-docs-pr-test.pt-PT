---
title: "aaaHow tooReprotect de efetuar a ativação pós-falha de máquinas virtuais do Azure back tooprimary região do Azure | Microsoft Docs"
description: "Após a ativação pós-falha de VMs de uma região do Azure tooanother, pode utilizar máquinas do Azure Site Recovery tooprotect Olá na direção inversa. Saiba como passos Olá toodo uma reproteção antes de uma ativação pós-falha novamente."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Reproteção da ativação pós-falha região de back-tooprimary região do Azure



>[!NOTE]
>
> Replicação de recuperação de site para máquinas virtuais do Azure está atualmente em pré-visualização.


## <a name="overview"></a>Descrição geral
Quando lhe [ativação pós-falha](site-recovery-failover.md) Olá máquinas virtuais de uma região do Azure tooanother, máquinas virtuais Olá estão num Estado não protegido. Se quiser toobring-los fazer uma cópia de região primária toohello, terá de toofirst proteger máquinas virtuais Olá e, em seguida, a ativação pós-falha novamente. Há qualquer diferença entre como a ativação pós-falha numa direção ou outros. De igual modo, após ativar a proteção de máquinas virtuais de Olá, há qualquer diferença entre Olá reproteção post ativação pós-falha, ou a reativação pós-falha da post.
tooexplain Olá os fluxos de trabalho de reproteção e tooavoid confusões, utilizaremos Olá sites principal de máquinas de Olá protegido como região Ásia Oriental e Olá recuperação de máquinas de Olá como Sudeste asiático região. Durante a ativação pós-falha, terá de região de Sudeste asiático de toohello de máquinas virtuais de Olá de ativação pós-falha. Antes de a reativação pós-falha, terá de tooreprotect Olá máquinas virtuais do Sudeste asiático back tooEast Ásia. Este artigo descreve os passos de Olá sobre tooreprotect.

> [!WARNING]
> Se tiver [concluído migração](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), o recurso de tooanother de máquina virtual movida Olá grupo ou eliminado Olá máquina virtual do Azure, não é possível reativação pós-falha depois disso.

Após a conclusão de reproteção e estiver a replicar máquinas virtuais Olá protegido, pode iniciar uma ativação pós-falha no Olá toobring de máquinas virtuais-los fazer uma cópia de região do tooEast Ásia.

Publique comentários ou perguntas na end Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Pré-requisitos
1. máquinas virtuais Olá deve ter sido consolidadas.
2. site de destino Olá - neste caso Olá Oriental Azure região deve estar disponível e deve ser capaz de tooaccess/criar novos recursos nessa região.

## <a name="steps-tooreprotect"></a>Passos tooreprotect

Seguintes são Olá passos tooreprotect uma máquina virtual utilizando as predefinições de Olá.

1. No **cofre** > **replicado itens**, faça duplo clique Olá virtual máquina que é foi efetuada a ativação pós-falha e, em seguida, selecione **voltar a proteger**. Também pode clicar em Olá máquina e selecione **voltar a proteger** de botões de comando Olá.

![Clique com o botão direito do rato em tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. No painel de Olá, tenha em atenção que direção Olá de proteção, **Sudeste asiático tooEast Ásia**, já está selecionada.

![Proteja o painel](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Olá revisão **conjuntos de disponibilidade do armazenamento e de grupos, rede, de recurso** informações e clique em OK. Se existirem quaisquer recursos marcados (novo), serão criados como parte da Olá voltar a proteger.

Isto irá acionar uma tarefa Proteja novamente a tarefa que será o seeding primeiro site de destino Olá (SEA neste caso) com dados mais recentes Olá, e assim que estiver concluída, serão replicadas deltas de Olá antes da ativação pós-falha faça uma cópia tooSoutheast Ásia.

### <a name="reprotect-customization"></a>Proteja personalização
Se quiser toochoose hello extrair conta ou Olá rede de armazenamento durante a voltar a proteger, pode fazê-lo para utilizar Olá personalizar opção fornecida no painel de reproteção Olá.

![Personalizar a opção](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

Pode personalizar Olá seguintes propriedades da máquina de virtual de destino putador durante reproteção.

![Personalizar o painel](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Propriedade |Notas  |
|---------|---------|
|Grupo de recursos de destino     | Pode escolher em que irá criar a máquina de virtual ésimo dos grupo de recursos de destino para Olá toochange. Como parte de Olá de reproteção, será eliminada Olá máquina virtual de destino, por conseguinte, pode escolher um novo grupo de recursos na qual pode criar Olá VM post ativação pós-falha         |
|Rede Virtual de destino     | Rede não pode ser alterada durante Olá reproteção. Olá toochange de rede, Refazer mapeamento da rede Olá.         |
|Armazenamento de destino     | Pode alterar a conta de armazenamento de Olá toowhich Olá máquina será ativação pós-falha de post criada.         |
|Armazenamento de cache     | Pode especificar uma conta de armazenamento de cache que será utilizada durante a replicação. Se com as predefinições de Olá, uma nova conta de armazenamento de cache será criada, se já existir.         |
|Conjunto de Disponibilidade     |Se a máquina virtual de Olá na Ásia Oriental faz parte de um conjunto de disponibilidade, pode escolher um conjunto de disponibilidade para a máquina virtual de destino Olá no Sudeste asiático. As predefinições irão encontrar o conjunto de disponibilidade SEA Olá existente e tente toouse-lo. Durante a personalização, pode especificar um conjunto de AV totalmente novo.         |


### <a name="what-happens-during-reprotect"></a>O que acontece durante reproteção?

Tal como após Olá primeiro ativar a proteção, seguem-se artefacts Olá obterem criado se utilizar as predefinições de Olá.
1. É criada uma conta de armazenamento de cache na região do Olá Ásia Oriental.
2. Se a conta de armazenamento de destino Olá (Olá original conta de armazenamento de Olá VM Sudeste asiático) não existe, é criado um novo. o nome de Olá é a conta de armazenamento da máquina de Olá, Ásia Oriental virtual com "asr" o sufixo.
3. Se o conjunto de destino AV de Olá não existe e predefinições Olá detetar que necessita de toocreate definir um novo AV, em seguida, será criado como parte da Olá Proteja tarefa. Se tiver personalizado Olá voltar a proteger, em seguida, conjunto de AV Olá selecionado será utilizado.
4.

Olá seguem-se a lista de Olá dos passos que se acontecer se acionar uma tarefa de reproteção. Trata-se no lado do destino de Olá maiúsculas Olá máquina virtual existe.

1. Olá necessário artefacts são criados como parte de reproteção. Se já existirem, em seguida, são reutilizados.
2. Olá destino lado (Sudeste asiático) máquina virtual é primeiro desativada, se estiver em execução.
3. Olá destino do lado do disco da máquina virtual é copiado pelo Azure Site Recovery num contentor como um blob de seed.
4. máquina de virtual do lado de destino Olá, em seguida, é eliminada.
5. blob de seed Olá é utilizado pelo tooreplicate de máquina virtual para Olá atual origem lado (Oriental). Isto garante que apenas deltas são replicadas.
6. alterações de principais de Olá entre o disco de origem Olá e BLOBs de seed Olá são sincronizadas. Esta operação pode demorar algum tempo toocomplete.
7. Assim que voltar a proteger Olá tarefa é concluída, começa a replicação de diferenças Olá que cria um ponto de recuperação de acordo com a política de Olá.

> [!NOTE]
> Não é possível proteger um nível de plano de recuperação. Apenas pode voltar a proteger a um nível VM por.

Depois de voltar a proteger Olá concluída com êxito, Olá máquina de virtual entrará num estado protegido.

## <a name="next-steps"></a>Passos seguintes

Depois de máquina virtual de Olá entrou num estado protegido, pode iniciar uma ativação pós-falha. ativação pós-falha de Olá irá encerrar a máquina virtual de Olá na região do Azure Ásia Oriental e, em seguida, criar e efetuar o arranque de máquina virtual do Olá Sudeste asiático região. Por conseguinte, não há um período de indisponibilidade breves para aplicação Olá. Por isso, escolha tempo Olá para ativação pós-falha quando a aplicação pode tolerar um tempo de inatividade. Recomenda-se que teste primeiro toomake de máquina virtual de Olá de ativação pós-falha se de que o se futuras cópias de segurança corretamente, antes de iniciar uma ativação pós-falha.

-   [Passos tooinitiate testar a ativação pós-falha da máquina virtual de Olá](site-recovery-test-failover-to-azure.md)

-   [Passos tooinitiate ativação pós-falha da máquina virtual de Olá](site-recovery-failover.md)
