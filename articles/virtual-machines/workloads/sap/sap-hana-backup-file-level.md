---
title: "aaaSAP HANA Azure Backup no nível de ficheiro | Microsoft Docs"
description: "Existem duas principais cópia de segurança as possibilidades de SAP HANA em máquinas virtuais do Azure, este artigo abrange SAP HANA Backup do Azure no nível de ficheiro"
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
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>Cópia de segurança do SAP HANA do Azure no nível de ficheiro

## <a name="introduction"></a>Introdução

Isto faz parte de uma série de três partes de artigos relacionados numa cópia de segurança de SAP HANA. [Cópia de segurança manual para SAP HANA em Azure Virtual Machines](./sap-hana-backup-guide.md) fornece uma descrição geral e informações de introdução, e [cópia de segurança de SAP HANA com base nos instantâneos de armazenamento](./sap-hana-backup-storage-snapshots.md) abrange Olá opção de cópia de segurança baseada em instantâneos de armazenamento.

Observar os tamanhos de VM do Azure Olá, um pode ver que um GS5 permite 64 discos de dados anexados. Para grandes sistemas de SAP HANA, um número significativo de discos já pode ser executado para ficheiros de registo e dados, possivelmente, em combinação com RAID de software para o débito de e/s de disco ideal. em seguida, a pergunta Olá é onde toostore SAP HANA cópia de segurança ficheiros, que foi cheias dados Olá ligado discos ao longo do tempo? Consulte [tamanhos de máquinas virtuais do Linux no Azure](../../linux/sizes.md) para tabelas de tamanho de VM do Azure Olá.

Não há nenhum integração de cópia de segurança de SAP HANA disponível com o serviço de cópia de segurança do Azure neste momento. forma padrão Olá toomanage cópia de segurança/restauro ao nível dos ficheiros Olá está com uma baseado no ficheiro de cópia de segurança por SAP HANA Studio ou através de instruções SQL do SAP HANA. Consulte [SAP HANA SQL e referência de vistas de sistema](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) para obter mais informações.

![Esta ilustração mostra diálogo Olá de item de menu de cópia de segurança de Olá no Studio do SAP HANA](media/sap-hana-backup-file-level/image022.png)

Esta ilustração mostra diálogo Olá de item de menu de cópia de segurança de Olá no Studio do SAP HANA. Quando escolher o tipo &quot;ficheiro,&quot; um tem toospecify um caminho no sistema de ficheiros de olá onde o SAP HANA escreve os ficheiros de cópia de segurança de Olá. Restauro funciona Olá mesma forma.

Embora esta opção SOA simples e reencaminhar diretamente, existem algumas considerações. Tal como mencionado anteriormente, uma VM do Azure tem uma limitação do número de discos de dados que podem ser anexados. Poderá não ser capacidade toostore SAP HANA ficheiros de cópia em sistemas de ficheiros de Olá de Olá VM, dependendo do tamanho de Olá Olá da base de dados e o disco débito requisitos, que poderão envolver software RAID utilizando striping em dados de vários discos. Várias opções para mover estes ficheiros de cópia de segurança e gerir as restrições de tamanho de ficheiro e o desempenho quando o processamento de terabytes de dados, são fornecidas posteriormente neste artigo.

Outra opção, o que oferece maior liberdade relativamente à capacidade total, é o armazenamento de Blobs do Azure. Enquanto um blob único também é restrito too1 TB, capacidade total do Olá de um contentor de blob único está atualmente 500 TB. Além disso, proporciona aos clientes Olá tooselect choice so-called &quot;frios&quot; armazenamento de BLOBs, que tem uma vantagem de custo. Consulte [Blob Storage do Azure: frequente e esporádico camadas de armazenamento](../../../storage/blobs/storage-blob-storage-tiers.md) para obter detalhes sobre o armazenamento de BLOBs de acesso esporádico.

Para segurança adicional, utilize um armazenamento georreplicação conta toostore Olá SAP HANA cópias de segurança. Consulte [replicação de armazenamento do Azure](../../../storage/common/storage-redundancy.md) para obter detalhes sobre replicação de conta de armazenamento.

Uma conta de armazenamento de cópia de segurança dedicado que seja georreplicação um foi colocar VHDs dedicados para cópias de segurança de SAP HANA. Caso contrário, é um copiar VHDs Olá manter cópias de segurança de SAP HANA de Olá tooa conta de armazenamento de georreplicação ou conta de armazenamento de tooa está numa região diferente.

## <a name="azure-backup-agent"></a>Agente de cópia de segurança do Azure

Ofertas de cópia de segurança do Azure Olá opção toonot apenas cópia de segurança completa nas VMs, mas também ficheiros e diretórios através do agente cópia de segurança Olá, que tem toobe instalado no convidado Olá SO. Mas a partir de Dezembro de 2016, este agente só é suportado no Windows (consulte [cópia de segurança uma tooAzure Windows Server ou o cliente utilizando o modelo de implementação do Resource Manager Olá](../../../backup/backup-configure-vault.md)).

Uma solução toofirst cópia tooa de ficheiros de cópia de segurança de SAP HANA VM do Windows no Azure (por exemplo, através de partilha SAMBA) e, em seguida, utilizar Olá agente de cópia de segurança do Azure a partir daí. Embora seja tecnicamente exequível,-seria adicionam complexidade e abrandar a cópia de segurança de Olá ou restaurar processo bastante um pouco devido toohello cópia entre Olá Linux e Olá VM do Windows. Não é recomendado toofollow esta abordagem.

## <a name="azure-blobxfer-utility-details"></a>Detalhes de utilitário blobxfer do Azure

toostore diretórios e ficheiros no armazenamento do Azure, pode utilizar um CLI ou PowerShell, ou desenvolva uma ferramenta utilizando um dos Olá [Azure SDKs](https://azure.microsoft.com/downloads/). Existe também um utilitário de prontos a utilizar, o AzCopy, para copiar tooAzure o armazenamento de dados, mas é apenas Windows (consulte [transferir dados com Olá utilitário de linha de comandos do AzCopy](../../../storage/common/storage-use-azcopy.md)).

Por conseguinte blobxfer foi utilizado para copiar ficheiros de cópia de segurança de SAP HANA. -Lo é open source, utilizado por vários clientes em ambientes de produção e disponível em [GitHub](https://github.com/Azure/blobxfer). Esta ferramenta permite uma toocopy dados diretamente tooeither Azure blob storage ou partilha de ficheiros do Azure. Também oferece uma gama de funcionalidades úteis, como md5 hash ou paralelismo automático quando copiar um diretório com vários ficheiros.

## <a name="sap-hana-backup-performance"></a>Desempenho de cópia de segurança de SAP HANA

![Nesta captura de ecrã é Olá SAP HANA cópia de segurança consola SAP HANA Studio](media/sap-hana-backup-file-level/image023.png)

É esta captura de ecrã da consola de cópia de segurança de SAP HANA de Olá no Studio do SAP HANA. Que demorou a cópia de segurança do minutos sobre 42 toodo Olá de Olá GB 230 num disco único armazenamento padrão do Azure anexados toohello HANA VM utilizando o sistema de ficheiros XFS.

![Nesta captura de ecrã é de YaST na VM de teste de SAP HANA Olá](media/sap-hana-backup-file-level/image024.png)

Nesta captura de ecrã é de YaST na VM de teste de SAP HANA Olá. Um pode ver Olá 1 TB um único disco para cópia de segurança de SAP HANA tal como mencionado anteriormente. Demorou cerca de 42 minutos toobackup 230 GB. Além disso, cinco discos de 200 GB estivesse anexados e software RAID md0 criados com striping sobre estas cinco discos de dados do Azure.

![Repetir Olá mesmo cópia de segurança no RAID de software com striping entre cinco ligado a discos de dados de armazenamento padrão do Azure](media/sap-hana-backup-file-level/image025.png)

Olá repetido mesmo cópia de segurança no RAID de software com striping entre cinco ligado armazenamento padrão do Azure dados discos colocados Olá hora da cópia de 42 minutos para baixo too10 minutos. discos de Olá foram anexados sem colocar em cache toohello VM. Para que fique óbvios débito de escrita de disco como importante é por período de tempo de cópia de segurança Olá. Um foi, em seguida, o comutador tooAzure premium storage toofurther acelerar o processo de Olá para um desempenho ideal. Em geral, o armazenamento do Azure premium deve ser utilizado para sistemas de produção.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Copie o armazenamento de BLOBs de tooAzure de ficheiros de cópia de segurança de SAP HANA

Como de Dezembro de 2016, Olá melhor opção tooquickly arquivo SAP HANA cópia de segurança de ficheiros é blob storage do Azure. Um contentor de blob único tem um limite de 500 TB suficiente para a maioria dos sistemas de SAP HANA, em execução numa GS5 VM no Azure, cópias de segurança tookeep suficientes SAP HANA. Os clientes têm a opção de Olá entre &quot;frequente&quot; e &quot;amovíveis&quot; armazenamento de BLOBs (consulte [Blob Storage do Azure: frequente e esporádico camadas de armazenamento](../../../storage/blobs/storage-blob-storage-tiers.md)).

Com a ferramenta de blobxfer Olá, é ficheiros de cópia de segurança fácil toocopy Olá SAP HANA diretamente o armazenamento de BLOBs de tooAzure.

![Aqui um pode ver ficheiros Olá de uma cópia de segurança de ficheiros de SAP HANA completa](media/sap-hana-backup-file-level/image026.png)

Aqui um pode ver ficheiros Olá de uma cópia de segurança de ficheiros de SAP HANA completa. Existem quatro ficheiros e hello maiores tem aproximadamente 230 GB.

![Demorou aproximadamente 3000 segundos toocopy Olá 230 GB tooan armazenamento padrão do Azure conta contentor do blob](media/sap-hana-backup-file-level/image027.png)

Não a utilizar no teste inicial Olá md5 hash, demorou aproximadamente 3000 segundos toocopy Olá 230 GB tooan armazenamento padrão do Azure conta contentor do blob.

![Nesta captura de ecrã, um pode ver aspeto no Olá portal do Azure](media/sap-hana-backup-file-level/image028.png)

Nesta captura de ecrã, um pode ver o aspeto no Olá portal do Azure. Um contentor do blob denominado &quot;sap-hana-cópias de segurança&quot; foi criado e inclui blobs Olá quatro, que representam os ficheiros de cópia de segurança Olá SAP HANA. Um dos atributos tem um tamanho de aproximadamente 230 GB.

consola de cópia de segurança do Olá HANA Studio permite um tamanho de ficheiro máximo de Olá de toorestrict dos ficheiros de cópia de segurança HANA. Num ambiente de exemplo de Olá, se um desempenho melhorado, tornando toohave possíveis cópia de segurança mais pequena vários ficheiros, em vez de um ficheiro grande de 230 GB.

![Definir o limite de tamanho de ficheiro de cópia de segurança de Olá no Olá HANA lado &#39; t melhorar o tempo de cópia de segurança de Olá](media/sap-hana-backup-file-level/image029.png)

Definir o limite de tamanho de ficheiro de cópia de segurança de Olá no Olá HANA lado &#39; t melhorar o tempo de cópia de segurança Olá, porque os ficheiros de Olá são escritos sequencialmente, como mostrado na figura que. limite de tamanho de ficheiro Olá foi definido too60 GB, pelo que a cópia de segurança de Olá criar quatro ficheiros de dados de grandes dimensões em vez de Olá 230-GB ficheiros única.

![tootest paralelismo da ferramenta de blobxfer Olá, o tamanho de ficheiro máximo Olá para cópias de segurança HANA, em seguida, foi definido too15 GB](media/sap-hana-backup-file-level/image030.png)

tootest paralelismo da ferramenta de blobxfer Olá, o tamanho de ficheiro máximo Olá para cópias de segurança HANA foi definido, em seguida, too15 GB, o que resultou no 19 ficheiros de cópia de segurança. Esta configuração colocados tempo Olá para armazenamento de BLOBs de tooAzure Olá 230 GB blobxfer toocopy de segundos 3000 baixo too875 segundos.

Este resultado é que devem estar toohello limite de 60 MB/seg de escrita de um blob do Azure. Paralelismo através de vários blobs resolve estrangulamento Olá, mas não existe um downside: aumentar o desempenho de Olá blobxfer ferramenta toocopy todos os tooAzure de ficheiros de cópia de segurança destes HANA armazenamento de BLOBs coloca carga Olá HANA VM e rede Olá. A operação do sistema HANA passa a ser afetada.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Cópia de BLOBs de discos de dados do Azure dedicada no RAID de software de cópia de segurança

Ao contrário Olá VM dados disco cópia de segurança manual, esta abordagem, um não fazer cópia de segurança todos os discos de dados de Olá numa VM toosave Olá todo SAP instalação, incluindo dados HANA HANA regista os ficheiros e ficheiros de configuração. Em vez disso, a ideia Olá é toohave dedicado RAID de software com striping em dados do Azure vários VHDs para armazenar uma cópia de segurança de ficheiros de SAP HANA completa. Um copia apenas estes discos, com a cópia de segurança do Olá SAP HANA. Pode facilmente seja mantidas uma conta de armazenamento de cópia de segurança HANA dedicada, ou ligados tooa dedicado &quot;gestão VM de cópia de segurança&quot; para processamento adicional.

![Todos os VHDs envolvidos foram copiados com Olá * * iniciar-azurestorageblobcopy * * comando do PowerShell](media/sap-hana-backup-file-level/image031.png)

Depois de Olá toohello cópia de segurança local RAID de software foi concluída, todos os VHDs envolvidos foram copiados com Olá **início azurestorageblobcopy** comando do PowerShell (consulte [início AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Como afeta apenas o sistema de ficheiros de Olá dedicado para manter os ficheiros de cópia de segurança de Olá, não existem sem preocupações de consistência de ficheiro de registo ou dados SAP HANA no disco Olá. Uma vantagem deste comando é que funciona enquanto Olá VM permanece online. toobe determinada-se de que nenhum processo escreve o conjunto de cópia de segurança stripe toohello, ser toounmount se antes de Olá cópia de BLOBs e montá-la novamente posteriormente. Ou um pode apropriadas forma demasiado&quot;fixar&quot; Olá sistema de ficheiros. Por exemplo, através de xfs\_fixar de sistema de ficheiros XFS Olá.

![Nesta captura de ecrã mostra a lista de Olá dos blobs no contentor de vhds Olá no Olá portal do Azure](media/sap-hana-backup-file-level/image032.png)

Nesta captura de ecrã mostra a lista de Olá dos blobs na Olá &quot;vhds&quot; contentor no Olá portal do Azure. Olá captura de ecrã mostra Olá cinco VHDs, que foram anexados toohello SAP HANA servidor VM tooserve como Olá software RAID tookeep SAP HANA ficheiros de cópia. Também mostra Olá cinco cópias efetuadas através do comando de cópia de BLOBs de Olá.

![Para fins de teste, cópias de Olá dos discos RAID de software de cópia de segurança de SAP HANA Olá foram toohello ligado ao servidor de aplicações VM](media/sap-hana-backup-file-level/image033.png)

Para fins de teste, as cópias de Olá dos discos RAID de software de cópia de segurança de SAP HANA Olá foram toohello ligado ao servidor de aplicações VM.

![servidor de aplicação Olá VM foi encerrado tooattach Olá disco cópias](media/sap-hana-backup-file-level/image034.png)

servidor de aplicação Olá VM foi encerrado tooattach Olá disco cópias. Depois de iniciar Olá VM, discos Olá e Olá RAID foram detetados corretamente (montado através do UUID). Apenas o ponto de montagem Olá estava em falta, o que foi criada através do particionador de YaST Olá. Seguidamente cópias de ficheiro de cópia de segurança de SAP HANA Olá deixou de estar visível no nível do SO.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Copiar ficheiros de cópia de segurança de SAP HANA tooNFS partilhar

toolessen Olá potencial impacto no Olá sistema de SAP HANA a partir de uma perspetiva de espaço em disco ou de desempenho, um pode considerar armazenar ficheiros de cópia de segurança de SAP HANA de Olá numa partilha NFS. Tecnicamente funciona, mas significa utilizar um segundo VM do Azure como anfitrião Olá de Olá de partilha NFS. Não deve ser um tamanho VM pequeno, devido a largura de banda de rede VM de toohello. Iria tornar sentido, em seguida, tooshut baixo isto &quot;cópia de segurança de VM&quot; e colocá-lo apenas para executar a cópia de segurança do Olá SAP HANA. Escrever em NFS partilha coloca a carga na rede de Olá e impactos Olá sistema de SAP HANA mas gerir simplesmente Olá ficheiros de cópia de segurança posteriormente no Olá &quot;cópia de segurança de VM&quot; seria não influenciam o sistema de SAP HANA Olá de todo.

![Uma partilha NFS a partir de outra VM do Azure foi montado toohello servidor de SAP HANA VM](media/sap-hana-backup-file-level/image035.png)

Olá tooverify NFS utilizar as maiúsculas e minúsculas, uma partilha NFS a partir de outra VM do Azure foi montado toohello servidor de SAP HANA VM. Não ocorreu nenhuma especial NFS otimização aplicado.

![Demorou cópia de segurança do 1 hora e 46 minutos toodo Olá diretamente](media/sap-hana-backup-file-level/image036.png)

partilha NFS incluída na Olá era um conjunto de stripe rápida, como Olá um no servidor de SAP HANA Olá. Contudo, demorou 1 hora e Olá de toodo 46 minutos cópia de segurança diretamente na partilha NFS incluída na Olá em vez de 10 minutos, ao escrever tooa local stripe conjunto.

![alternativa Olá não foi muito mais rápida em 1 hora e 43 minutos](media/sap-hana-backup-file-level/image037.png)

alternativa Olá de fazer um conjunto de local stripe de cópia de segurança tooa e copiar toohello de partilha NFS no nível do SO (simples **cp - avr** comandos) não foi muito mais rápida. Demorou 1 hora e 43 minutos.

Funciona, mas o desempenho não foi boa para teste de cópia de segurança Olá 230 GB. Deverá ver mesmo um para vários terabytes.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Copie o serviço de tooAzure de ficheiros de cópia de segurança de ficheiros de SAP HANA

É possível toomount partilhar um ficheiro do Azure dentro de uma VM com Linux do Azure. artigo de Olá [como toouse File storage do Azure com o Linux](../../../storage/files/storage-how-to-use-files-linux.md) fornece detalhes sobre como toodo-lo. Tenha em atenção que não há atualmente um limite de quota de 5 TB de uma partilha de ficheiros do Azure e um limite de tamanho de ficheiro de 1 TB por ficheiro. Consulte [metas de desempenho e escalabilidade do Storage do Azure](../../../storage/common/storage-scalability-targets.md) para obter informações sobre limites de armazenamento.

Testes demonstraram, no entanto, que não de cópia de segurança de SAP HANA &#39; t trabalhar diretamente com este tipo de montagem CIFS. Também é declarado no [1820529 de nota SAP](https://launchpad.support.sap.com/#/notes/1820529) que CIFS não é recomendada.

![Esta ilustração mostra um erro na caixa de diálogo de cópia de segurança Olá no SAP HANA Studio](media/sap-hana-backup-file-level/image038.png)

Esta ilustração mostra um erro na caixa de diálogo de cópia de segurança Olá no SAP HANA Studio, quando tenta tooback cópias de segurança diretamente tooa partilha de ficheiros do Azure CIFS montada. Para um tem toodo uma cópia de segurança de SAP HANA padrão para um sistema de ficheiros VM primeiro e, em seguida, a cópia de segurança de Olá ficheiros da tooAzure há serviço ficheiro.

![Esta ilustração mostra que demorou sobre 929 segundos toocopy 19 SAP HANA ficheiros de cópia](media/sap-hana-backup-file-level/image039.png)

Esta ilustração mostra que demorou sobre 929 segundos toocopy 19 ficheiros de cópia de segurança de SAP HANA com um tamanho total aproximadamente 230 GB toohello do Azure da partilha de ficheiros.

![estrutura de diretórios origem Olá Olá SAP HANA VM foi copiado toohello partilha de ficheiros do Azure](media/sap-hana-backup-file-level/image040.png)

Nesta captura de ecrã, um pode ver que a estrutura de diretórios origem Olá Olá SAP HANA VM foi copiado toohello partilha de ficheiros do Azure: um diretório (hana\_cópia de segurança\_fsl\_15 gb) e 19 ficheiros de cópia de segurança individuais.

Armazenamento de ficheiros de cópia de segurança de SAP HANA nos ficheiros do Azure pode ser uma opção interessante na Olá futura quando cópias de segurança de ficheiros de SAP HANA suportam diretamente. Ou quando se torna possível toomount Azure ficheiros através de NFS e o limite de quota máxima de Olá é consideravelmente maior 5 TB.

## <a name="next-steps"></a>Passos seguintes
* [Cópia de segurança manual para SAP HANA em Azure Virtual Machines](sap-hana-backup-guide.md) fornece uma descrição geral e informações sobre começar a utilizar.
* [Cópia de segurança de SAP HANA com base nos instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md) descreve Olá baseado no instantâneo cópia de segurança opção de armazenamento.
* toolearn como tooestablish elevada disponibilidade e o plano de recuperação de desastres do SAP HANA no Azure (instâncias de grande), consulte [SAP HANA (instâncias de grande) elevada disponibilidade e recuperação após desastre no Azure](hana-overview-high-availability-disaster-recovery.md).
