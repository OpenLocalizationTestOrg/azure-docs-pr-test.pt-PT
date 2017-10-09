---
title: 'Armazenamento Premium do Azure: Estruturar para desempenho | Microsoft Docs'
description: "Conceber aplicações de elevado desempenho com o Premium Storage do Azure. Armazenamento Premium oferece suporte de disco de elevado desempenho, baixa latência para cargas de trabalho de I/O intensivo em execução em máquinas de virtuais do Azure."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: dde3e60ae4c8387150b65f0715166b5d549891e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Armazenamento do Azure Premium: Conceção de elevado desempenho
## <a name="overview"></a>Descrição geral
Este artigo fornece diretrizes para a criação de aplicações de elevado desempenho com o Premium Storage do Azure. Pode utilizar as instruções de Olá fornecidas neste documento juntamente com desempenho melhores práticas aplicáveis tootechnologies utilizado pela sua aplicação. diretrizes de Olá tooillustrate, ter utilizámos o SQL Server em execução no armazenamento Premium como um exemplo ao longo deste documento.

Enquanto que tratam cenários de desempenho para a camada de armazenamento Olá neste artigo, terá de camada de aplicação Olá toooptimize. Por exemplo, se alojar um Farm do SharePoint no armazenamento do Azure Premium, pode utilizar os exemplos do SQL Server Olá deste servidor de base de dados do artigo toooptimize Olá. Além disso, Otimize o servidor de Web do Farm do SharePoint Olá e hello de tooget do servidor de aplicação a maioria das desempenho.

Este artigo irá podem ajudar a responder a perguntas comuns sobre a otimização do desempenho de aplicações no armazenamento do Azure Premium, os seguintes

* Como toomeasure o desempenho da sua aplicação?  
* Por que motivo não lhe existem esperado de elevado desempenho?  
* Os fatores que influenciam o desempenho de aplicações no armazenamento Premium?  
* Como é que estes fatores influenciam o desempenho da sua aplicação no armazenamento Premium?  
* Como pode otimizar de IOPS, largura de banda e latência?  

Fornecemos-estas diretrizes especificamente para o Premium Storage porque as cargas de trabalho em execução no armazenamento Premium altamente confidencial de desempenho. Fornecemos exemplos apropriado. Também pode aplicar algumas das tooapplications diretrizes em execução em VMs de IaaS com discos de armazenamento Standard.

Antes de começar, se forem tooPremium novo armazenamento, leia primeiro Olá [Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](../storage-premium-storage.md) e [metas de desempenhoeescalabilidadedoStoragedoAzure](storage-scalability-targets.md)artigos.

## <a name="application-performance-indicators"></a>Indicadores de desempenho de aplicações
Iremos avaliar se uma aplicação está a funcionar corretamente ou não a utilizar como indicadores de desempenho, a rapidez uma aplicação está a processar um pedido de utilizador, a quantidade de dados está a processar uma aplicação por pedido, pedidos quantos é uma aplicação em processamento no específico período de tempo, como um utilizador tiver toowait tooget uma resposta depois de submeter o pedido. Olá técnica termos para estes indicadores de desempenho encontram-se, IOPS, débito ou largura de banda e latência.

Nesta secção, vamos abordar indicadores de desempenho comuns Olá no contexto de Olá do Premium Storage. Olá, secção a seguir, recolha os requisitos da aplicação, ficará a saber como toomeasure estes indicadores de desempenho para a sua aplicação. Mais tarde otimizar o desempenho da aplicação, irá aprender sobre fatores Olá afetar estes toooptimize de recomendações e os indicadores de desempenho-los.

## <a name="iops"></a>IOPS
IOPS é o número de pedidos que a aplicação está a enviar toohello discos de armazenamento num segundo. Uma operação de entrada/saída foi possível ler ou escrever, sequenciais ou aleatório. Aplicações de OLTP como um site de revenda online tem tooprocess utilizador simultâneas muitos pedidos imediatamente. pedidos de utilizador Olá são insert e atualizar as transações de base de dados que consomem muita, que aplicação Olá tem de processar rapidamente. Por conseguinte, aplicações de OLTP necessitam de IOPS muito elevada. Essas aplicações processam milhões de pedidos de e/s pequenos e aleatórios. Se tiver uma aplicação deste tipo, tem de design toooptimize de infraestrutura de aplicação Olá para o IOPS. No Olá secção mais tarde, *otimizar o desempenho da aplicação*, vamos discutir detalhadamente todos os fatores de Olá que tem de considerar tooget IOPS elevado.

Quando anexa uma premium storage disco tooyour escala elevada VM, do Azure Aprovisiona para que um número garantido de IOPS de acordo com a especificação de disco Olá. Por exemplo, um disco de P50 Aprovisiona 7500 IOPS. Cada grande escala de tamanho VM também tem um limite IOPS específico que possa suportar. Por exemplo, uma VM GS5 padrão tem 80.000 IOPS limitar.

## <a name="throughput"></a>Débito
Débito ou largura de banda é a quantidade de Olá de envio de dados que a aplicação é toohello discos de armazenamento num intervalo especificado. Se a aplicação está a efetuar operações de entrada/saída com o tamanho de unidade de e/s grande, requer o débito elevado. Aplicações de armazém de dados tendem tooissue análise operações intensivas que aceder a grandes partes dos dados de cada vez e normalmente efetuarem operações em massa. Por outras palavras, essas aplicações requerem um maior débito. Se tiver uma aplicação deste tipo, tem de design toooptimize respetiva infraestrutura de débito. Na secção seguinte, Olá, vamos discutir fatores de Olá de detalhe de tem otimizar tooachieve isto.

Quando anexa uma premium storage disco tooa escala elevada VM, do Azure Aprovisiona débito de acordo com esse especificação de disco. Por exemplo, um disco de P50 Aprovisiona 250 MB por segundo disco débito. Cada grande escala de tamanho VM também tem como limite de débito específico que possa suportar. Por exemplo, o padrão de GS5 de VM tem um débito máximo de 2.000 MB por segundo. 

Há uma relação entre o débito e IOPS, conforme mostrado na fórmula Olá abaixo.

![](media/storage-premium-storage-performance/image1.png)

Por conseguinte, é importante toodetermine Olá ideal débito e IOPS valores que requer a sua aplicação. Como tente toooptimize um, Olá outro também obtém afetado. Numa secção posterior, *otimizar o desempenho da aplicação*, vamos abordar em obter mais detalhes sobre a otimização de IOPS e débito.

## <a name="latency"></a>Latência
Latência está na altura de Olá demora um tooreceive de aplicação único pedido, envia-as toohello discos de armazenamento e enviar Olá resposta toohello cliente. Esta é uma medida crítico de desempenho de uma aplicação na adição tooIOPS e débito. Olá latência de um disco de armazenamento premium está na altura de Olá-utiliza informações de Olá tooretrieve para um pedido e comunicar-criar uma aplicação tooyour. Armazenamento Premium fornece baixas latências consistentes. Se ativar anfitrião só de leitura a colocação em cache nos discos de armazenamento premium, pode obter muito menor latência de leitura. Vamos abordar colocação em cache do disco mais detalhadamente na secção posterior no *otimizar o desempenho da aplicação*.

Quando são otimizar o seu tooget aplicação superior IOPS e débito, afetará Olá latência da sua aplicação. Após a otimização do desempenho da aplicação Olá, avaliar sempre Olá latência de Olá aplicação tooavoid comportamento inesperado latência elevada.

## <a name="gather-application-performance-requirements"></a>Recolher requisitos de desempenho de aplicações
Olá primeiro passo para conceber aplicações de elevado desempenho em execução no armazenamento do Azure Premium é, requisitos de desempenho de Olá toounderstand da sua aplicação. Depois de recolher requisitos de desempenho, pode otimizar a sua aplicação tooachieve Olá mais um desempenho ideal.

Na secção anterior Olá, é explicado Olá comuns indicadores de desempenho, IOPS, débito e latência. Tem de identificar que estes indicadores de desempenho experiência de utilizador do tooyour críticos aplicação toodeliver Olá assim o desejar. Por exemplo, o IOPS elevado é importante maioria das aplicações de tooOLTP processar milhões de transações num segundo. Enquanto, é essencial para aplicações de armazém de dados grandes quantidades de dados de processamento em segundo débito elevado. Latência extremamente baixa é fundamental para aplicações em tempo real, como as vídeo em direto Web sites de transmissão em fluxo.

Em seguida, medir os requisitos de desempenho máximo Olá da sua aplicação ao longo da respetiva duração. Utilize a lista de verificação de exemplo de Olá abaixo como um início. Requisitos de desempenho máximo de registos Olá durante normal, máximos e off-hours períodos de carga de trabalho. Ao identificar os requisitos para todos os níveis de cargas de trabalho, será capaz de toodetermine Olá requisito de desempenho global da sua aplicação. Por exemplo, a carga de trabalho normal do Olá de um Web site de comércio eletrónico será transações Olá serve durante a maior parte dos dias num ano. carga de trabalho do Olá pico do site de Olá será transações Olá serve durante a época ou eventos de venda especiais. carga de trabalho de pico de Olá é normalmente experiente por um período limitado, mas pode exigir a tooscale aplicação dois ou mais vezes o funcionamento normal. Descobrir percentil 50 Olá, percentil 90 e 99 requisitos de percentil. Isto ajuda a filtrar quaisquer valores atípicos nos requisitos de desempenho de Olá e pode concentrar-se os esforços na otimizar para os valores corretos Olá.

**Lista de verificação de requisitos de desempenho de aplicações**

| **Requisitos de desempenho** | **Percentil 50** | **Percentil 90** | **Percentil 99** |
| --- | --- | --- | --- |
| Um máximo de Transações por segundo | | | |
| Operações de leitura % | | | |
| Operações de escrita % | | | |
| Operações aleatório % | | | |
| Operações sequenciais % | | | |
| Tamanho do pedido de e/s | | | |
| Débito médio | | | |
| Um máximo de Débito | | | |
| Min. Latência | | | |
| Latência média de | | | |
| Um máximo de CPU | | | |
| CPU média | | | |
| Um máximo de Memória | | | |
| Memória média | | | |
| Profundidade de fila | | | |

> [!NOTE]
> Deve considerar o dimensionamento estes números com base no esperado crescimento futuro da sua aplicação. É uma boa ideia tooplan crescimento antecedência, porque pode ser mais difícil toochange Olá a infraestrutura para melhorar o desempenho mais tarde.
>
>

Se tiver uma aplicação existente e pretender toomove tooPremium armazenamento, primeiro crie Olá lista de verificação acima para a aplicação existente Olá. Em seguida, criar um protótipo da sua aplicação na aplicação de Olá Premium Storage e de design, com base em diretrizes descritas em *otimizar o desempenho da aplicação* numa secção posterior deste documento. Step-by-Olá seguinte secção descreve as ferramentas de Olá que pode utilizar medidas de desempenho de Olá toogather.

Crie uma lista de verificação semelhante tooyour aplicação existente para protótipo Olá. Utilizar ferramentas de Benchmarking pode simular cargas de trabalho Olá e medir o desempenho na aplicação de protótipo Olá. Consulte a secção de Olá no [Benchmarking](#benchmarking) toolearn mais. Por se o fizer, pode determinar se o armazenamento Premium podem corresponder ou surpass os seus requisitos de desempenho de aplicações. Em seguida, pode implementar Olá mesmas diretrizes para a sua aplicação de produção.

### <a name="counters-toomeasure-application-performance-requirements"></a>Contadores toomeasure requisitos de desempenho de aplicações
Olá melhor forma toomeasure desempenho os requisitos da sua aplicação, as ferramentas de monitorização de desempenho do toouse fornecidas pelo sistema de operativo hello do servidor de Olá. Pode utilizar PerfMon para Windows e iostat para Linux. Estas ferramentas capturam os contadores de medidas correspondente, o tooeach explicada Olá acima secção. Quando a aplicação está a executar o normal, cargas de trabalho das horas de ponta e off-hours, tem de capturar valores Olá um destes contadores.

contadores de PerfMon Olá estão disponíveis para processador, memória e, como cada disco lógico e disco físico do seu servidor. Quando utilizar discos de armazenamento premium com uma VM, contadores de disco físico Olá são para cada disco de armazenamento premium e contadores de disco lógico são para cada volume criado nos discos de armazenamento premium Olá. Tem de capturar Olá os valores para os discos de Olá que alojam a carga de trabalho da aplicação. Se existir um mapeamento de tooone um entre os discos lógicos e físicos, pode consultar os contadores de disco toophysical; caso contrário, consulte toohello contadores de disco lógico. No Linux, o comando de iostat Olá gera um relatório de utilização da CPU e de disco. relatório de utilização do disco de Olá fornece estatísticas por partição ou o dispositivo físico. Se tiver um servidor de base de dados com a dados e registo nos discos separados, recolha estes dados para os dois discos. Tabela abaixo descreve os contadores de discos, processadores e memória:

| Contador | Descrição | PerfMon | Iostat |
| --- | --- | --- | --- |
| **IOPS ou de transações por segundo** |Número de pedidos de e/s emitido toohello de disco de armazenamento por segundo. |Leituras de disco/seg <br> Escritas de disco/seg |tps <br> r/s <br> w/s |
| **Leituras de disco e de escrita** |% de leituras exibidas as operações executadas no disco Olá. |% Tempo de leitura do disco <br> % De tempo de escrita de disco |r/s <br> w/s |
| **Débito** |Quantidade de dados lidas ou escritas toohello de disco por segundo. |Bytes lidos/seg de disco <br> Bytes de escrita de disco/seg |kB_read/s <br> kB_wrtn/s |
| **Latência** |Total de tempo toocomplete um pedido de e/s de disco. |Médio disco seg/leitura <br> Média de disco seg/escrita |await <br> svctm |
| **Tamanho de e/s** |tamanho de Olá de pedidos de e/s emite toohello discos de armazenamento. |Bytes de média de disco/leitura <br> Bytes de média de disco/escrita |avgrq sz |
| **Profundidade de fila** |Número de e/s pendentes pedidos a aguardar toobe formulário de leitura ou escrita toohello disco de armazenamento. |Comprimento da fila de disco |avgqu sz |
| **Máx. Memória** |Quantidade de memória necessária toorun aplicação facilmente |% Dos Bytes consolidados em utilização |Utilizar vmstat |
| **Máx. CPU** |Quantidade de CPU necessário toorun aplicação facilmente |% Tempo do processador |% util |

Saiba mais sobre [iostat](http://linuxcommand.org/man_pages/iostat1.html) e [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Otimizar o desempenho de aplicações
fatores de principais de Olá que influenciam o desempenho de uma aplicação em execução no armazenamento Premium são natureza de e/s pedidos, tamanho da VM, o tamanho do disco, número de discos, colocação em cache do disco, Multithreading e profundidade de fila. Pode controlar algumas destes fatores com botões fornecidos pelo sistema Olá. A maioria das aplicações poderão não dão-lhe um Olá tooalter de opção tamanho de e/s e a profundidade de fila diretamente. Por exemplo, se estiver a utilizar o SQL Server, não é possível escolher a profundidade de fila e de tamanho de e/s de Olá. SQL Server escolhe Olá ideal e/s tamanho e a fila de profundidade valores tooget Olá mais desempenho. É importante toounderstand Olá afeta de ambos os tipos de fatores, o desempenho da aplicação, para que possa aprovisionar necessidades de desempenho de toomeet recursos adequados.

Ao longo de nesta secção, consulte toohello aplicação requisitos lista de verificação que criou, tooidentify quanto precisa toooptimize o desempenho da sua aplicação. Com base no que, será capaz de toodetermine que factors desta secção, irá precisar tootune. toowitness Olá afeta o desempenho da aplicação, executar ferramentas na sua configuração de aplicação de direcionamento de caminhos de cada fator. Consulte toohello [Benchmarking](#Benchmarking) secção no final Olá deste artigo para toorun passos comuns direcionamento de caminhos de ferramentas no Windows e VMs com Linux.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>Otimizar o IOPS, débito e latência num instante
tabela de Olá abaixo resume todos os fatores de desempenho de Olá e Olá passos toooptimize IOPS, débito e latência. Olá secções apresentadas a seguir este resumo descrevem cada fator é profundidade muito mais.

| &nbsp; | **ESP** | **Débito** | **Latência** |
| --- | --- | --- | --- |
| **Cenário de exemplo** |Aplicação de OLTP de Enterprise que requerem muito elevadas transações por segundo taxa. |Aplicação processamento vastos volumes de dados de armazém de dados da empresa. |Quase em tempo real aplicações que necessitam de pedidos de toouser respostas instantâneas, como jogos online. |
| Fatores de desempenho | &nbsp; | &nbsp; | &nbsp; |
| **Tamanho de e/s** |Tamanho mais pequeno de e/s gera IOPS superior. |Tooyields de tamanho de e/s maior débito mais elevado. | &nbsp;|
| **Tamanho da VM** |Utilize um tamanho VM que oferece maior do que o requisito da aplicação de IOPS. Consulte os tamanhos de VM e os respetivos limites IOPS aqui. |Utilize um tamanho VM com limite de débito maior do que o requisito da aplicação. Consulte os tamanhos de VM e os respetivos limites de débito aqui. |Utilize um tamanho VM que oferece Dimensionar limites maiores do que o requisito da aplicação. Consulte os respetivos limites aqui e tamanhos VM. |
| **Tamanho do disco** |Utilize um tamanho de disco que oferece maior do que o requisito da aplicação de IOPS. Consulte os tamanhos de disco e os respetivos limites IOPS aqui. |Utilize um tamanho de disco com limite de débito maior do que o requisito da aplicação. Consulte os tamanhos de disco e os respetivos limites de débito aqui. |Utilize um tamanho de disco que ofertas aumentar os limites de maiores do que o requisito da aplicação. Consulte os respetivos limites aqui e tamanhos de disco. |
| **VM e os limites de escala de disco** |Limite IOPS de escolhido de tamanho VM Olá deve ser maior do que os ESP totais condicionados pelos discos de armazenamento premium ligados tooit. |Limite de débito de escolhido de tamanho VM Olá deve ser maior do que o débito total conduzido pelos discos de armazenamento premium ligados tooit. |Os limites de escala de escolhido de tamanho VM Olá tem de ser maiores do que os limites de escala total dos discos de armazenamento premium ligados. |
| **Colocação em cache do disco** |Ativar a Cache de só de leitura nos discos de armazenamento premium com tooget pesada de operações de leitura mais elevado de leitura de IOPS. | &nbsp; |Ative a Cache de só de leitura nos discos de armazenamento premium com latências de leitura do operations pesada pronto tooget muito baixos. |
| **Disco Striping** |Utilizar vários discos e stripe-los em conjunto tooget um IOPS superior combinado e limite de débito. Tenha em atenção que Olá limite combinado por VM deve ser superior ao hello limites combinados de discos premium ligados. | &nbsp; | &nbsp; |
| **Tamanho do stripe** |Tamanho mais pequeno do stripe para padrão de e/s pequena aleatória visto nas aplicações OLTP. Por exemplo, utilize o tamanho do stripe de 64KB para a aplicação do SQL Server OLTP. |Tamanho maior de stripe para padrão de e/s grande sequencial visto nas aplicações do armazém de dados. Por exemplo, utilize o tamanho do stripe de 256KB para a aplicação de armazém de dados do SQL Server. | &nbsp; |
| **Multithreading** |Utilize multithreading toopush maior número de pedidos tooPremium armazenamento irá causar toohigher IOPS e débito. Por exemplo, no SQL Server definir um valor tooallocate elevada do MAXDOP mais CPUs tooSQL servidor. | &nbsp; | &nbsp; |
| **Profundidade de fila** |Maior profundidade de fila gera IOPS superior. |Maior profundidade de fila gera um maior débito. |Profundidade de fila menor gera latências inferiores. |

## <a name="nature-of-io-requests"></a>Natureza dos pedidos de e/s
Um pedido de e/s é uma unidade de operação de entrada/saída que irão realizar a aplicação. Identificar a natureza Olá pedidos de e/s aleatórias ou sequenciais, leitura ou escrita, tamanho, irá ajudá-lo a determinar os requisitos de desempenho de Olá da sua aplicação. É muito importante toounderstand natureza Olá pedidos de e/s, toomake Olá direita decisões quando conceber a infraestrutura de aplicação.

Tamanho de e/s é uma das Olá fatores mais importantes. Olá tamanho de e/s é o tamanho de Olá de pedido de operação de entrada/saída Olá gerado pela sua aplicação. Olá tamanho de e/s tem um impacto significativo no desempenho, especialmente em Olá IOPS e largura de banda que Olá a aplicação é capaz de tooachieve. Olá fórmula seguinte mostra Olá relação entre o IOPS, tamanho de e/s e largura de banda/débito.  
    ![](media/storage-premium-storage-performance/image1.png)

Algumas aplicações permitem-lhe tooalter as e/s tamanho, enquanto algumas aplicações não compatíveis. Por exemplo, o SQL Server determina o tamanho e/s ideal Olá próprio e não fornecer aos utilizadores quaisquer toochange botões-lo. No Olá por outro lado, Oracle fornece um parâmetro denominado [DB\_bloquear\_tamanho](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) através do qual pode configurar Olá tamanho do pedido de e/s da base de dados de Olá.

Se estiver a utilizar uma aplicação, o que não permite toochange Olá tamanho de e/s, utilize as diretrizes de Olá do desempenho de Olá toooptimize artigo KPI que é mais relevante tooyour aplicação. Por exemplo,

* Uma aplicação OLTP gera milhões de pedidos de e/s pequenos e aleatórios. pedidos de toohandle estes tipo de e/s, deve conceber a tooget de infraestrutura de aplicação IOPS superior.  
* Uma aplicação de armazém de dados gera pedidos de e/s grande e sequenciais. toohandle estes tipo de pedidos de e/s, deve conceber a tooget de infraestrutura de aplicação largura de banda superior ou de débito.

Se estiver a utilizar uma aplicação, o que permite o tamanho de e/s de Olá toochange, utilizar esta regra prática para Olá e/s tamanho, além disso, tooother diretrizes de desempenho,

* Menor tooget de tamanho de e/s IOPS superior. Por exemplo, 8 KB para uma aplicação OLTP.  
* Tooget de tamanho de e/s maior largura de banda superior/débito. Por exemplo, 1024 KB para uma aplicação de armazém de dados.

Eis um exemplo sobre como calcular Olá IOPS e débito/largura de banda para a sua aplicação. Considere uma aplicação utilizando um disco de P30. Olá IOPS máximo e débito/largura de banda de um disco de P30 pode alcançar é 5000 IOPS e 200 MB por segundo, respetivamente. Se a sua aplicação requer Olá que IOPS máximo do disco de Olá P30 e utilizar um tamanho mais pequeno de e/s como 8 KB, hello resultante da largura de banda será capaz de tooget está agora 40 MB por segundo. No entanto, se a aplicação requer Olá débito/largura de banda máxima do disco P30 e utilizar um tamanho maior de e/s como 1024 KB, hello IOPS resultante será inferior, 200 IOPS. Por conseguinte, Otimize o tamanho de e/s de Olá, de forma a que ele cumpra o requisito de IOPS e débito/largura de banda de ambos da sua aplicação. Tabela a seguir resume os tamanhos de e/s diferentes Olá e os respetivos IOPS correspondente e o débito para um disco de P30.

| Requisito da aplicação | Tamanho de e/s | IOPS | Débito/largura de banda |
| --- | --- | --- | --- |
| IOPS máximo |8 KB |5,000 |40 MB por segundo |
| Débito máximo |1024 KB |200 |200 MB por segundo |
| Débito máximo + IOPS elevado |64 KB |3,200 |200 MB por segundo |
| IOPS máximo + débito elevado |32 KB |5,000 |160 MB por segundo |

tooget IOPS e largura de banda superior ao valor máximo de Olá de um disco de armazenamento premium único, utilizar vários discos premium repartidos em conjunto. Por exemplo, stripe dois tooget de discos de P30 um IOPS combinado de IOPS 10 000 ou um débito combinado de 400 MB por segundo. Conforme explicado na secção seguinte, Olá, tem de utilizar um tamanho VM que suporte Olá combinado disco IOPS e débito.

> [!NOTE]
> Como aumentar o IOPS ou Olá débito outros também aumenta, certifique-se de que não atingiu o débito ou limites IOPS de VM ou disco Olá quando aumento deles.
>
>

toowitness Olá efeitos do tamanho de e/s no desempenho da aplicação, pode executar as ferramentas de direcionamento de caminhos na sua VM e os discos. Criar várias execuções do teste e utilizar o tamanho de e/s diferente para cada impacto de Olá toosee execução. Consulte toohello [Benchmarking](#Benchmarking) secção no final Olá deste artigo para obter mais detalhes.

## <a name="high-scale-vm-sizes"></a>Tamanhos de VM de grande escala
Quando inicia a conceber uma aplicação, uma das Olá primeiro coisas toodo é, escolha uma VM toohost a aplicação. Armazenamento Premium inclui os tamanhos de VM de escala elevada que podem ser executadas as aplicações que requerem maior capacidade de computação e um elevado desempenho de e/s de disco local. Estas VMs fornecem processadores mais rápidos, um rácio superior de memória-core e um Solid-State unidade (SSD) para disco local Olá. Exemplos de elevada de dimensionamento de VMs que suportam o Premium Storage são Olá DS, série DSv2 e GS série VMs.

Elevada de dimensionamento de VMs estão disponíveis em diferentes tamanhos com um número diferente de núcleos CPU, memória, SO e tamanho de disco temporário. Cada tamanho da VM também tem o número máximo de discos de dados que pode anexar toohello VM. Por conseguinte, o tamanho da VM Olá escolhido irá afetar quanta capacidade de processamento, memória e armazenamento está disponível para a sua aplicação. Também afeta Olá computação e o custo de armazenamento. Por exemplo, se as especificações de Olá do tamanho do maior VM Olá numa série DS, série DSv2 série e uma série GS abaixo:

| Tamanho da VM | Núcleos de CPU | Memória | Tamanhos de disco da VM | Um máximo de discos de dados | Tamanho da cache | IOPS | Limites de Cache e/s de largura de banda |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |SO = 1023 GB <br> Local SSD = 224 GB |32 |576 GB |50 000 IOPS <br> 512 MB por segundo |4000 IOPS e 33 MB por segundo |
| Standard_GS5 |32 |448 GB |SO = 1023 GB <br> Local SSD = 896 GB |64 |4224 GB |80.000 IOPS <br> 2.000 MB por segundo |5000 IOPS e 50 MB por segundo |

tooview uma lista completa de todos os tamanhos de VM do Azure disponíveis, consulte demasiado[tamanhos de Windows VM](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tamanhos de VM com Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Escolha um tamanho VM que pode satisfazer e dimensionar os requisitos de desempenho de aplicações tooyour assim o desejar. Além do toothis, tenha em conta considerações importantes sobre a seguir ao escolher tamanhos de VM.

*Limites de escala*  
Olá limites IOPS máximos por VM e por disco são diferentes e independentes entre si. Certifique-se de que a aplicação de Olá está a ocasionar IOPS dentro dos limites de Olá de Olá VM, bem como Olá premium discos anexados tooit. Caso contrário, o desempenho da aplicação verificará a limitação.

Por exemplo, suponha que um requisito da aplicação é um máximo de 4000 IOPS. tooachieve, aprovisionar um disco de P30 numa DS1 VM. disco de P30 Olá pode proporcionar segurança too5, 000 IOPS. No entanto, Olá DS1 VM é limitado too3, 200 IOPS. Por conseguinte, desempenho da aplicação Olá irá ser restrita por limite VM Olá em 3,200 IOPS e será degradação do desempenho. tooprevent nesta situação, escolha uma VM e tamanho que irá ambos os requisitos de aplicação do disco.

*Custo de operação*  
Em muitos casos, é possível que o custo global de operação de utilizar o Premium Storage é inferior ao utilizar o armazenamento Standard.

Por exemplo, considere uma aplicação que requerem 16,000 IOPS. tooachieve este desempenho, precisa de um padrão\_D14 Azure VM do IaaS, que pode dar um IOPS máximo de 16.000 utilizando 32 discos de 1 TB de armazenamento standard. Cada disco de armazenamento standard de 1TB pode alcançar um máximo de 500 IOPS. Olá calcular o custo desta VM por mês será $1,570. custo mensal do Olá 32 padrão dos discos de armazenamento será $1,638. Olá estimado total mensal de custos será $3,208.

No entanto, se lhe alojada Olá mesmo aplicação no armazenamento Premium, precisa de um tamanho VM mais pequeno e menos discos de armazenamento premium, reduzindo assim Olá custo global. Um padrão\_DS13 VM pode cumpre o requisito de IOPS de Olá 16.000 utilizando quatro P30 discos. Olá DS13 VM tem um IOPS máximo de 25,600 e cada disco P30 tem um IOPS máximo de 5000. Em geral, esta configuração pode alcançar a 5000, 4 = 20.000 IOPS. Olá calcular o custo desta VM por mês será $1,003. custo mensal do Olá quatro P30 premium dos discos de armazenamento será $544.34. Olá estimado total mensal de custos será $1,544.

Tabela a seguir resume repartição de custo de Olá deste cenário para Standard e Premium Storage.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **Custo de VM por mês** |$1,570.58 (padrão\_D14) |$1,003.66 (padrão\_DS13) |
| **Custo de discos por mês** |$1,638.40 (discos de 32 x 1 TB) |$544.34 (4 discos de x P30) |
| **Custo global por mês** |$3,208.98 |$1,544.34 |

*Distros do Linux*  

Com o Premium Storage do Azure, que obtém Olá mesmo nível de desempenho para as VMs que executam o Windows e Linux. Iremos suportar muitos tipos de Linux distros e pode ver a lista completa de Olá [aqui](../../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). É importante toonote que distros diferentes são melhor adequados para diferentes tipos de cargas de trabalho. Verá diferentes níveis de desempenho dependendo distro Olá que a carga de trabalho está em execução. Testar Olá Linux distros com a sua aplicação e escolha Olá que funciona melhor.

Quando executar o Linux com o Premium Storage, verificar atualizações mais recentes do Olá sobre os controladores necessários tooensure de elevado desempenho.

## <a name="premium-storage-disk-sizes"></a>Tamanhos de disco de armazenamento Premium
Armazenamento Premium do Azure oferece atualmente sete tamanhos de disco. Cada tamanho do disco tem um limite de escala diferentes de IOPS, largura de banda e de armazenamento. Escolha Olá tamanho de disco de armazenamento Premium direita consoante os requisitos da aplicação Olá e escala elevada de Olá tamanho da VM. tabela de Olá abaixo mostra os tamanhos de sete discos Olá e respetivas funcionalidades. Os tamanhos de P4 e P6 são atualmente só é suportada para discos geridos.

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPs por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Débito por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 


Quantos discos a escolher dependem Olá escolhida de tamanho de disco. Pode utilizar um disco de P50 único ou vários toomeet de discos de P10 o requisito da aplicação. Tenha em considerações de conta listadas abaixo quando efetuar a escolha de Olá.

*Limites de escala (IOPS e débito)*  
os limites IOPS e débito Olá de cada tamanho do disco Premium é diferente e independente de Olá limites de dimensionamento VM. Certifique-se de que Olá ESP totais e débito de discos de Olá são escolhidos, dentro dos limites de escala de Olá, tamanho da VM.

Por exemplo, se for um requisito da aplicação um máximo de 250 MB/seg débito e está a utilizar uma VM DS4 com um único disco P30. Olá DS4 VM pode desistiam too256 MB/seg débito. No entanto, um único disco P30 tem limite de débito de 200 MB/seg. Por conseguinte, irá ser restrita aplicação Olá, 200 MB por segundo devido toohello limite de disco. tooovercome este limite, aprovisionar toohello de discos dados mais do que uma VM ou redimensionar o tooP40 de discos ou P50.

> [!NOTE]
> Leituras servidas pela cache de Olá não estão incluídas no disco Olá IOPS e débito, por conseguinte, não do requerente toodisk limites. Cache tem o limite de IOPS e débito separado por VM.
>
> Por exemplo, inicialmente as leituras e escritas são 60MB/seg e 40MB/seg, respetivamente. Ao longo do tempo, a cache de Olá warms cópias de segurança e serve mais e muito mais de leituras de Olá da cache de Olá. Em seguida, pode obter escrita maior débito do disco de Olá.
>
>

*Número de discos*  
Determine o número de Olá de discos, terá de ao avaliar os requisitos da aplicação. Cada tamanho da VM também tem um limite no número de Olá de discos que pode anexar toohello VM. Normalmente, é duas vezes Olá número de núcleos. Certifique-se de que Olá tamanho da VM que escolher pode suportar Olá número de discos necessários.

Lembre-se de que tem de discos de armazenamento Premium Olá superiores discos de armazenamento do tooStandard capacidades em comparação com desempenho. Por conseguinte, se estiver a migrar a aplicação da VM do IaaS do Azure utilizando o armazenamento Standard tooPremium armazenamento, provavelmente terá menos discos premium tooachieve Olá um desempenho igual ou superior para a sua aplicação.

## <a name="disk-caching"></a>Colocação em cache do disco
VMs de escala elevada que tiram partido do Premium Storage do Azure tem uma tecnologia de colocação em cache de várias camada chamada BlobCache. BlobCache utiliza uma combinação de Olá RAM de Máquina Virtual e o local SSD para colocar em cache. Esta cache está disponível para Olá Premium Storage persistentes discos e para discos locais do Olá VM. Por predefinição, esta definição de cache é definida tooRead/escrita para discos de SO e só de leitura de discos de dados alojadas no armazenamento Premium. Com a colocação em cache no disco ativada nos discos de armazenamento Premium Olá, escala elevada de Olá VMs pode alcançar níveis de desempenho extremamente elevados que excedem o desempenho de disco subjacente Olá.

> [!WARNING]
> Alterar a definição de cache de Olá de um disco do Azure Desanexa e anexa novamente o disco de destino Olá. Se se tratar de disco do sistema operativo Olá, Olá VM é reiniciado. Pare todas as aplicações/serviços que poderão ser afetados por este interrupção antes de alterar a definição de cache do disco Olá.
>
>

toolearn mais informações sobre como funciona o BlobCache, consulte toohello dentro [Premium Storage do Azure](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) blogue.

É importante tooenable cache no conjunto de discos correto Olá. Indica se deve ativar a colocação em cache no disco num disco premium ou não irão depender padrão de carga de trabalho de Olá esse disco irá processar. Tabela abaixo mostra as predefinições de Olá definições da cache para o SO e discos de dados.

| **Tipo de disco** | **Definição de Cache predefinida** |
| --- | --- |
| Disco do SO |ReadWrite |
| Disco de dados |Nenhuma |

Seguintes são Olá definições de cache do disco recomendado para discos de dados

| **Definição de colocação em cache em disco** | **Recomendação no quando toouse esta definição** |
| --- | --- |
| Nenhuma |Configure a cache de anfitriões como None para só de escrita e pesado de escrita de discos. |
| Só de leitura |Configure a cache de anfitriões como só de leitura para só de leitura e de leitura-escrita de discos. |
| ReadWrite |Configure a cache de anfitriões como ReadWrite apenas se a aplicação processa corretamente escrita colocados em cache os discos de toopersistent de dados quando necessário. |

*Só de leitura*  
Ao configurar a colocação em cache nos dados de armazenamento Premium discos de só de leitura, pode alcançar baixa latência de leitura e obter muito elevado de IOPS de leitura e débito para a sua aplicação. Isto é por duas razões,

1. Leituras efetuada a partir da cache, o que se encontre na memória da VM Olá e local SSD, são muito mais rápidas do que leituras de disco de dados de Olá, que se encontre na Olá blob storage do Azure.  
2. Armazenamento Premium não contagem Olá leituras servidas a partir da cache, para o disco de Olá IOPS e débito. Por conseguinte, a aplicação é capaz de tooachieve superior total de IOPS e débito.

*ReadWrite*  
Por predefinição, os discos de SO Olá têm ReadWrite colocação em cache ativada. Foi recentemente adicionado suporte para a colocação em cache nos dados, bem como discos de ReadWrite. Se estiver a utilizar ReadWrite colocação em cache, tem de ter uma forma adequada toowrite Olá de dados dos discos de toopersistent da cache. Por exemplo, os identificadores SQL Server ao escrever em cache discos de armazenamento persistente de toohello de dados no seu próprio. Utilizar a cache de ReadWrite com uma aplicação que não processa Olá persistentes é necessário dados podem levar a perda de toodata, se Olá VM falhas.

Por exemplo, pode aplicar tooSQL estas diretrizes servidor em execução no armazenamento Premium efetuando o seguinte Olá,

1. Configure a cache de "ReadOnly" nos discos de armazenamento premium que alojem ficheiros de dados.  
   a.  Olá rápida lê a partir da hora de consulta de SQL Server cache inferior Olá, uma vez que as páginas de dados são obtidas muito mais rapidamente do Olá toodirectly de cache em comparação comparada discos de dados de Olá.  
   b.  Servir leituras da cache, significa que existe débito adicional disponíveis a partir dos discos de dados premium. SQL Server pode utilizar este débito adicional para obter mais páginas de dados e outras operações como a cópia de segurança/restauro, lote de cargas e Reconstrói do índice.  
2. Configurar "None" ficheiros de registo do alojamento Olá de discos de cache no armazenamento premium.  
   a.  Ficheiros de registo têm principalmente as operações de escrita pesado. Por conseguinte, estes não beneficiam das Olá cache só de leitura.

## <a name="disk-striping"></a>Disco Striping
Quando uma escala elevada de que VM está ligada com vários armazenamento persistente discos premium, discos Olá pode estar em conjunto repartidos tooaggregate os IOPs, a largura de banda e a capacidade de armazenamento.

No Windows, pode utilizar discos de toostripe de espaços de armazenamento em conjunto. Tem de configurar uma coluna para cada disco num agrupamento. Caso contrário, hello desempenho global do volume repartido pode ser menor do que o esperado devido toouneven distribuição de tráfego entre discos Olá.

Importante: Através da IU do Gestor de servidor, pode definir o número total de Olá de colunas segurança too8 para um volume repartido. Ao anexar mais de 8 discos, utilize o volume do PowerShell toocreate Olá. Utilizar o PowerShell, pode definir Olá número de colunas toohello igual número de discos. Por exemplo, se existirem 16 discos num conjunto único stripe; especificar 16 colunas na Olá *NumberOfColumns* parâmetro de Olá *New-VirtualDisk* cmdlet do PowerShell.

No Linux, utilize discos de toostripe Olá MDADM utilitário em conjunto. Para obter passos detalhados sobre discos striping no Linux, consulte demasiado[configurar RAID de Software no Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Tamanho do stripe*  
Tamanho do stripe Olá não é uma configuração importante no striping de disco. tamanho do stripe Olá ou tamanho do bloco é segmentos de menor Olá dos dados que pode abordar aplicação num volume repartido. tamanho do stripe Olá que configurar depende do tipo de Olá da aplicação e o padrão de pedido. Se escolher o tamanho do stripe errado Olá, pode levar tooIO desalinhamento, o que conduz toodegraded desempenho da sua aplicação.

Por exemplo, se um pedido de e/s gerado pela sua aplicação é superior ao tamanho do disco do stripe Olá, sistema de armazenamento Olá grava-lo entre stripe limites de unidade em mais de um disco. Quando este é tempo tooaccess esses dados, terá tooseek em mais do que um pedido de Olá do toocomplete de unidades do stripe. efeito cumulativa Olá esse comportamento pode provocar a degradação do desempenho toosubstantial. No Olá por outro lado, se Olá tamanho do pedido de e/s é inferior ao tamanho do stripe, e se é aleatória natureza, pedidos de e/s de Olá podem adicionar cópias de segurança no Olá mesmo disco causar um estrangulamento e, em última análise degradar o desempenho de e/s de Olá.

Consoante o tipo de Olá da carga de trabalho da aplicação está a executar, escolha um tamanho adequado stripe. Para pedidos de e/s pequenos aleatórios, utilize um tamanho mais pequeno do stripe. Enquanto que, para e/s sequenciais grandes de pedidos de utilizam um tamanho maior do stripe. Descobrir Olá stripe tamanho recomendações para a aplicação Olá que vai estar em execução no armazenamento Premium. Para o SQL Server, configure o tamanho do stripe de 64KB para cargas de trabalho OLTP e 256KB para cargas de trabalho de armazenamento de dados. Consulte [práticas recomendadas do SQL Server em VMs do Azure](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn mais.

> [!NOTE]
> Pode stripe em conjunto um máximo de 32 discos de armazenamento premium numa série DS VM e 64 discos de armazenamento premium numa série GS VM.
>
>

## <a name="multi-threading"></a>Os vários segmentos
Azure foi concebido toobe de plataforma de armazenamento Premium paralelo em grande escala. Por conseguinte, uma aplicação multi-thread permite um desempenho muito superior que uma aplicação single-threaded. Uma aplicação multi-thread divide as tarefas de cópia de segurança através de vários threads e aumenta a eficiência da respetiva execução por Olá através das VM e toohello de recursos de disco máximo.

Por exemplo, se a aplicação estiver a executar um único núcleo de VM com dois threads, Olá da CPU pode alternar entre eficiência de tooachieve Olá dois threads. Enquanto está em espera um thread num toocomplete de e/s de disco, Olá da CPU pode mudar toohello outro thread. Desta forma, podem realizar dois threads mais do que seria de um único thread. Se Olá VM tiver mais do que uma core, mais diminui tempo de execução, uma vez que cada core pode executar tarefas em paralelo.

Não pode ser forma de Olá toochange capaz de uma aplicação off-the-shelf implementa único thread ou vários segmentos. Por exemplo, o SQL Server é capaz de processar várias CPU e vários núcleos. No entanto, o SQL Server decide em que condições-irá tirar partido de uma ou mais threads tooprocess uma consulta. -Pode executar consultas e criar os índices com vários segmentos. Para uma consulta que envolve a associar a tabelas grandes e ordenar dados antes de o devolver toohello utilizador, SQL Server, provavelmente, irá utilizar vários threads. No entanto, um utilizador não é possível controlar se o SQL Server executa uma consulta com um thread único ou vários threads.

Existem definições de configuração que pode alterar tooinfluence neste vários segmentos ou paralela de processamento de uma aplicação. Por exemplo, no caso do SQL Server é configuração de grau de paralelismo máxima Olá. Esta definição denominada MAXDOP, permite-lhe o número máximo de Olá tooconfigure de processadores do SQL Server pode utilizar durante o processamento efetuada em paralelo. Pode configurar MAXDOP para consultas individuais ou as operações do índice. Este é vantajoso quando quiser toobalance recursos do sistema para uma aplicação de crítico de desempenho.

Por exemplo, diga a sua aplicação com o SQL Server está a executar uma grande consulta e uma operação do índice Olá mesmo tempo. Informe-nos partem do princípio de que pretendia toobe de operação do índice Olá mais performant em comparação com toohello grande consulta. Nesse caso, pode definir valor MAXDOP Olá índice operação toobe superior ao valor MAXDOP para consulta Olá de Olá. Desta forma, o SQL Server tem o número mais elevado de processadores que pode tirar partido das Olá índice operação em comparação com toohello número de processadores podem dedicar consulta grande toohello. Lembre-se de que não controla o número de Olá de threads do SQL Server irá utilizar para cada operação. Pode controlar o número máximo de Olá de processadores que está a ser dedicado para os vários segmentos.

Saiba mais sobre [graus de paralelismo](https://technet.microsoft.com/library/ms188611.aspx) no SQL Server. Determinar as definições desse tipo que influencia os vários segmentos na sua aplicação e o desempenho toooptimize configurações.

## <a name="queue-depth"></a>Profundidade de fila
Olá profundidade de fila ou o comprimento da fila ou o tamanho da fila é o número de Olá de pedidos de e/s pendentes no sistema de Olá. valor de Olá de profundidade de fila determina quantas operações e/s a aplicação pode linha, que discos de armazenamento Olá vai estar a processar. Afetará todos os Olá três aplicação indicadores de desempenho que discutimos na viz. neste artigo, IOPS, débito e latência.

Fila de profundidade e tem vários segmentos estritamente relacionados. Olá valor de profundidade de fila indica quanto os vários segmentos pode ser conseguido através da aplicação Olá. Se for grande Olá profundidade de fila, aplicação pode executar mais operações em simultâneo, por outras palavras, mais vários segmentos. Se Olá profundidade de fila é pequeno, mesmo que a aplicação tem vários threads, não terá suficiente pedidos lined cópias de segurança para execução em simultâneo.

Normalmente, desativar Olá shelf aplicações não permitem a profundidade de fila do toochange Olá, porque se configurado incorretamente executará mais perigo que boa. Aplicações definirá o valor da direita Olá de fila profundidade tooget Olá um desempenho ideal. No entanto, é importante toounderstand este conceito, de modo a que pode resolver problemas de desempenho com a sua aplicação. Também pode observar Olá os efeitos da profundidade de fila pela execução de ferramentas de direcionamento de caminhos no seu sistema.

Algumas aplicações fornecem definições tooinfluence Olá profundidade de fila. Por exemplo, definição de MAXDOP (máximo grau de paralelismo) Olá no SQL Server explicado na secção anterior. MAXDOP é uma forma tooinfluence profundidade de fila e os vários segmentos, apesar de não alterar diretamente valor de profundidade de fila de Olá do SQL Server.

*Profundidade de fila elevada*  
Uma profundidade de fila elevada de linhas de cópia de segurança mais operações no disco Olá. disco Olá sabe próximo pedido de Olá na respetiva fila de antecedência. Por conseguinte, o disco Olá pode agendar operações antecedência e processá-los numa sequência ideal. Uma vez que a aplicação Olá está a enviar mais disco de toohello de pedidos, disco de Olá pode processar mais IOs paralelas. Em última análise, a aplicação Olá será tooachieve capaz de IOPS superior. Uma vez que a aplicação está a processar mais pedidos, hello débito total da aplicação Olá também aumenta.

Normalmente, uma aplicação pode alcançar o débito máximo com 8-16 + IOs pendentes por disco ligado. Se uma profundidade de fila, aplicações não estão a enviar suficiente sistema toohello de IOs e processará menor quantidade de num determinado período. Por outras palavras, a menos débito.

Por exemplo, no SQL Server, Olá definição MAXDOP o valor para uma consulta demasiado "4" informa o SQL Server que pode utilizar segurança consulta do toofour núcleos tooexecute Olá. SQL Server irá determinar qual é melhor fila profundidade valor e Olá número de núcleos para a execução da consulta Olá.

*Profundidade de fila ideal*  
Valor de profundidade de fila muito elevado tem também as desvantagens. Se o valor de profundidade de fila é demasiado elevado, a aplicação Olá tentará toodrive IOPS muito elevada. A menos que a aplicação tem discos persistentes com IOPS aprovisionado suficientes, isto pode afetar negativamente latências da aplicação. Fórmula a seguir mostra a relação de Olá entre IOPS, a latência e a profundidade de fila.  
    ![](media/storage-premium-storage-performance/image6.png)

Não deve configurar a profundidade de fila tooany valor, mas o valor ideal tooan, que pode fornecer suficiente IOPS para a aplicação Olá sem afetar as latências. Por exemplo, se precisar de latência de aplicação Olá toobe 1 milissegundo, Olá profundidade de fila necessário tooachieve é 5000 IOPS, QD = 5000 x 0,001 = 5.

*Profundidade de fila para o Volume repartido*  
Para um volume repartido, manter uma profundidade de fila suficientemente elevada, de forma a que cada disco tem uma profundidade de fila de pico individualmente. Por exemplo, considere uma aplicação que envia uma profundidade de fila de 2 e existem 4 discos stripe Olá. pedidos de e/s dois Olá passará tootwo discos e restantes dois discos de estar inativo. Por conseguinte, configure a profundidade de fila de Olá, de modo a que todos os discos de Olá podem estar ocupados. Fórmula abaixo mostra como toodetermine Olá profundidade de fila de volumes repartidos.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Limitação
Aprovisiona de Premium Storage do Azure especificado o número de IOPS e débito dependendo dos tamanhos da VM Olá e tamanhos de disco que escolher. Sempre que a aplicação tenta toodrive IOPS ou débito acima estes limites de que Olá VM ou disco pode processar, o armazenamento Premium limitá-lo. Isto manifestos no formato Olá degradação do desempenho na sua aplicação. Isto pode significar latência superior, reduzir o débito ou reduzir o IOPS. Se não limitar o armazenamento Premium, a aplicação foi completamente falhar por exceder o que são capazes de atingirem a total dos respetivos recursos. Por isso, o desempenho tooavoid emite devida toothrottling, sempre Aprovisionar recursos suficientes para a sua aplicação. Tenha em consideração que discutimos na tamanhos de VM Olá e secções de tamanhos de disco acima. Direcionamento de caminhos é Olá melhor forma toofigure saída que recursos irá necessitar toohost a aplicação.

## <a name="benchmarking"></a>Direcionamento de caminhos
Direcionamento de caminhos é o processo de Olá de simulando diferentes cargas de trabalho na sua aplicação e medir o desempenho da aplicação Olá para cada carga de trabalho. Utilizando os passos de Olá descritos uma secção anterior, se recolheu requisitos de desempenho de aplicação Olá. Ao executar o direcionamento de caminhos de ferramentas em VMs Olá alojar a aplicação Olá, pode determinar os níveis de desempenho de Olá que a aplicação pode alcançar com o Premium Storage. Nesta secção, iremos fornecer exemplos de direcionamento de caminhos de uma VM DS14 padrão aprovisionado com discos Premium Storage do Azure.

Ter utilizámos ferramentas comuns de direcionamento de caminhos Iometer e FIO, para o Windows e Linux, respetivamente. Estas ferramentas gerar vários threads simulando uma produção, como a carga de trabalho e o desempenho do sistema de Olá de medida. Utilizar ferramentas de Olá também pode configurar parâmetros, como o bloco a profundidade tamanho e a fila, que normalmente não é possível alterar para uma aplicação. Isto fornece mais flexibilidade toodrive Olá máximo desempenho numa escala elevada VM aprovisionado com discos premium para diferentes tipos de cargas de trabalho da aplicação. toolearn mais informações sobre cada ferramenta benchmarking visitam [Iometer](http://www.iometer.org/) e [FIO](http://freecode.com/projects/fio).

Exemplos de Olá toofollow abaixo, crie uma VM DS14 padrão e anexe 11 toohello de discos de armazenamento Premium VM. Discos de Olá 11, configure 10 discos com o anfitrião a colocação em cache como "None" e stripe-los para um volume chamado NoCacheWrites. Configurar o anfitrião como "ReadOnly" colocação em cache em disco restante Olá e criar um volume chamado CacheReads com este disco. Utilizar esta configuração, será capaz de toosee Olá máximo leitura e escrita de desempenho de uma VM DS14 padrão. Para obter passos detalhados sobre como criar uma VM DS14 com discos premium, aceda demasiado[criar e utilizar a conta de armazenamento Premium para um disco de dados de máquina virtual](../storage-premium-storage.md).

*Aquecer Olá Cache*  
disco Olá com anfitrião só de leitura a colocação em cache será capaz de toogive IOPS superior ao limite de disco Olá. tooget deste máximo ler o desempenho da cache do anfitrião de Olá, primeiro tem warm cache Olá este disco. Isto garante que Olá IOs de leitura que ferramenta benchmarking provocarão no volume de CacheReads, na verdade, chega a cache de Olá e não discos de Olá diretamente. resultado de pedidos com êxito na cache Olá no adicionais de IOPS de cache individual Olá ativada disco.

> **Importante:**  
> Tem warm cache Olá antes de executar o direcionamento de caminhos, sempre que a VM é reiniciada.
>
>

#### <a name="iometer"></a>Iometer
[Transferir a ferramenta de Iometer Olá](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) no Olá VM.

*Ficheiro de teste*  
Iometer utiliza um ficheiro de teste que está armazenado no volume de Olá em que serão executadas Olá direcionamento de caminhos de teste. Unidades de leituras e escritas neste teste disco dos ficheiros toomeasure Olá IOPS e débito. Iometer cria este ficheiro de teste se não tiver sido fornecido um. Crie um ficheiro de teste de 200GB chamado iobw.tst nos volumes de CacheReads e NoCacheWrites Olá.

*Especificações de acesso*  
Olá especificações, tamanho do pedido e/s, % leitura/escrita, % aleatório/sequenciais são configurados utilizando o separador de "Acesso especificações" Olá no Iometer. Crie uma especificação de acesso para cada um dos cenários de Olá descritos abaixo. Criar as especificações de acesso de Olá e "Guardar" apropriadas com o nome como – RandomWrites\_8K, RandomReads\_8 K. Selecione especificação correspondente Olá ao executar o cenário de teste de Olá.

Um exemplo de especificações de acesso para o cenário de escrever IOPS máximo é mostrado abaixo,  
    ![](media/storage-premium-storage-performance/image8.png)

*Especificações de teste IOPS máximo*  
máximo de toodemonstrate IOPs, utilize o tamanho mais pequeno do pedido. Utilize o tamanho do pedido de 8K e criar especificações das escritas aleatórias e leituras.

| Especificação de acesso | Tamanho do pedido | % Aleatório | % De leitura |
| --- | --- | --- | --- |
| RandomWrites\_8 K |8K |100 |0 |
| RandomReads\_8 K |8K |100 |100 |

*Especificações de teste de débito máximo*  
toodemonstrate débito máximo, utilize maior tamanho do pedido. Utilize o tamanho do pedido de 64 KB e crie especificações das escritas aleatórias e leituras.

| Especificação de acesso | Tamanho do pedido | % Aleatório | % De leitura |
| --- | --- | --- | --- |
| RandomWrites\_64K |64 KB |100 |0 |
| RandomReads\_64K |64 KB |100 |100 |

*Executar Olá Iometer teste*  
Execute os passos de Olá abaixo toowarm segurança cache

1. Criar dois especificações de acesso com valores mostrados abaixo,

   | Nome | Tamanho do pedido | % Aleatório | % De leitura |
   | --- | --- | --- | --- |
   | RandomWrites\_1 MB |1MB |100 |0 |
   | RandomReads\_1 MB |1MB |100 |100 |
2. Execute o teste de Iometer Olá para inicializar o disco de cache com os seguintes parâmetros. Utilize três threads de trabalho para o volume de destino Olá e uma profundidade de fila de 128. Definir Olá duração Olá teste too2hrs no separador de "Testar o programa de configuração" Olá "Tempo de execução".

   | Cenário | Volume de destino | Nome | Duração |
   | --- | --- | --- | --- |
   | Inicialize o disco de Cache |CacheReads |RandomWrites\_1 MB |2hrs |
3. Execute o teste de Iometer Olá para aquecer os discos de cache com os seguintes parâmetros. Utilize três threads de trabalho para o volume de destino Olá e uma profundidade de fila de 128. Definir Olá duração Olá teste too2hrs no separador de "Testar o programa de configuração" Olá "Tempo de execução".

   | Cenário | Volume de destino | Nome | Duração |
   | --- | --- | --- | --- |
   | Transfira a cópia de segurança disco de Cache |CacheReads |RandomReads\_1 MB |2hrs |

Depois de disco de cache é preparado, prossiga com cenários de teste de Olá listados abaixo. Olá toorun Iometer teste, utilizar, pelo menos, três threads de trabalho para **cada** volume de destino. Para cada thread de trabalho, selecione o volume de destino Olá, definir a profundidade de fila e selecione uma das especificações de teste de Olá guardada, conforme mostrado na tabela de Olá abaixo, o cenário de teste do toorun Olá correspondente. tabela de Olá também mostra resultados esperados para o IOPS e débito ao executar estes testes. Para todos os cenários, são utilizados um tamanho de e/s pequeno de 8KB e uma profundidade de fila elevada de 128.

| Cenário de teste | Volume de destino | Nome | resultado |
| --- | --- | --- | --- |
| Um máximo de IOPS de leitura |CacheReads |RandomWrites\_8 K |50 000 IOPS |
| Um máximo de Escrever IOPS |NoCacheWrites |RandomReads\_8 K |64,000 IOPS |
| Um máximo de IOPS combinada |CacheReads |RandomWrites\_8 K |100 000 IOPS |
| NoCacheWrites |RandomReads\_8 K | &nbsp; | &nbsp; |
| Um máximo de Ler MB/seg |CacheReads |RandomWrites\_64K |524 MB/seg |
| Um máximo de Escrever MB/seg |NoCacheWrites |RandomReads\_64K |524 MB/seg |
| Combinado MB/seg |CacheReads |RandomWrites\_64K |1000 MB/seg |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

Seguem-se capturas de ecrã da Olá Iometer resultados do teste para cenários combinados de IOPS e débito.

*IOPS máximo combinado de leituras e escritas*  
![](media/storage-premium-storage-performance/image9.png)

*Débito máximo combinado de leituras e escritas*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO é um armazenamento toobenchmark ferramenta populares Olá VMs com Linux. Tem tamanhos de e/s Olá flexibilidade tooselect diferentes, de leituras sequenciais ou aleatórias e de escrita. -Cria threads de trabalho ou Olá tooperform de processos especificado operações de e/s. Pode especificar tipo de Olá de operações de e/s, que cada thread de trabalho tem de efetuar a utilizar ficheiros de tarefa. Foi criada uma tarefa ficheiro por cenário ilustrado nos exemplos de Olá abaixo. Pode alterar as especificações de Olá nestes tarefa ficheiros toobenchmark diferentes cargas de trabalho em execução no armazenamento Premium. Nos exemplos de Olá, estamos a utilizar uma execução de VM de 14 DS Standard **Ubuntu**. Olá de utilizar a mesma configuração descrita no início Olá Olá [direcionamento de caminhos de secção](#Benchmarking) e transfira a cópia de segurança cache Olá antes de executar Olá direcionamento de caminhos de testes.

Antes de começar, [transferir FIO](https://github.com/axboe/fio) e instalá-lo na sua máquina virtual.

Execute os seguintes comandos para Ubuntu, de Olá

```
apt-get install fio
```

Utilizaremos quatro threads de trabalho para influenciar a operações de escrita e quatro threads de trabalho para operações de leitura despertar nos discos de Olá. Olá trabalhadores de escrita irão ser impulsionar o tráfego no volume de nocache"Olá", que tem 10 discos com a cache de definido demasiado "None". Olá trabalhadores de leitura irão ser impulsionar o tráfego no volume de readcache"Olá", cujo 1 disco com o conjunto de cache demasiado "ReadOnly".

*Escrita máxima IOPS*  
Criar ficheiro de tarefa Olá com as seguintes especificações tooget IOPS máximo de escrita. Nome "fiowrite.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Olá nota siga coisas chaves que estão de acordo com as diretrizes de conceção de Olá abordadas nas secções anteriores. Estas especificações são essencial toodrive IOPS máximo,  

* Uma profundidade de fila elevada de 256.  
* Um tamanho de pequeno bloco de 8KB.  
* Vários threads efetuar gravações aleatórias.

Execute os seguintes comandos tookick desativar Olá FIO testar para 30 segundos, de Olá  

```
sudo fio --runtime 30 fiowrite.ini
```

Enquanto executa o teste de Olá, será o número de Olá toosee capaz de escrita de discos VM e Premium da Olá IOPS estão a fornecer. Conforme mostrado no exemplo Olá abaixo, Olá DS14 VM é a distribuição respetiva limite de IOPS de 50 000 IOPS de escrita máxima.  
    ![](media/storage-premium-storage-performance/image11.png)

*Leitura máxima IOPS*  
Criar ficheiro de tarefa Olá com as seguintes especificações tooget IOPS máximo de leitura. Nome "fioread.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Olá nota siga coisas chaves que estão de acordo com as diretrizes de conceção de Olá abordadas nas secções anteriores. Estas especificações são essencial toodrive IOPS máximo,

* Uma profundidade de fila elevada de 256.  
* Um tamanho de pequeno bloco de 8KB.  
* Vários threads efetuar gravações aleatórias.

Execute os seguintes comandos tookick desativar Olá FIO testar para 30 segundos, de Olá

```
sudo fio --runtime 30 fioread.ini
```

Enquanto executa o teste de Olá, será capaz de toosee Olá diversas leitura IOPS Olá VM e os discos Premium são entrega. Conforme mostrado no exemplo Olá abaixo, Olá DS14 VM é a distribuição 64,000 mais de IOPS de leitura. Esta é uma combinação de disco Olá e desempenho da cache de Olá.  
    ![](media/storage-premium-storage-performance/image12.png)

*IOPS máxima leitura e escrita*  
Criar ficheiro de tarefa Olá com seguintes tooget especificações máximo combinado de leitura e escrita IOPS. Nome "fioreadwrite.ini".

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Olá nota siga coisas chaves que estão de acordo com as diretrizes de conceção de Olá abordadas nas secções anteriores. Estas especificações são essencial toodrive IOPS máximo,

* Uma profundidade de fila elevada de 128.  
* Um tamanho de pequenos blocos de 4KB.  
* Vários threads efetuar aleatório lê e escreve.

Execute os seguintes comandos tookick desativar Olá FIO testar para 30 segundos, de Olá

```
sudo fio --runtime 30 fioreadwrite.ini
```

Enquanto executa o teste de Olá, irá ser capaz de toosee Olá número combinado leitura e escrita IOPS Olá VM e os discos Premium são entrega. Conforme mostrado no exemplo Olá abaixo, Olá DS14 VM é a distribuição de IOPS de escrita e leitura de combinado mais de 100 000. Esta é uma combinação de disco Olá e desempenho da cache de Olá.  
    ![](media/storage-premium-storage-performance/image13.png)

*Máximo combinado de débito*  
Olá tooget máximo combinado de leitura e escrita débito, utilize um tamanho de bloco maior e a profundidade de fila grande com vários threads efetuar leituras e escritas. Pode utilizar um tamanho de bloco de 64KB e a profundidade de fila de 128.

## <a name="next-steps"></a>Passos Seguintes
Saiba mais sobre o Premium Storage do Azure:

* [Armazenamento Premium: Armazenamento de Elevado Desempenho para Cargas de Trabalho de Máquinas Virtuais do Azure](../storage-premium-storage.md)  

Para utilizadores do SQL Server, leia os artigos sobre melhores práticas de desempenho para o SQL Server:

* [Melhores práticas do desempenho para o SQL Server em Virtual Machines do Azure](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Armazenamento Premium do Azure fornece mais elevado desempenho para o SQL Server na VM do Azure](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
