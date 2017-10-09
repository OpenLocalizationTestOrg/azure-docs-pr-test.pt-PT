---
title: "cópia de segurança do HANA Azure aaaSAP com base nos instantâneos de armazenamento | Microsoft Docs"
description: "Existem duas principais cópia de segurança as possibilidades de SAP HANA em máquinas virtuais do Azure, este artigo abrange a cópia de segurança de SAP HANA com base nos instantâneos de armazenamento"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Cópia de segurança SAP HANA baseada em instantâneos de armazenamento

## <a name="introduction"></a>Introdução

Isto faz parte de uma série de três partes de artigos relacionados numa cópia de segurança de SAP HANA. [Cópia de segurança manual para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md) fornece uma descrição geral e informações de introdução, e [SAP HANA Backup do Azure no nível de ficheiro](sap-hana-backup-file-level.md) abrange Olá opção de cópia de segurança baseada em ficheiros.

Quando utilizar uma funcionalidade de cópia de segurança de VM para um sistema de instância única tudo-em-um demonstração, um deve considerar a fazer uma cópia de segurança VM em vez de gerir cópias de segurança de HANA Olá ao nível do SO. Uma alternativa é tootake BLOBs do Azure instantâneos toocreate cópias individuais discos virtuais, que são a máquina virtual de tooa anexado e mantém os ficheiros de dados do Olá HANA. Mas um ponto de crítico consistência de aplicações quando criar um instantâneo de cópia de segurança ou de disco da VM, enquanto o sistema de Olá está ativo e em execução. Consulte _consistência de dados SAP HANA quando tirar instantâneos de armazenamento_ no artigo relacionado Olá [guia de cópia de segurança para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md). SAP HANA tem uma funcionalidade que suporta estes tipos de instantâneos de armazenamento.

## <a name="sap-hana-snapshots"></a>Instantâneos de SAP HANA

Não há uma funcionalidade de SAP HANA que suporte um instantâneo de armazenamento. No entanto, a partir de Dezembro de 2016, há uma restrição sistemas toosingle do contentor. Configurações de contentor multi-inquilino não suportam este tipo de instantâneo de base de dados (consulte [criar um instantâneo de armazenamento (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).

Funciona da seguinte forma:

- Preparar para um instantâneo de armazenamento ao iniciar o instantâneo de SAP HANA Olá
- Executar o instantâneo de armazenamento de Olá (por exemplo, o instantâneo de Blobs do Azure)
- Confirme o instantâneo de SAP HANA Olá

![Nesta captura de ecrã mostra que um instantâneo de dados SAP HANA pode ser criado através de uma instrução SQL](media/sap-hana-backup-storage-snapshots/image011.png)

Nesta captura de ecrã mostra que um instantâneo de dados SAP HANA pode ser criado através de uma instrução SQL.

![Olá instantâneo, em seguida, também aparece no catálogo de cópias de segurança de Olá no SAP HANA Studio](media/sap-hana-backup-storage-snapshots/image012.png)

Olá instantâneo, em seguida, também aparece no catálogo de cópias de segurança de Olá no Studio do SAP HANA.

![No disco, o instantâneo de Olá aparece no diretório de dados SAP HANA Olá](media/sap-hana-backup-storage-snapshots/image013.png)

No disco, o instantâneo de Olá aparece no diretório de dados SAP HANA Olá.

Um tem tooensure consistência do sistema de ficheiros Olá também é garantida antes de executar o instantâneo de armazenamento Olá enquanto SAP HANA está em modo de preparação de instantâneo Olá. Consulte _consistência de dados SAP HANA quando tirar instantâneos de armazenamento_ no artigo relacionado Olá [guia de cópia de segurança para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md).

Depois de concluído o instantâneo de armazenamento Olá, é instantâneo de SAP HANA de Olá tooconfirm críticos. Há um toorun de instrução de SQL correspondente: INSTANTÂNEO de fecho de dados de cópia de segurança (consulte [dados FECHAR INSTANTÂNEO instrução BACKUP (cópia de segurança e recuperação)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Confirme o instantâneo do Olá HANA. Devida demasiado&quot;cópia ao escrever,&quot; SAP HANA poderá necessitar de espaço em disco adicional no instantâneo-preparar modo, e não é possível toostart novas cópias de segurança até que o instantâneo de SAP HANA Olá é confirmado.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Cópia de segurança de HANA VM através do serviço de cópia de segurança do Azure

A partir de Dezembro de 2016, o agente de cópia de segurança de Olá de Olá serviço cópia de segurança do Azure não está disponível para VMs com Linux. Utilize toomake da cópia de segurança do Azure no nível de ficheiro ou directório Olá, um de copiar ficheiros de cópia de segurança de SAP HANA tooa VM do Windows e, em seguida, utilizar o agente de cópia de segurança de Olá. Caso contrário, apenas uma VM com Linux cópia de segurança completa é possível através do serviço de cópia de segurança do Azure Olá. Consulte [descrição geral do Olá funcionalidades na cópia de segurança do Azure](../../../backup/backup-introduction-to-azure-backup.md) toofind mais informações.

Olá serviço de cópia de segurança do Azure oferece uma opção tooback cópias de segurança e restaurar uma VM. Podem encontrar mais informações sobre este serviço e como funciona no artigo Olá [planear a infraestrutura de cópia de segurança de VM no Azure](../../../backup/backup-azure-vms-introduction.md).

Existem duas considerações importantes sobre o artigo toothat de acordo com:

_&quot;Para máquinas virtuais do Linux, apenas as cópias de segurança consistente com ficheiros são possíveis, uma vez que o Linux não tem um tooVSS plataforma equivalente.&quot;_

_&quot;As aplicações precisam de tooimplement os seus próprios &quot;corrigir-se&quot; mecanismo no Olá restaurado.&quot;_

Por conseguinte, um tem toomake se que SAP HANA está num estado consistente no disco quando inicia a cópia de segurança de Olá. Consulte _instantâneos de SAP HANA_ descrito anteriormente Olá documento. Mas não existe um potencial problema quando SAP HANA permanece neste modo de preparação do instantâneo. Consulte [criar um instantâneo de armazenamento (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) para obter mais informações.

Esse artigo Estados:

_&quot;Este é vivamente recomendado tooconfirm ou abandone um instantâneo de armazenamento logo que possível após ter sido criado. Enquanto instantâneos de armazenamento Olá está a ser preparado ou criados, Olá dados relevantes do instantâneo está fixa. Enquanto os dados de instantâneos relevantes Olá permanecem congelados, podem ainda efetuadas alterações na base de dados de Olá. Essas alterações não irão causar Olá congelado toobe dados relevantes para o instantâneo foi alterado. Em vez disso, as alterações de Olá são escritas toopositions na área de dados de Olá que são separados dos instantâneos de armazenamento Olá. As alterações também são escritas toohello registo. No entanto, as mais dados relevantes para o instantâneo de Olá de Olá são mantidos congelados, hello mais Olá pode crescer, volume de dados.&quot;_

Cópia de segurança do Azure encarrega-se de consistência do sistema de ficheiros Olá através de extensões de VM do Azure. Estas extensões não estão disponível autónoma e funcionarão apenas em combinação com o serviço de cópia de segurança do Azure. Contudo, ainda é um requisito toomanage uma consistência de aplicações de tooguarantee de instantâneo de SAP HANA.

Cópia de segurança do Azure tem duas fases principais:

- Criar instantâneo
- Transferência de dados toovault

Por isso, um foi confirmar o instantâneo de SAP HANA Olá depois de concluída a fase de serviço de cópia de segurança do Azure Olá de um instantâneo. Poderá demorar vários minutos toosee no Olá portal do Azure.

![Esta ilustração mostra a parte da lista de tarefas de cópia de segurança de Olá de um serviço de cópia de segurança do Azure](media/sap-hana-backup-storage-snapshots/image014.png)

Esta ilustração mostra a parte da lista de tarefas de cópia de segurança de Olá de um serviço de cópia de segurança do Azure, que foi utilizado tooback segurança de VM de teste do Olá HANA.

![Detalhes da tarefa tooshow Olá, clique em tarefa de cópia de segurança de Olá na Olá portal do Azure](media/sap-hana-backup-storage-snapshots/image015.png)

Detalhes da tarefa tooshow Olá, clique em tarefa de cópia de segurança de Olá na Olá portal do Azure. Aqui, um pode ver Olá duas fases. Poderá demorar alguns minutos até que mostra a fase de instantâneo Olá como concluído. A maioria do tempo de Olá é despendido na fase de transferência de dados de Olá.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Automatização de cópia de segurança de HANA VM através do serviço de cópia de segurança do Azure

Um foi de confirmar manualmente instantâneo de SAP HANA Olá assim que a fase de instantâneo de cópia de segurança do Azure Olá estiver concluída, conforme descrito anteriormente, mas é útil tooconsider automatização porque um administrador não pode monitorizar a lista de tarefa de cópia de segurança de Olá no Olá portal do Azure.

Eis uma explicação de como pode ser conseguido através de cmdlets do Azure PowerShell.

![Um serviço de cópia de segurança do Azure foi criado com o nome de Olá hana-cópia de segurança-Cofre](media/sap-hana-backup-storage-snapshots/image016.png)

Um serviço de cópia de segurança do Azure foi criado com o nome de Olá &quot;hana-cópia de segurança-cofre.&quot; Olá comando PS **Get AzureRmRecoveryServicesVault-nome do Cofre de cópia de segurança hana** obtém Olá objeto correspondente. Este objeto é utilizado tooset Olá contexto de cópia de segurança, como mostrado na figura seguinte Olá.

![Um pode procurar a tarefa de cópia de segurança de Olá atualmente em curso](media/sap-hana-backup-storage-snapshots/image017.png)

Após a definição Olá correto contexto de um pode procurar a tarefa de cópia de segurança de Olá atualmente em curso e, em seguida, procure os detalhes da tarefa. lista de subtarefa Olá mostra se a fase de instantâneo de Olá de Olá tarefa de cópia de segurança do Azure já está concluída:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Valor de Olá de consulta em ciclo até que transforma tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Depois dos detalhes da tarefa Olá são armazenados numa variável, é simplesmente PS sintaxe tooget toohello primeiro entrada de matriz e obter o valor de estado de Olá. script de automatização do toocomplete Olá, consulta Olá valor num ciclo até ter fica demasiado&quot;concluído.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Restaurar a chave de licença HANA e VM através do serviço de cópia de segurança do Azure

Olá serviço de cópia de segurança do Azure é toocreate concebida uma nova VM durante o restauro. Não há nenhum plano direito agora toodo um &quot;direta&quot; restauro de uma VM do Azure existente.

![Esta ilustração mostra opção para restaurar Olá Olá serviço do Azure no Olá portal do Azure](media/sap-hana-backup-storage-snapshots/image019.png)

Esta ilustração mostra opção para restaurar Olá Olá serviço do Azure no Olá portal do Azure. Um pode escolher entre a criação de uma VM durante o restauro ou o restauro de discos de Olá. Depois de restaurar os discos de Olá, é ainda necessário toocreate uma nova VM em cima-lo. Sempre que uma nova VM é criada sobre as alterações de ID de VM exclusivas Olá do Azure (consulte [Accessing e utilizar ID exclusivo de VM do Azure](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Esta ilustração mostra ID exclusivo da VM do Azure Olá antes e depois do restauro Olá através do serviço de cópia de segurança do Azure](media/sap-hana-backup-storage-snapshots/image020.png)

Esta ilustração mostra ID exclusivo da VM do Azure Olá antes e depois do restauro Olá através do serviço de cópia de segurança do Azure. Olá SAP hardware chave, o que é utilizado para SAP licenciamento, está a utilizar este ID de VM exclusivo. Como consequence, uma nova licença SAP tem toobe instalado após um restauro de VM.

Uma nova funcionalidade de cópia de segurança do Azure foi apresentada no modo de pré-visualização durante a criação de Olá deste guia de cópia de segurança. Permite que um restauro de nível de ficheiro com base no instantâneo VM Olá que foi feito para Olá VM cópia de segurança. Isto evita Olá necessidade toodeploy uma nova VM e, por conseguinte, permanece VM ID exclusivo do Olá Olá mesmo e não é necessária nenhuma nova chave de licença de SAP HANA. Obter mais documentação sobre esta funcionalidade será fornecida depois foi totalmente testada.

Cópia de segurança do Azure, eventualmente, irá permitir cópia de segurança de individuais discos virtuais do Azure, mais ficheiros e diretórios a partir de dentro de Olá VM. Das principais vantagens da cópia de segurança do Azure é a gestão de todos os Olá cópias de segurança, guardar cliente Olá de ter toodo-lo. Se for necessário um restauro, cópia de segurança do Azure irá selecionar Olá toouse de cópia de segurança correto.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>Cópia de segurança de SAP HANA VM através de instantâneos de disco manual

Em vez de utilizar o serviço de cópia de segurança do Azure Olá, um conseguiu configurar uma solução de cópia de segurança individuais através da criação de instantâneos do blob do Azure VHDs manualmente através do PowerShell. Consulte [utilizar instantâneos de blob com o PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) para obter uma descrição dos passos de Olá.

Fornece uma maior flexibilidade mas não a resolver problemas de Olá explicados anteriormente neste documento:

- Um ainda tem de se certificar de que o SAP HANA está num estado consistente
- Não é possível substituir o disco do SO Olá, mesmo se Olá que VM é desalocada devido a um erro a indicar que uma concessão existe. Só funciona depois de eliminar Olá VM, o que poderia levar tooa novo exclusivo ID de VM e Olá necessidade tooinstall uma licença SAP nova.

![É possível toorestore apenas Olá discos de dados de uma VM do Azure](media/sap-hana-backup-storage-snapshots/image021.png)

É toorestore possíveis apenas Olá os discos de dados de uma VM do Azure, evitando problemas de Olá de obter um novo ID exclusivo do VM e, por conseguinte, invalidados licença SAP Olá:

- Para o teste de Olá, dois discos de dados do Azure foram anexado tooa VM e RAID de software foi definido por cima-las 
- Foi confirmada que SAP HANA estava num estado consistente através da funcionalidade de instantâneos de SAP HANA
- Parar de sistema de ficheiros (consulte _consistência de dados SAP HANA quando tirar instantâneos de armazenamento_ no artigo relacionado Olá [guia de cópia de segurança para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md))
- Instantâneos do blob foram executados a partir de ambos os discos de dados
- Libertar poder por do sistema de ficheiros
- Confirmação de instantâneo de SAP HANA
- discos de dados do toorestore Olá, Olá VM foi encerrado e os dois discos desligados
- Depois de anular a exposição de discos de Olá, foram substituídos com instantâneos de blob anteriores Olá
- Em seguida, os discos virtuais Olá restaurada estivesse anexados toohello novamente a VM
- Depois do tempo de instantâneos inicial Olá VM, tudo no software Olá RAID trabalhado ajustar e foi definido novamente toohello blob
- HANA foi definido novamente instantâneo HANA toohello

Se estava tooshut possíveis para baixo de SAP HANA antes de instantâneos do blob de Olá, procedimento Olá será menos complexo. Nesse caso, um pode ignorar o instantâneo HANA Olá e, se mais nada se passa no sistema de Olá, também ignorar congelar de sistema de ficheiros de Olá. Foram adicionada complexidade entra imagem Olá quando for necessário toodo instantâneos enquanto tudo está online. Consulte _consistência de dados SAP HANA quando tirar instantâneos de armazenamento_ no artigo relacionado Olá [guia de cópia de segurança para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Passos seguintes
* [Cópia de segurança manual para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md) fornece uma descrição geral e informações sobre começar a utilizar.
* [Cópia de segurança de SAP HANA com base no nível de ficheiro](sap-hana-backup-file-level.md) abrange Olá opção de cópia de segurança baseada em ficheiros.
* toolearn como tooestablish elevada disponibilidade e o plano de recuperação de desastres do SAP HANA no Azure (instâncias de grande), consulte [SAP HANA (instâncias de grande) elevada disponibilidade e recuperação após desastre no Azure](hana-overview-high-availability-disaster-recovery.md).
