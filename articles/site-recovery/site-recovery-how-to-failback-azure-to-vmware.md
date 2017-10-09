---
title: aaaHow toofail novamente a partir do Azure tooVMware | Microsoft Docs
description: "Após a ativação pós-falha de máquinas virtuais tooAzure, pode iniciar uma reativação pós-falha toobring máquinas virtuais back tooon local. Saiba Olá os passos para como toofail fazer uma cópia."
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
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Falhar novamente a partir do site no local de tooan do Azure

Este artigo descreve como toofail fazer uma cópia de máquinas virtuais do site do Azure Virtual Machines toohello no local. Siga instruções Olá toofail este artigo fazer uma cópia das máquinas virtuais VMware ou servidores físicos Windows/Linux depois que tem a ativação pós-falha de Olá local no site tooAzure utilizando Olá [VMware replicar máquinas virtuais e físicos tooAzure de servidores com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) tutorial.

> [!WARNING]
> Se tiver [concluído migração](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), o recurso de tooanother de máquina virtual movida Olá grupo ou eliminado Olá máquina virtual do Azure, não é possível reativação pós-falha depois disso.

> [!NOTE]
> Se tiver a executar a ativação pós-falha de máquinas virtuais VMware, em seguida, não é possível reativação pós-falha tooa Hyper-v anfitrião.

## <a name="overview-of-failback"></a>Descrição geral da reativação pós-falha
Eis como funciona a reativação pós-falha. Depois de ter pós-falha tooAzure, falhar site no local de back-tooyour em alguns fases:

1. [Proteja](site-recovery-how-to-reprotect.md) Olá máquinas virtuais no Azure, para que possam iniciar tooVMware tooreplicate máquinas virtuais no seu site no local. Como parte deste processo, terá também de:
    1. Configurar um destino principal no local: destino principal do Windows para máquinas virtuais Windows e [destino principal do Linux](site-recovery-how-to-install-linux-master-target.md) para máquinas virtuais do Linux.
    2. Configurar um [servidor de processos](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Iniciar [Proteja](site-recovery-how-to-reprotect.md). Esta ação irá desativar a máquina de virtual Olá no local e sincronizar Olá Azure dados da máquina virtual com Olá no local discos.
5. Depois das máquinas virtuais no Azure são replicar site no local de tooyour, iniciar uma falha através do site do Azure toohello no local.

Depois dos dados falhou novamente, proteja Olá no local as máquinas virtuais que não foi possível voltar a, para que possam iniciar tooreplicate tooAzure.

Para uma descrição geral, veja Olá seguir as vídeo sobre como toofail através do Azure tooan-local no site.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Falhar a localização original ou alternativa de back-toohello

Se tiver falhado através de uma máquina virtual VMware, pode falhar back toohello mesma origem no local máquina virtual se esta ainda existe. Neste cenário, apenas Olá replicar as alterações novamente. Este cenário é conhecido como a recuperação da localização original. Se a máquina de virtual Olá no local não existe, o cenário de Olá é uma recuperação numa localização alternativa.

> [!NOTE]
> Pode apenas a reativação pós-falha toohello original vCenter e o servidor de configuração. Não é possível implementar um novo servidor de configuração e a reativação pós-falha utilizá-la. Além disso, não é possível adicionar um novo vCenter toohello a sair com o servidor de configuração e a reativação pós-falha no vCenter Olá de novo.

#### <a name="original-location-recovery"></a>Recuperação da localização original

Se a reativação pós-falha da máquina virtual original back toohello, Olá seguintes condições é necessária:
* Se a máquina virtual de Olá é gerida por um servidor vCenter, em seguida, Olá anfitrião do ESX de destino principal deve ter arquivo de dados de acesso toohello máquina virtual.
* Se a máquina virtual de Olá está num anfitrião ESX, mas não é gerida pelo vCenter, em seguida, o disco de rígido Olá da máquina virtual de Olá tem de ser um arquivo de dados pode aceder a esse Olá mestre do anfitrião de destino.
* Se a máquina virtual está num anfitrião do ESX e não utilize o vCenter, deve efetuar a deteção do anfitrião do ESX Olá de destino mestre Olá antes que voltar a proteger. Isto aplica-se se está a reativar novamente físicas, demasiado.
* Pode efetuar a tooa back-rede de área de armazenamento virtual (vSAN) ou um disco com base no dispositivo sem formato mapeamento (RDM) se os discos de Olá já existem e estão a máquina de virtual toohello ligado no local.

#### <a name="alternate-location-recovery"></a>Recuperação numa localização alternativa
Se a máquina de virtual Olá no local não existir antes da nova máquina virtual de Olá, cenário Olá chama-se uma recuperação numa localização alternativa. o fluxo de trabalho do Olá reproteção cria a máquina de virtual Olá no local novamente. Isto também fará com que uma transferência de dados completa.

* Quando houver uma localização alternativa de back-tooan, máquina virtual de Olá será recuperada toohello mesmo ESX anfitrião no qual Olá servidor de destino mestre está implementada. Olá arquivo de dados que tenha utilizado o disco de Olá toocreate será Olá mesmo arquivo de dados que foi selecionado quando a nova máquina virtual de Olá.
* Pode efetuar o arquivo de dados de volta apenas tooa máquina virtual ficheiro system (VMFS). Se tiver uma vSAN ou RDM, reproteção e a reativação pós-falha não irão funcionar.
* Reproteção envolve uma transferência de dados inicial grande que é seguida de alterações de Olá. Este processo existe porque a máquina virtual de Olá não existe no local. data de conclusão de Olá tem toobe replicada de volta. Este reproteção também irá demorar mais tempo do que uma recuperação da localização original.
* Não pode falhar novamente toovSAN ou RDM baseada em discos. Apenas novos discos da máquina virtual (VMDKs) podem ser criados num arquivo de dados VMFS.

Um computador físico, quando a ativação pós-falha tooAzure, pode ser não conseguiu fazer uma cópia só como máquina virtual VMware (também referida tooas P2A2V). Este fluxo recai em recuperação numa localização alternativa Olá.

* Um servidor físico do Windows Server 2008 R2 SP1, se protegido e efetuar a ativação pós-falha tooAzure, não é possível efetuar a novamente.
* Certifique-se de que o se detetar, pelo menos, um destino principal servidor e Olá necessário ESX/ESXi anfitriões toowhich terá toofail novamente.

## <a name="have-you-completed-reprotection"></a>Concluiu o só?
Antes de continuar, Olá concluída Proteja novamente os passos para que as máquinas virtuais de Olá estão num estado replicado e podem iniciar um site de no local de back-tooan ativação pós-falha. Para obter mais informações, consulte [como tooreprotect tooon local do Azure](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Pré-requisitos

* É necessário um servidor de configuração no local quando fizer uma reativação pós-falha. Durante a reativação pós-falha, máquina virtual de Olá tem de existir na base de dados de servidor de configuração de Olá ou reativação pós-falha não será concluída com êxito. Assim, certifique-se de que demorar agendadas regularmente cópias de segurança do seu servidor. Se tiver ocorrido um desastre, terá de servidor de Olá toorestore com Olá mesmo endereço IP para toowork de reativação pós-falha.
* servidor de destino mestre Olá não deve ter todos os instantâneos antes de acionar a reativação pós-falha.

## <a name="steps-toofail-back"></a>Passos toofail novamente

> [!IMPORTANT]
> Antes de iniciar a reativação pós-falha, certifique-se de que concluiu voltar Olá máquinas de virtuais. máquinas virtuais Olá deve estar num estado protegido e deve ser o respetivo estado de funcionamento **OK**. máquinas virtuais Olá tooreprotect, leis [como tooreprotect](site-recovery-how-to-reprotect.md).

1. No Olá itens replicados página, selecione a máquina virtual de Olá em faça duplo clique nele tooselect **ativação pós-falha não planeada**.
2. No **confirmar ativação pós-falha**, certifique-se a direção de ativação pós-falha de Olá (a partir do Azure) e, em seguida, selecione Olá ponto de recuperação (mais recente ou Olá mais recente aplicação consistente) que pretende que toouse para Olá de ativação pós-falha. ponto consistente de aplicação Olá é por trás do ponto mais recente Olá no tempo e faz com que alguma perda de dados.
3. Durante a ativação pós-falha, a recuperação de Site encerra Olá máquinas de virtuais no Azure. Depois de verificar que esse reativação pós-falha concluída conforme esperado, pode verificar que foi encerradas Olá máquinas de virtuais no Azure.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>ponto de recuperação toowhat posso falhar back Olá máquinas de virtuais?

Durante a reativação pós-falha, tem duas opções toofail Olá back/recuperação da máquina virtual planear.

Se selecionar ponto Olá mais recentes processado atempadamente, todas as máquinas virtuais serão ativadas pós-falha tootheir mais recente disponível ponto no tempo. No caso de existir um grupo de replicação no plano de recuperação Olá, em seguida, cada máquina virtual do grupo de replicação de Olá serão ativadas pós-falha tooits independentes último ponto no tempo.

Não pode falhar novamente uma máquina virtual até ter, pelo menos, um ponto de recuperação. Não pode falhar novamente um plano de recuperação até que todas as respetivas máquinas virtuais tenha, pelo menos, um ponto de recuperação.

> [!NOTE]
> Um ponto de recuperação mais recente é um ponto de recuperação consistentes com falhas.

Se selecionar o ponto de recuperação consistente de aplicação Olá, uma reativação pós-falha única máquina virtual será recuperada tooits último ponto de recuperação consistentes com aplicações disponíveis. No caso de Olá de um plano de recuperação com um grupo de replicação, cada grupo de replicação irá recuperar tooits comuns ponto de recuperação disponível.
Tenha em atenção que os pontos de recuperação consistentes com aplicações podem ser atrás no tempo e poderá haver perda de dados.

### <a name="what-happens-toovmware-tools-post-failback"></a>O que acontece tooVMware ferramentas após a reativação pós-falha?

Durante tooAzure de ativação pós-falha, as ferramentas do VMware Olá não podem estar a executar no Olá máquina virtual do Azure. Em caso de uma máquina virtual do Windows, a ASR desativa as ferramentas do VMware Olá durante a ativação pós-falha. Em caso de máquina virtual do Linux, a ASR desinstala as ferramentas do VMware Olá durante a ativação pós-falha.

Durante a reativação pós-falha da máquina de virtual do Windows hello, as ferramentas do VMware Olá são novamente ativadas após a reativação pós-falha. Da mesma forma, para uma máquina virtual do linux, as ferramentas do VMware Olá são reinstaladas na máquina de Olá durante a reativação pós-falha.

## <a name="next-steps"></a>Passos seguintes

Após a conclusão da reativação pós-falha, é necessário toocommit tooensure de máquina virtual de Olá recuperar máquinas virtuais no Azure são eliminados.

### <a name="commit"></a>Consolidação
Consolidação é Olá tooremove necessário efetuada a ativação pós-falha da máquina virtual do Azure.
Clique no item de Olá protegido e, em seguida, clique em **consolidar**. Uma tarefa irá remover Olá efetuada a ativação pós-falha de máquinas virtuais no Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Voltar a proteger no local tooAzure

Após a consolidação, a máquina virtual está novamente no site no local de Olá, mas não será possível protegê-lo. toostart tooreplicate tooAzure novamente, Olá seguintes:

1. No **cofre** > **definição** > **replicado itens**, selecione Olá máquinas virtuais que falharam novamente e, em seguida, clique em  **Voltar a proteger**.
2. Atribua o valor de Olá hello do servidor de processos que tem toobe utilizado toosend dados back-tooAzure.
3. Clique em **OK** tarefas de reproteção toobegin Olá.

> [!NOTE]
> Depois de uma máquina de virtual no local é iniciada, demora algum tempo para o agente de Olá servidor de configuração de back-toohello tooregister (cópia de segurança too15 minutos). Durante este período, proteja falha e devolve uma mensagem de erro a indicar que o agente Olá não está instalada. Aguarde alguns minutos e, em seguida, tente reproteção novamente.

Depois de voltar a proteger Olá conclusão da tarefa, máquina virtual de Olá está a replicar tooAzure back- e pode efetuar uma ativação pós-falha.

## <a name="common-issues"></a>Problemas comuns
Certifique-se de que vCenter Olá está num estado ligado antes de efetuar uma reativação pós-falha. Caso contrário, desligar discos e ligá-las back toohello máquina virtual irá falhar.
