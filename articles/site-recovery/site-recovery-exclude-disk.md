---
title: "discos de aaaExclude da proteção ao utilizar o Azure Site Recovery | Microsoft Docs"
description: "Descreve a razão pela qual e como tooexclude VM discos de replicação para cenários de VMware tooAzure e tooAzure de Hyper-V."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Excluir discos da replicação
Este artigo descreve como tooexclude discos de replicação. Esta exclusão pode otimizar a largura de banda de replicação de Olá consumido ou otimizar os recursos do lado do destino de Olá que utilizam esses discos. funcionalidade de hello é suportada para cenários de VMware tooAzure e tooAzure de Hyper-V.

## <a name="prerequisites"></a>Pré-requisitos

Por predefinição, todos os discos numa máquina são replicados. tooexclude um disco de replicação, tem de instalar manualmente Olá serviço de mobilidade na máquina de Olá antes de ativar a replicação, se estiver a replicar de tooAzure de VMware.


## <a name="why-exclude-disks-from-replication"></a>Porquê excluir discos da replicação?
Muitas vezes, é necessário excluir discos da replicação porque:

- os dados de Olá que é churned no disco Olá excluído não são importantes ou não necessita de toobe replicado.

- Pretende toosave recursos de armazenamento e de rede através da replicação não este volume de alterações.

## <a name="what-are-hello-typical-scenarios"></a>Quais são os cenários típicos de Olá?
Pode identificar exemplos específicos de alterações a dados que são excelentes candidatos para exclusão. Exemplos podem incluir escreve o ficheiro de paginação tooa (pagefile.sys) e escreve os ficheiros de tempdb toohello do Microsoft SQL Server. Dependendo da carga de trabalho Olá e subsistema de armazenamento Olá, o ficheiro de paginação Olá pode registar uma quantidade significativa de volume de alterações. No entanto, a replicar estes dados a partir de Olá site primário tooAzure seria intensiva de recursos. Assim, pode utilizar Olá replicação toooptimize de passos de uma máquina virtual com um único disco virtual que tenha o sistema de operativo Olá e ficheiro de paginação Olá os seguintes:

1. Divisão Olá único disco virtual em dois discos virtuais. Um disco virtual possui um sistema de operativo Olá e Olá outro tem o ficheiro de paginação Olá.
2. Exclua o disco do ficheiro de paginação de Olá da replicação.

Da mesma forma, pode utilizar Olá os seguintes passos toooptimize um disco que tem ambos os tempdb do Microsoft SQL Server Olá fie e Olá o ficheiro de base de dados de sistema:

1. Manter base de dados de sistema de Olá e tempdb dois discos diferentes.
2. Exclua o disco de tempdb Olá da replicação.

## <a name="how-tooexclude-disks-from-replication"></a>Como tooexclude discos de replicação?

### <a name="vmware-tooazure"></a>TooAzure de VMware
Siga Olá [ativar a replicação](site-recovery-vmware-to-azure.md) tooprotect de fluxo de trabalho uma máquina virtual do portal do Azure Site Recovery Olá. Olá quarto passo de fluxo de trabalho Olá, utilizar Olá **disco tooREPLICATE** discos tooexclude de coluna da replicação. Por predefinição, todos os discos estão selecionados para replicação. Desmarque a caixa de verificação de Olá dos discos que pretende que o tooexclude de replicação e a replicação de tooenable Olá, em seguida, concluir os passos.

![Excluir discos de replicação e ativar a replicação de reativação pós-falha tooAzure de VMware](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Pode excluir apenas os discos que já tem Olá serviço de mobilidade instalado. Terá de toomanually instalar o serviço de mobilidade de Olá, porque Olá serviço de mobilidade só é instalado utilizando o mecanismo de push Olá depois da replicação está ativada.
> * Apenas os discos básicos podem ser excluídos da replicação. Não é possível excluir discos do sistema operativo ou discos dinâmicos.
> * Após ativar a replicação, não pode adicionar ou remover discos para replicação. Se pretender tooadd ou excluir um disco, tem de toodisable proteção da máquina de Olá e, em seguida, ative-a novamente.
> * Se excluir um disco que tem necessários para uma aplicação toooperate, após a ativação pós-falha tooAzure, terá disco de Olá toocreate manualmente no Azure para que possam executar a aplicação Olá replicado. Em alternativa, pode integrar da automatização do Azure para um disco de Olá de toocreate de plano de recuperação durante a ativação pós-falha da máquina de Olá.
> * Máquina virtual do Windows: os discos que criar manualmente no Azure não poderão realizar a reativação pós-falha. Por exemplo, se realizar a ativação pós-falha de três discos e criar dois discos diretamente em Máquinas Virtuais do Azure, apenas três discos em que foi realizada a ativação pós-falha realizarão a reativação pós-falha. Não é possível incluir discos que criou manualmente na reativação pós-falha ou em reproteção de tooAzure no local.
> * Máquina virtual do Linux: os discos que criar manualmente no Azure poderão realizar a reativação pós-falha. Por exemplo, se realizar a ativação pós-falha de três discos e criar dois discos diretamente em Máquinas Virtuais do Azure, os cinco discos realizarão a reativação pós-falha. Não pode excluir da reativação pós-falha os discos que foram criados manualmente.
>

### <a name="hyper-v-tooazure"></a>TooAzure de Hyper-V
Siga Olá [ativar a replicação](site-recovery-hyper-v-site-to-azure.md) tooprotect de fluxo de trabalho uma máquina virtual do portal do Azure Site Recovery Olá. Olá quarto passo de fluxo de trabalho Olá, utilizar Olá **disco tooREPLICATE** discos tooexclude de coluna da replicação. Por predefinição, todos os discos estão selecionados para replicação. Desmarque a caixa de verificação de Olá dos discos que pretende que o tooexclude de replicação e a replicação de tooenable Olá, em seguida, concluir os passos.

![Excluir discos de replicação e ativar a replicação de reativação pós-falha tooAzure do Hyper-V](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * Só pode excluir discos básicos de replicação. Não é possível excluir discos do sistema operativo. Recomendamos que não exclua discos dinâmicos. O Azure Site Recovery não consegue identificar o disco rígido virtual (VHD) é básicos ou dinâmicos na máquina de virtual de convidado Olá.  Se todos os discos de volume dinâmico dependentes não são excluídos, Olá de disco dinâmico protegido torna-se um disco com falha numa máquina virtual de ativação pós-falha e hello dados esse disco não estão acessíveis.
> * Após ativar a replicação, não pode adicionar ou remover discos para replicação. Se pretender tooadd ou excluir um disco, tem de toodisable proteção da máquina virtual de Olá e, em seguida, ative-a novamente.
> * Se excluir um disco que tem necessários para uma aplicação toooperate, após a ativação pós-falha tooAzure terá de disco de Olá toocreate manualmente no Azure para que possam executar a aplicação Olá replicado. Em alternativa, pode integrar da automatização do Azure para um disco de Olá de toocreate de plano de recuperação durante a ativação pós-falha da máquina de Olá.
> * Os discos que criar manualmente no Azure não realizarão a reativação pós-falha. Por exemplo, se falhar mais três discos e criar dois discos diretamente no Virtual Machines do Azure, apenas três discos que foram a ativação pós-falha serão efetuados a reativação a partir do Azure tooHyper-V. Não é possível incluir discos que foram criados manualmente na reativação pós-falha ou na replicação inversa do tooAzure de Hyper-V.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Cenários ponto a ponto da exclusão de discos
Vejamos dois cenários toounderstand Olá excluir disco funcionalidade:

- Disco tempdb do SQL Server
- Disco do ficheiro de paginação (pagefile.sys)

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Excluir o disco de tempdb Olá do SQL Server
Consideremos uma máquina virtual do SQL Server que tem um tempdb que pode ser excluído.

Olá o nome do disco virtual Olá é SalesDB.

Discos na máquina de virtual de origem Olá são os seguintes:


**Nome do disco** | **Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operativo
DB-Disk1| Disk1 | D:\ | Base de dados do sistema SQL e User Database1
Base de dados-Disk2 (disco de Olá excluídas da proteção) | Disk2 | E:\ | Ficheiros temporários
Base de dados-Disk3 (disco de Olá excluídas da proteção) | Disk3 | F:\ | Base de dados do SQL Server tempdb (caminho da pasta (F:\MSSQL\Data\) </br/>< / br/>, escreva o caminho da pasta Olá antes da ativação pós-falha.
DB-Disk4 | Disk4 |G:\ |User Database2

Porque o fluxo de dados em dois discos da máquina virtual de Olá é temporário, ao proteger máquinas de virtuais SalesDB Olá, exclua Disk2 e Disk3 da replicação. O Azure Site Recovery não irá replicar esses discos. Na ativação pós-falha, os discos não estará presentes na máquina virtual de ativação pós-falha de Olá no Azure.

Discos da máquina virtual do Azure após a ativação pós-falha de Olá são os seguintes:

**Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | ---
DISK0 | C:\ | Disco do sistema operativo
Disk1 | E:\ | Armazenamento temporário </br / >< / br / > Azure adiciona neste disco e atribui a primeira letra de unidade disponível Olá.
Disk2 | D:\ | Base de dados do sistema SQL e User Database1
Disk3 | G:\ | User Database2

Porque Disk2 e Disk3 foram excluídos da máquina de virtual SalesDB Olá, e é Olá letra de unidade primeiro da lista de Olá disponíveis. Azure atribui o volume de armazenamento temporário de toohello e:. Para todos os discos de Olá replicado, permanecem letras de unidade de Olá Olá mesmo.

Disk3, que era o disco de tempdb Olá SQL (caminho da pasta tempdb F:\MSSQL\Data\), foi excluído da replicação. disco Olá não está disponível na máquina de virtual Olá ativação pós-falha. Como resultado, Olá serviço SQL Server está no estado parado e necessita de caminho de F:\MSSQL\Data Olá.

Existem duas formas toocreate este caminho:

- Adicionar um disco novo e atribuir o caminho da pasta tempdb.
- Utilize um disco de armazenamento temporário existente para o caminho de pasta Olá tempdb.

#### <a name="add-a-new-disk"></a>Adicionar um disco novo:

1. Anote caminhos Olá do SQL Server tempdb.mdf e tempdb.ldf antes da ativação pós-falha.
2. De Olá portal do Azure, adicione uma nova disco toohello ativação pós-falha máquina virtual com Olá iguais ou tamanho mais que o disco de tempdb SQL do Olá origem (Disk3).
3. Inicie sessão no toohello máquina virtual do Azure. Na consola de gestão (diskmgmt.msc) de disco Olá, inicializar e formatar Olá recém-adicionada disco.
4. Atribuir Olá mesmo unidade de letra que era utilizada pelo disco de tempdb Olá SQL (f:).
5. Crie uma pasta de tempdb num Olá volume f: (F:\MSSQL\Data).
6. Inicie o serviço do SQL Server de Olá partir da consola de serviço Olá.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Utilize um disco de armazenamento temporário existente para o caminho da pasta Olá SQL tempdb:

1. Abra uma linha de comandos.
2. Execute o SQL Server no modo de recuperação da linha de comandos Olá.

        Net start MSSQLSERVER /f / T3608

3. Execute Olá seguir sqlcmd toochange Olá tempdb caminho toohello novo caminho.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Pare o serviço do Microsoft SQL Server de Olá.

        Net stop MSSQLSERVER
5. Inicie o serviço do Microsoft SQL Server de Olá.

        Net start MSSQLSERVER

Consulte toohello seguindo a orientação do Azure para o disco de armazenamento temporário:

* [Utilizar SSDs em VMs do Azure toostore TempDB do SQL Server e as extensões de conjunto de memória intermédia](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Melhores práticas de desempenho do SQL Server nas Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Reativação pós-falha (a partir do anfitrião do Azure tooan no local)
Agora vamos compreender discos Olá que são replicados quando efetuar a ativação pós-falha do anfitrião de VMware ou o Hyper-V do local de tooyour do Azure. Os discos que criar manualmente no Azure não serão replicados. Por exemplo, se realizar a ativação pós-falha de três discos e criar dois diretamente em Máquinas Virtuais do Azure, apenas três discos em que foi realizada a ativação pós-falha realizarão a reativação pós-falha. Não é possível incluir discos que foram criados manualmente na reativação pós-falha ou em reproteção de tooAzure no local. Também não replica anfitriões de tooon local de disco de armazenamento temporário de Olá.

#### <a name="failback-toooriginal-location-recovery"></a>Recuperação para localização toooriginal reativação pós-falha

No exemplo anterior Olá, configuração de disco de máquina virtual do Azure Olá é o seguinte:

**Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | ---
DISK0 | C:\ | Disco do sistema operativo
Disk1 | E:\ | Armazenamento temporário </br / >< / br / > Azure adiciona neste disco e atribui a primeira letra de unidade disponível Olá.
Disk2 | D:\ | Base de dados do sistema SQL e User Database1
Disk3 | G:\ | User Database2


#### <a name="vmware-tooazure"></a>TooAzure de VMware
Quando a reativação pós-falha é efetuada toohello a localização original, a configuração de disco de máquina virtual de reativação pós-falha Olá não tem discos excluídos. Os discos que foram excluídos da VMware tooAzure não estará disponíveis na máquina de virtual Olá reativação pós-falha.

Após a ativação pós-falha planeada do VMware tooon local do Azure, discos na máquina de virtual Olá VMWare (localização original) são:

**Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | ---
DISK0 | C:\ | Disco do sistema operativo
Disk1 | D:\ | Base de dados do sistema SQL e User Database1
Disk2 | G:\ | User Database2

#### <a name="hyper-v-tooazure"></a>TooAzure de Hyper-V
Quando a reativação pós-falha é a localização original toohello, permanece de configuração do disco de máquina virtual do Olá reativação pós-falha hello mesmo da configuração original do disco de máquina virtual do Hyper-V. Os discos que foram excluídos tooAzure de site Hyper-V estão disponíveis na máquina de virtual Olá reativação pós-falha.

Após a ativação pós-falha planeada do Azure tooon local. o Hyper-V, discos na máquina de virtual de Hyper-V Olá (localização original) são:

**Nome do Disco** | **Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | Disco do sistema operativo
DB-Disk1 | Disk1 | D:\ | Base de dados do sistema SQL e User Database1
BD-Disk2 (disco excluído) | Disk2 | E:\ | Ficheiros temporários
DB-Disk3 (disco excluído) | Disk3 | F:\ | Base de dados tempdb do SQL (caminho da pasta (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | User Database2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Excluir o disco do ficheiro (pagefile.sys) de paginação de Olá

Consideremos uma máquina virtual que tem um disco de ficheiro de paginação que pode ser excluído.
Existem dois casos.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Caso 1: o ficheiro de paginação Olá está configurado no Olá unidade d:
Segue-se a configuração do disco Olá:


**Nome do disco** | **Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operativo
Base de dados-Disk1 (disco de Olá excluídas da proteção de Olá) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Seguem-se Olá paginação ficheiro definições Olá máquina virtual de origem:

![Definições de ficheiro de paginação na máquina virtual de origem](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Após a ativação pós-falha da máquina virtual de Olá do VMware tooAzure ou tooAzure de Hyper-V, discos Olá máquina virtual do Azure são:

**Nome do disco** | **Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operativo
DB-Disk1 | Disk1 | D:\ | Armazenamento temporário</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Porque Disk1 (D:) foi excluída, D: é Olá letra de unidade primeiro da lista de Olá disponíveis. Azure atribui o volume de armazenamento temporário de toohello d:. Porque não está disponível na máquina virtual do Azure de Olá D:, definição de paginação ficheiros Olá de Olá máquina virtual permanece Olá mesmo.

Seguem-se Olá paginação ficheiro definições Olá máquina virtual do Azure:

![Definições de ficheiro de paginação na máquina virtual do Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Caso 2: o ficheiro de paginação Olá está configurado na outra unidade (que não seja a unidade d:)

Segue-se a configuração de disco da máquina virtual de origem de Olá:

**Nome do disco** | **Sistema operativo convidado disco#** | **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operativo
Base de dados-Disk1 (disco de Olá excluídas da proteção) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Seguem-se definições ficheiros de paginação do Olá na máquina de virtual Olá no local:

![Definições de ficheiros na máquina de virtual Olá no local de paginação](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Após a ativação pós-falha da máquina de virtual Olá do VMware/Hyper-V tooAzure, discos Olá máquina virtual do Azure são:

**Nome do disco**| **Sistema operativo convidado disco#**| **Letra da unidade** | **Tipo de dados no disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |Disco do sistema operativo
DB-Disk1 | Disk1 | D:\ | Armazenamento temporário</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Porque D: é Olá letra de unidade primeiro da lista de disponíveis Olá, Azure atribui o volume de armazenamento temporário de toohello d:. Para todos os discos de Olá replicado, permanece de letra de unidade de Olá Olá mesmo. Porque Olá g disco não está disponível, o sistema de Olá utilizará unidade c: de Olá para Olá ficheiro de paginação.

Seguem-se Olá paginação ficheiro definições Olá máquina virtual do Azure:

![Definições de ficheiro de paginação na máquina virtual do Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Passos seguintes
Depois da implementação estar instalada e em execução, [saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativação pós-falha.
