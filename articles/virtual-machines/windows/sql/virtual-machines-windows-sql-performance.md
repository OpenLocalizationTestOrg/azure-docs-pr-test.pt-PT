---
title: "aaaPerformance melhores práticas para o SQL Server no Azure | Microsoft Docs"
description: "Apresenta as melhores práticas para otimizar o desempenho de SQL Server em VMs do Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Melhores práticas de desempenho do SQL Server nas Máquinas Virtuais do Azure

## <a name="overview"></a>Descrição geral

Este tópico fornece as melhores práticas para otimizar o desempenho de SQL Server na máquina de Virtual do Microsoft Azure. Ao executar o SQL Server em Azure Virtual Machines, recomendamos que continue a utilizar Olá mesmo desempenho de base de dados de otimização de opções que são aplicável tooSQL servidor num ambiente de servidor no local. No entanto, desempenho Olá da base de dados relacional numa nuvem pública depende de vários fatores, tais como o tamanho de Olá de uma máquina virtual e a configuração de Olá Olá de discos de dados.

Quando criar imagens do SQL Server, [considere aprovisionamento as suas VMs no portal do Azure de Olá](virtual-machines-windows-portal-sql-server-provision.md). Todas estas melhores práticas, incluindo a configuração do armazenamento Olá de implementar VMs de SQL Server aprovisionados na Olá Portal com o Resource Manager.

Este artigo concentra-se sobre a obtenção de Olá *melhor* desempenho para o SQL Server em VMs do Azure. Se a carga de trabalho for inferior pedir o seu trabalho, não poderá necessitar de cada otimização listada abaixo. Considere as necessidades de desempenho e padrões de carga de trabalho como avaliar estas recomendações.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Lista de verificação rápida

Olá segue-se uma lista de verificação rápida para um desempenho ideal do SQL Server em Azure Virtual Machines:

| Área | Otimizações de |
| --- | --- |
| [Tamanho da VM](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) ou superior para o SQL Server Enterprise edition.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) ou superior para edições Standard do SQL Server e Web. |
| [Armazenamento](#storage-guidance) |Utilize [armazenamento Premium](../../../storage/common/storage-premium-storage.md). Armazenamento Standard só é recomendado para dev/teste.<br/><br/>Manter Olá [conta de armazenamento](../../../storage/common/storage-create-storage-account.md) e VM do SQL Server no Olá mesma região.<br/><br/>Desativar o Azure [armazenamento georredundante](../../../storage/common/storage-redundancy.md) (georreplicação) da conta do storage Olá. |
| [Discos](#disks-guidance) |Utilize um mínimo de 2 [P30 discos](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 para ficheiros de registo; 1 para ficheiros de dados e o TempDB).<br/><br/>Evite utilizar o sistema operativo ou discos temporários para o armazenamento de base de dados ou registo.<br/><br/>Ative colocação em cache de leitura em discos de Olá que aloja os ficheiros de dados de Olá e TempDB.<br/><br/>Não ative a colocação em cache no ficheiro de registo Olá de alojamento de discos.<br/><br/>Importante: Parar serviço do SQL Server Olá quando alterar as definições da cache de Olá para um disco da VM do Azure.<br/><br/>Stripe vários débito de e/s do tooget aumentada de discos de dados do Azure.<br/><br/>O formato com o tamanho de alocação documentado. |
| [E/S](#io-guidance) |Ative a compressão de página de base de dados.<br/><br/>Ative a inicialização instantânea de ficheiros para ficheiros de dados.<br/><br/>Limitar ou desativar a opção autogrow na base de dados de Olá.<br/><br/>Desative autoshrink na base de dados de Olá.<br/><br/>Mova todos os discos de toodata de bases de dados, incluindo bases de dados do sistema.<br/><br/>Mova SQL Server erro registo e rastreio diretórios toodata discos de ficheiro.<br/><br/>Configure localizações de ficheiros de cópia de segurança e a base de dados predefinidos.<br/><br/>Ative páginas bloqueadas.<br/><br/>Aplica correções de desempenho de SQL Server. |
| [Funcionalidades específicas](#feature-specific-guidance) |Cópia de segurança diretamente tooblob armazenamento. |

Para mais informações sobre *como* e *por que motivo* toomake estas otimizações, reveja os detalhes de Olá e as orientações fornecidas nas secções seguintes.

## <a name="vm-size-guidance"></a>Orientações de tamanho VM

Para aplicações confidenciais de desempenho, é recomendado que utilize o seguinte Olá [tamanhos de máquinas virtuais](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 ou superior
* **As edições Web e SQL Server Standard**: DS2 ou superior

## <a name="storage-guidance"></a>Orientações de armazenamento

Suporte de VMs de série DS (juntamente com a série dsv2 e GS série) [armazenamento Premium](../../../storage/common/storage-premium-storage.md). Armazenamento Premium é recomendado para todas as cargas de trabalho de produção.

> [!WARNING]
> Armazenamento standard tem largura de banda e latências variando e só é recomendado para cargas de trabalho de programador/teste. Cargas de trabalho de produção devem utilizar o armazenamento Premium.

Além disso, recomendamos que crie a sua conta do storage do Azure no Olá mesmo centro de dados como os atrasos de transferência do tooreduce de máquinas virtuais do SQL Server. Ao criar uma conta de armazenamento, desative a georreplicação conforme a ordem de escrita consistente entre múltiplos discos não é garantida. Em vez disso, considere configurar uma tecnologia de recuperação de desastres do SQL Server entre centros de dados do Azure dois. Para obter mais informações, consulte [elevada disponibilidade e recuperação após desastre do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Documentação de orientação dos discos

Existem três tipos de disco principal numa VM do Azure:

* **Disco do SO**: ao criar uma Máquina Virtual do Azure, a plataforma de Olá ligará pelo menos um disco (identificados como Olá **C** unidade) toohello VM para o disco de sistema operativo. Este disco é um VHD armazenado como um blob de página no armazenamento.
* **Disco temporário**: máquinas virtuais do Azure contêm outro disco designado por disco temporário Olá (identificados como Olá **D**: unidade). Este é um disco num nó de Olá que pode ser utilizado para o espaço scratch.
* **Os discos de dados**: também pode anexar mais discos tooyour máquina como discos de dados, e estas serão armazenadas no armazenamento como blobs de páginas.

Olá secções seguintes descrevem recomendações para utilizar estes discos diferentes.

### <a name="operating-system-disk"></a>Disco do sistema operativo

Um disco de sistema operativo é um VHD que pode efetuar o arranque e montar como uma versão de um sistema operativo em execução e está assinalada como como **C** unidade.

Predefinição a colocação em cache da política no disco do sistema operativo Olá é **leitura/escrita**. Para aplicações confidenciais de desempenho, recomendamos que utilize discos de dados em vez de disco do sistema operativo Olá. Consulte a secção de Olá em discos de dados abaixo.

### <a name="temporary-disk"></a>Disco temporário

Olá, unidade de armazenamento temporário, identificada como Olá **D**: disco, não é o armazenamento de BLOBs de tooAzure persistente. Não armazene os ficheiros de base de dados de utilizador ou ficheiros de registo de transação de utilizador de Olá **D**: unidade.

Para a série D, série Dv2 e VMs de série de G, unidade temporária de Olá nestas VMS é baseadas em SSD. Se a carga de trabalho fizer utilização intensa de TempDB (por exemplo, para objetos temporários ou associações complexas) a armazenar TempDB Olá **D** unidade pode resultar numa maior débito de TempDB e reduzir a latência de TempDB.

Para VMs que suportam o Premium Storage (série DS, série dsv2 e GS série), recomendamos o armazenamento de TempDB num disco que suporte o Premium Storage com cache de leitura ativado. Há uma recomendação de toothis exceção; Se a utilização de TempDB escrita intensivas, pode alcançar um desempenho superior armazenando TempDB no local de Olá **D** unidade, o que também seja baseadas em SSD nestes tamanhos de máquina.

### <a name="data-disks"></a>discos de dados

* **Utilizar discos de dados de ficheiros de registo e dados**: no mínimo, utilize 2 Premium Storage [P30 discos](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) em que um disco contém ficheiros de registo de Olá e Olá outro contém dados Olá e ficheiros de TempDB. Cada disco de armazenamento Premium fornece um número de IOPs e largura de banda (MB/s), dependendo do tamanho, conforme descrito no seguinte artigo de Olá: [utilizando o Premium Storage para discos](../../../storage/common/storage-premium-storage.md).

* **Disco Striping**: para obter mais débito, pode adicionar discos de dados adicionais e utilizar Striping de disco. número de Olá toodetermine de discos de dados, terá de tooanalyze Olá diversas IOPS e largura de banda necessária para os ficheiros de registo de e para os seus dados e ficheiros de TempDB. Tenha em atenção que os tamanhos de VM diferentes têm limites diferentes no número de Olá de IOPs e largura de banda suportadas, consulte as tabelas de Olá no IOPS por [tamanho da VM](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Utilize Olá seguintes diretrizes:

  * Para Windows 8/Windows Server 2012 ou posterior, utilize [espaços de armazenamento](https://technet.microsoft.com/library/hh831739.aspx) com Olá seguintes diretrizes:

      1. Conjunto Olá intercalação (tamanho do stripe) too64 KB (65536 bytes) para cargas de trabalho OLTP e 256 KB (262144 bytes) para o impacto do desempenho tooavoid cargas de trabalho devido toopartition desalinhamento do armazém de dados. Isto deve ser definido com o PowerShell.
      1. Definir o número de colunas = número de discos físicos. Utilize o PowerShell quando configurar mais de 8 discos (não IU do Gestor de servidor). 

    Por exemplo, Olá PowerShell a seguir cria um novo agrupamento de armazenamento com Olá intercalação tamanho too64 KB e Olá número de colunas too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Para o Windows 2008 R2 ou anterior, pode utilizar discos dinâmicos (volumes repartido do SO) e o tamanho do stripe Olá sempre é 64 KB. Tenha em atenção que esta opção é preterida a partir do Windows 8/Windows Server 2012. Para obter informações, consulte a declaração de suporte de Olá em [serviço de discos virtuais está em transição tooWindows API da gestão de armazenamento](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Se a carga de trabalho não é exigente em termos de registo e não precisa de IOPs dedicados, pode configurar um agrupamento de armazenamento. Caso contrário, crie dois conjuntos de armazenamento, um para ficheiros de registo de Olá e outro agrupamento de armazenamento para ficheiros de dados de Olá e TempDB. Determine o número de Olá de discos associados a cada agrupamento de armazenamento com base nas suas expectativas de carga. Tenha em atenção que os tamanhos de VM diferentes permitem números diferentes de discos de dados anexados. Para obter mais informações, consulte [tamanhos das Virtual Machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Se não estiver a utilizar o armazenamento Premium (cenários de desenvolvimento/teste), recomendação de Olá é o número máximo de Olá tooadd de discos de dados suportados pela sua [tamanho da VM](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e utilizar Striping de disco.

* **Política de colocação em cache**: os discos de dados para o Premium Storage, ativar a colocação em cache de leitura em discos de dados de Olá apenas a alojar os ficheiros de dados e o TempDB. Se não estiver a utilizar o armazenamento Premium, não ative a qualquer colocação em cache em qualquer discos de dados. Para obter instruções sobre como configurar a colocação em cache em disco, consulte Olá os seguintes tópicos: [conjunto AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) e [conjunto AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Pare o serviço do SQL Server Olá quando alterar a definição de cache de Olá da VM do Azure discos tooavoid Olá conhecimento possibilidade de quaisquer danos na base de dados.

* **Tamanho de unidade de alocação de NTFS**: quando formatar o disco de dados de Olá, é recomendado que utilize um tamanho de unidade de alocação de 64 KB para ficheiros de registo e dados, bem como TempDB.

* **Melhores práticas de gestão de disco**: quando o tipo de remoção de um disco de dados ou alterar a respetiva cache, parar o serviço do SQL Server de Olá durante a alteração de Olá. Quando as definições de colocação em cache Olá são alterado no disco do SO de Olá, Azure interrompe Olá VM, altera o tipo de cache de Olá e reinicia Olá VM. Quando as definições de cache de Olá de um disco de dados foram alteradas, Olá VM não está parado, mas o disco de dados de Olá se desliga de Olá VM durante Olá alterar e, em seguida, novamente ligado.

  > [!WARNING]
  > Olá de toostop falha serviço do SQL Server durante estas operações pode danificá-la.

## <a name="io-guidance"></a>Orientações de e/s

* Olá obter os melhores resultados com o Premium Storage são obtidos quando parallelize a sua aplicação e os pedidos. Armazenamento Premium foi concebido para cenários onde profundidade de fila de e/s de Olá é superior a 1, pelo que verá pouco ou nenhum ganhos de desempenho para pedidos de série single-threaded (mesmo que se encontrem exigente em termos de armazenamento). Por exemplo, isto poderia afetar os resultados de teste único thread Olá das ferramentas de análise de desempenho, tais como SQLIO.

* Considere a utilização de [compressão da página de base de dados](https://msdn.microsoft.com/library/cc280449.aspx) como pode ajudar a melhorar o desempenho das cargas de trabalho exigente em termos de e/s. No entanto, a compressão de dados de Olá pode aumentar o consumo de CPU Olá no servidor de base de dados de Olá.

* Considere ativar instantâneas inicialização tooreduce Olá hora do ficheiro que é necessária para alocação de ficheiro inicial. tootake partido de inicialização instantânea de ficheiros, conceder a conta de serviço do SQL Server (MSSQLSERVER) Olá com SE_MANAGE_VOLUME_NAME e adicioná-lo toohello **efetuar tarefas de manutenção de Volume** política de segurança. Se estiver a utilizar uma imagem de plataforma do SQL Server para o Azure, a conta de serviço predefinido Olá (NT Service\MSSQLSERVER) não está adicionada toohello **efetuar tarefas de manutenção de Volume** política de segurança. Por outras palavras, inicialização instantânea de ficheiros não está ativada numa imagem de plataforma do Azure do SQL Server. Depois de adicionar Olá do SQL Server service conta toohello **efetuar tarefas de manutenção de Volume** política de segurança, o serviço do SQL Server de Olá de reinício. Podem existir considerações de segurança para utilizar esta funcionalidade. Para obter mais informações, consulte [inicialização de ficheiro de base de dados](https://msdn.microsoft.com/library/ms175935.aspx).

* **o aumento automático** é considerado toobe simplesmente plano de contingência para crescimento inesperado. Não é gerir o seu crescimento de dados e de registo numa base diária com o aumento automático. Se for utilizada a opção autogrow, aumente previamente ficheiro Olá utilizando o comutador de tamanho de Olá.

* Certifique-se **autoshrink** é o overhead de desnecessários tooavoid desativado que pode afetar negativamente o desempenho.

* Mova todos os discos de toodata de bases de dados, incluindo bases de dados do sistema. Para obter mais informações, consulte [mover bases de dados de sistema](https://msdn.microsoft.com/library/ms345408.aspx).

* Mova SQL Server erro registo e rastreio diretórios toodata discos de ficheiro. Isto pode ser feito no Gestor de configuração de servidor do SQL Server ao clicar a instância do SQL Server e ao selecionar propriedades. Olá definições de ficheiros de registo e rastreio de erro podem ser alteradas no Olá **parâmetros de arranque** Olá separador. diretório de informação do estado é especificado em Olá **avançadas** Olá separador captura de ecrã a seguir mostra onde toolook para parâmetro de arranque do registo de erro do Olá.

    ![Captura de ecrã de registo de erros SQL](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Configure localizações de ficheiros de cópia de segurança e a base de dados predefinidos. Utilize recomendações Olá neste tópico e efetuar alterações de Olá na janela de propriedades do servidor de Olá. Para obter instruções, consulte [Olá ver ou alterar as localizações predefinidas para dados e ficheiros de registo (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Olá captura de ecrã seguinte demonstra onde toomake estas alterações.

    ![Ficheiros de registo de dados do SQL Server e de cópia de segurança](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Ativar bloqueado tooreduce de páginas e/s e quaisquer atividades de paginação. Para obter mais informações, consulte [ativar Olá páginas de bloqueio na opção de memória (Windows)](https://msdn.microsoft.com/library/ms190730.aspx).

* Se estiver a executar o SQL Server 2012, instale o Service Pack 1 a atualização cumulativa 10. Esta atualização contém correção de Olá para fraco desempenho em e/s ao executar selecione numa declaração de tabela temporária no SQL Server 2012. Para obter informações, consulte este [artigo da base de dados de conhecimento](http://support.microsoft.com/kb/2958012).

* Considere a compressão de quaisquer ficheiros de dados ao transferir/fora do Azure.

## <a name="feature-specific-guidance"></a>Orientações específicas de funcionalidade

Algumas implementações poderão alcançar os benefícios de desempenho adicionais utilizando técnicas de configuração mais avançadas. Olá lista seguinte destaca com algumas funcionalidades do SQL Server que podem ajudá-lo tooachieve um melhor desempenho:

* **Cópia de segurança de armazenamento tooAzure**: quando efetuar cópias de segurança para o SQL Server em execução em máquinas virtuais do Azure, pode utilizar [tooURL de cópia de segurança do SQL Server](https://msdn.microsoft.com/library/dn435916.aspx). Esta funcionalidade está disponível, começando pelo SQL Server 2012 SP1 CU2 e recomendados para criar cópias de segurança toohello ligado discos de dados. Quando a cópia de segurança/restauro para/de armazenamento do Azure, siga as recomendações de Olá fornecidas no [cópia de segurança do SQL Server tooURL melhores práticas e resolução de problemas e restaurar a partir de cópias de segurança armazenadas no armazenamento do Azure](https://msdn.microsoft.com/library/jj919149.aspx). Também pode automatizar estas cópias de segurança utilizando [cópia de segurança automatizada do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

    TooSQL anterior Server 2012, pode utilizar [tooAzure de cópia de segurança do SQL Server ferramenta](https://www.microsoft.com/download/details.aspx?id=40740). Esta ferramenta pode ajudar o débito de cópia de segurança tooincrease com vários destinos de cópia de segurança do stripe.

* **Ficheiros de dados do SQL Server no Azure**: esta nova funcionalidade, [ficheiros de dados do SQL Server no Azure](https://msdn.microsoft.com/library/dn385720.aspx), está disponível a partir de com o SQL Server 2014. Executar o SQL Server com ficheiros de dados no Azure demonstra comparável características de desempenho e como utilizar discos de dados do Azure.

## <a name="next-steps"></a>Passos Seguintes

Para melhores práticas de segurança, consulte [considerações de segurança para o SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-security.md).

Reveja os outros tópicos de Máquina Virtual do SQL Server em [do SQL Server na descrição geral de máquinas virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).
