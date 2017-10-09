---
title: "recuperação após desastre e aaaBackup para discos IaaS do Azure | Microsoft Docs"
description: "Neste artigo, vamos explicar como tooplan para cópia de segurança e recuperação de desastre (DR) de máquinas virtuais (VMs) IaaS e os discos no Azure. Este documento abrange gerido e discos não gerido"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 49b0e7732d6df9407e1e44d9af2500c99a85b37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Cópia de segurança e recuperação após desastre para discos IaaS do Azure

Neste artigo, vamos explicar como tooplan para cópia de segurança e recuperação de desastre (DR) de máquinas virtuais (VMs) IaaS e os discos no Azure. Este documento abrange gerido e discos não gerido.

Iremos falar primeiro sobre Olá incorporada capacidades tolerância a falhas em Olá plataforma Azure que ajudam a proteger contra falhas locais. Em seguida, vamos abordar cenários de desastre Olá totalmente não abrangidos por capacidades incorporadas Olá, que é o tópico principal Olá abordado neste documento. Também vamos mostrar vários exemplos de cenários de carga de trabalho onde pode aplicar diferentes considerações sobre a cópia de segurança e de DR. Em seguida, iremos deverá consultar possíveis soluções para os discos de DR de IaaS. 

## <a name="introduction"></a>Introdução

Olá plataforma do Azure utiliza vários métodos para a redundância e toohelp de tolerância a falhas proteger clientes de falhas de hardware localizada que podem ocorrer. Falhas locais podem incluir problemas com um computador de servidor de armazenamento do Azure que armazena a parte dos dados de Olá para um disco virtual ou falhas de um SSD ou HDD nesse servidor. Estas falhas de componente de hardware isolado podem acontecer durante as operações normais e plataforma Olá é concebida toobe toothese resiliente falhas. Principais perante desastres podem resultar em falhas ou inaccessibility de um grande número de servidores de armazenamento ou de todo um centro de dados. Enquanto as VMs e os discos estão normalmente protegidos de falhas localizadas, são tooprotect necessário passos adicionais a carga de trabalho de toda a região catastrófica falhas (por exemplo, um desastre grave) que podem afetar o VM e os discos.

Além disso toohello possibilidade de falhas da plataforma, podem ocorrer problemas com a aplicação de cliente de Olá ou dados. Por exemplo, uma nova versão da aplicação poderá inadvertidamente fazer uma quebra toohello dados de alteração. Nesse caso, poderá pretender que aplicações de Olá toorevert e Olá dados tooa versão anterior que contêm Olá último bom estado conhecido. É necessário manter cópias de segurança regulares.

Recuperação de desastres regionais, deve efetuar cópias de segurança sua VM do IaaS discos tooa noutra região. 

Antes de vamos ver as opções de cópia de segurança e de DR, vamos recap alguns métodos disponíveis para processamento de falhas localizadas.

### <a name="azure-iaas-resiliency"></a>Resiliência de IaaS do Azure

*Resiliência* refere-se toohello tolerância de falhas normais que ocorrem nos componentes de hardware. Resiliência é Olá capacidade toorecover contra falhas e continuar toofunction. Não é sobre evitando falhas, mas responder toofailures de uma forma que evita o período de indisponibilidade ou perda de dados. objetivo Olá resiliência é tooreturn Olá tooa ao funcionamento integral estado da aplicação após uma falha. Máquinas virtuais do Azure e os discos são falhas de hardware de toocommon resiliente toobe concebida. Informe-nos observe como a plataforma de IaaS do Azure Olá fornece este resiliência.

Uma máquina virtual consiste principalmente de duas partes: (1) A computação servidor e discos persistente Olá (2). Ambos afetam tolerância a falhas Olá de uma máquina virtual.

Se o servidor de anfitrião de computação do Azure Olá que aloja a VM sofre uma falha de hardware (que é raro), o Azure é concebida tooautomatically restauro Olá VM noutro servidor. Se isto acontecer, irá ocorrer uma reinicialização e Olá VM será uma cópia de segurança após algum tempo. Azure Deteta essas falhas de hardware automaticamente e executa recuperações toohelp Certifique-se o cliente de Olá VM ficará disponível logo que possível.

Relativas aos discos IaaS, é essencial para a plataforma de armazenamento persistente Olá durabilidade dos dados. Clientes do Azure tem aplicações de negócio importantes em execução no IaaS e dependem de persistência de Olá dos dados de Olá. Proteção de estruturas do Azure para estes discos de IaaS com três cópias redundantes dos dados armazenados localmente, fornecendo uma durabilidade elevada contra falhas locais. Se um dos componentes de hardware de Olá que contém o disco falhar, a VM não é afetada porque existem dois cópias adicionais toosupport disco pedidos. Funciona bem mesmo se dois componentes de hardware diferentes a suportar um disco falharem Olá mesmo tempo (que seria muito raros). Certifique-se toohelp vamos manter sempre três réplicas, serviço de armazenamento do Azure Olá cria automaticamente uma nova cópia dos dados em segundo plano de Olá se um dos três cópias de Olá ficar indisponível. Por conseguinte, não deve ser necessário toouse RAID com discos do Azure para tolerância a falhas. Um simple RAID 0 configuração deve ser suficiente para striping discos Olá, se necessário toocreate maiores volumes.

Devido a esta arquitetura, **Azure consistentemente tem entregar a nível empresarial durabilidade para IaaS discos, com um líder da indústria ZERO % [Annualized taxa de falhas](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Falhas de hardware localizada no Olá de computação de anfitrião ou no armazenamento de Olá plataforma, por vezes, pode resultar em indisponibilidade temporária para Olá VM que é abrangido por Olá [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) para disponibilidade de VM. Azure também fornece um SLA de líder da indústria para único instâncias VM que utilizam discos de armazenamento Premium.

toosafeguard a cargas de trabalho de aplicação do período de indisponibilidade devido a indisponibilidade temporária do toohello de uma VM ou disco, os clientes podem tirar partido [conjuntos de disponibilidade](../../virtual-machines/windows/manage-availability.md). Dois ou mais máquinas virtuais num conjunto de disponibilidade fornece redundância para aplicação Olá. O Azure, em seguida, cria nessas VMs e discos em domínios de falhas separados com vários componentes de alimentação, rede e servidor. Assim, falhas de hardware localizada normalmente não afetam várias VMs no Olá definido em Olá mesmo tempo, fornecer elevada disponibilidade para a sua aplicação. É considerada que uma disponibilidade de toouse boa prática define quando for necessária uma elevada disponibilidade. Para obter mais informações, consulte aspetos de recuperação após desastre Olá detalhados abaixo.

### <a name="backup-and-disaster-recovery"></a>Cópia de segurança e recuperação após desastre

Recuperação após desastre (DR) é Olá toorecover de capacidade de incidentes raros mas principais: falhas não transitório, dimensionamento wide, tais como a interrupção do serviço que afeta uma região de toda. Recuperação após desastre inclui a cópia de segurança de dados e o arquivamento e pode incluir intervenção manual, como restaurar uma base de dados a partir da cópia de segurança.

Olá proteção incorporada da plataforma Azure contra falhas localizadas poderá não proteger totalmente Olá VMs/discos no caso de Olá de perante desastres principais que pode provocar falhas em grande escala. Isto inclui eventos catastrófica, tais como o Centro de dados que está a ser atingido por um furacão, terramoto, fire ou falhas de unidade de hardware de grande escala. Além disso, podem ocorrer falhas devido a problemas de tooapplication ou dados.

toohelp proteger as cargas de trabalho IaaS contra falhas, deve planear a recuperação de tooenable redundância e cópias de segurança. Recuperação de desastres, deve planear a redundância e cópia de segurança numa localização geográfica diferente na direção oposta ao site primário Olá. Isto ajuda a garantir a cópia de segurança não é afetada por Olá mesmo evento originalmente afetado Olá VM ou discos. Para obter mais informações, consulte [recuperação após desastre para aplicações incorporada no Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

As considerações de DR podem incluir Olá os seguintes aspetos:

1. Elevada disponibilidade (ed) é a capacidade de Olá de Olá toocontinue de aplicação em execução em bom estado de funcionamento, sem períodos de indisponibilidade significativo. Por "bom estado de funcionamento," estamos significa aplicação Olá está a responder e que os utilizadores podem ligar aplicação toohello e interagir com ele. Determinadas aplicações fundamentais e bases de dados poderão ser necessário toobe disponível sempre, mesmo quando ocorrem falhas na plataforma de Olá. Estas cargas de trabalho, poderá ter tooplan redundância para aplicação Olá, bem como em dados de Olá.

2. Dados durabilidade: Em alguns casos, consideração principal Olá é assegurar que os dados de Olá são preservados no Olá maiúsculas e minúsculas de um desastre. Por conseguinte, poderá ter uma cópia de segurança dos seus dados num site diferente. Para essas cargas de trabalho, pode não necessitar de redundância completa para a aplicação Olá, mas uma cópia de segurança regular dos discos de Olá.

## <a name="backup-and-dr-scenarios"></a>Cópia de segurança e cenários de DR

Vamos ver alguns exemplos típicos de cenários de carga de trabalho de aplicações e considerações de Olá para planear a recuperação após desastre.

### <a name="scenario-1-major-database-solutions"></a>Cenário 1: Principal da base de dados soluções

Considere um servidor de base de dados de produção, como o SQL Server ou Oracle pode suportar a elevada disponibilidade. Os utilizadores e aplicações de produção crítico dependem desta base de dados. plano de recuperação após desastre Olá para este sistema poderá ter Olá toosupport os seguintes requisitos:

1. Dados tem de ser protegido e recuperáveis.
2.  Servidor tem de estar disponível para utilização.

Esta operação pode requerer a manter uma réplica da base de dados de Olá numa região diferente como uma cópia de segurança. Dependendo dos requisitos de Olá para disponibilidade de servidor e recuperação de dados, a solução de Olá pode ir desde um ativo-ativo ou ativo-passivo réplica site tooperiodic cópias de segurança offline dos dados de Olá. Bases de dados relacionais, como o SQL Server e Oracle fornecem várias opções para replicação. Para o SQL Server, [SQL Server em grupos de disponibilidade Always](https://msdn.microsoft.com/library/hh510230.aspx) podem ser utilizados para elevada disponibilidade.

Também suportam bases de dados NoSQL como MongoDB [réplicas](https://docs.mongodb.com/manual/replication/) para redundância. réplicas Olá para elevada disponibilidade podem ser utilizadas.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Cenário 2: Um cluster de VMs redundantes

Considere uma carga de trabalho processada por um cluster de VMs que fornecer redundância e balanceamento de carga. Um exemplo seria um cluster de Cassandra implementado numa região. Este tipo de arquitetura já fornece um elevado nível de redundância nessa região. No entanto, tooprotect a carga de trabalho de Olá de uma falha de nível regional, deve considerar propagando-se o cluster de Olá em duas regiões ou efetuar a região de tooanother de cópias de segurança periódica.

### <a name="scenario-3-iaas-application-workload"></a>Cenário 3: Carga de trabalho de aplicação de IaaS

Isto pode ser uma carga de trabalho de produção normal em execução numa VM do Azure. Por exemplo, poderia ser um servidor web ou um servidor de ficheiro que contém conteúdo Olá e outros recursos de um site. Também poderia ser uma aplicação de negócio personalizada em execução numa VM que armazenados os respetivos dados, a recursos e o estado da aplicação em discos VM Olá. Neste caso, é importante toomake se que efetuar cópias de segurança regulares. Frequência de cópia de segurança deve ser baseada no natureza Olá da carga de trabalho do Olá VM. Por exemplo, se a aplicação Olá é executado diariamente e modifica dados, em seguida, cópia de segurança de Olá deverão ser executada a cada hora.

Outro exemplo é um servidor de relatórios que retirar dados de outras origens e gera relatórios agregados. Perda desta VM ou discos direciona toohello perda de Olá relatórios. No entanto, poderá ser Olá toorerun possíveis processo e saída de Olá voltar a gerar relatórios. Nesse caso, realmente não tem uma perda de dados, mesmo se o servidor de relatórios Olá é acessos com um desastre, pelo que pode ter um nível mais elevado de tolerância de perda de parte dos dados de Olá na Olá servidor de relatórios. Nesse caso, as cópias de segurança menos frequentes é um custo de Olá tooreduce opção.

### <a name="scenario-4-iaas-application-data-issues"></a>Cenário 4: Problemas de dados de aplicação de IaaS

Tiver uma aplicação que calcula, mantém e serve de dados comerciais críticos, como obter informações sobre preços. Uma nova versão da sua aplicação tinha um erro de software que incorretamente calculada Olá preços e danificado dados comércio existentes Olá servidos pela plataforma de Olá. Aqui, Olá melhor procedimento seria toorevert toohello versão anterior da aplicação Olá e os dados de Olá primeiro. tooenable, tome periódica as cópias de segurança do seu sistema.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Solução de recuperação após desastre: Serviço de cópia de segurança do Azure

[Serviço de cópia de segurança do Azure](https://azure.microsoft.com/services/backup/) é pode ser utilizado para cópia de segurança e DR e funciona com [discos geridos](../../virtual-machines/windows/managed-disks-overview.md) , bem como [discos não gerido](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). Pode criar uma tarefa de cópia de segurança com políticas de retenção de cópias de segurança, fácil restauro de VM e cópias de segurança baseados no tempo. 

Se utilizar [discos de armazenamento Premium](storage-premium-storage.md), [discos geridos](../../virtual-machines/windows/managed-disks-overview.md), ou outros tipos de disco com Olá [armazenamento localmente redundante (LRS)](storage-redundancy.md#locally-redundant-storage) opção, é especialmente importante tooleverage cópias de segurança periódicas do DR. Cópia de segurança do Azure armazena os dados de Olá no seu Cofre de serviços de recuperação para a retenção de longo prazo. Escolha Olá [armazenamento georredundante (GRS)](storage-redundancy.md#geo-redundant-storage) opção para o Cofre dos serviços de recuperação de cópia de segurança Olá. Que irá garantir cópias de segurança são replicadas tooa diferentes região do Azure para salvaguardar de perante desastres regionais.

Para [discos não gerido](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), pode utilizar o tipo de armazenamento LRS Olá para discos IaaS, mas certifique-se de que a cópia de segurança do Azure está ativada com Olá opção GRS para Olá cofre dos serviços de recuperação.

**Se utilizar Olá [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) opção para os discos não gerido, que ainda precisa de instantâneos consistentes para cópia de segurança e de DR.** Tem de utilizar um [serviço de cópia de segurança do Azure](https://azure.microsoft.com/services/backup/) ou [instantâneos consistentes](#alternative-solution-consistent-snapshots).

Olá segue-se um resumo das soluções de DR.

| Cenário | Replicação automática | Solução de DR |
| --- | --- | --- |
| *Discos de armazenamento Premium* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Discos LRS não gerido* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Discos GRS não gerido* | Cruzada região ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Instantâneos consistentes](#alternative-solution-consistent-snapshots) |
| *Discos de RA-GRS não gerido* | Cruzada região ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Instantâneos consistentes](#alternative-solution-consistent-snapshots) |

Elevada disponibilidade melhor pode pelo satisfeito através da utilização de Olá de gerido discos num conjunto de disponibilidade, juntamente com a cópia de segurança do Azure. Se estiver a utilizar discos não gerido, pode continuar a utilizar a cópia de segurança do Azure para DR. Se não é possível toouse cópia de segurança do Azure, em seguida, colocar [instantâneos consistentes](#alternative-solution-consistent-snapshots) conforme descrito na secção posterior é uma solução alternativa para cópia de segurança e de DR.

As opções de elevada disponibilidade, cópia de segurança e DR em níveis de infraestrutura ou de aplicação pode ser representado como abaixo:

| *Nível* | Elevada disponibilidade   | Cópia de segurança / DR |
| --- | --- | --- |
| *Aplicação* | SQL Server Always On | Azure Backup |
| *Infraestrutura*  | Conjunto de Disponibilidade  | GRS com instantâneos consistentes |

### <a name="using-hello-azure-backup-service"></a>Utilizar Olá serviço de cópia de segurança do Azure

[Cópia de segurança do Azure](../../backup/backup-azure-vms-introduction.md) pode criar cópias de segurança as VMs do Windows ou Linux toohello Cofre de serviços de recuperação do Azure em execução. Cópia de segurança e restaurar dados críticos da empresa é complicou pelo facto de Olá dados críticos da empresa tem uma cópia de segurança ao aplicações Olá que produzem Olá dados estão em execução. tooaddress, cópia de segurança do Azure fornece cópias de segurança consistentes com aplicações para cargas de trabalho Microsoft com Olá tooensure de serviço de sombra de volumes (VSS) que dados são escritos corretamente toostorage. Para VMs com Linux, apenas as cópias de segurança consistente com ficheiros são possíveis, uma vez que o Linux não tem tooVSS equivalente de funcionalidade.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Quando a cópia de segurança do Azure inicia uma tarefa de cópia de segurança no momento de Olá agendada, aciona Olá cópia de segurança de extensão instaladas no Olá VM tootake um instantâneo de ponto no tempo. É obtido um instantâneo em coordenação com VSS tooget um instantâneo consistente de discos de Olá na máquina virtual de Olá sem ter tooshut-lo para baixo. todas as escritas antes de instantâneo consistentes Olá de todos os discos de Olá de limpezas da extensão de cópia de segurança de Olá na Olá VM. Depois de Olá instantâneo é tirado dados Olá são transferidos pelo Cofre de cópia de segurança toohello cópias de segurança do Azure. toomake Olá cópia de segurança processo mais eficiente, serviço Olá identifica e transfere apenas os blocos de Olá dos dados que foram alterados desde a última cópia de segurança Olá.


toorestore, pode ver Olá disponíveis as cópias de segurança através de cópia de segurança do Azure e, em seguida, iniciar um restauro. Pode criar e restaurar cópias de segurança do Azure através de Olá [portal do Azure](https://portal.azure.com/), [através do PowerShell](../../backup/backup-azure-vms-automation.md ), ou utilizando Olá [CLI do Azure](https://docs.microsoft.com/azure/xplat-cli-install). Para obter mais informações, consulte o Backup do Azure.

### <a name="steps-tooenable-backup"></a>Passos tooEnable cópia de segurança

Olá passos seguintes são normalmente utilizados tooenable cópias de segurança das suas VMs através de Olá [Portal do Azure](https://portal.azure.com/). Será algumas variações dependendo do seu cenário exato. Consulte toohello [cópia de segurança do Azure](../../backup/backup-azure-vms-introduction.md) documentação para obter detalhes completos. Azure cópia de segurança também [suporta VMs com discos geridos](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Crie um cofre dos serviços de recuperação para uma VM utilizando Olá os seguintes passos:

    a.  Utilizar Olá [portal do Azure](https://portal.azure.com/), procurar todos os recursos e localize "Cofres dos serviços de recuperação".

    b.  No Olá recuperação cofres dos serviços de menu, clique em Adicionar e siga os passos de Olá toocreate um novo cofre Olá mesma região que Olá VM. Por exemplo, se a VM está na região EUA oeste, escolha EUA oeste para o Cofre de Olá.

2.  Certifique-se a replicação de armazenamento Olá para Olá recém-criado cofre. toodo esta, o Cofre de Olá acesso partir Olá dos serviços de recuperação cofres painel aceda toohello definições/cópia de segurança e configuração. Certifique-se de que Olá opção GRS está selecionada por predefinição. Isto irá garantir que o Cofre é automaticamente replicadas tooa Datacenter secundário. Por exemplo, o Cofre nos EUA oeste será automaticamente replicada tooEast E.U.A..

3.  Configurar a política de cópia de segurança de Olá e selecione Olá VM Olá mesma IU.

4.  Certifique-se Olá que Olá VM está instalado o agente de cópia de segurança. Se a VM é criada utilizando uma imagem de galeria do Azure, agente de cópia de segurança de Olá já está instalado. Caso contrário (ou seja, se estiver a utilizar uma imagem personalizada), utilize instruções demasiado[Olá de instalar o agente de VM na máquina virtual de Olá](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Certifique-se de que Olá VM possibilita a conectividade de rede para Olá toofunction de serviço de cópia de segurança. Siga estas instruções para [conectividade de rede](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Depois de concluídas Olá os passos acima, a cópia de segurança de Olá será executado em intervalos regulares, conforme especificado na política de cópia de segurança de Olá. Se necessário, pode acionar Olá primeira cópia de segurança manualmente a partir do dashboard do cofre Olá no Olá portal do Azure.

Para automatizar Backup do Azure com scripts, consulte demasiado[cmdlets do PowerShell para cópia de segurança VM](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Passos de recuperação

Se precisar de toorepair ou reconstruir uma VM, pode restaurar Olá VM a partir de qualquer um dos pontos de recuperação de cópia de segurança de Olá no Cofre de Olá. Existem algumas das diferentes opções para efetuar a recuperação de Olá:

1.  Pode criar uma nova VM como uma representação de ponto no tempo da sua VM de cópia de segurança.

2.  Pode restaurar Olá discos e, em seguida, utilize o modelo de Olá para Olá VM toocustomize e reconstrução Olá restaurada VM. 

Consulte as instruções demasiado[máquinas de virtuais do Azure de utilização portal toorestore](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). documento de Olá também explica os passos específicos Olá para restaurar a cópia de segurança VMs toohello emparelhado de centro de dados utilizando o seu Cofre de cópia de segurança georredundante Olá maiúsculas e minúsculas de um desastre no Centro de dados principal Olá. Nesse caso, a cópia de segurança do Azure utiliza o serviço de computação de Olá da máquina de virtual Olá região secundária toocreate Olá restaurada.

Também pode utilizar o PowerShell para [restaurar uma VM](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) ou para [criar uma nova VM do restaurada discos](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Solução alternativa: Instantâneos consistentes

Se não é possível toouse Olá serviço de cópia de segurança do Azure, pode implementar o seus próprios mecanismo de cópia de segurança através de instantâneos. É mais complicada toocreate instantâneos consistentes para todos os discos utilizados por uma VM e, em seguida, replicar esses região tooanother de instantâneos. Por este motivo, o Azure considera Olá aproveitamento serviço de cópia de segurança uma opção melhor a criação de uma solução personalizada. Se utilizar o armazenamento RA-GRS/GRS para discos, os instantâneos são automaticamente replicadas tooa Datacenter secundário. Se utilizar o armazenamento LRS para discos, será necessário dados de Olá tooreplicate. Para obter mais informações, consulte [cópia de segurança do Azure discos VM não geridos com instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md).

Um instantâneo é uma representação de um objeto de um ponto específico no tempo. Um instantâneo será cobrado de faturação para o tamanho de incremental Olá dos dados de Olá contém. Para obter mais informações, consulte [criar um instantâneo de blob](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>Criação de instantâneos ao hello VM está em execução

Enquanto pode tirar um instantâneo em qualquer altura, se hello VM está em execução, ainda está a ser transmissão em fluxo toohello discos de dados e instantâneos de Olá podem conter operações parciais que estavam em trânsito. Além disso, se existirem vários discos envolvidas, Olá os instantâneos de discos diferentes podem ter ocorrido em alturas diferentes, que significa que estes instantâneos podem não ser coordenados. Isto é particularmente problemático para os volumes repartidos cujos ficheiros podem estar danificados se a ser efetuadas alterações durante a cópia de segurança.

tooavoid nesta situação, processo de cópia de segurança de Olá tem de implementar Olá os seguintes passos:

1.  Parar todos os discos de Olá

2.  Esvaziar todos os Olá pendentes escritas

3.  Em seguida, [criar um instantâneo de blob](../blobs/storage-blob-snapshots.md) para todos os discos de Olá

Algumas aplicações de Windows como o SQL Server fornecem um mecanismo de cópia de segurança coordenado através de cópias de segurança consistentes com aplicações VSS toocreate. No Linux, pode utilizar uma ferramenta como fsfreeze para coordenar a discos de Olá, que irão fornecer cópias de segurança consistente com ficheiros, mas não consistentes com aplicações instantâneos. Este processo é complexa, por isso, e deve considerar a utilização [cópia de segurança do Azure](../../backup/backup-azure-vms-introduction.md) ou uma solução de cópia de segurança de terceiros que já proceder a esta.

Olá acima processo resultará numa coleção de instantâneos coordenadas para todos os discos VM de Olá, que representa uma vista de ponto no tempo específica de Olá VM. Este é um ponto de restauro de cópia de segurança para Olá VM. Pode repetir o processo de Olá em intervalos agendados toocreate periódica as cópias de segurança. Consulte abaixo para obter os passos Olá demasiado[região de tooanother de cópias de segurança de Olá cópia](#copy-the-snapshots-to-another-region) para DR.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Criação de instantâneos ao hello a VM está offline

Outra opção toocreate consistente cópias de segurança está a encerrar Olá VM e tendo blob instantâneos de cada disco. Isto é mais fácil de instantâneos em coordenação de uma VM em execução, mas requer alguns minutos de indisponibilidade. Para que este processo, siga estes passos:

1. Encerre Olá VM.

2. Crie um instantâneo de cada blob VHD, que demora apenas alguns segundos.

    toocreate um instantâneo, pode utilizar [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), Olá [API de Rest do Storage do Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [CLI do Azure](https://docs.microsoft.com/azure/xplat-cli-install), ou um dos Olá bibliotecas de cliente de armazenamento do Azure, tal como [ biblioteca de clientes de armazenamento Olá para .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Inicie Olá VM, que termina o período de indisponibilidade Olá. Normalmente, o processo completo de Olá conclui dentro de alguns minutos.

Este processo gera uma coleção de instantâneos consistentes para todos os discos de Olá, fornecer um ponto de restauro de cópia de segurança para Olá VM. Veja a seguir região tooanother de instantâneos Olá Olá passos toocopy DR.

### <a name="copy-hello-snapshots-tooanother-region"></a>Copie a região de tooanother Olá instantâneos

Não pode ser suficiente para DR a criação de instantâneos de Olá individualmente. Também têm de replicar região de tooanother Olá instantâneo cópias de segurança.

Se estiver a utilizar o GRS ou RA-GRS para os discos, em seguida, Olá os instantâneos são região secundária toohello replicadas automaticamente. Pode haver alguns minutos do desfasamento antes de replicação de Olá, e se o Datacenter primário Olá ficar inativo antes de instantâneos de Olá concluir a replicação, não será capaz de tooaccess instantâneos de Olá partir do Centro de dados secundária Olá. probabilidade Olá desta situação é pequena.

> [!Note] 
> Ter apenas discos Olá numa conta GRS ou RA-GRS protege Olá VM contra desastres inesperados. Também tem de criar instantâneos coordenados ou utilizar o Backup do Azure. Isto é necessário toorecover num estado consistente de tooa VM.

Se estiver a utilizar o LRS, tem de copiar conta de armazenamento diferente do Olá instantâneos tooa imediatamente após a criação de um instantâneo de Olá. destino de cópia de Olá pode ser uma conta de armazenamento LRS numa região diferente, resultando em cópia de Olá está a ser uma região remota. Também pode copiar conta de armazenamento do Olá instantâneo tooan RA-GRS no Olá mesma região. Neste caso, o instantâneo Olá será toohello lenta replicadas de região secundária remoto. A cópia de segurança se encontra protegida contra desastres inesperados no site primário Olá depois de copiar Olá e da replicação estar concluída.

toocopy o seu incrementais instantâneos do DR rever de forma eficiente, instruções Olá [cópia de segurança do Azure discos VM não geridos com instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Recuperação a partir de instantâneos

tooretrieve um instantâneo, copie-toomake um blob de novo. Se estiver a copiar o instantâneo de Olá da conta primária Olá, pode copiar Olá instantâneo através de toohello BLOBs base do instantâneo Olá, assim reverter Olá disco toohello instantâneo; Isto é conhecido como promover instantâneo Olá. Se estiver a copiar a cópia de segurança do Olá instantâneo de uma conta secundária (no caso de Olá de RA-GRS), tem de ser copiados conta principal tooa. Pode copiar um instantâneo [através do PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) ou utilizando o utilitário do AzCopy Olá. Para obter mais informações, consulte [transferir dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md).

No caso de Olá de VMs com vários discos, tem de copiar todos os instantâneos de Olá que fazem parte do mesmo coordenado de Olá ponto de restauro. Depois de copiar os blobs VHD do Olá instantâneos toowritable, pode utilizar Olá blobs toorecreate VM utilizando o modelo de Olá para Olá VM.

## <a name="other-options"></a>Outras opções

### <a name="sql-server"></a>SQL Server

SQL Server em execução numa VM tem a suas próprias toobackup capacidades incorporadas tooAzure de base de dados do SQL Server armazenamento de BLOBs ou uma partilha de ficheiros. Se a conta de armazenamento de Olá é GRS ou RA-GRS, pode aceder a essas cópias de segurança no Centro de dados secundária de uma conta de armazenamento Olá no evento Olá de um desastre, com Olá mesmas restrições, como explicado anteriormente. Para obter mais informações, consulte [cópia de segurança e restaurar para o SQL Server em Azure Virtual Machines](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Na adição toobackup e restauro, [SQL Server em grupos de disponibilidade Always](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) pode manter réplicas secundárias de bases de dados toogreatly reduzir o tempo de recuperação de desastre Olá.

## <a name="other-considerations"></a>Outras considerações

Este artigo foi abordado como toobackup ou tirar instantâneos das suas VMs e recuperação de desastre toosupport os respetivos discos e como toouse esses toorecover. Com o modelo do Azure Resource Manager Olá, muitas pessoas utilizam modelos toocreate as respetivas VMs e outra infraestrutura no Azure. Pode utilizar um modelo toocreate uma VM que tenha Olá mesma configuração de cada vez. Se utilizar imagens personalizadas para criar as suas VMs, também deve certificar-se de que as imagens estão protegidas através da utilização de um toostore de conta de RA-GRS-los.

Por conseguinte, o processo de cópia de segurança pode ser uma combinação de duas coisas:

1. Dados de cópia de segurança Olá (discos)
2. Configuração de cópia de segurança Olá (modelos, imagens personalizadas)

Consoante a opção de cópia de segurança Olá que escolher, poderá ter toohandle Olá de cópia de segurança dados Olá e configuração de Olá ou serviço de cópia de segurança de Olá pode lidar com todo que para si.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Apêndice - compreender o impacto de Olá do LRS, GRS e RA-GRS

Para contas de armazenamento do Azure, existem três tipos de redundância de dados que deve considerar relativamente a recuperação após desastre – localmente redundante (LRS), georredundante (GRS), ou ler georredundante com acesso (RA-GRS). 

Localmente armazenamento redundante (LRS) mantém três cópias dos dados Olá Olá mesmo centro de dados. Quando são escritos dados Olá, todos os três cópias são atualizadas antes de sucesso é devolvido toohello chamador, para saber que se são idênticos. O disco se encontra protegido contra falhas locais, uma vez que não é muito provável que todos os três cópias iriam ficar comprometidas em Olá mesmo tempo. No caso de Olá do LRS, não há nenhum georredundância para que disco Olá não se encontra protegido contra falhas catastrófica, que podem afetar uma unidade de armazenamento ou centro de dados completo.

Com a GRS e RA-GRS, três cópias dos seus dados são mantidas na região primária Olá (selecionado por si) e, mais três cópias dos seus dados são mantidas numa região secundária correspondente (definida pelo Azure). Por exemplo, se armazenar dados nos EUA oeste, dados de Olá serão replicada tooEast E.U.A.. Isto é feito de forma assíncrona e, existe um pequeno atraso entre atualizações toohello primária e secundária. As réplicas dos discos de Olá no site secundário Olá são consistentes numa base por disco (com atraso Olá), mas as réplicas de vários discos de Active Directory poderão não estar sincronizadas **entre si**. são necessários toohave réplicas consistente entre múltiplos discos, os instantâneos consistentes.

Olá a principal diferença entre GRS e RA-GRS é a que com RA-GRS, pode ler cópia secundário Olá em qualquer altura. Se existir um problema que compõe dados Olá na região primária Olá inacessível, Olá equipa do Azure faz com que cada acesso de toorestore esforço. Enquanto Olá primário está inativo, se tiver ativado o RA-GRS, pode aceder a dados de Olá no Centro de dados secundária Olá. Por conseguinte, se planear tooread da réplica de Olá enquanto Olá primário está inacessível, em seguida, RA-GRS devem ser consideradas.

Se, fica fora toobe uma interrupção significativa, Olá equipa do Azure pode acionar uma ativação pós-falha georreplicação e alterar Olá primário DNS entradas toopoint toosecondary armazenamento. Neste momento, se tiver o GRS ou RA-GRS ativado, pode aceder a dados Olá na região de Olá que utilizado toobe Olá secundário. Por outras palavras, se a sua conta de armazenamento GRS e não existe um problema, pode aceder armazenamento secundário Olá apenas se não houver uma ativação pós-falha georreplicação.

Para obter mais informações, consulte [que toodo se ocorrer uma falha de armazenamento do Azure](storage-disaster-recovery-guidance.md). 

Tenha em atenção que a Microsoft controla se ocorrer uma ativação pós-falha. Ativação pós-falha não é controlada por conta de armazenamento, por conseguinte não foi decidido por clientes individuais. tooimplement recuperação após desastre para as contas de armazenamento específicas ou discos da máquina virtual, tem de utilizar as técnicas de Olá descritas anteriormente neste artigo.
