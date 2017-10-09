---
title: "níveis de aaaConsistency do BD Azure Cosmos | Microsoft Docs"
description: "BD do Azure do Cosmos tem cinco consistência níveis toohelp saldo eventual consistência, disponibilidade e a latência compromissos."
keywords: "consistência eventual, azure cosmos db, do azure, do Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Níveis de consistência sincronizáveis dados na base de dados do Azure Cosmos
BD do Azure do Cosmos foi concebido de Olá fundo cópias de segurança com distribuição global em mente para cada modelo de dados. É garantias de latência baixa previsível toooffer concebida, um SLA de disponibilidade de 99,99%, e vários bem definidos flexibilizadas modelos de consistência. Atualmente, a base de dados do Azure Cosmos fornece cinco níveis de consistência: forte, consistência vinculada, sessão, prefixo consistente e eventual. 

Besides **forte** e **consistência eventual** modelos normalmente oferecidas pelas bases de dados distribuídas, BD do Cosmos Azure oferece três modelos de consistência cuidadosamente codified e operacionalizado mais e validou as respetivas utilidade contra casos de utilização do mundo real. Estes são Olá **tem um vínculo vinculada**, **sessão**, e **prefixo consistente** níveis de consistência. Estes níveis de cinco consistência ativar coletivamente toomake bem reasoned compromissos entre consistência, disponibilidade e a latência. 

## <a name="distributed-databases-and-consistency"></a>Bases de dados distribuídas e consistência
As bases de dados comerciais distribuídas enquadram-se em duas categorias: bases de dados que não oferecem escolhas de consistência prováveis e bem definidas e bases de dados que oferecem duas opções de programação extremas (consistência forte versus eventual). 

Olá, os programadores de aplicações de burdens anteriores com minutia dos protocolos de replicação e espera-los toomake fala difícil entre consistência, disponibilidade, débito e latência. Olá última coloca uma toochoose pressão um dois extremes Olá. Apesar abundance Olá de investigação e propostas de mais de 50 modelos de consistência, hello Comunidade de base de dados distribuída não foi possível toocommercialize níveis de consistência para além de consistência forte e eventual. BD do cosmos permite aos programadores toochoose entre cinco modelos de consistência bem definidos ao longo do espetro de consistência Olá – forte, consistência vinculada, [sessão](http://dl.acm.org/citation.cfm?id=383631), prefixo consistente e eventual. 

![BD do Cosmos do Azure oferece vários bem definidos toochoose de modelos de consistência (simples) do](./media/consistency-levels/five-consistency-levels.png)

Olá, a tabela seguinte ilustra garantias específico Olá que fornece a cada nível de consistência.
 
**Níveis de Consistência e garantias**

| Nível de Consistência | Garantias |
| --- | --- |
| Forte | Transação Atómica |
| Estagnação Limitada | Prefixo Consistente. Tempo de desfasamento de leituras em escritas por prefixos k ou intervalo t |
| Sessão   | Prefixo Consistente. Leituras monotónicas, escritas monotónicas, leitura das próprias escritas, escrita de acordo com leituras |
| Prefixo Consistente | Atualizações devolvidas são alguns prefixo de todas as atualizações de Olá, com nenhuma lacunas |
| Eventual  | Leituras fora de ordem |

Pode configurar o nível de consistência Olá predefinido na sua conta de base de dados do Cosmos (e mais tarde substituir consistência Olá num pedido de leitura específico). Internamente, nível de consistência Olá predefinido aplica-se toodata dentro de conjuntos de partição Olá que pode abranger regiões. Prestes 73% dos nossos inquilinos utilizar a consistência de sessão e 20% preferir obsoletismo. Vamos observar que cerca de 3% dos nossos clientes experimentar vários níveis de consistência inicialmente antes settling numa escolha específica de consistência para a respetiva aplicação. Também iremos reparar que apenas 2% dos nossos inquilinos substituir níveis de consistência numa base por pedido. 

Na base de dados do Cosmos, leituras servido em sessão, prefixo consistente e a consistência eventual duas vezes são como cheap como leituras com consistência forte ou vinculada vinculada. BD do cosmos tem abrangente SLA de 99,99% incluindo garantias de consistência, juntamente com a disponibilidade, débito e latência de líderes da indústria. Que podemos utilizar um [verificador linearizability](http://dl.acm.org/citation.cfm?id=1806634), que funciona continuamente ao longo do nosso telemetria de serviço e reporta abertamente qualquer tooyou de violações de consistência. Para consistência vinculada, iremos monitorizar e gerar relatórios quaisquer violações demorou e limites de t. Para todos os cinco níveis de consistência simples, iremos também comunicar Olá [métrica obsoletismo probabilistic](http://dl.acm.org/citation.cfm?id=2212359) tooyou diretamente.  

## <a name="scope-of-consistency"></a>Âmbito de consistência
granularidade de Olá de consistência é confinada tooa pedido de utilizador único. Um pedido de escrita pode correspondem tooan inserir, substituir, upsert ou eliminar a transação. Tal como acontece com escritas, uma transação de leitura/consulta também é confinada tooa pedido de utilizador único. utilizador de Olá pode ser necessário toopaginate através de um grande conjunto de resultados, a expansão de várias partições, mas cada ler a transação é confinada tooa única página e servido a partir de uma única partição.

## <a name="consistency-levels"></a>Níveis de consistência
Pode configurar um nível de consistência predefinida na sua conta de base de dados que se aplica tooall coleções (e as bases de dados) na sua conta de base de dados do Cosmos. Por predefinição, todas as operações de leitura e consultas emitidas relativamente Olá recursos definidos pelo utilizador utilizam o nível de consistência Olá predefinido especificado na conta de base de dados de Olá. Pode reduzir o nível de consistência Olá de uma consulta/leitura específica utilização em cada um dos Olá suportada APIs do pedido. Existem cinco tipos de níveis de consistência suportados pelo protocolo de replicação de base de dados do Azure Cosmos Olá que fornecem um compromisso claro entre garantias de consistência específico e o desempenho, conforme descrito nesta secção.

**Forte**: 

* A consistência forte oferece um [linearizability](https://aphyr.com/posts/313-strong-consistency-models) garantia com Olá lê a versão mais recente de Olá tooreturn garantido de um item. 
* A consistência forte garante que uma escrita apenas seja visível depois de ser consolidada de forma durável pela quórum maioria de Olá das réplicas. Uma operação de escrita é colocada em sincronia consolidada de forma durável Olá primário e o quórum de Olá de bases de dados secundárias ou foi abortada. Uma leitura é sempre confirmada pela maioria Olá ler quórum, um cliente nunca pode ver uma escrita não consolidada ou parcial e sempre é garantido tooread Olá mais recente confirmado escrita. 
* As contas de Cosmos BD do Azure que estão a consistência forte toouse configurado não é possível associar mais do que uma região do Azure com a conta de base de dados do Azure Cosmos. 
* Olá custo de uma operação de leitura (em termos de [unidades de pedido](request-units.md) consumido) com consistência forte é superior a sessão e eventual, mas Olá mesmo como obsoletismo.

**Tem um vínculo vinculada**: 

* Consistência de obsoletismo limitado garante que leituras Olá podem ficar mais lentos durante escritas no máximo *K* versões ou prefixos de um item ou *t* intervalo de tempo. 
* Por conseguinte, quando escolher consistência vinculada, Olá "vinculada" pode ser configurado de duas formas: número de versões *K* do item de Olá através do qual Olá leituras ficar mais lentos durante escritas de paginações hello e o intervalo de tempo de Olá *t* 
* Tem um vínculo vinculada ofertas global ordem total, exceto no Olá "janela vinculada." Olá monotonic ler garantias existe numa região dentro e fora da Olá "janela vinculada." 
* Obsoletismo fornece uma mais forte garantia de consistência de sessão ou a consistência eventual. Para aplicações distribuídas globalmente, recomendamos que utilize obsoletismo para cenários em que teria como consistência forte toohave mas também é aconselhável 99,99% de disponibilidade e a latência baixa. 
* As contas de base de dados do Cosmos do Azure que estão configuradas com consistência de obsoletismo podem associar a respetiva conta de base de dados do Azure Cosmos qualquer número de regiões do Azure. 
* Olá custo de uma operação de leitura (em termos de RUs consumido) com obsoletismo é superior a sessão e a consistência eventual, mas Olá mesmo como consistência forte.

**Sessão**: 

* Ao contrário de modelos de consistência global Olá oferecidos pelos níveis de consistência forte e vinculada vinculada, a consistência de sessão é confinada tooa sessão de cliente. 
* A consistência de sessão é ideal para todos os cenários em que uma sessão de dispositivo ou utilizador está envolvida uma vez que esta situação garante monotonic leituras, escritas monotonic e leitura garante que os seus próprios escritas (RYW). 
* A consistência de sessão fornece a consistência previsível para uma sessão e débito de leitura máximo oferecendo Olá mais baixas latência escritas e leituras. 
* As contas de base de dados do Cosmos do Azure que estão configuradas com consistência de sessão podem associar a respetiva conta de base de dados do Azure Cosmos qualquer número de regiões do Azure. 
* Olá custo de uma operação de leitura (em termos de RUs consumido) com a sessão de nível de consistência é inferior ao vinculada vinculada e segura, mas a consistência eventual mais do que

<a id="consistent-prefix"></a>
**Prefixo consistente**: 

* Prefixo consistente garante que na ausência de mais escritas, as réplicas de Olá dentro do grupo de Olá eventualmente convergir. 
* Prefixo consistente garante que leituras nunca veem escritas fora de ordem. Se escritas foram executadas por ordem de Olá `A, B, C`, em seguida, um cliente vê o `A`, `A,B`, ou `A,B,C`, mas nunca fora de ordem como `A,C` ou `B,A,C`.
* As contas de base de dados do Cosmos do Azure que estão configuradas com consistência de prefixo consistentes podem associar a respetiva conta de base de dados do Azure Cosmos qualquer número de regiões do Azure. 

**Eventual**: 

* A consistência eventual garante que na ausência de mais escritas, as réplicas de Olá dentro do grupo de Olá eventualmente convergir. 
* A consistência eventual é formulário mais fraca do Olá de consistência em que um cliente pode obter valores de Olá que são mais antigos do que Olá aqueles que tinha vistos anteriormente.
* A consistência eventual fornece a consistência de leitura mais fraca Olá mas ofertas hello latência mais baixa para leituras e escritas.
* As contas de base de dados do Cosmos do Azure que estão configuradas com a consistência eventual podem associar a respetiva conta de base de dados do Azure Cosmos qualquer número de regiões do Azure. 
* Olá custo de uma operação de leitura (em termos de RUs consumido) com a consistência eventual Olá nível é Olá mais baixo de todos os níveis de consistência de base de dados do Azure Cosmos Olá.

## <a name="configuring-hello-default-consistency-level"></a>Configurar o nível de consistência Olá predefinido
1. No Olá [portal do Azure](https://portal.azure.com/), no Olá Jumpbar, clique em **Azure Cosmos DB**.
2. No Olá **Azure Cosmos DB** painel, toomodify de conta de base de dados de Olá selecione.
3. No painel de conta Olá, clique em **predefinido consistência**.
4. No Olá **consistência predefinida** painel, o novo nível de consistência Olá selecione e clique em **guardar**.
   
    ![Captura de ecrã, realce o ícone de definições de Olá e entrada de consistência predefinida](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Níveis de consistência para consultas
Por predefinição, para obter recursos definida pelo utilizador, nível de consistência Olá para consultas é Olá mesmo como nível de consistência Olá para leituras. Por predefinição, o índice de Olá é atualizado em sincronia cada inserir, substituir ou eliminar de um contentor do item toohello BD do Cosmos. Esta permite que as consultas de Olá toohonor Olá mesmo nível de consistência da ponto leituras. Apesar de base de dados do Azure Cosmos escrita otimizada e suporta volumes constante de escritas, índice síncrona e de manutenção que serve consultas consistentes, pode configurar determinada tooupdate coleções respetivo índice lenta. Ainda mais lento de indexação boosts desempenho de escrita de Olá e é ideal para cenários de ingestão em massa, quando uma carga de trabalho é principalmente leitura extremamente encriptados.  

| Modo de indexação | Lê | Consultas |
| --- | --- | --- |
| Consistente (predefinição) |Selecione a partir de vinculada forte e vinculada, sessão, prefixo consistente ou eventual |Selecione a partir de vinculada forte e vinculada, sessão, ou eventual |
| Lento |Selecione a partir de vinculada forte e vinculada, sessão, prefixo consistente ou eventual |Eventual |
| Nenhuma |Selecione a partir de vinculada forte e vinculada, sessão, prefixo consistente ou eventual |Não aplicável |

Como com pedidos de leitura, pode reduzir Olá nível de consistência de um pedido de consulta específicas em cada API.

## <a name="next-steps"></a>Passos seguintes
Se desejar toodo mais ao ler sobre níveis de consistência e fala, recomendamos Olá os seguintes recursos:

* Tiago Doug. Consistência de dados replicadas explicado através de baseball (vídeo).   
  [https://www.YouTube.com/Watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Tiago Doug. Consistência de dados replicadas explicado através de baseball.   
  [http://Research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Tiago Doug. Garantias de sessão para os dados replicados consistentes Weakly.   
  [http://DL.ACM.org/CITATION.cfm?ID=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. Consistência fala moderna design de sistemas de base de dados distribuída: CAP é apenas uma parte do bloco de Olá ".   
  [http://Computer.org/CSDL/mags/co/2012/02/mco2012020037-Abs.HTML](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis Shivaram Venkataraman, Miguel J. Franklin, Joseph M. Hellerstein, Stoica período. Probabilistic tem um vínculo vinculada (. PBS) para práticas Quorums parciais.   
  [http://VLDB.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Eventual consistente - Revisitado.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.HTML](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor, Avishai Wool, Olá carga, a capacidade e disponibilidade de quórum sistemas, SIAM diário de alterações na computação, v.27 n.2, p.423-447, Abril de 1998.
  [http://epubs.siam.org/DOI/Abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Roy Tan, Line-up: um linearizability completa e automática verificador, Proceedings de conferência ACM SIGPLAN 2010 Olá no idioma de conceção e implementação, 05 10 de Junho de 2010, Toronto, Ontario, de programação Canadá [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Miguel J. Franklin, Joseph M. Hellerstein, período Stoica, Probabilistically tem um vínculo vinculada para práticas quorums parciais, Proceedings de Olá VLDB Endowment, v.5 n.8, p.776-787, Abril de 2012 [http:// DL.ACM.org/CITATION.cfm?ID=2212359](http://dl.acm.org/citation.cfm?id=2212359)
