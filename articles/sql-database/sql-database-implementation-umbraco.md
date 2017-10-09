---
title: "aaaAzure caso prático de SQL da base de dados do Azure - Umbraco | Microsoft Docs"
description: "Saiba mais sobre como Umbraco utiliza serviços de dimensionamento para milhares de inquilinos e aprovisionar tooquickly de base de dados do SQL Server na nuvem de Olá"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco utiliza serviços de dimensionamento para milhares de inquilinos e aprovisionar tooquickly de SQL Database do Azure na nuvem de Olá
![Logótipo de Umbraco](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco é um populares open source gestão de conteúdo (CMS) que pode executar nada de pequenas sites campanha ou brochure toocomplex aplicações para as empresas de Fortune 500 e Web sites do suporte de dados globais. 

> "Temos bastante uma grande Comunidade de programadores que utilizam o sistema de Olá, com mais de 100 000 programadores nos nossos fóruns e 350,000 mais de sites que estão em direto, executar Umbraco."
> 
> — Morten Christensen, oportunidades potenciais técnica, Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

implementações de cliente toosimplify, Umbraco adicionado Umbraco-como-um-serviço (UaaS): uma oferta de software-como-um-serviço (SaaS) que elimina a necessidade de Olá para implementações no local, fornece a ampliação incorporadas e remove a gestão de sobrecarga Ativando os programadores toofocus na inovação em vez de solução de gestão do produto. Umbraco é capaz de tooprovide todas essas vantagens pela entidade confiadora no Olá flexível modelo de (PaaS) de plataforma-como-um-serviço oferecido pelo Microsoft Azure.

UaaS permite que os clientes de SaaS toouse Umbraco CMS capacidades que foram anteriormente fora do seu alcance. Estes clientes são aprovisionados com um ambiente de CMS de trabalho que inclui uma base de dados de produção. Os clientes podem aumentar bases de dados adicionais do tootwo para desenvolvimento e teste ambientes, consoante os requisitos. Quando é pedido um novo ambiente, um processo automatizado atribui desse cliente uma base de dados automaticamente. nova base de dados Olá está pronto em segundos, porque a base de dados de Olá já foi previamente aprovisionada por Umbraco do Azure agrupamento elástico de bases de dados disponíveis (consulte a figura 1).

![Ciclo de vida de aprovisionamento Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Figura 1. Ciclo de vida de aprovisionamento para Umbraco como um serviço (UaaS)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Azure conjuntos elásticos e automatização simplificam as implementações
Com a SQL Database do Azure e outros serviços do Azure, Umbraco clientes podem aprovisionar respetivos ambientes e Umbraco facilmente pode monitorizar e gerir bases de dados como parte de um fluxo de trabalho intuitivo:

1. Aprovisionar
   
   Umbraco mantém uma capacidade de 200 pré-aprovisionada as bases de dados de conjuntos elásticos. Quando um cliente novo inscreve UaaS, Umbraco fornece cliente Olá com um novo ambiente CMS em tempo real ao atribuir-lhes uma base de dados do conjunto de disponibilidade de Olá.
   
   Quando um conjunto de disponibilidade atinge o limiar, é criado um novo conjunto elástico e novas bases de dados são toobe pré-aprovisionada atribuído toocustomers conforme necessário.
   
   Implementação é totalmente automatizada utilizando bibliotecas de gestão do c# e filas do Service Bus do Azure.
2. Utilizar
   
   Os clientes utilizar uma toothree ambientes (para produção, transição, e/ou desenvolvimento), cada com a sua própria base de dados. Bases de dados do cliente estão em conjuntos elásticos, que permite Umbraco tooprovide eficiente de dimensionamento sem ter de aprovisionar tooover.
   
   ![Descrição geral do projeto Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Detalhe de projeto Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Figura 2. Web site do cliente Umbraco-como-um-serviço (UaaS), que mostra detalhes e descrição geral do projeto
   
   Base de dados SQL do Azure utiliza unidades de transação de base de dados (DTUs) toorepresent Olá relativa energia necessária para transações da base de dados do mundo real. Para clientes de UaaS, bases de dados funcionam normalmente em cerca de 10 DTUs, mas cada um tem Olá elasticidade tooscale a pedido. Isto significa que UaaS pode Certifique-se de que os clientes têm sempre recursos necessários, mesmo em situações das horas de ponta. Por exemplo, durante um evento de desporto Domingos recente, um cliente UaaS teve picos de base de dados se too100 DTUs Olá enquanto estiver em curso jogo Olá. Azure conjuntos elásticos disponibilizada-lo para Umbraco toosupport esse elevada procura sem degradação do desempenho.
3. Monitorizar
   
   Monitores de Umbraco da base de dados atividade utilizar os dashboards Olá portal do Azure, juntamente com alertas de e-mail personalizadas.
4. Recuperação após desastre
   
   Azure fornece duas opções de recuperação após desastre (DR): georreplicação ativa e georrestauro. Olá opção de DR que deve selecionar uma empresa depende em seu [objetivos de continuidade do negócio](sql-database-business-continuity.md).
   
   replicação geográfica activa fornece o nível mais rápido do Olá de resposta no evento Olá período de indisponibilidade. Utilizar a georreplicação ativa, pode criar cópias de segurança toofour de dados secundárias legíveis em servidores em regiões diferentes e, em seguida, pode iniciar a ativação pós-falha tooany de bases de dados secundárias Olá no evento Olá de uma falha.
   
   Umbraco não requer a georreplicação, mas tirar partido do Azure georrestauro toohelp Certifique-se o período de indisponibilidade mínimo eventos Olá de indisponibilidade. georrestauro baseia-se em cópias de segurança da base de dados no armazenamento do Azure com redundância geográfica. Que permite que os utilizadores toorestore de uma cópia de segurança quando houver uma falha na região primária Olá.
5. Aprovisionar desativação
   
   Quando é eliminado um ambiente de projeto, são removidas quaisquer bases de dados associadas (desenvolvimento, teste ou em direto) durante a limpeza de filas do Service Bus do Azure. Automatizar este processo restauros Olá conjunto de disponibilidade de base de dados elásticas do tooUmbraco de bases de dados não utilizados, disponibilizando-as para o aprovisionamento de futuro, mantendo a máxima utilização.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Conjuntos elásticos permitem UaaS tooscale com facilidade
Ao tirar partido dos conjuntos elásticos do Azure, Umbraco pode otimizar o desempenho para que os seus clientes sem ter tooover - ou o under-aprovisionar. Umbraco tem atualmente quase 3,000 bases de dados em 19 conjuntos elásticos, com Olá capacidade tooeasily Dimensionar como tooaccommodate necessário qualquer um dos respetivos 325,000 clientes existentes ou novos clientes que estão pronto toodeploy um CMS na nuvem de Olá.

Na verdade, tooMorten Christensen, levar técnica em Umbraco, de acordo com "UaaS agora estão a ocorrer crescimento de cerca de 30 novos clientes por dia. Os nossos clientes são delighted com conveniência Olá ser capaz de tooprovision novos projetos em segundos, de forma instantânea publicar atualizações tootheir sites em direto de um ambiente de desenvolvimento utilizando a 'implementação de um clique' e efetuar alterações, tal como a rapidamente se encontrarem erros . "

Se um cliente não necessita de um segundo e/ou terceiro ambiente, pode simplesmente remova nesses ambientes. Que liberta recursos que podem ser utilizados para outros clientes como parte da Olá Umbraco conjunto de disponibilidade de base de dados elásticas.

![Arquitetura de implementação Umbraco](./media/sql-database-implementation-umbraco/figure4.png)

Figura 3. Arquitetura de implementação de UaaS no Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>caminho de Olá do Centro de dados toocloud
Quando os programadores de Umbraco Olá inicialmente efetuada Olá decisão toomove tooa modelo de SaaS, estes deverem que têm um toobuild de forma económica e dimensionável saída serviço Olá.

> "conjuntos elásticos são uma opção perfeita para a nossa oferta de SaaS porque, pode marcar capacidade e reduzir verticalmente conforme necessário. O aprovisionamento é fácil e com a nossa configuração, vamos manter as utilização no máximo."
> 
> — Morten Christensen, oportunidades potenciais técnica, Umbraco
> 
> 

"Queremos toospend nosso tempo em resolver problemas dos nossos clientes, não infraestrutura a gerir. Queremos toomake-lo mais fácil para os nosso clientes tooget Olá máximo valor, "indica Niels Hartvig, founder de Umbraco. "Estamos inicialmente considerados servidores Olá ourselves de alojamento, mas o planeamento de capacidade seria ter um nightmare." Por coincidência, Umbraco não utilizar qualquer administradores de base de dados, que uma proposta de valor de chave para utilizar UaaS de carateres de sublinhado.

Um objetivo importante para os programadores de Umbraco Olá foi tooprovide uma forma de ambientes de tooprovision UaaS clientes rapidamente e sem limitações de capacidade. Mas, fornecer que um serviço alojado dedicado nos centros de dados Umbraco teria necessários muitos excesso de capacidade toohandle bursts no processamento. Que seria ter se destinam a adição de infraestrutura de computação considerável que poderia ter sido regularmente subutilizada.

Além disso, a equipa de desenvolvimento de Umbraco Olá pretendia uma solução que lhe permita-tooreuse como grande parte do respetivo código existente conforme possível. Como Umbraco programadores Estados Mikkel Madsen, "foi satisfeitos com ferramentas de desenvolvimento de Microsoft Olá já foi familiarizados, como o Microsoft SQL Server, a base de dados do Microsoft Azure SQL, ASP.net e serviços de informação Internet (IIS). Antes de investir num IaaS ou uma PaaS na nuvem solução, queremos toomake certificar-se de que o que seria suporta os nossos ferramentas da Microsoft e plataformas, para que não tenhamos toomake alterações em grande escala tooour base de código. "

todos os toomeet dos seus critérios, Umbraco comparados para um parceiro da nuvem com Olá qualificações os seguintes:

* Fiabilidade e capacidade suficiente
* Suporte para ferramentas de desenvolvimento Microsoft, pelo que esse Umbraco engenheiros não seria forçado toocompletely reinvent respetivo ambiente de desenvolvimento
* Presença em todos os mercados geográfica Olá na qual UaaS compete (empresas necessidade tooensure que eles podem aceder aos respetivos dados rapidamente e que os dados são armazenados numa localização que cumpra os requisitos de regulamentação regionais)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Por que motivo o Umbraco selecionou do Azure para UaaS
De acordo com tooMorten Christensen "após a consideração dos nossas as opções, selecionamos Azure porque-cumprido todos os nossos critérios de capacidade de gestão e a escalabilidade toofamiliarity e a eficácia de custos. Vamos configurar ambientes de Olá em VMs do Azure e cada ambiente tem a suas próprias instância de SQL Database do Azure, com todas as instâncias de Olá conjuntos elásticos. Ao separar as bases de dados entre o desenvolvimento, teste e ambientes em direto, pode oferecer os nossos clientes desempenho robusto isolamento correspondência tooscale — uma enorme win. "

Morten continua, "antes, tivemos tooprovision servidores de bases de dados web manualmente. Agora, não temos toothink acerca do mesmo. Tudo é um processo automatizado — desde o aprovisionamento toocleanup. "

Morten também é satisfeito com Olá dimensionamento funcionalidades fornecidas pelo Azure. "conjuntos elásticos são uma opção perfeita para a nossa oferta de SaaS porque, pode marcar capacidade e reduzir verticalmente conforme necessário. O aprovisionamento é fácil e com a nossa configuração, vamos manter as utilização no máximo." Estados de Morten, "simplicidade Olá dos conjuntos elásticos, juntamente com a garantia de Olá de DTUs baseada em camada de serviço, nos dá Olá energia tooprovision novos agrupamentos de recursos no pedido. Recentemente, um dos nossos clientes maior peaked too100 DTUs no respetivo ambiente em direto. Utilizar o Azure, o nosso conjuntos elásticos fornecido bases de dados do cliente Olá com recursos de Olá que são necessários em tempo real sem ter requisitos de DTU toopredict. Resumindo, os nossos clientes obter Olá desative-em torno de data/hora que se esperam e pode satisfazer os nossos contratos de nível de serviço de desempenho."

Mikkel Madsen soma-la: "estamos tiver embraced Olá poderosas Azure algoritmo que liga um comuns SaaS cenário (integração novos clientes em tempo real na escala) tooour padrão de aplicação (pré-aprovisionar bases de dados, o desenvolvimento e live) em cima Olá tecnologia subjacente (utilizando as filas do Service Bus do Azure em conjunto com a SQL Database do Azure)."

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Com o Azure, UaaS está a exceder as expectativas de cliente
Dado que escolher Azure como o parceiro de nuvem, Umbraco foi capaz de tooprovide UaaS clientes com desempenho otimizado de gestão de conteúdo, sem investimento Olá IT recursos necessário a partir de uma solução personalizada alojada. Como Morten indica, "estamos adoram comodidade do programador Olá e escalabilidade, o que dá-na Azure e os nossos clientes são thrilled com funcionalidades de Olá e fiabilidade. Em geral, foi um excelente win para-nos!"

## <a name="more-information"></a>Mais informações
* toolearn mais informações sobre conjuntos elásticos do Azure, consulte [conjuntos elásticos](sql-database-elastic-pool.md).
* toolearn mais informações sobre o Service Bus do Azure, consulte [Service Bus do Azure](https://azure.microsoft.com/services/service-bus/).
* toolearn mais informações sobre funções da Web e funções de trabalho, consulte [as funções de trabalho](../fundamentals-introduction-to-azure.md#compute).    
* toolearn mais informações sobre redes virtuais, consulte [redes virtuais](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn mais informações sobre a cópia de segurança e recuperação, consulte [continuidade do negócio](sql-database-business-continuity.md).    
* toolearn mais informações sobre monitorização ppols, consulte [monitorização agrupamentos](sql-database-elastic-pool-manage-portal.md).    
* toolearn mais informações sobre Umbraco como um serviço, consulte [Umbraco](https://umbraco.com/cloud).

