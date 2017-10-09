---
title: Guia de aaaBackup para SAP HANA em Azure Virtual Machines | Microsoft Docs
description: "Guia de cópia de segurança para SAP HANA fornece duas principais possibilidades de cópia de segurança para SAP HANA em máquinas virtuais do Azure"
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
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Guia de segurança para SAP HANA em Máquinas Virtuais do Azure

## <a name="getting-started"></a>Introdução

Guia de cópia de segurança de Olá para SAP HANA em execução em máquinas virtuais do Azure apenas descrevem tópicos específicos do Azure. Para gerais SAP HANA cópia de segurança itens relacionados, consulte a documentação de SAP HANA Olá (consulte _documentação de cópia de segurança de SAP HANA_ posteriormente neste artigo).

Olá foco este artigo é dois principais cópia de segurança as possibilidades de SAP HANA em máquinas virtuais do Azure:

- Sistema de ficheiros de cópia de segurança toohello HANA numa máquina de Virtual do Linux do Azure (consulte [SAP HANA Backup do Azure no nível de ficheiro](sap-hana-backup-file-level.md))
- Cópia de segurança HANA com base nos instantâneos de armazenamento utilizando a funcionalidade de instantâneos de blob de armazenamento do Azure Olá manualmente ou o serviço de cópia de segurança do Azure (consulte [cópia de segurança de SAP HANA com base nos instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md))

SAP HANA oferece uma cópia de segurança API, o que permite que as ferramentas de cópia de segurança de terceiros toointegrate diretamente com SAP HANA. (Que não está dentro do âmbito deste guia Olá.) Não há nenhum integração direta de SAP HANA com o serviço de cópia de segurança do Azure direito disponível com base nesta API.

SAP HANA é oficialmente suportado no tipo de VM do Azure GS5 como única instância com cargas de trabalho de tooOLAP uma restrição adicional (consulte [localizar plataformas IaaS certificadas](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) no Web site SAP Olá). Este artigo será atualizado como novas ofertas de SAP HANA no Azure fique disponível.

Há também uma solução híbrida de SAP HANA disponíveis no Azure, onde SAP HANA é executada não virtualizados em servidores físicos. No entanto, este guia de cópia de segurança de SAP HANA Azure inclui um ambiente do Azure puro onde SAP HANA é executado numa VM do Azure, não SAP HANA em execução no &quot;instâncias grandes.&quot; Consulte [descrição geral de SAP HANA (instâncias de grandes dimensões) e arquitetura no Azure](hana-overview-architecture.md) para obter mais informações sobre esta solução de cópia de segurança no &quot;instâncias grande&quot; com base nos instantâneos de armazenamento.

Informações gerais sobre os produtos SAP suportadas no Azure podem ser encontradas no [1928533 de nota SAP](https://launchpad.support.sap.com/#/notes/1928533).

Olá seguintes três figuras dar uma descrição geral de Olá opções de cópia de segurança de SAP HANA atualmente a utilizar as capacidades do Azure nativas e também mostram três cenários de cópia de segurança futuros potenciais. Olá artigos relacionados [SAP HANA Backup do Azure no nível de ficheiro](sap-hana-backup-file-level.md) e [cópia de segurança de SAP HANA com base nos instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md) descrevem estas opções em mais detalhe, incluindo as considerações de desempenho e de tamanho para SAP HANA cópias de segurança que são várias-terabytes de tamanho.

![Esta ilustração mostra duas possibilidades para guardar o estado de VM Olá atual](media/sap-hana-backup-guide/image001.png)

Esta ilustração mostra a possibilidade de Olá de guardar Olá VM estado atual, ou através do serviço de cópia de segurança do Azure ou manual instantâneos de discos VM. Com esta abordagem, um &#39; t ter cópias de segurança do toomanage SAP HANA. desafio Olá do cenário de instantâneo de disco Olá é consistência do sistema de ficheiros e um Estado de disco com consistência de aplicações. tópico de consistência Olá mencionado na secção de Olá _consistência de dados SAP HANA quando tirar instantâneos de armazenamento_ posteriormente neste artigo. Funcionalidades e restrições do serviço de cópia de segurança do Azure relacionados com tooSAP HANA as cópias de segurança também são abordadas neste artigo.

![Esta ilustração mostra as opções para colocar um SAP HANA ficheiro de cópia de segurança dentro Olá VM](media/sap-hana-backup-guide/image002.png)

Esta ilustração mostra as opções para colocar uma cópia de segurança de ficheiros de SAP HANA dentro Olá VM e, em seguida, armazenar ficheiros de cópia de segurança HANA algures senão utilizando ferramentas diferentes. Fazer uma cópia de segurança HANA necessita de mais tempo do que uma solução de cópia de segurança baseada em instantâneo, mas tem vantagens relativamente a integridade e consistência. Obter mais detalhes são fornecidos neste artigo.

![Este figura mostra um potencial futuro SAP HANA cópia de segurança cenário](media/sap-hana-backup-guide/image003.png)

Este figura mostra um potencial futuro SAP HANA cópia de segurança cenário. Se SAP HANA permitido fazer cópias de segurança de uma replicação secundária, deverá adicionar a opções adicionais para estratégias de cópia de segurança. Atualmente, não é possível tooa post no Olá SAP HANA Wiki de acordo com:

_&quot;É possível tootake cópias de segurança no lado secundário Olá?_

_Não, atualmente pode apenas colocar dados e iniciar as cópias de segurança no lado primário Olá. Se estiver ativada a cópia de segurança automática de registos, após toohello alimentar de lado secundária, cópias de segurança de registo de Olá automaticamente serão escritas não existe.&quot;_

## <a name="sap-resources-for-hana-backup"></a>Recursos SAP para cópia de segurança HANA

### <a name="sap-hana-backup-documentation"></a>Documentação de cópia de segurança de SAP HANA

- [Introdução tooSAP HANA administração](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Planear a sua estratégia de recuperação e cópia de segurança](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [Agendar cópia de segurança HANA utilizando ABAP DBACOCKPIT](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [Cópias de segurança de dados agendadas (SAP HANA Cockpit)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- FAQ sobre SAP HANA de cópia de segurança no [1642148 de nota SAP](https://launchpad.support.sap.com/#/notes/1642148)
- FAQ sobre instantâneos de base de dados e armazenamento de SAP HANA no [2039883 de nota SAP](https://launchpad.support.sap.com/#/notes/2039883)
- Sistemas de ficheiros de rede unsuitable para cópia de segurança e recuperação no [1820529 de nota SAP](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Por que motivo SAP cópia de segurança HANA?

Storage do Azure oferece a disponibilidade e fiabilidade Box Olá (consulte [introdução tooMicrosoft Storage do Azure](../../../storage/common/storage-introduction.md) para obter mais informações sobre o storage do Azure).

Olá mínimo para &quot;cópia de segurança&quot; é toorely no Olá SLA do Azure, Olá manter ficheiros de registo e dados de SAP HANA no servidor de SAP HANA Azure VHDs toohello anexado VM. Esta abordagem abrange falhas VM, mas não potenciais danos toohello SAP HANA dados e ficheiros de registo ou erros lógicos, como a eliminação de dados ou ficheiros acidentalmente. As cópias de segurança também são necessárias para compatibilidade ou motivos legais. Em suma, não há sempre uma necessidade para cópias de segurança de SAP HANA.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Como tooverify correcção de cópia de segurança de SAP HANA
Quando é recomendado utilizar instantâneos de armazenamento, executar um restauro de teste num sistema diferente. Esta abordagem fornece uma forma tooensure uma cópia de segurança está corretos e internos processos de trabalho de cópia de segurança e restauro, conforme esperado. Apesar de ser um impacto significativo hurdle no local, é muito mais fácil tooaccomplish na nuvem de Olá, fornecendo temporariamente os recursos necessários para esta finalidade.

Tenha em atenção que efetuar um restauro simple e a verificar se HANA está ativo e em execução não são suficiente. Idealmente, um deve executar um toobe de verificação de consistência de tabela se que a base de dados de Olá restaurada é adequado. SAP HANA oferece vários tipos de verificações de consistência descritos [1977584 de nota SAP](https://launchpad.support.sap.com/#/notes/1977584).

Também pode encontrar informações sobre a verificação de consistência de tabela Olá no site SAP Olá em [tabela e verificações de consistência do catálogo](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Para cópias de segurança de ficheiros padrão, um restauro de teste não é necessário. Existem duas ferramentas de SAP HANA ajudam toocheck que cópia de segurança pode ser utilizada para restauro: hdbbackupdiag e hdbbackupcheck. Consulte [manualmente a verificar se a recuperação é possível](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) para obter mais informações sobre estas ferramentas.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Os profissionais de TI e contras de cópia de segurança HANA versus instantâneos de armazenamento

SAP & #39 t conceder preferência tooeither HANA cópia de segurança; versus instantâneos de armazenamento. Lista os respetivos os profissionais de TI e contras, para que um pode determinar que toouse dependendo da situação de Olá e tecnologia de armazenamento disponível (consulte [planear a cópia de segurança e a estratégia de recuperação](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

No Azure, lembre-se de que de facto de Olá Olá não de funcionalidade de instantâneos do blob do Azure &#39; t garantir a consistência do sistema de ficheiros (consulte [utilizar instantâneos de blob com o PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Olá secção seguinte, _consistência de dados SAP HANA quando tirar instantâneos de armazenamento_, descreve algumas considerações relativas a esta funcionalidade.

Além disso, tem um toounderstand Olá implicações de faturação ao trabalhar com frequência com instantâneos do blob, conforme descrito neste artigo: [compreender como instantâneos acumular encargos](/rest/api/storageservices/understanding-how-snapshots-accrue-charges)— se encontra &#39; t como óbvios como utilizar o Azure discos virtuais.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Consistência de dados SAP HANA quando tirar instantâneos de armazenamento

Consistência de aplicações e de sistema de ficheiros é um problema complexo quando tirar instantâneos de armazenamento. problemas de tooavoid de forma mais fácil Olá iriam ser tooshut para baixo de SAP HANA ou, talvez mesmo Olá máquina todo. Um encerramento pode ser doable com uma demonstração ou criar protótipos ou até mesmo um sistema de desenvolvimento, mas não é uma opção para um sistema de produção.

No Azure, um tem tookeep em atenção que Olá não de funcionalidade de instantâneos do blob do Azure &#39; t garantir a consistência do sistema de ficheiros. Ajustar funciona no entanto, utilizando Olá SAP HANA instantâneo funcionalidade, desde que não há um único disco virtual envolvidos. Mas, mesmo com um único disco itens adicionais têm toobe marcada. [SAP nota 2039883](https://launchpad.support.sap.com/#/notes/2039883) tem informações importantes sobre as cópias de segurança de SAP HANA através de instantâneos de armazenamento. Por exemplo, menciona que, com o sistema de ficheiros XFS Olá, é necessário toorun **xfs\_fixar** antes de iniciar um armazenamento de instantâneos tooguarantee consistência (consulte [xfs\_freeze(8) - man do Linux página](https://linux.die.net/man/8/xfs_freeze) para obter detalhes sobre **xfs\_fixar**).

tópico de Olá de consistência fica ainda mais difícil caso em que um sistema de ficheiro único abranja vários discos/volumes. Por exemplo, ao utilizar mdadm ou LVM e striping. Olá nota SAP mencionado Estados:

_&quot;Mas tenha em atenção que o sistema de armazenamento Olá tem consistência tooguarantee e/s ao criar um instantâneo de armazenamento por volume de dados SAP HANA, ou seja, tem de ser uma operação atómica snapshotting de um volume de dados específicos do serviço de SAP HANA.&quot;_

Pressupondo que há um sistema de ficheiros XFS expansão quatro discos virtuais do Azure, hello passos seguintes fornecem um instantâneo consistente que representa a área de dados HANA Olá:

- Preparar o instantâneo HANA
- Fixar o sistema de ficheiros de Olá (por exemplo, utilizar **xfs\_fixar**)
- Criar todos os instantâneos do blob necessários no Azure
- Libertar poder por sistema de ficheiros de Olá
- Confirme o instantâneo HANA Olá

Recomenda-se toouse Olá procedimento acima todos os casos toobe no lado seguro Olá, independentemente do sistema de ficheiros. Ou, se se tratar de um único disco ou striping, através de mdadm ou LVM entre múltiplos discos.

É importante tooconfirm Olá HANA instantâneo. Toohello devida &quot;cópia ao escrever,&quot; SAP HANA poderão não requerer o espaço em disco adicional nisto preparar instantâneo modo. &#39; s toostart também não é possível novas cópias de segurança até que o instantâneo de SAP HANA Olá é confirmado.

Serviço de cópia de segurança do Azure utiliza tootake de extensões de VM do Azure care of Olá consistência do sistema de ficheiros. Estas extensões VM não estão disponíveis para utilização autónoma. Um ainda tem toomanage consistência de SAP HANA. Consulte o artigo relacionado Olá [SAP HANA Azure Backup no nível de ficheiro](sap-hana-backup-file-level.md) para obter mais informações.

### <a name="sap-hana-backup-scheduling-strategy"></a>Estratégia de agendamento de cópia de segurança de SAP HANA

artigo de SAP HANA Olá [planear a cópia de segurança e a estratégia de recuperação](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) Estados uma basic planear toodo cópias de segurança:

- Armazenamento de instantâneos (diário)
- Cópia de segurança de dados completo com o formato de ficheiro ou bacint (uma vez por semana)
- Cópias de segurança do registo automática

Opcionalmente, um foi possível ir completamente sem instantâneos de armazenamento pode ser substituídos HANA diferenças das cópias de segurança, como as cópias de segurança incrementais ou diferenciais (consulte [cópias de segurança diferencial](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)).

Guia de administração de HANA Olá fornece uma lista de exemplo. -Sugere que um recuperar ponto do SAP HANA tooa específico no tempo utilizando Olá seguinte sequência das cópias de segurança:

1. Cópia de segurança de dados completa
2. Cópia de segurança diferencial
3. Cópia de segurança incremental 1
4. Cópia de segurança incremental 2
5. Cópias de segurança do registo

Relativamente a um agendamento exato como toowhen e com que frequência deverá ocorrer um tipo específico de cópia de segurança, não é possível toogive orientação geral — é demasiado específicas do cliente e depende ocorrem quantos alterações de dados no sistema de Olá. Uma recomendação básica do lado do SAP, que pode ser visto como orientação geral, é toomake um HANA cópia de segurança completa, uma vez por semana.
Sobre cópias de segurança de registo, consulte a documentação de SAP HANA Olá [cópias de segurança do registo](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP recomenda também fazer alguma manutenção de Olá catálogo cópia de segurança tookeep a crescer infinitamente (consulte [Housekeeping de catálogo de cópias de segurança e de armazenamento de cópia de segurança](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>Ficheiros de configuração de SAP HANA

Conforme indicado na Olá FAQ no [1642148 de nota SAP](https://launchpad.support.sap.com/#/notes/1642148), ficheiros de configuração de SAP HANA Olá não fazem parte de uma cópia de segurança HANA padrão. Não são essencial toorestore um sistema. Olá HANA foi possível alterar a configuração manualmente após o restauro de Olá. No caso de um gostaria tooget Olá configuração personalizada mesma durante o processo de restauro de Olá, é necessário tooback dos ficheiros de configuração de HANA Olá separadamente.

Se padrão HANA as cópias de segurança são tooa dedicado sistema de ficheiros de cópia de segurança de HANA, um também pode copiar toohello de ficheiros de configuração de Olá mesmo sistema de ficheiros de cópia de segurança e, em seguida, copie tudo como destino de armazenamento final toohello em conjunto esporádico armazenamento de Blobs.

### <a name="sap-hana-cockpit"></a>SAP HANA Cockpit

SAP HANA Cockpit oferece a possibilidade de Olá da monitorização e gestão de SAP HANA através de um browser. Também permite que o processamento de cópias de segurança de SAP HANA e, por conseguinte, podem ser utilizado como uma alternativa tooSAP HANA Studio e ABAP DBACOCKPIT (consulte [SAP HANA Cockpit](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) para obter mais informações).

![Esta ilustração mostra Olá ecrã de administração do SAP HANA Cockpit da base de dados](media/sap-hana-backup-guide/image004.png)

Este figura mostra Olá ecrã de administração do SAP HANA Cockpit da base de dados e o mosaico de cópia de segurança de Olá no Olá à esquerda. Mosaico de cópia de segurança Olá ver necessita de permissões de utilizador adequada para a conta de início de sessão.

![As cópias de segurança podem ser monitorizadas no SAP HANA Cockpit enquanto estiverem em curso](media/sap-hana-backup-guide/image005.png)

As cópias de segurança podem ser monitorizadas no SAP HANA Cockpit enquanto estiverem em curso e, assim que estiver concluído, todos os detalhes de cópia de segurança de Olá estão disponíveis.

![Um exemplo utilizando o Firefox numa VM do Azure SLES 12 com ambiente de trabalho Gnome](media/sap-hana-backup-guide/image006.png)

capturas de ecrã anterior Olá foram efetuadas a partir de uma VM do Windows Azure. Este é um exemplo utilizando o Firefox numa VM do Azure SLES 12 com ambiente de trabalho Gnome. Mostra agendas cópia de segurança de SAP HANA toodefine de opção Olá no Cockpit do SAP HANA. Como um também pode ver, sugere data/hora como um prefixo para ficheiros de cópia de segurança de Olá. No Studio do SAP HANA, Olá predefinido prefixo é constituído pelos &quot;concluída\_dados\_cópia de segurança&quot; ao efetuar uma cópia de segurança completa. É recomendado utilizar um prefixo exclusivo.

### <a name="sap-hana-backup-encryption"></a>Encriptação de cópias de segurança de SAP HANA

SAP HANA oferece a encriptação de dados e de registo. Se os dados de SAP HANA e de registo não estão encriptados, em seguida, as cópias de segurança Olá também não estão encriptadas. Está a funcionar toohello cliente toouse alguma forma de cópias de segurança de solução de terceiros tooencrypt Olá SAP HANA. Consulte [dados e encriptação de Volume de registo](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind mais informações sobre a encriptação de SAP HANA.

No Microsoft Azure, um cliente poderia utilizar Olá tooencrypt de funcionalidade de encriptação de VM do IaaS. Por exemplo, um utilizar dados dedicado discos anexados toohello VM, que são utilizado toostore cópias de segurança de SAP HANA, em seguida, faça cópias destes discos.

Serviço de cópia de segurança do Azure pode processar VMs/discos encriptados (consulte [como tooback cópias de segurança e restauro encriptados máquinas virtuais com o Backup do Azure](../../../backup/backup-azure-vms-encryption.md)).

Outra opção teria de ser toomaintain Olá SAP HANA VM e os respetivos discos sem encriptação e armazenar ficheiros de cópia de segurança de SAP HANA Olá numa conta do storage para o qual foi ativada a encriptação (consulte [encriptação do serviço de armazenamento do Azure para dados Inativos](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Configuração de teste

### <a name="test-virtual-machine-on-azure"></a>Máquina Virtual de teste no Azure

Uma instalação de SAP HANA na VM do Azure GS5 foi utilizada para Olá seguintes testes de cópia de segurança/restauro.

![Esta ilustração mostra parte Olá descrição geral do portal do Azure para a VM de teste HANA Olá](media/sap-hana-backup-guide/image007.png)

Esta ilustração mostra parte Olá descrição geral do portal do Azure para a VM de teste do Olá HANA.

### <a name="test-backup-size"></a>Tamanho de cópia de segurança de teste

![Este figura foi executada a partir da consola de cópia de segurança de Olá no HANA Studio e mostra o tamanho do ficheiro de cópia de segurança Olá de 229 GB para o servidor de índice HANA Olá](media/sap-hana-backup-guide/image008.png)

Uma tabela fictício foi preenchida cópias de segurança com dados tooget um tamanho de cópia de segurança de dados total mais de 200 GB tooderive realistas de dados de desempenho. figura Olá foi executada a partir da consola de cópia de segurança de Olá no HANA Studio e mostra o tamanho do ficheiro de cópia de segurança Olá de 229 GB para o servidor de índice Olá HANA. Para testes de Olá, foi utilizado o prefixo de cópia de segurança Olá predefinido "COMPLETE_DATA_BACKUP" no Studio do SAP HANA. Nos sistemas de produção real, deve ser definido um prefixo mais útil. SAP HANA Cockpit sugere data/hora.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Teste ferramenta toocopy diretamente ficheiros tooAzure armazenamento

ficheiros de cópia de segurança de SAP HANA de tootransfer diretamente o armazenamento de BLOBs de tooAzure ou partilhas de ficheiros do Azure, Olá blobxfer ferramenta foi utilizada porque suporta tanto destinos e podem ser facilmente integrados em scripts de automatização devido tooits interface de linha de comandos. Olá blobxfer ferramenta está disponível em [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Estimativa do tamanho de cópia de segurança de teste

É importante tooestimate Olá cópia de segurança o tamanho de SAP HANA. Esta estimativa ajuda tooimprove desempenho ao definir o tamanho de ficheiro de cópia de segurança máximo Olá para um número de ficheiros de cópia de segurança, tooparallelism devida durante uma cópia de ficheiros. (Os detalhes são explicados posteriormente neste artigo.) Um também tem de decidir se toodo um completo de cópia de segurança ou de um delta de cópia de segurança (incremental ou diferencial).

Felizmente, há uma instrução SQL simple que calcula o tamanho de Olá dos ficheiros de cópia de segurança de Olá: **selecione \* do M\_cópia de segurança\_tamanho\_estimativas** (consulte [ Olá estimativa espaço necessário no hello sistema de ficheiros para uma cópia de segurança de dados](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![saída de Olá da declaração SQL corresponde quase exatamente Olá real tamanho da cópia de segurança de dados completa de Olá no disco](media/sap-hana-backup-guide/image009.png)

Sistema de teste de Olá, saída Olá da declaração SQL corresponde quase exatamente Olá real tamanho da cópia de segurança de dados completa de Olá no disco.

### <a name="test-hana-backup-file-size"></a>Tamanho do ficheiro de cópia de segurança de HANA de teste

![consola de cópia de segurança do Olá HANA Studio permite um tamanho de ficheiro máximo de Olá de toorestrict dos ficheiros de cópia de segurança HANA](media/sap-hana-backup-guide/image010.png)

consola de cópia de segurança do Olá HANA Studio permite um tamanho de ficheiro máximo de Olá de toorestrict dos ficheiros de cópia de segurança HANA. Num ambiente de exemplo de Olá, essa funcionalidade torna possível tooget várias cópias de segurança mais pequenas ficheiros em vez de um ficheiro de cópia de segurança de 230 GB. Ficheiro mais pequeno tem um impacto significativo no desempenho (consulte o artigo relacionado Olá [SAP HANA Azure Backup no nível de ficheiro](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Resumo

Com base nos resultados de teste de Olá Olá tabelas a seguir mostra os profissionais de TI e contras de soluções tooback segurança uma base de dados SAP HANA em execução em máquinas virtuais do Azure.

**Cópia de segurança sistema de ficheiros do SAP HANA toohello e copie cópia de segurança, posteriormente, ficheiros toohello final destino de cópia de segurança**

|Solução                                           |Profissionais de TI                                 |Contras                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Manter cópias de segurança HANA em discos VM                      |Sem esforços de gestão adicional     |Eats local espaço em disco VM           |
|Armazenamento de tooblob Blobxfer ferramenta toocopy ficheiros de cópia de segurança |Paralelismo toocopy vários ficheiros, armazenamento de BLOBs frios toouse de escolha | Manutenção de ferramenta adicionais e de script personalizado | 
|Cópia de BLOBs através do Powershell ou a CLI                    |Nenhuma ferramenta adicional necessária, pode ser efetuada através do Azure Powershell ou a CLI |processo manual, o cliente tem tootake care of scripting e a gestão de blobs copiados do restauro|
|Copiar tooNFS partilha                                  |Pós-processamento de ficheiros de cópia de segurança em outro VM sem impacto no servidor HANA Olá|Processo de cópia lenta|
|Blobxfer cópia tooAzure serviço de ficheiros                |Não eat espaço no locais discos VM|Não existem direta escrever suporte por restrição de cópia de segurança, tamanho HANA da partilha de ficheiros atualmente em 5 TB|
|Agente de cópia de segurança do Azure                                 | Seria solução preferencial         | Atualmente não está disponível no Linux    |



**Cópia de segurança SAP HANA com base nos instantâneos de armazenamento**

|Solução                                           |Profissionais de TI                                 |Contras                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Serviço de cópia de segurança do Azure                               | Permite a cópia de segurança VM com base nos instantâneos do blob | Quando não utilizar o restauro ao nível do ficheiro, necessita de criação de Olá de uma nova VM para o processo de restauro de Olá, em seguida, implica necessidade de Olá de uma nova chave de licença de SAP HANA|
|Instantâneos do manual blob                              | Flexibilidade toocreate e restauro VM discos específicos sem alterar Olá ID exclusivo da VM|Todas as tarefas manuais, que tem toobe efetuada pelo cliente de Olá|

## <a name="next-steps"></a>Passos seguintes
* [SAP HANA Backup do Azure no nível de ficheiro](sap-hana-backup-file-level.md) descreve a opção de cópia de segurança baseada em ficheiros de Olá.
* [Cópia de segurança de SAP HANA com base nos instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md) descreve Olá baseado no instantâneo cópia de segurança opção de armazenamento.
* toolearn como tooestablish elevada disponibilidade e o plano de recuperação de desastres do SAP HANA no Azure (instâncias de grande), consulte [SAP HANA (instâncias de grande) elevada disponibilidade e recuperação após desastre no Azure](hana-overview-high-availability-disaster-recovery.md).
