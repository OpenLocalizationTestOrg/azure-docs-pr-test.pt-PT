---
title: "aaaBack segurança portal clássico do DPM cargas de trabalho tooAzure | Microsoft Docs"
description: "Um toobacking de introdução dos servidores do DPM com o serviço de cópia de segurança do Azure Olá"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "System Center Data Protection Manager, o data protection manager, a cópia de segurança do dpm"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>A preparar tooback segurança tooAzure de cargas de trabalho com o DPM
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Servidor do Backup do Azure (clássica)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clássica)](backup-azure-dpm-introduction-classic.md)
>
>

Este artigo fornece uma tooprotect de cópia de segurança do Microsoft Azure toousing introdução os servidores de System Center Data Protection Manager (DPM) e cargas de trabalho. Leia-lo, irá compreender:

* Como funciona a cópia de segurança do Azure DPM server
* Pré-requisitos de Olá tooachieve uma experiência de cópia de segurança uniforme
* Olá típicos erros encontrados e como toodeal com as mesmas
* Cenários suportados

O System Center DPM cria cópias de segurança de ficheiros e dados de aplicações. Dados de cópia de segurança tooDPM podem ser armazenados na banda, disco ou uma cópia de segurança tooAzure no Microsoft Azure Backup. O DPM interage com o Backup do Azure da seguinte forma:

* **DPM implementado como uma máquina virtual do servidor ou no local física** — se o DPM for implementado como um servidor físico ou como uma máquina de virtual de Hyper-V no local que pode fazer uma cópia de segurança de dados tooan cópia de segurança do Azure cofre além disso toodisk e cópia de segurança da banda.
* **DPM implementado como uma máquina virtual do Azure** — do System Center 2012 R2 com Update 3, o DPM pode ser implementado como uma máquina virtual do Azure. Se o DPM for implementado como uma máquina virtual do Azure, pode criar cópias de segurança tooAzure os discos de dados ligados toohello do DPM Azure virtual machine, ou pode descarregar o armazenamento de dados de Olá através de cópias de segurança tooan Cofre de cópia de segurança do Azure.

## <a name="why-backup-your-dpm-servers"></a>Por que motivo de cópia de segurança os servidores DPM?
vantagens de negócio Olá da utilização da cópia de segurança do Azure para cópia de segurança de servidores do DPM incluem:

* Para implementação do DPM no local, pode utilizar o backup do Azure como um tootape de implementação do prazo toolong alternativo.
* Para implementações do DPM no Azure, cópia de segurança do Azure permite-lhe armazenamento toooffload de Olá disco do Azure, permitindo-lhe tooscale segurança armazenando dados mais antigos na cópia de segurança do Azure e novos dados em disco.

## <a name="how-does-dpm-server-backup-work"></a>Como funciona a cópia de segurança do DPM server?
tooback de uma máquina virtual, primeiro é necessário um instantâneo de ponto no tempo dos dados de Olá. Olá cópia de segurança do Azure service inicia Olá tarefa de cópia em Olá hora agendada e acionadores Olá tootake de extensão de cópia de segurança um instantâneo. Olá coordenadas de extensão de cópia de segurança com Olá no convidado VSS tooachieve consistência de serviço e invoca Olá blob instantâneo API de Olá serviço Storage do Azure, depois de consistência foi atingida. Isto é feito tooget um instantâneo consistente de discos de Olá da máquina virtual de Olá, sem ter tooshut-lo para baixo.

Depois de já foi tomado instantâneo Olá, dados de Olá são transferidos por Olá cópia de segurança do Azure service toohello cofre cópias de segurança. serviço de Olá encarrega-se de identificar e transferir apenas os blocos de Olá que foram modificados do Olá última cópia de segurança tornar o armazenamento de cópias de segurança de Olá e de rede eficiente. Quando estiver concluída a transferência de dados de Olá, instantâneo Olá é removido e é criado um ponto de recuperação. Este ponto de recuperação pode ser visto na Olá portal clássico do Azure.

> [!NOTE]
> Para máquinas virtuais do Linux, é possível apenas ficheiro de cópias de segurança consistentes.
>
>

## <a name="prerequisites"></a>Pré-requisitos
Prepare a cópia de segurança do Azure tooback dos dados do DPM da seguinte forma:

1. **Criar um cofre de cópia de segurança**. Se ainda não criou um cofre de cópia de segurança na sua subscrição, consulte Olá Azure portal versão deste artigo - [preparar tooback segurança tooAzure de cargas de trabalho com o DPM](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > A partir de Março de 2017, já não pode utilizar cofres de cópia de segurança Olá toocreate portal clássico.
  > Agora pode atualizar os cópia de segurança cofres tooRecovery os cofres dos serviços. Para obter mais informações, consulte o artigo de Olá [atualizar um tooa do Cofre de cópia de segurança do cofre dos serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft encoraja tooupgrade a cópia de segurança cofres dos cofres dos serviços de tooRecovery.<br/> Após 15 de Outubro de 2017, não é possível utilizar cofres de cópia de segurança de toocreate do PowerShell. **Até 1 de novembro de 2017**:
  >- Todos os cofres de cópia de segurança restantes serão os cofres dos serviços de tooRecovery automaticamente atualizado.
  >- Não será capaz de tooaccess os dados de cópia de segurança no portal clássico Olá. Em vez disso, utilize Olá tooaccess portal do Azure os dados de cópia de segurança cofres dos serviços de recuperação.
  >

2. **Transferir as credenciais do cofre** — no Azure Backup, certificado de gestão do carregamento Olá criou toohello cofre.
3. **Instalar Olá agente de cópia de segurança do Azure e registar o servidor de Olá** — do Backup do Azure, instale o agente de Olá em cada servidor DPM e registar o servidor do DPM Olá no Cofre de cópias de segurança de Olá.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Requisitos (e limitações)
* O DPM pode estar em execução como um servidor físico ou uma máquina virtual de Hyper-V instalada no System Center 2012 SP1 ou System Center 2012 R2. Também pode executar como uma máquina virtual do Azure em execução no System Center 2012 R2 com, pelo menos, o DPM 2012 R2 Update Rollup 3 ou uma máquina virtual do Windows no VMWare, pelo menos, a ser executado no System Center 2012 R2 com Update Rollup 5.
* Se estiver a executar o DPM com o System Center 2012 SP1, deve instalar o Update Rollup 2 para o System Center Data Protection Manager SP1. Isto é necessário antes de poder instalar Olá Azure Backup Agent.
* servidor do DPM Olá deve ter o Windows PowerShell e .net Framework 4.5 instalados.
* O DPM pode criar cópias de segurança a maioria das cargas de trabalho tooAzure cópia de segurança. Para obter uma lista completa de que tem suportado Consulte Olá cópia de segurança do Azure suporta itens abaixo.
* Não não possível recuperar os dados armazenados em cópia de segurança do Azure com a opção de "copiar tootape" Olá.
* Irá precisar de uma conta do Azure com a funcionalidade de cópia de segurança do Azure Olá ativada. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Leia sobre [preços da cópia de segurança do Azure](https://azure.microsoft.com/pricing/details/backup/).
* A utilização de cópia de segurança do Azure requer Olá Azure Backup Agent toobe instalado nos servidores de Olá que pretende tooback cópias de segurança. Cada servidor tem de ter, pelo menos, 10% do tamanho de Olá Olá de dados de que está a ser efetuados, disponível como armazenamento local livre. Por exemplo, a cópia de segurança de 100 GB de dados requer um mínimo de 10 GB de espaço livre na localização de scratch Olá. Enquanto Olá mínimo é de 10, 15% de espaço de armazenamento local livre espaço toobe utilizado para a localização da cache Olá é recomendada.
* No Olá armazenamento cofre do Azure, os dados serão armazenados. Existem não quantidade de toohello de limite de dados que pode criar cópias de segurança tooan Cofre de cópia de segurança do Azure, mas tamanho Olá de uma origem de dados (por exemplo uma máquina virtual ou a base de dados) não deve exceder 54,400 GB.

Estes tipos de ficheiro são suportados para cópia de segurança tooAzure:

* Encriptados (cópias de segurança completas só)
* Comprimidos (cópias de segurança incrementais suportadas)
* Dispersos (cópias de segurança incrementais suportadas)
* Comprimidos e dispersos (tratados como dispersos)

E estes não são suportadas:

* Não são suportados servidores em sistemas de ficheiros sensíveis a maiúsculas.
* Ligações diretas (ignorados)
* (Ignorados) de pontos de reanálise
* Encriptados e comprimidos (ignorados)
* Encriptados e dispersos (ignorados)
* Sequência comprimida
* Sequência dispersa

> [!NOTE]
> No System Center 2012 DPM com SP1 em diante, pode efetuar cópias de segurança segurança de cargas de trabalho protegidas pelo tooAzure do DPM com cópia de segurança do Microsoft Azure.
>
>
