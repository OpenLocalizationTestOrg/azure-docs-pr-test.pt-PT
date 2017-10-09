---
title: aaaDesign e implementar uma Oracle da base de dados no Azure | Microsoft Docs
description: Conceber e implementar uma base de dados Oracle no seu ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Conceber e implementar uma base de dados Oracle no Azure

## <a name="assumptions"></a>Pressupostos

- Está a planear toomigrate uma base de dados Oracle de tooAzure no local.
- Ter uma compreensão dos Olá várias métricas nos relatórios de Oracle AWR.
- Ter uma compreensão de linha de base de desempenho da aplicação e a utilização de plataforma.

## <a name="goals"></a>Objetivos

- Compreender como toooptimize a implementação da Oracle no Azure.
- Explore as opções para uma base de dados Oracle num ambiente do Azure de otimização do desempenho.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Olá diferenças entre no local e a implementação do Azure 

Seguem-se algumas importante coisas tookeep em mente quando estiver a migrar no local tooAzure de aplicações. 

Uma diferença importante é que uma implementação do Azure, recursos, tais como VMs, discos e redes virtuais são partilhados entre os outros clientes. Além disso, os recursos podem ser limitados com base nos requisitos de Olá. Em vez de concentrar-se no evitando (MTBF) a falhar, Azure mais concentra-se no reiniciadas falha Olá (MTTR).

Olá tabela seguinte lista algumas das diferenças de Olá entre uma implementação no local e uma implementação do Azure de uma base de dados Oracle.

> 
> |  | **Implementação no local** | **Implementação do Azure** |
> | --- | --- | --- |
> | **Redes** |LAN/WAN  |SDN (redes definidas por software)|
> | **Grupo de segurança** |Ferramentas de restrição de IP/porta |[Grupo de segurança de rede (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Resiliência** |MTBF (tempo médio entre falhas) |MTTR (toorecovery de Greenwich)|
> | **Manutenção planeada** |Aplicação de patches/atualizações|[Conjuntos de disponibilidade](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (aplicação de patches/atualizações geridas pelo Azure) |
> | **Recurso** |Dedicado  |Partilhada com outros clientes|
> | **Regiões** |Datacenters |[Pares de região](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Armazenamento** |Discos físicos/SAN |[Armazenamento gerido pelo Azure](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Dimensionamento** |Escala vertical |Dimensionamento horizontal|


### <a name="requirements"></a>Requisitos

- Determine a taxa de tamanho e crescimento da base de dados Olá.
- Determine os requisitos de IOPS Olá, o que pode fazer a estimativa baseada em relatórios Oracle AWR ou outra ferramentas de monitorização de rede.

## <a name="configuration-options"></a>Opções de configuração

Existem quatro áreas potenciais que pode otimizar o desempenho de tooimprove num ambiente do Azure:

- Tamanho da máquina virtual
- Débito de rede
- Configurações e os tipos de disco
- Definições de cache do disco

### <a name="generate-an-awr-report"></a>Gerar um relatório AWR

Se tiver uma base de dados Oracle existente e estiver a planear toomigrate tooAzure, tem várias opções. Pode executar Olá Oracle AWR relatório tooget Olá métricas (IOPS, Mbps, GiBs e assim sucessivamente). Em seguida, escolha Olá que VM com base nas métricas Olá que recolheu. Ou pode contactar a sua infraestrutura equipa tooget semelhante as informações.

Poderá considerar executar relatório AWR durante regulares e pico cargas de trabalho, pelo que pode comparar. Com base nestes relatórios, pode tamanho Olá VMs com base na carga de trabalho médio Olá ou carga de trabalho máximo Olá.

Segue-se um exemplo de como toogenerate um relatório AWR:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Métricas-chave

Seguem-se as métricas de Olá que pode obter de Olá relatório AWR:

- Número total de núcleos
- Velocidade de relógio de CPU
- Total de memória em GB
- Utilização da CPU
- Velocidade de transferência de dados das horas de ponta
- Taxa de alterações de e/s (leitura/escrita)
- Refazer a taxa de registo (MBPs)
- Débito de rede
- Taxa de latência de rede (baixa/alta)
- Tamanho de base de dados em GB
- Bytes recebidos através de SQL * Net da / tooclient

### <a name="virtual-machine-size"></a>Tamanho da máquina virtual

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Estimar o tamanho da VM com base na utilização da CPU, memória e e/s de Olá relatório AWR

Um aspeto que poderá ver é Olá superior cinco excedeu o tempo limite em primeiro plano eventos que indicam onde são congestionamentos de sistema Olá.

Por exemplo, Olá diagrama a seguir, sincronização de ficheiros de registo Olá é na parte superior do Olá. Indica número de Olá de aguarda que sejam necessários antes de Olá LGWR escreve o ficheiro de registo de Refazer da memória intermédia toohello Olá registo. Estes resultados indicam que o melhor desempenho de armazenamento ou discos são necessários. Além disso, Olá diagrama também mostra o número de Olá de CPU (núcleos) e quantidade Olá de memória.

![Captura de ecrã da página do relatório Olá AWR](./media/oracle-design/cpu_memory_info.png)

Olá diagrama seguinte mostra Olá e/s total de leitura e escrita. Ocorreram GB 59 ler e GB 247.3 escritos durante a hora de Olá do relatório de Olá.

![Captura de ecrã da página do relatório Olá AWR](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Escolha uma VM

Com base nas informações de Olá recolhidos a partir de Olá relatório AWR, o passo seguinte Olá é toochoose uma VM de um tamanho semelhante aos seus requisitos. Pode encontrar uma lista de VMs disponíveis no artigo Olá [com otimização de memória](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Otimizar o dimensionamento de VM Olá com uma série VM semelhante com base no Olá ACU

Depois que escolheu Olá VM, preste atenção toohello ACU para Olá VM. Pode optar por utilizar uma VM diferente com base no Olá valor ACU que melhor se adequa aos seus requisitos. Para obter mais informações, consulte [unidade de computação do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Captura de ecrã da página de unidades ACU Olá](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Débito de rede

Olá seguinte diagrama mostra a relação de Olá entre débito e IOPS:

![Captura de ecrã de débito](./media/oracle-design/throughput.png)

débito de rede total Olá é estimado com base no Olá seguintes informações:
- SQL * tráfego de rede
- MBps x o número de servidores (sequência de saída, tais como o Oracle Data Guard)
- Outros fatores, tais como replicação de aplicação

![Captura de ecrã do Olá SQL * débito Net](./media/oracle-design/sqlnet_info.png)

Com base nos seus requisitos de largura de banda de rede, existem vários tipos de gateway para toochoose do. Estes incluem basic VpnGw e Azure ExpressRoute. Para obter mais informações, consulte Olá [página de preços de gateway VPN](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Recommendations (Recomendações)**

- Latência de rede é a implementação de local de tooan em comparação com superior. Reduzir rede arredondar viagens pode significativamente melhorar o desempenho.
- consolidar de ida e volta de tooreduce, as aplicações que têm aplicações "chatty" ou de transações elevadas em Olá mesma máquina virtual.

### <a name="disk-types-and-configurations"></a>Configurações e os tipos de disco

- *Predefinição discos de SO*: estes tipos de disco oferecem dados persistentes e colocação em cache. Estes estão otimizados para acesso de SO no arranque e não são concebidos para um transacional ou cargas de trabalho (analíticas) do armazém de dados.

- *Não gerido discos*: com estes tipos de disco, gere contas de armazenamento de Olá que armazenam ficheiros de disco rígido virtual (VHD) de Olá que correspondem tooyour discos da VM. Ficheiros VHD são armazenados como blobs de páginas em contas do storage do Azure.

- *Discos geridos pelo*: Azure gere contas de armazenamento de Olá que utilizar para os discos VM. Especifique o tipo de disco Olá (standard ou premium) e o tamanho de Olá do disco de Olá que precisa. Azure cria e gere o disco de Olá por si.

- *Discos de armazenamento Premium*: estes tipos de disco são mais adequados para cargas de trabalho de produção. Premium storage suporta discos de VM que podem ser anexados a série de tamanho toospecific VMs, tais como série DS, série DSv2, GS e F VMs. disco de premium Olá vem com tamanhos diferentes e pode escolher entre discos de 32 GB too4, 096 GB. Cada tamanho do disco tem as suas próprias especificações de desempenho. Dependendo dos requisitos de aplicação, poderá anexar um ou mais discos tooyour VM.

Quando criar um novo disco gerido a partir do portal de Olá, pode escolher Olá **tipo de conta** para o tipo de Olá de disco que pretende toouse. Tenha em atenção que nem todos os discos disponíveis são apresentados no menu pendente de Olá. Depois de escolher um tamanho VM específico, o menu Olá mostra apenas Olá disponível armazenamento premium SKUs que se baseiam nesse tamanho VM.

![Captura de ecrã da página de disco gerido Olá](./media/oracle-design/premium_disk01.png)

Para obter mais informações, consulte [elevado desempenho Premium Storage e discos geridos para VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Depois de configurar o armazenamento numa VM, pode querer discos de Olá tooload teste antes de criar uma base de dados. Saber a taxa de e/s de Olá em termos de latência e débito pode ajudar a determinar se Olá VMs suportam Olá esperado débito com destinos de latência.

Existem várias ferramentas para a aplicação teste de carga, como Oracle Orion, Sysbench e Fio.

Execute o teste de carga Olá novamente depois de implementar uma base de dados Oracle. Iniciar as cargas de trabalho normais e utilização máxima e Olá Mostrar resultados Olá da linha de base do seu ambiente.

Poderá ser mais importante toosize Olá no armazenamento baseado em taxa IOPS Olá em vez de tamanho de armazenamento Olá. Por exemplo, se necessário Olá IOPS é 5.000, mas só precisa de 200 GB, poderá obter disco premium do Olá P30 classe, apesar de este inclui mais de 200 GB de armazenamento.

taxa IOPS Olá pode ser obtida a partir Olá relatório AWR. Este é determinado pelo registo de Refazer Olá, leituras físicas e velocidade de escritas.

![Captura de ecrã da página do relatório Olá AWR](./media/oracle-design/awr_report.png)

Por exemplo, o tamanho de Refazer Olá é 12,200,000 bytes por segundo, que é igual too11.63 MBPs.
Olá IOPS é 12,200,000 / 2,358 = 5,174.

Depois de ter uma visão clara dos requisitos de e/s de Olá, pode escolher uma combinação de unidades que melhor se adequam toomeet esses requisitos.

**Recommendations (Recomendações)**

- Para o espaço de tabelas de dados, distribuídos carga de trabalho de e/s de Olá por um número de discos utilizando o armazenamento gerido ou Oracle ASM.
- À medida que aumenta o tamanho do bloco Olá e/s para operações que exigem muita leitura e escrita intensivas, adicione mais discos de dados.
- Aumente o tamanho do bloco Olá para processos sequenciais grandes.
- Utilize a e/s tooreduce de compressão de dados (para dados e índices).
- Separe os registos de Refazer, sistema e temps e anular TS em discos de dados separada.
- Não coloque os ficheiros de aplicação em discos de SO predefinido (dev/sda). Estes discos não estão otimizados para a VM rápida tempos de arranque e poderá não fornecer um bom desempenho para a sua aplicação.

### <a name="disk-cache-settings"></a>Definições de cache do disco

Existem três opções para a colocação em cache do anfitrião:

- *Só de leitura*: todos os pedidos são colocados em cache para leituras futuras. Todas as escritas são mantidas diretamente tooAzure armazenamento de Blobs.

- *Leitura e escrita*: Este é um algoritmo "antecipadas". Olá lê e escreve é colocadas em cache para leituras futuras. Não-escrita-through escreve são persistente toohello local cache primeiro. Para o SQL Server, escreve são tooAzure persistente armazenamento porque utiliza através de escrita. Também fornece mais baixa latência de disco Olá para cargas de trabalho leves.

- *Nenhum* (desativada): ao utilizar esta opção, pode ignorar a cache de Olá. Todos os dados de Olá é toodisk transferido e persistente tooAzure armazenamento. Este oferece método hello mais elevada taxa de e/s para cargas de trabalho exigente em termos de e/s. Também precisa de tootake "custos de transação" em consideração.

**Recommendations (Recomendações)**

débito do toomaximize Olá, recomendamos que comece com **nenhum** para a colocação em cache do anfitrião. Para o Premium Storage, tenha em atenção que tem de desativar Olá "barreiras as eficazes" ao montar o sistema de ficheiros de Olá com Olá **ReadOnly** ou **nenhum** opções. Atualize ficheiro de /etc/fstab Olá com discos de toohello Olá UUID.

Para obter mais informações, consulte [Premium Storage para VMs com Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Captura de ecrã da página de disco gerido Olá](./media/oracle-design/premium_disk02.png)

- Para discos de SO, utilizar a predefinição **leitura/escrita** colocação em cache.
- Para o sistema, TEMP e anulação utilizar **nenhum** para colocar em cache.
- Para os dados, utilize **nenhum** para colocar em cache. Mas se a base de dados é só de leitura ou de leitura intensiva, utilize **só de leitura** colocação em cache.

Depois da definição de disco de dados é guardada, não é possível alterar a definição de cache do anfitrião de Olá, a menos que desmonte a unidade de Olá em Olá ao nível do SO e, em seguida, voltar a montá-lo Depois de efetuadas Olá alterar.


## <a name="security"></a>Segurança

Depois de configurar e configurar o seu ambiente do Azure, o passo seguinte Olá é toosecure sua rede. Seguem-se algumas recomendações:

- *Política NSG*: NSG pode ser definido por uma sub-rede ou NIC. É mais simples toocontrol acesso ao nível de sub-rede Olá para segurança e a imposição de encaminhamento para coisas como firewalls de aplicação.

- *Jumpbox*: para um acesso mais seguro, os administradores devem não ligar diretamente toohello serviço de aplicações ou a base de dados. Um jumpbox é utilizado como um suporte de dados entre a máquina de administrador de Olá e de recursos do Azure.
![Captura de ecrã da página de topologia de Jumpbox Olá](./media/oracle-design/jumpbox.png)

    máquina de administrador Olá deve oferecer apenas o acesso restrito de IP toohello jumpbox. Olá jumpbox deve ter acesso toohello aplicação e a base de dados.

- *Rede privada* (sub-redes): Recomendamos que tenha o serviço de aplicações de Olá e base de dados em sub-redes diferentes, para melhorar o controlo pode ser definido pela política NSG.


## <a name="additional-reading"></a>Leitura adicional

- [Configurar Oracle ASM](configure-oracle-asm.md)
- [Configurar a proteção de dados Oracle](configure-oracle-dataguard.md)
- [Configurar a porta de Golden Oracle](configure-oracle-golden-gate.md)
- [Cópia de segurança do Oracle e recuperação](oracle-backup-recovery.md)

## <a name="next-steps"></a>Passos seguintes

- [Tutorial: Criar as VMs de elevada disponibilidade](../../linux/create-cli-complete.md)
- [Explorar amostras de CLI do Azure de implementação de VM](../../linux/cli-samples.md)
