---
title: desempenho aaaHigh Premium Storage e o Azure discos geridos para VMs | Microsoft Docs
description: "Saiba mais sobre armazenamento de Premium de elevado desempenho e os discos geridos para VMs do Azure. Azure série DS, série DSv2-série, série GS e VMs de série Fs suporta o Premium Storage."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 5f08e615869ed59a9d80d798ec191dd4d3abc3e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Armazenamento Premium de elevado desempenho e discos geridos para VMs
Armazenamento Premium do Azure fornece suporte de disco de elevado desempenho, baixa latência para máquinas virtuais (VMs) com a entrada/saída (e/s)-as cargas de trabalho que consomem muita. Discos VM que utilizam o armazenamento Premium armazenam dados em unidades de estado sólido (SSDs). tootake partido de velocidade de Olá e o desempenho dos discos de armazenamento premium, pode migrar existente tooPremium de discos VM armazenamento.

No Azure, pode anexar vários premium storage discos tooa VM. Utilizar vários discos fornece as suas aplicações segurança too256 TB de armazenamento por VM. Armazenamento Premium, as suas aplicações podem alcançar 80.000 operações de e/s por segundo (IOPS) por VM e um débito de disco de cópia de segurança too2, 000 megabytes por segundo (MB/s) por VM. As operações de leitura dão-lhe latências muito baixos.

Armazenamento Premium, Azure oferece a capacidade de Olá tootruly comparação de precisão e shift pedir o seu trabalho as aplicações empresariais, como nuvem de toohello de farms do Dynamics AX, o Dynamics CRM, o Exchange Server, o SAP Business Suite e o SharePoint. Pode executar cargas de trabalho de base de dados de desempenho intensivas em aplicações como o SQL Server, Oracle, MongoDB, MySQL e Redis, que necessitam de elevado desempenho consistente e a latência baixa.

> [!NOTE]
> Para Olá melhor desempenho para a sua aplicação, recomendamos que migrar qualquer disco da VM que exija elevada IOPS tooPremium armazenamento. Se o disco não necessita de IOPS elevado, pode ajudar os custos de limite ao mantê-la no armazenamento do Azure standard. No armazenamento standard, os dados de disco da VM são armazenados em unidades de disco rígido (HDDs), em vez de em SSDs.
> 

O Azure disponibiliza duas formas discos de armazenamento premium toocreate para VMs:

* **Discos não geridos**

    o método original Olá é discos toouse não gerido. Um disco não geridos, gerir as contas de armazenamento de Olá que utiliza ficheiros de disco rígido virtual (VHD) de Olá toostore que correspondem tooyour discos da VM. Ficheiros VHD são armazenados como blobs de páginas em contas do storage do Azure. 

* **Discos geridos**

    Quando escolhe [Azure geridos discos](../../virtual-machines/windows/managed-disks-overview.md), Azure gere contas de armazenamento de Olá que utilizar para os discos VM. Especifique o tipo de disco Olá (Premium ou Standard) e o tamanho de Olá do disco de Olá que precisa. Azure cria e gere o disco de Olá por si. Não tem tooworry sobre colocação discos Olá num vários tooensure de contas de armazenamento que permanecem dentro dos limites de escalabilidade para as contas do storage. Azure processa que por si.

Recomendamos que escolha discos geridos, tootake partido das respetivas funcionalidades várias.

tooget iniciado com o Premium Storage, [criar a sua conta do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/). 

Para obter informações sobre como migrar a sua tooPremium de VMs de armazenamento existente, consulte [converter uma VM do Windows a partir de discos de toomanaged discos não gerido](../../virtual-machines/windows/convert-unmanaged-to-managed-disks.md) ou [converter uma VM com Linux a partir de discos de toomanaged discos não gerido](../../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Armazenamento Premium está disponível na maior parte das regiões. Para Olá obter lista de regiões disponíveis, no [serviços do Azure por região](https://azure.microsoft.com/regions/#services), olhos regiões Olá na qual suportado VMs de série de tamanho de suporte Premium (séries DS, série DSV2-série, série GS e VMs Fs-série) são suportados.
> 

## <a name="features"></a>Funcionalidades

Seguem-se algumas das funcionalidades de Olá do Premium Storage:

* **Discos de armazenamento Premium**

    Premium Storage suporta discos de VM que podem ser anexados a série de tamanho toospecific VMs. Armazenamento Premium suporta-série DS, série DSv2-série GS série, série Ls e série Fs VMs. Tem uma opção de sete tamanhos de discos: P4 (32GB), P6 (64GB), P10 (128GB), P20 (GB de 512), P30 (1024GB), P40 (GB de 2048), P50 (4095GB). P4 e tamanhos de disco P6 ainda só são suportados para discos geridos. Cada tamanho do disco tem as suas próprias especificações de desempenho. Dependendo dos requisitos de aplicação, poderá anexar um ou mais discos tooyour VM. Iremos descrever as especificações de Olá com maior detalhe em [metas de desempenho e escalabilidade do armazenamento Premium](#scalability-and-performance-targets).

* **Blobs de páginas Premium**

    Armazenamento Premium suporta blobs de páginas. Utilize a página blobs toostore persistente, não geridos discos para as VMs do Premium Storage. Ao contrário do armazenamento do Azure standard, armazenamento Premium não suportam blobs de blocos, blobs, ficheiros, tabelas ou filas de acréscimo. Os blobs de páginas Premium suporta tamanhos de seis P10 tooP50 e P60 (8191GiB). Blob de páginas P60 Premium não é suportado toobe anexado como discos VM. 

    Qualquer objeto colocado numa conta de armazenamento premium será um blob de página. blob de página Olá ajusta tooone de Olá suportado tamanhos aprovisionados. É por isso uma conta de armazenamento premium não se destina toobe utilizado blobs muito pequena toostore.

* **Conta de armazenamento Premium**

    toostart utilizar o Premium Storage, criar uma conta de armazenamento premium para os discos não geridos. No Olá [portal do Azure](https://portal.azure.com), toocreate uma conta de armazenamento premium, escolha Olá **Premium** camada de desempenho. Selecione Olá **armazenamento localmente redundante (LRS)** opção de replicação. Também pode criar uma conta do premium storage ao definir o tipo de Olá demasiado**Premium_LRS** dos Olá seguintes localizações:
    * [API REST do Storage](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (versão 2014-02-14 ou uma versão posterior)
    * [API de REST de gestão do serviço](http://msdn.microsoft.com/library/azure/ee460799.aspx) (versão 2014-10-01 ou uma versão posterior; para implementações clássicas do Azure)
    * [Azure API de REST do fornecedor de recursos de armazenamento](https://docs.microsoft.com/rest/api/storagerp) (para implementações do Azure Resource Manager)
    * [O Azure PowerShell](/powershell/azureps-cmdlets-docs.md) (versão 0.8.10 ou uma versão posterior)

    toolearn sobre limites de conta de armazenamento premium, consulte [metas de desempenho e escalabilidade do armazenamento Premium](#premium-storage-scalability-and-performance-targets).

* **Armazenamento localmente redundante Premium**

    Uma conta do premium storage suporta armazenamento apenas localmente redundante como opção de replicação de Olá. Armazenamento localmente redundante mantém três cópias dos dados de Olá numa única região. Regional recuperação de desastres, tem de copiar os discos VM numa região diferente utilizando [cópia de segurança do Azure](../../backup/backup-introduction-to-azure-backup.md). Também tem de utilizar uma conta de armazenamento georredundante (GRS) como o Cofre de cópia de segurança de Olá. 

    Azure utiliza a conta de armazenamento como um contentor para os discos não geridos. Quando criar uma Azure-série DS, série DSv2-série GS série, ou Fs-série VM com discos não geridos e selecione uma conta de armazenamento premium, o sistema operativo e os discos de dados são armazenados na conta do storage.

## <a name="supported-vms"></a>VMs suportadas
Armazenamento Premium suporta-série DS, série DSv2-série GS série, série Ls e série Fs VMs. Pode utilizar discos de armazenamento standard e premium com estes tipos VM. Não é possível utilizar discos de armazenamento premium com a série VM que não é Premium compatível com o armazenamento.

Para obter informações sobre tipos VM e tamanhos do Azure para Windows, consulte [tamanhos de Windows VM](../../virtual-machines/virtual-machines-windows-sizes-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para obter informações sobre os tamanhos no Azure e tipos VM Linux, consulte [tamanhos de VM com Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Estas são algumas das funcionalidades de Olá do Olá-série DS, série DSv2-série, série GS, série Ls e série Fs VMs:

* **Serviço em nuvem**

    Pode adicionar o serviço em nuvem do DS-série VMs tooa que tenha apenas as VMs de série DS. Não adicione VMs-série DS tooan serviço em nuvem existente com qualquer tipo que não sejam-série DS VMs. Pode migrar os seus VHDs tooa novo serviço em nuvem existente que é executado apenas as VMs de série DS. Se quiser toouse Olá mesmo endereço IP virtual para Olá novo serviço em nuvem que aloja as VMs de série DS, utilize [endereços IP reservados](../../virtual-network/virtual-networks-instance-level-public-ip.md). Série GS VMs podem ser adicionadas serviço em nuvem existente tooan que tenha apenas as VMs de série GS.

* **Disco do sistema operativo**

    Pode configurar a VM do Premium Storage toouse um premium ou um disco de sistema operativo padrão. Para uma experiência otimizada Olá, recomendamos que utilize um disco de sistema operativo baseado no armazenamento Premium.

* **Discos de dados**

    Pode utilizar o premium e Olá de discos padrão na mesma VM do Premium Storage. Armazenamento Premium, pode aprovisionar uma VM e anexar vários toohello de discos de dados persistentes VM. Se necessário, a capacidade de Olá tooincrease e o desempenho de volume Olá, pode stripe em todos os discos.

    > [!NOTE]
    > Se lhe stripe discos de dados de armazenamento premium utilizando [espaços de armazenamento](http://technet.microsoft.com/library/hh831739.aspx), configurar os espaços de armazenamento com 1 coluna para cada disco que utiliza. Caso contrário, global o desempenho do volume de Olá repartido poderá ser menor do que o esperado devido a distribuição desigual de tráfego entre discos Olá. Por predefinição, no Gestor de servidores, pode configurar colunas para a cópia de segurança too8 discos. Se tiver mais de 8 discos, utilize o volume do PowerShell toocreate Olá. Especifique manualmente o número de Olá de colunas. Caso contrário, Olá da IU do Gestor de servidor continua toouse 8 colunas, mesmo que tenha mais discos. Por exemplo, se tiver 32 discos num conjunto único stripe, especifique 32 colunas. número de Olá toospecify de colunas Olá utilizações de disco virtual, no Olá [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) cmdlet do PowerShell, utilize Olá *NumberOfColumns* parâmetro. Para obter mais informações, consulte [descrição geral dos espaços de armazenamento](http://technet.microsoft.com/library/hh831739.aspx) e [perguntas mais frequentes sobre espaços de armazenamento](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Cache**

    VMs na série de tamanho de Olá que suporta o Premium Storage tem uma capacidade de colocação em cache exclusiva para níveis elevados de débito e latência. Olá, capacidade de colocação em cache excede o desempenho do disco de armazenamento premium subjacente. Pode definir o disco de Olá a colocação em cache política nos discos de armazenamento premium demasiado**ReadOnly**, **ReadWrite**, ou **nenhum**. Olá predefinido disco política de colocação em cache é **ReadOnly** para todos os discos de dados premium, e **ReadWrite** para discos de sistema operativo. Para um desempenho ideal para a sua aplicação, utilize Olá corrigir a definição de cache. Por exemplo, para discos de dados de leitura pesado ou só de leitura, tais como ficheiros de dados do SQL Server, defina disco Olá a colocação em cache política demasiado**ReadOnly**. Pesado de escrita ou só de escrita para discos de dados, tais como ficheiros de registo do SQL Server, defina disco Olá a colocação em cache política demasiado**nenhum**. toolearn mais informações sobre a otimizar o seu design com o Premium Storage, consulte [conceção para desempenho com o Premium Storage](storage-premium-storage-performance.md).

* **Análise**

    desempenho de VM tooanalyze utilizando discos no armazenamento Premium, ative os diagnósticos VM na Olá [portal do Azure](https://portal.azure.com). Para obter mais informações, consulte [monitorização VM do Azure com a extensão de diagnóstico do Azure](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    desempenho de disco toosee, utilizar ferramentas com base no sistema operativo como [Monitor de desempenho do Windows](https://technet.microsoft.com/library/cc749249.aspx) para VMs do Windows e Olá [iostat](http://linux.die.net/man/1/iostat) comando para VMs com Linux.

* **Desempenho e limites de dimensionamento VM**

    Cada tamanho da VM de armazenamento Premium-suportado tem limites de escala e as especificações de desempenho de IOPS, largura de banda e Olá número de discos que podem ser anexados por VM. Quando utilizar discos de armazenamento premium com VMs, certifique-se de que existe espaço suficiente IOPS e largura de banda no seu tráfego de disco de toodrive VM.

    Por exemplo, uma VM STANDARD_DS1 tem uma largura de banda dedicada de 32 MB/s para o tráfego de disco de armazenamento premium. Um disco de armazenamento premium P10 pode fornecer uma largura de banda de 100 MB/s. Se um disco de armazenamento premium P10 toothis anexado VM, pode aceder apenas cópias de segurança too32 MB/s. Não é possível utilizar o Olá que máximo 100 MB/s desse disco de P10 Olá pode fornecer.

    Atualmente, hello VM maior na Olá-série DS é Olá Standard_DS15_v2. Olá Standard_DS15_v2 pode fornecer segurança too960 MB/s através de todos os discos. Olá VM maior na Olá série GS é Olá Standard_GS5. Olá Standard_GS5 pode fornecer segurança too2, 000 MB/s em todos os discos.

    Tenha em atenção que estes limites para o tráfego de disco apenas. Estes limites não incluem acertos na cache e o tráfego de rede. Uma largura de banda separada está disponível para o tráfego de rede VM. Largura de banda para tráfego de rede é diferente da largura de banda de Olá dedicado utilizada pelos discos de armazenamento premium.

    Para Olá informações mais atualizadas sobre IOPS máximo e de débito (largura de banda) para as VMs de armazenamento Premium-suportados, consulte [tamanhos de Windows VM](/azure/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tamanhos de VM com Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Para obter mais informações sobre os discos de armazenamento premium e os respetivos limites IOPS e de débito, consulte a tabela de Olá na secção seguinte Olá.

## <a name="scalability-and-performance-targets"></a>Metas de escalabilidade e desempenho
Nesta secção, iremos descrevem tooconsider de destinos de desempenho e escalabilidade Olá quando utilizar o armazenamento Premium.

Contas de armazenamento Premium têm Olá seguintes destinos de escalabilidade:

| Capacidade total de conta | Largura de banda total de uma conta de armazenamento localmente redundante |
| --- | --- | 
| Capacidade do disco: 35 TB <br>Capacidade de instantâneos: 10 TB | Cópia de segurança too50 gigabits por segundo para entrada<sup>1</sup> + saída<sup>2</sup> |

<sup>1</sup> todos os dados (pedidos) que são enviados tooa conta de armazenamento

<sup>2</sup> todos os dados (respostas) que são recebidos a partir de uma conta de armazenamento

Para obter mais informações, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md).

Se estiver a utilizar contas de armazenamento premium para os discos não geridos e a aplicação excede os objetivos de escalabilidade Olá de uma única conta de armazenamento, pode querer toomigrate toomanaged discos. Se não quiser toomigrate toomanaged discos, crie várias contas do storage toouse a aplicação. Em seguida, particionar os dados entre essas contas de armazenamento. Por exemplo, se quiser discos de 51 TB tooattach através de várias VMs, distribuídos-los por duas contas de armazenamento. 35 TB é o limite de Olá para uma conta de armazenamento premium único. Certifique-se de que uma conta de armazenamento premium único nunca tem mais de 35 TB de discos aprovisionados.

### <a name="premium-storage-disk-limits"></a>Limites de disco de armazenamento Premium
Quando aprovisionar um disco de armazenamento premium, o tamanho do disco de Olá Olá determina Olá IOPS máximo e de débito (largura de banda). O Azure disponibiliza sete tipos de discos de armazenamento premium: P4 (geridos discos apenas), P6 (geridos discos apenas), P10, P20, P30, P40 e P50. Cada tipo de disco de armazenamento premium tem limites específicos para o IOPS e débito. Os limites para os tipos de disco Olá descritos Olá a tabela seguinte:

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPs por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Débito por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 

> [!NOTE]
> Certifique-se de largura de banda suficiente disponível no seu tráfego de disco de toodrive VM, conforme descrito em [VMs de armazenamento Premium-suportado](#premium-storage-supported-vms). Caso contrário, o débito de disco e o IOPS é restrita toolower valores. Débito máximo e IOPS baseiam-se nos limites VM Olá, não nos limites de disco de Olá descritos Olá anterior a tabela.  
> 
> 

Seguem-se tooknow alguns pontos importantes sobre metas de desempenho e escalabilidade do armazenamento Premium:

* **Capacidade de aprovisionamento e o desempenho**

    Quando aprovisiona um disco de armazenamento premium, ao contrário do armazenamento padrão, são garantida Olá capacidade, IOPS e débito desse disco. Por exemplo, se criar um disco de P50, Azure Aprovisiona capacidade de armazenamento 4,095 GB, o 7.500 IOPS e 250 MB/s débito para esse disco. A aplicação pode utilizar a totalidade ou parte da capacidade de Olá e o desempenho.

* **Tamanho do disco**

    Azure maps Olá toohello de tamanho (arredondar por excesso) de disco mais próximo da opção de disco de armazenamento premium, conforme especificado na tabela de Olá no Olá anterior a secção. Por exemplo, um tamanho de disco de 100 GB é classificado como uma opção de P10. Pode efetuar cópias de segurança too500 IOPS, com cópia de segurança too100 débito de MB/s. Da mesma forma, um disco de tamanho que 400 GB é classificado como um P20. Pode efetuar a cópia de segurança too2, 300 IOPS, com débito do 150 MB/s.
    
    > [!NOTE]
    > Facilmente pode aumentar o tamanho de Olá dos discos existentes. Por exemplo, poderá pretender tamanho de Olá tooincrease de um disco de 30 GB too128 GB ou TB too1 mesmo. Em alternativa, pode querer tooconvert seu disco P20 tooa P30 disco porque necessita de mais capacidade ou mais de IOPS e de débito. 
    > 
 
* **Tamanho de e/s**

    tamanho de Olá de e/s é 256 KB. Se os dados de Olá a serem transferidos ficarem inferior a 256 KB, considera-se 1 unidade de e/s. Tamanhos maiores de e/s são contados como várias e/s do tamanho de 256 KB. Por exemplo, e/s de 1,100 KB é contabilizado como 5 unidades de e/s.

* **Débito**

    limite de débito Olá inclui escritas toohello disco e inclui as operações de leitura do disco que não são servidas da cache de Olá. Por exemplo, um disco de P10 tem 100 MB/s débito por disco. Alguns exemplos de débito válido para um disco de P10 são mostrados nas Olá a tabela seguinte:

    | Débito máximo por disco P10 | Leituras de não-cache do disco | Escritas de cache não toodisk |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/s | 40 MB/s |

* **Acertos na cache**

    Acertos na cache não estão limitados pelo Olá alocado IOPS ou de débito do disco de Olá. Por exemplo, quando utilizar um disco de dados com um **ReadOnly** definição de cache numa VM que é suportada pelo armazenamento Premium, leituras são servidas da cache de Olá não é do requerente toohello IOPS e caps de débito do disco de Olá. Se a carga de trabalho Olá de um disco for predominantemente leituras, poderá obter débito muito elevado. cache de Olá é requerente tooseparate IOPS e limites de débito no Olá nível VM, com base no Olá tamanho da VM. VMs de série DS tem aproximadamente 4000 IOPS e 33 MB/s débito por núcleo para a cache de e/s de SSD local. VMs de série GS têm um limite de 5000 IOPS e 50 MB/s débito por núcleo para a cache de e/s de SSD local. 

## <a name="throttling"></a>Limitação
Limitação poderão ocorrer, se a aplicação IOPS ou débito excede os limites de Olá atribuído para um disco de armazenamento premium. Também limitação poderá ocorrer se o tráfego total do disco em todos os discos Olá VM excede o limite de largura de banda de disco Olá disponível para Olá VM. tooavoid limitação, recomendamos que limite Olá número de pedidos de e/s de disco Olá pendentes. Utilize um limite baseado em destinos de escalabilidade e desempenho para o disco de Olá que ter aprovisionado e Olá disco largura de banda disponível toohello VM.  

A aplicação pode obter com a latência mais baixa Olá concebido tooavoid limitação. No entanto, se hello número de pedidos de e/s de disco Olá pendentes é demasiado pequeno, a aplicação não é possível tirar partido de Olá níveis IOPS e débito máximos que estão disponíveis toohello disco.

Olá seguir exemplos demonstram como toocalculate limitação níveis. Todos os cálculos baseiam-se um tamanho de unidade de e/s de 256 KB.

### <a name="example-1"></a>Exemplo 1
A aplicação processou 495 e/s unidades de tamanho de 16 KB num segundo num disco P10. unidades de e/s de Olá são contadas como 495 IOPS. Se tentar uma e/s de 2 MB no Olá mesmo segundo, total de Olá de unidades de e/s too495 igual + 8 IOPS. Isto acontece porque e/s de 2 MB = unidades de 256 KB/KB 2.048 = 8 e/s, quando Olá tamanho da unidade de e/s é 256 KB. Porque a soma de Olá de 495 + 8 excede o limite de 500 IOPS Olá para disco Olá, limitação ocorre.

### <a name="example-2"></a>Exemplo 2
A aplicação tem de processar 400 e/s unidades de tamanho de 256 KB num disco P10. Olá largura de banda total consumido (400 &#215; 256) / 1.024 KB = 100 MB/s. Um disco de P10 tem um limite de débito de 100 MB/s. Se a aplicação tenta tooperform mais operações de e/s nesse segundo, está limitada porque excede o limite de Olá atribuído.

### <a name="example-3"></a>Exemplo 3
Tiver uma VM DS4 com dois P30 discos anexados. Cada disco P30 é capaz de débito do 200 MB/s. No entanto, uma VM DS4 tem uma capacidade de largura de banda total do disco de 256 MB/s. Não é possível unidade ambos os discos ligados toohello o débito máximo nesta VM DS4 em Olá mesmo tempo. tooresolve, pode suportar o tráfego de 200 MB/s num disco e 56 MB/s no Olá outro disco. Se ficar soma Olá do tráfego disco através de 256 MB/s, o tráfego do disco é limitado.

> [!NOTE]
> Se o tráfego de disco consiste principalmente tamanhos de e/s pequenos, a aplicação provável será atingiu o limite de IOPS Olá antes de limite de débito Olá. No entanto, se o tráfego de disco Olá consiste principalmente tamanhos de e/s grande, a aplicação provável será atingiu o limite de débito Olá em primeiro lugar, em vez de limite de IOPS Olá. Pode maximizar IOPS da sua aplicação e a capacidade de débito utilizando tamanhos ideal de e/s. Além disso, pode limitar o número Olá de pedidos de e/s para um disco pendentes.
> 

toolearn mais informações sobre a conceção de elevado desempenho ao utilizar o Premium Storage, consulte [conceção para desempenho com o Premium Storage](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Instantâneos e BLOBs de cópia

toohello serviço de armazenamento, o ficheiro VHD Olá é um blob de página. Pode criar instantâneos de blobs de páginas e copiá-los tooanother localização, tais como a conta de armazenamento diferente tooa.

### <a name="unmanaged-disks"></a>Discos não geridos

Criar [instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md) para discos premium não gerido Olá igual forma utilizar instantâneos de armazenamento standard. Armazenamento Premium suporta armazenamento apenas localmente redundante como opção de replicação de Olá. Recomendamos que crie instantâneos e, em seguida, copie a conta de armazenamento standard georredundante Olá instantâneos tooa. Para obter mais informações, consulte [opções de redundância do armazenamento do Azure](storage-redundancy.md).

Se um disco for anexado tooa VM, algumas operações de API no disco Olá não são permitidas. Por exemplo, não é possível efetuar um [copiar Blob](/rest/api/storageservices/Copy-Blob) operação nesse blob se Olá disco ligado tooa VM. Em vez disso, primeiro de criar um instantâneo desse blob utilizando Olá [instantâneo Blob](/rest/api/storageservices/Snapshot-Blob) REST API. Em seguida, efetuar Olá [copiar Blob](/rest/api/storageservices/Copy-Blob) de Olá do Olá instantâneo toocopy o disco foi exposto. Em alternativa, pode desanexar o disco de Olá e, em seguida, executar quaisquer operações necessárias.

Olá seguintes limites aplicam-se os instantâneos de blob de armazenamento toopremium:

| Limite de armazenamento Premium | Valor |
| --- | --- |
| Número máximo de instantâneos por blob | 100 |
| Capacidade da conta de armazenamento de instantâneos<br>(Inclui dados apenas com instantâneos. Não incluem dados no base blob). | 10 TB |
| Tempo mínimo entre instantâneos consecutivos | 10 minutos |

toomaintain georredundante cópias da sua instantâneos, pode copiar instantâneos de uma conta de armazenamento standard georredundante tooa conta do premium storage ao utilizar o AzCopy ou BLOBs de cópia. Para obter mais informações, consulte [transferir dados com o utilitário da linha de comandos do AzCopy Olá](storage-use-azcopy.md) e [copiar Blob](/rest/api/storageservices/Copy-Blob).

Para obter informações detalhadas sobre como efetuar as operações REST contra os blobs de páginas numa conta de armazenamento premium, consulte [Blob operações de serviço com o Premium Storage do Azure](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Managed disks

Um instantâneo de um disco gerido é uma cópia só de leitura do disco Olá de gerido. instantâneo de Olá é armazenado como um disco gerido standard. Atualmente, [instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md) não são suportadas para discos geridos. toolearn como tootake um instantâneo de um disco gerido, consulte [criar uma cópia de um VHD armazenado como um Azure gerido disco utilizando gerido instantâneos no Windows](../../virtual-machines/windows/snapshot-copy-managed-disk.md) ou [criar uma cópia de um VHD armazenado como um Azure gerido disco utilizando geridos instantâneos no Linux](../../virtual-machines/linux/snapshot-copy-managed-disk.md).

Se um disco gerido está ligado ao tooa VM, algumas operações de API no disco Olá não são permitidas. Por exemplo, não é possível gerar um tooperform de assinatura (SAS) de acesso partilhado uma operação de cópia, enquanto o disco de Olá está anexado tooa VM. Em vez disso, primeiro criar um instantâneo do disco de Olá e, em seguida, efetuar cópia de Olá do instantâneo Olá. Em alternativa, pode desligar o disco de Olá e, em seguida, gerar uma operação de cópia do SAS tooperform Olá.


## <a name="premium-storage-for-linux-vms"></a>Armazenamento Premium para VMs com Linux
Pode utilizar Olá toohelp informações que configurou as VMs do Linux no armazenamento Premium os seguintes:

escalabilidade tooachieve destina-se no armazenamento Premium, para todos os discos de armazenamento premium com cache definido demasiado**ReadOnly** ou **nenhum**, tem de desativar "barreiras as eficazes" ao montar o sistema de ficheiros de Olá. Não precisa de barreiras as eficazes neste cenário porque Olá escreve toopremium discos de armazenamento são duráveis para estas definições de cache. Quando o pedido de escrita de Olá for concluída com êxito, dados foi escritos arquivo persistente toohello. toodisable "barreiras as eficazes", utilize um dos seguintes métodos de Olá. Escolha Olá um para o seu sistema de ficheiros:
  
* Para **reiserFS**, barreiras as de toodisable eficazes, utilize Olá `barrier=none` montar opção. (barreiras as de tooenable eficazes, utilize `barrier=flush`.)
* Para **ext3/ext4**, barreiras as de toodisable eficazes, utilize Olá `barrier=0` montar opção. (barreiras as de tooenable eficazes, utilize `barrier=1`.)
* Para **XFS**, barreiras as de toodisable eficazes, utilize Olá `nobarrier` montar opção. (barreiras as de tooenable eficazes, utilize `barrier`.)
* Para discos de armazenamento premium com a cache de definido demasiado**ReadWrite**, ativar barreiras as eficazes para uma durabilidade de escrita.
* Para toopersist etiquetas de volume após o reinício Olá VM, tem de atualizar /etc/fstab com Olá Identificador universalmente exclusivo (UUID) referências toohello discos. Para obter mais informações, consulte [adicionar tooa um disco gerido VM com Linux](../../virtual-machines/linux/add-disk.md).

Olá, seguindo as distribuições do Linux tem foi validada para Premium Storage do Azure. Para um melhor desempenho e a estabilidade com o Premium Storage, recomendamos que Atualize o tooone de VMs destas versões, no mínimo (ou tooa versão posterior). Alguns dos Olá versões requerem hello mais recente Linux Integration Services (LIS), v 4.0, para o Azure. toodownload e instalar uma distribuição, siga a ligação Olá listada no Olá a tabela seguinte. Iremos adicionar a lista de toohello imagens à medida que concluir a validação. Tenha em atenção que o nosso validações mostram que o desempenho varia de cada imagem. Desempenho depende características de carga de trabalho e as definições de imagem. Imagens de diferentes são otimizadas para diferentes tipos de cargas de trabalho.

| Distribuição | Versão | Kernel suportado | Detalhes |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-Server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-Server-20150123-en-us-30GB |
| Debian | 7, 8. x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| SUSE-sles-12-prioridade-v20150213 <br> SUSE-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 necessário](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Consulte a nota na secção seguinte, Olá* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 recomendado](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Consulte a nota na secção seguinte, Olá* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 ou RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 ou RHCK com[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 ou RHCK com[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Controladores LIS para OpenLogic CentOS

Se estiver a executar OpenLogic CentOS VMs, execute os seguintes controladores mais recentes do comando tooinstall Olá de Olá:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate Olá novos controladores, reinicie o computador de Olá.

## <a name="pricing-and-billing"></a>Preços e faturação

Quando utiliza o Premium Storage, aplicam-se Olá seguintes considerações de faturação:

* **Tamanho do disco e BLOBs de armazenamento Premium**

    Faturação de um blob ou um disco de armazenamento premium depende do tamanho de Olá aprovisionado de disco de Olá ou BLOBs. Azure maps Olá toohello aprovisionado tamanho (arredondar por excesso) mais próximo da opção de disco de armazenamento premium. Para obter detalhes, consulte a tabela de Olá na [metas de desempenho e escalabilidade do armazenamento Premium](#premium-storage-scalability-and-performance-targets). Cada tooa de mapas de disco suportada aprovisionado tamanho do disco e é faturada em conformidade. A faturação para qualquer disco aprovisionado é proporcional numa base horária, utilizando o preço mensal Olá oferta de armazenamento Premium Olá. Por exemplo, se aprovisionado um disco de P10 e eliminado depois de 20 horas, é-lhe faturado para Olá P10 oferta too20 proporcional horas. Isto é, independentemente da quantidade de Olá de dados reais escritos toohello disco ou Olá IOPS e débito utilizado.

* **Instantâneos de discos não gerido Premium**

    Instantâneos em discos premium não gerido são cobrados capacidade adicional Olá utilizada pelo instantâneos Olá. Para obter mais informações sobre instantâneos, consulte [criar um instantâneo de um blob](/rest/api/storageservices/Snapshot-Blob).

* **Instantâneos de discos Premium gerido**

    Um instantâneo de um disco gerido é uma cópia só de leitura do disco de Olá. disco Olá é armazenado como um disco gerido standard. Custos de instantâneo Olá mesmo como um padrão gerido disco. Por exemplo, se tirar um instantâneo de um disco gerido de 128 GB premium, o custo de Olá de instantâneo Olá é tooa equivalente de 128 GB de disco gerido standard.  

* **Transferências de dados de saída**

    [Transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) (dados ficar fora de centros de dados do Azure) cobrança para utilização de largura de banda.

Para obter informações detalhadas sobre os preços para o Premium Storage, suportada de armazenamento Premium VMs e discos geridos, consulte estes artigos:

* [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Máquinas virtuais de preços](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Discos geridos de preços](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Suporte de cópia de segurança do Azure 

Regional recuperação de desastres, tem de copiar os discos VM numa região diferente utilizando [cópia de segurança do Azure](../../backup/backup-introduction-to-azure-backup.md) e uma conta de armazenamento GRS como um cofre de cópia de segurança.

toocreate uma tarefa de cópia de segurança com cópias de segurança baseados no tempo, fácil restauro de VM e políticas de retenção de cópias de segurança, utilize a cópia de segurança do Azure. Pode utilizar a cópia de segurança ambos os com discos não geridos e geridos. Para obter mais informações, consulte [cópia de segurança do Azure para as VMs com discos não geridos](../../backup/backup-azure-vms-first-look-arm.md) e [cópia de segurança do Azure para as VMs com discos geridos](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre o Premium Storage, consulte Olá seguintes artigos.

### <a name="design-and-implement-with-premium-storage"></a>Conceber e implementar com o Premium Storage
* [Estruturar para desempenho com o Premium Storage](storage-premium-storage-performance.md)
* [Operações de armazenamento de Blobs com o Premium Storage](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Orientação operacional
* [Migrar tooAzure Premium Storage](../common/storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Publicações no blogue
* [Armazenamento Premium do Azure geralmente disponível](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Anunciar Olá série GS: Adicionar toohello de suporte de armazenamento Premium maior Olá, VMs na nuvem pública](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
