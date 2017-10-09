---
title: aaaDistribute dados globalmente com a base de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre a recuperação de dados, ativação pós-falha e a georreplicação de planet escala bases de dados global do Azure Cosmos DB, um serviço de base de dados globalmente distribuídas, o modelo de estiverem a utilizar."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Como toodistribute dados globalmente com o Azure Cosmos DB
Azure ubíquo - tem um requisitos de espaço global em 30 + regiões geográficas e continuamente está a expandir. Com a presença em todo o mundo, uma das capacidades de Olá diferenciada que Azure oferece aos programadores de tooits é Olá toobuild de capacidade, implementar e gerir facilmente aplicações distribuídas global. 

O [Azure Cosmos DB](../cosmos-db/introduction.md) é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft para aplicações críticas para atividades. BD do Azure do Cosmos fornece chave na mão distribuição global, [dimensionamento elástico de débito e armazenamento](../cosmos-db/partition-data.md) latências milissegundo em todo o mundo, dígito em percentil de 99th Olá, [cinco níveis de consistência bem definidos ](consistency-levels.md)e garantida elevada disponibilidade, todas as cópia por [líder da indústria SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/). BD do Azure do Cosmos [indexa automaticamente os dados](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sem necessidade de toodeal com a gestão de esquema e o índice. É multimodal e suporte modelos de dados em documentos, chaves-valores, gráficos e em colunas. Como um serviço em nuvem-born, base de dados do Azure Cosmos cuidadosamente foi desenvolvido com vários inquilinos e global a distribuição de Olá fundo cópias de segurança.

**Uma única coleção da base de dados do Azure Cosmos particionado e distribuídos por várias regiões do Azure**

![Coleção do Azure do Cosmos DB particionado e distribuídos três regiões](./media/distribute-data-globally/global-apps.png)

Como podemos ter aprendidas durante a criação da base de dados do Azure Cosmos, distribuição global a adicionar não é possível posteriori - não pode ser "bolted-ativado" visível um sistema de base de dados "único site". capacidades de Olá oferecidas por uma base de dados globalmente distribuída span se para além dos que de desastre geográfica tradicional recuperação (Georreplicação DR) oferecidas pelas bases de dados "site único". Bases de dados de site único oferece a capacidade de DR Georreplicação são um subconjunto restrito de bases de dados globalmente distribuídas. 

Com distribuição global chave na mão da BD do Cosmos do Azure, os programadores não dispõe de toobuild os seus próprios andaime de replicação ao empregar o padrão de Lambda Olá (por exemplo, [AWS DynamoDB replicação](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) ao longo do registo da base de dados de Olá ou pelo a fazer "escritas duplas" em várias regiões. Não foi recomendado estas abordagens, uma vez que é impossível tooensure correcção de tais abordagens e fornecer SLAs de som. 

Neste artigo, podemos fornecer uma descrição geral das capacidades de distribuição global da BD do Cosmos do Azure. Podemos também descrevem tooproviding de abordagem exclusivo da BD do Azure Cosmos SLAs abrangentes. 

## <a id="EnableGlobalDistribution"></a>Ativar distribuição global chave na mão
BD do Azure do Cosmos fornece seguinte Olá capacidades tooenable tooeasily escrever as aplicações de dimensionamento planet. Estas capacidades estão disponíveis através do recurso da BD de Olá, Azure Cosmos baseado em fornecedores [REST APIs](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) , bem como Olá portal do Azure.

### <a id="RegionalPresence"></a>Presença regional ubíqua 
Azure está constantemente a crescer a presença geográfica colocando [regiões novo](https://azure.microsoft.com/regions/) online. BD do Cosmos do Azure está disponível em todas as regiões do Azure nova por predefinição. Isto permite-lhe tooassociate uma região geográfica com a sua conta de base de dados de base de dados do Azure Cosmos assim que a Azure abre-se a região de nova hello para empresas.

**BD do Cosmos do Azure está disponível em todas as regiões do Azure por predefinição**

![DB de Cosmos do Azure disponíveis em todas as regiões do Azure](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Associar um número ilimitado de regiões com a sua conta de base de dados de base de dados do Azure Cosmos
BD do Cosmos do Azure permite-lhe tooassociate qualquer número de regiões do Azure com a base de dados do Azure Cosmos conta de base de dados. Fora geométrico restrições (por exemplo, China, Datacenters), existem não existem limitações número Olá das regiões que podem ser associados a sua conta de base de dados de base de dados do Azure Cosmos. Olá figura a seguir mostra um toospan da conta configurada de base de dados em 25 regiões do Azure.  

**Conta de expansão 25 regiões do Azure da base de dados do Azure Cosmos DB um inquilino**

![Conta de base de dados do Azure do Cosmos DB expansão 25 regiões do Azure](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Baseado na política barreiras geográficas
BD do Azure do Cosmos é concebida toohave baseadas em políticas geométrico capacidades. Geométrico é um componente importante tooensure restrições de governação e conformidade de dados e pode impedir a associação de uma região específica com a sua conta. Exemplos de geométrico incluir (mas não estão limitados a), o âmbito de regiões de toohello distribuição global dentro de uma nuvem sovereign (por exemplo, China e na Alemanha) ou numa zona de taxation government (por exemplo, da Austrália). políticas de Olá são controladas através de metadados de Olá da sua subscrição do Azure.

### <a id="DynamicallyAddRegions"></a>Adicionar e remover regiões dinamicamente
BD do Cosmos do Azure permite-lhe tooadd (associar) ou remova (desassociar) conta de base de dados de tooyour regiões em qualquer altura (consulte [figura anterior](#UnlimitedRegionsPerAccount)). Em virtude replicar dados em partições em paralelo, base de dados do Azure Cosmos assegura que quando uma região de novo a ficar online, BD do Cosmos Azure está disponível dentro de 30 minutos em qualquer local no mundo Olá para cópia de segurança too100 TBs. 

### <a id="FailoverPriorities"></a>Prioridades de ativação pós-falha
toocontrol sequência exato de ativações pós-falha regional quando existe uma falha de múltiplos regional, base de dados do Azure Cosmos permite-lhe tooassociate Olá prioridade toovarious as regiões associadas à conta de base de dados de Olá (consulte Olá figura a seguir). BD do Azure do Cosmos garante que a sequência de ativação pós-falha automática Olá ocorre por ordem de prioridade de Olá que especificou. Para obter mais informações sobre as ativações pós-falha regional, consulte [automáticas ativações pós-falha regional para continuidade do negócio do BD Azure Cosmos](regional-failover.md).

**Um inquilino do Azure Cosmos DB pode configurar a ordem de prioridade de ativação pós-falha do Olá (painel direito) para regiões associadas com uma conta de base de dados**

![Configuração de ativação pós-falha de prioridades, com base de dados do Azure Cosmos](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Dinamicamente a demorar "offline" de uma região
BD do Cosmos do Azure permite-lhe tootake a base de dados offline da conta numa região específica e colocá-lo novamente online mais tarde. Regiões marcadas offline não ativamente participam na replicação e não fazem parte da sequência de ativação pós-falha de Olá. Isto permite-lhe Olá toofreeze conhecido última imagem da base de dados bom dos Olá leia regiões antes disponibilizando potencialmente arriscados atualiza tooyour aplicação.

### <a id="ConsistencyLevels"></a>Vários modelos de consistência bem definidos para as bases de dados global replicadas
BD do Azure do Cosmos expõe [vários níveis de consistência bem definidos](consistency-levels.md) SLAs de segurança. Pode escolher um modelo de consistência específico (partir Olá disponíveis lista de opções), dependendo da carga de trabalho de Olá/cenários. 

### <a id="TunableConsistency"></a>Consistência ajustáveis para bases de dados globalmente replicadas
BD do Cosmos do Azure permite-lhe ignorar tooprogrammatically e reduzir a escolha de consistência predefinida Olá numa base por pedido, em tempo de execução. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Leitura dinamicamente configurável e regiões de escrita
BD do Cosmos do Azure permite-lhe regiões de Olá tooconfigure (associada à base de dados de Olá) para "leitura", "escrever" ou "leitura/escrita" regiões. 

### <a id="ElasticallyScaleThroughput"></a>Débito aprovisionadas dimensionamento em regiões do Azure
Pode dimensionar uma coleção de base de dados do Azure Cosmos pelo débito aprovisionamento através de programação. débito Olá é aplicado tooall regiões de Olá coleção Olá é distribuída no.

### <a id="GeoLocalReadsAndWrites"></a>Georreplicação local lê e escreve
Olá principal vantagem de uma base de dados globalmente distribuída é toooffer baixa latência acesso toohello dados em qualquer lugar Olá mundo. BD do Azure do Cosmos oferece garantias de latência baixa em P99 para várias operações de base de dados. Assegura que todas as leituras são encaminhadas toohello região de leitura local mais próximo. é utilizado tooserve um pedido de leitura, região local toohello quórum de Olá em que é emitido Olá, ler; Olá mesmo se aplica toohello escritas. Uma operação de escrita é confirmada apenas depois de a maioria das réplicas de forma durável consolidou escrita Olá localmente, mas sem ser gated em réplicas remoto tooacknowledge Olá escritas. Protocolo de replicação de Olá da base de dados do Azure Cosmos colocar de forma diferente, funciona em pressuposto Olá que Olá leitura e escrita quorums são sempre local toohello leitura e escrita regiões, respetivamente, no qual pedido Olá é emitido.

### <a id="ManualFailover"></a>Iniciar manualmente a ativação pós-falha
BD do Cosmos do Azure permite-lhe tootrigger Olá ativação pós-falha de Olá de toovalidate de conta de base de dados de Olá *terminar tooend* propriedades de disponibilidade da aplicação todo do Olá (para além da base de dados de Olá). Uma vez que ambos Olá segurança e propriedades de liveness de eleição de deteção e leader de falha de Olá garantidas, garante que a base de dados do Azure Cosmos *perda de dados de zero* para uma operação de ativação pós-falha manual iniciadas por inquilino.

### <a id="AutomaticFailover"></a>Ativação pós-falha automática
BD do Cosmos do Azure suporta a ativação pós-falha automática no caso de um ou mais falhas regionais. Durante uma ativação pós-falha regional, base de dados do Azure Cosmos mantém a leitura, disponibilidade de tempo de atividade, consistência, débito e latência SLAs. BD do Cosmos do Azure fornece um limite superior no Olá enquanto estiver em curso uma toocomplete de operação de ativação pós-falha automática. Esta é a janela de Olá da potencial perda de dados durante a falha regional Olá.

### <a id="GranularFailover"></a>Concebido para granularidades diferentes de ativação pós-falha
Atualmente Olá automática e capacidades de ativação pós-falha manual são expostas granularidade Olá da conta de base de dados de Olá. Tenha em atenção, internamente BD do Azure Cosmos é concebida toooffer *automática* ativação pós-falha granularidade melhorar de uma base de dados, coleção ou mesmo uma partição (de uma coleção de proprietário de um intervalo de chaves). 

### <a id="MultiHomingAPIs"></a>APIs multi homing no Azure Cosmos DB
BD do Cosmos do Azure permite-lhe toointeract com base de dados de Olá utilizando lógica (agnóstico de região) ou físicos (região específicos) pontos finais. Utilizar pontos finais lógicos garante que a aplicação de Olá transparente pode ser multihomed em caso de ativação pós-falha. Olá pontos finais de última, físicos, indique um controlo detalhado toohello aplicação tooredirect lê e escreve toospecific regiões.

Pode encontrar informações sobre como tooconfigure ler preferências para Olá [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md), [Graph API](../cosmos-db/tutorial-global-distribution-graph.md), [API de tabela](../cosmos-db/tutorial-global-distribution-table.md), e [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)no seu respetivo ligado artigos.

### <a id="TransparentSchemaMigration"></a>Migração de esquema e o índice da base de dados transparente e consistente 
BD do Azure do Cosmos é totalmente [agnóstico esquema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). estrutura de exclusivo Olá do seu motor de base de dados permite tooautomatically e forma síncrona índice todos os dados de Olá-ingere sem necessidade de qualquer esquema ou índices secundários do utilizador. Isto permite tooiterate a aplicação distribuída globalmente rapidamente sem ter de se preocupar sobre a migração de esquema e o índice da base de dados ou coordenar a implementação de aplicação de fase multi de alterações ao esquema. BD do Azure do Cosmos garante que as políticas de tooindexing de alterações que tiver realizadas explicitamente não resultar numa degradação do desempenho ou disponibilidade.  

### <a id="ComprehensiveSLAs"></a>SLAs abrangentes (para além das apenas elevada disponibilidade)
Como um serviço de base de dados globalmente distribuída, base de dados do Azure Cosmos oferece SLA definida especificamente para **perda de dados**, **disponibilidade**, **latência em P99**, **débito**  e **consistência** da base de dados de Olá como um todo, independentemente do número de Olá das regiões associadas a base de dados de Olá.  

## <a id="LatencyGuarantees"></a>Garantias de latência
Olá vantagem de um serviço de base de dados globalmente distribuída como base de dados do Azure Cosmos é toooffer baixa latência acesso tooyour dados em qualquer lugar Olá mundo. BD do Azure do Cosmos oferece garantida baixa latência em P99 para várias operações de base de dados. protocolo de replicação de Olá BD do Cosmos Azure emprega garante que Olá operações de base de dados (Idealmente, lê e escreve) são sempre executados no Olá região toothat local do cliente de Olá. Latência de Olá que BD do Cosmos SLA do Azure inclui P99 para leituras, escritas (forma síncrona) indexadas e consultas para vários tamanhos de pedido e resposta. Olá garantias de latência para escritas incluem consolidações de quórum maioria durável num centro de dados local Olá.

### <a id="LatencyAndConsistency"></a>Relação da latência com consistência 
Para uma serviço globalmente distribuído toooffer consistência forte na configuração globalmente distribuída, tem de toosynchronously Olá replicar escritas ou síncrona efetuar por várias regiões leituras – velocidade Olá de claro e Olá alargada rede fiabilidade da sua organização ditarem a consistência forte resulta no latências altas e baixa disponibilidade das operações de base de dados. Por conseguinte, na ordem toooffer garantida baixas latências P99 e disponibilidade 99.99, serviço Olá tem de utilizar replicação assíncrona. Esta por sua vez requer que o serviço de Olá tem também oferecem [choice(s) de consistência bem definidos, simples](consistency-levels.md) – mais fraco que segura (toooffer baixas latência e disponibilidade garantias) e Idealmente mais forte do que (consistência "eventual" toooffer um modelo de programação intuitivo).

BD do Azure do Cosmos garante que uma operação de leitura não é necessário toocontact réplicas em várias regiões toodeliver Olá consistência específico nível garantia. Da mesma forma, garante que uma operação de escrita não obter bloqueada enquanto está a ser replicados dados Olá em todas as regiões de Olá (ou seja, escritas no modo assíncrono replicadas em regiões). Para contas de base de dados de multirregião estão disponíveis vários níveis de consistência simples. 

### <a id="LatencyAndAvailability"></a>Relação da latência com disponibilidade 
Disponibilidade e latência são dois lados de Olá de Olá coin mesmo. Iremos falar sobre latência da operação de Olá num Estado de repouso e disponibilidade, em enfrentam Olá de falhas. A partir do ponto de vista de aplicação Olá, uma operação de base de dados em execução lenta é indistinguishable da base de dados que não está disponível. 

toodistinguish latência elevada de indisponibilidade, base de dados do Azure Cosmos fornece um limite superior absoluto de latência de várias operações de base de dados. Se a operação de base de dados de Olá demora mais que toocomplete de limite superior de Olá, Azure Cosmos DB devolve um erro de tempo limite. Olá SLA de disponibilidade de base de dados do Azure Cosmos garante que os tempos limite de Olá são contados face às SLA de disponibilidade de Olá. 

### <a id="LatencyAndThroughput"></a>Relação da latência com débito
BD do Azure do Cosmos não fazer com que escolher entre a latência e débito. Este honra Olá SLA para ambos os latência em P99 e fornecer o débito de Olá que aprovisionou. 

## <a id="ConsistencyGuarantees"></a>Garantias de consistência
Ao hello [modelo consistência forte](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) é Olá gold padrão de programação para, vem no preço muito acentuada Olá latência elevada (no estado de repouso) e a perda de disponibilidade (em enfrentam Olá de falhas). 

BD do Cosmos do Azure oferece uma bem definidos tooreason de tooyou de modelo programação sobre consistência de dados replicados. Na ordem tooenable toobuild multihomed aplicações, modelos de consistência Olá expostos pela base de dados do Azure Cosmos desconhecem toobe concebida região e não dependem da região de Olá de onde são servidas Olá leituras e escritas. 

Azure DB de Cosmos consistência SLA garante que cumpra garantia de consistência de Olá para o nível de consistência Olá pedida por si o (Olá nível predefinido de consistência na conta de base de dados de Olá ou valor de Olá substituída no pedido de Olá 100% de pedidos de leitura ). Um pedido de leitura é considerado toohave cumprido Olá consistência SLA se todas as garantias de consistência Olá associadas a nível de consistência Olá forem satisfeitas. Olá seguinte tabela captura garantias de consistência de Olá que correspondem níveis de consistência toospecific oferecidas pelo Azure Cosmos DB.

**Garantias de consistência associadas a um nível de consistência indicado do BD Azure Cosmos**

<table>
    <tr>
        <td><strong>Nível de consistência</strong></td>
        <td><strong>Características de consistência</strong></td>
        <td><strong>SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">Sessão</td>
        <td>Ler a suas próprias escrita</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Leitura monotonic</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefixo consistente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Obsoletismo</td>
        <td>Ler Monotonic (dentro de uma região)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefixo consistente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Vinculada vinculada &lt; K, T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefixo consistente</td>
        <td>Prefixo consistente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Forte</td>
        <td>Linearizable</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relação da consistência com a disponibilidade
Olá [resultado impossibility](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) de Olá [theorem extremidade](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) comprova que é realmente impossível para Olá sistema tooremain disponível e consistência linearizable de oferta no enfrentam Olá de falhas. serviço de base de dados de Olá tem de escolher toobe CP ou AP - sistemas CP potente disponibilidade favor consistência linearizable enquanto sistemas Olá da Ásia-Pacífico potente [consistência linearizable](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) favor de disponibilidade. BD do Azure do Cosmos nunca viola Olá nível de consistência, o que torna formally um sistema de CP de pedido. No entanto, na prática, consistência não é uma proposta todas ou nada – existem vários modelos de consistência bem definidos ao longo do espetro de consistência Olá entre consistência linearizable e eventual. Na base de dados do Azure Cosmos ter tentámos tooidentify vários Olá flexibilizadas modelos de consistência com a aplicabilidade de mundo real e um modelo de programação intuitivo. BD do Azure do Cosmos navega fala de disponibilidade de consistência Olá, oferecendo juntamente com um SLA de disponibilidade 99.99 [flexibilizadas de vários níveis de consistência ainda bem definidos](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Relação da consistência com latência
Uma variação mais abrangente da extremidade foi proposta por Prof. Daniel Abadi e é denominado [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), que também as contas do fala latência e consistência no estado de repouso. Indica que o estado de repouso, sistema de base de dados de Olá tem de escolher entre a consistência e latência. Com vários modelos de consistência simples (associados a replicação assíncrona e local leitura, escrita quorums), a base de dados do Azure Cosmos garante que todas as leituras e escritas são local toohello leitura e escrita regiões, respetivamente.  Isto permite que a base de dados do Azure Cosmos toooffer baixa latência garante numa região de Olá para níveis de consistência Olá.  

### <a id="ConsistencyAndThroughput"></a>Relação da consistência com débito
Uma vez que a implementação de Olá de um modelo de consistência específico depende de escolha de Olá de um [tipo quórum](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), débito de Olá também varia com base na escolha de Olá de consistência. Por exemplo, na base de dados do Azure Cosmos hello débito com leituras vivamente consistentes é toothat aproximadamente meio de leituras eventualmente consistentes. 
 
**Relação de capacidade de leitura para um nível específico de consistência na base de dados do Azure Cosmos**

![Relação entre a consistência e débito](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Garantias de débito 
BD do Cosmos do Azure permite-lhe tooscale débito (bem como, armazenamento), aprovisionadas em regiões diferentes consoante a pedido de Olá. 

**Uma única coleção da base de dados do Azure Cosmos particionados (em três shards) e, em seguida, distribuída em três regiões do Azure**

![BD do Azure do Cosmos distribuída e coleções de partições](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Uma coleção de base de dados do Azure Cosmos obtém distribuída utilizando duas dimensões – numa região e, em seguida, em regiões. Eis como: 

* Numa única região, uma coleção de base de dados do Azure Cosmos é ampliada em termos de partições de recursos. Cada partição de recursos gere um conjunto de chaves e é vivamente consistente e altamente disponível em virtude da replicação da máquina de estado entre um conjunto de réplicas. BD do Cosmos do Azure é um sistema de recurso regido totalmente onde uma partição de recursos é responsável por fornecer a partilha de débito para atribuição de Olá de sistema recursos alocados tooit. Olá dimensionamento de uma coleção de base de dados do Azure Cosmos é completamente transparente – BD do Cosmos Azure gere as partições de recursos de Olá divide e intercala-la conforme necessário. 
* Em seguida, cada uma das partições de recursos de Olá é distribuída em várias regiões. O proprietário de partições de recurso Olá mesmo conjunto de chaves em várias regiões o formulário partição conjunto (consulte [figura anterior](#ThroughputGuarantees)).  As partições de recursos dentro de um conjunto de partição são coordenadas utilizando a replicação da máquina de estado entre Olá várias regiões. Dependendo do nível de consistência de Olá configurado, as partições de recursos de Olá dentro de um conjunto de partição estão configuradas dinamicamente com diferentes topologias (por exemplo, Estrela daisy cadeia, árvore etc.). 

Em virtude de uma partição extremamente reativo gestão, o balanceamento de carga e governação de recursos restrito, base de dados do Azure Cosmos permite-lhe tooelastically débito de escala em várias regiões do Azure de uma coleção de BD do Cosmos do Azure. Débito de mudança de uma coleção é uma operação de tempo de execução na base de dados do Azure Cosmos - como com outras operações de base de dados do Azure Cosmos DB garante Olá absoluto limite superior de latência para o débito do pedido toochange Olá. Por exemplo, Olá figura a seguir mostra a coleção de um cliente com débito aprovisionado aprovisionadas (entre 1 milhão - 10M pedidos/seg em duas regiões) com base na procura Olá.
 
**Coleção de um cliente com débito aprovisionado aprovisionadas (1 milhão - 10M pedidos por segundo)**

![BD do Azure do Cosmos aprovisionadas aprovisionado débito](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Relação de débito com consistência 
Igual ao [relação da consistência com débito](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Relação de débito com disponibilidade
BD do Azure do Cosmos continua toomaintain a disponibilidade do mesmo quando as alterações de Olá são efetuadas toohello débito. BD do Azure do Cosmos transparente gere partições (por exemplo, divisão intercalação, operações de clonagem) e assegura que as operações de Olá não degradar o desempenho ou disponibilidade, enquanto a aplicação Olá aprovisionadas aumenta ou diminui o débito. 

## <a id="AvailabilityGuarantees"></a>Garantias de disponibilidade
BD do Azure do Cosmos oferece um SLA de disponibilidade mensal de 99,99% para cada um dos Olá operações de plane de controlo e dados. Tal como descrito anteriormente, garantias de disponibilidade da BD do Azure Cosmos incluem um limite superior absoluto de latência para operações de plane todos os dados e o controlo. Olá garantias de disponibilidade são steadfast e não de alteração com o número de Olá de regiões ou geográfica distância entre regiões. As garantias de disponibilidade aplicam-se com os manual, bem como, automática de ativação pós-falha. BD do Azure do Cosmos oferece transparentes APIs multi homing que certifique-se de que a aplicação pode funcionar nos pontos finais lógicos e transparente pode encaminhar a região novo do Olá pedidos toohello em caso de ativação pós-falha. Colocar de forma diferente, a aplicação não precisa de toobe implementada novamente após a ativação pós-falha e disponibilidade de Olá SLAs são mantidas.

### <a id="AvailabilityAndConsistency"></a>Relação de disponibilidade com consistência, débito e latência
Relação de disponibilidade com consistência, débito e latência está descrita em [relação da consistência com disponibilidade](#ConsistencyAndAvailability), [relação da latência com disponibilidade](#LatencyAndAvailability) e [Relação do débito com disponibilidade](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garante e o comportamento do sistema para "perda de dados"
Na base de dados do Azure Cosmos, cada partição (de uma coleção) é disponibilizada altamente por um número de réplicas, que são distribuídos por domínios de falhas, pelo menos, 10-20. Todas as escritas são forma síncrona e forma durável consolidadas por um quórum maioria das réplicas antes de estes são confirmadas toohello cliente. Replicação assíncrona foi aplicada com coordenação em partições distribuídos por várias regiões. BD do Azure do Cosmos garante que não há nenhuma perda de dados para uma ativação pós-falha de manual iniciadas por inquilino. Durante a ativação pós-falha automática, a base de dados do Azure Cosmos garante um limite superior de Olá configurado tem um vínculo intervalo vinculada na janela de perda de dados de Olá como parte do seu SLA.

## <a id="CustomerFacingSLAMetrics"></a>Métricas do SLA orientado para o cliente
BD do Azure do Cosmos transparente expõe as métricas de débito, latência, consistência e disponibilidade de Olá. Estas métricas estão acessíveis através de programação e via Olá portal do Azure (consulte a figura a seguir). Também pode definir alertas em vários limiares de utilizar o Azure Application Insights.
 
**A métrica de consistência, a latência, débito e disponibilidade está disponível de forma transparente tooeach inquilino**

![Azure métricas SLA visíveis para o cliente Cosmos DB](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Passos seguintes
* replicação global de tooimplement na sua conta de base de dados do Azure Cosmos utilizando Olá Consulte portal, do Azure [como tooperform BD do Cosmos Azure base de dados global replicação utilizar Olá portal do Azure](tutorial-global-distribution-documentdb.md).
* toolearn sobre como tooimplement arquiteturas multi-mestre com BD do Cosmos do Azure, consulte [arquiteturas multi-mestre de base de dados com base de dados do Azure Cosmos](multi-region-writers.md).
* toolearn mais sobre como funcionam as ativações pós-falha automáticas e manual na base de dados do Azure Cosmos, consulte [as ativações pós-falha Regional do BD Azure Cosmos](regional-failover.md).

## <a id="References"></a>Referências
1. Eric Brewer. [Para sistemas distribuídos robustos](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Eric Brewer. [CAP doze anos mais tarde – como regras de Olá foram alterados](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer &#39; s Conjecture e viabilidade da consistente, disponíveis, de serviços Web de tolerância a falhas de partição](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf)
4. Daniel Abadi. [Consistência fala no moderna distribuídas Design de sistemas de base de dados](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)
5. Martin Kleppmann. [Pare a chamar bases de dados CP ou da Ásia-Pacífico](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)
6. Peter Bailis ter usados. [Probabilistic Obsoletismo (. PBS) para práticas Quorums parciais](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
7. Naor e Wool. [Carga, a capacidade e a disponibilidade em sistemas de quórum](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf)
8. Herlihy e satisfeitas. [Lineralizability: Uma correcção condição para objetos em simultâneo](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)
9. [SLA de BD do Cosmos do Azure](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
