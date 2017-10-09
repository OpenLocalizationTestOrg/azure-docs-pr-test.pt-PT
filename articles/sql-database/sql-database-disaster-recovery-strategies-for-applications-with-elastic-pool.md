---
title: "soluções de recuperação de desastre aaaDesign - SQL Database do Azure | Microsoft Docs"
description: "Saiba como toodesign sua solução de nuvem de recuperação após desastre ao escolher o padrão de ativação pós-falha à direita Olá."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Estratégias de recuperação de desastre para aplicações que utilizam conjuntos elásticos da base de dados SQL
Ao longo de anos Olá podemos ter aprendidas que serviços em nuvem não são foolproof e ocorrem de incidentes catastrófica. Base de dados do SQL Server fornece várias capacidades tooprovide para continuidade do negócio Olá da sua aplicação quando ocorrem estes incidentes. [Conjuntos elásticos](sql-database-elastic-pool.md) e bases de dados individuais suportam Olá mesmo tipo de funcionalidades de recuperação após desastre. Este artigo descreve várias estratégias de DR para conjuntos elásticos que tiram partido destas funcionalidades de continuidade empresarial da base de dados do SQL Server.

Este artigo utiliza Olá seguir o padrão de aplicação SaaS ISV canónica:

<i>Uma aplicação web baseados na nuvem modernas Aprovisiona uma base de dados do SQL Server para cada utilizador final. Olá ISV tem muitos clientes e, por conseguinte, utiliza muitas bases de dados, conhecidos como bases de dados do inquilino. Uma vez Olá inquilino as bases de dados têm normalmente padrões de atividade imprevisíveis, Olá ISV utiliza um conjunto elástico toomake Olá da base de dados custo muito previsível ao longo de períodos de tempo prolongados. agrupamento elástico Olá também simplifica a gestão de desempenho de Olá quando picos de atividade do utilizador Olá. Além disso aplicação Olá do toohello inquilino bases de dados também utiliza várias bases de dados toomanage perfis de utilizador, segurança, recolher padrões de utilização etc. Disponibilidade de inquilinos individuais Olá não afeta a disponibilidade da aplicação Olá como todo. No entanto, hello disponibilidade e o desempenho das bases de dados de gestão é essenciais para a função da aplicação Olá e bases de dados de gestão de Olá são aplicação completo Olá offline estiver offline.</i>  

Este artigo aborda as estratégias de DR que abrangem uma gama de cenários do custo arranque confidenciais aplicações tooones com requisitos de disponibilidade rigorosos.

## <a name="scenario-1-cost-sensitive-startup"></a>Cenário 1. Custo arranque confidencial
<i>Posso estou uma empresa de arranque e estou de custo extremamente confidencial.  Pretendo toosimplify implementação e gestão da aplicação Olá e pode tiver um SLA limitado de clientes individuais. Mas pretendo que a aplicação de Olá tooensure como um todo nunca está offline.</i>

requisito de simplicidade do toosatisfy Olá, implementar todas as bases de dados do inquilino para um conjunto elástico em Olá região do Azure à sua escolha e implementar as bases de dados de gestão como georreplicação bases de dados individuais. Recuperação de desastres Olá de inquilinos, utilize georrestauro, vem sem custos adicionais. disponibilidade de Olá tooensure de Olá bases de dados de gestão, georreplicação replicá-los região tooanother utilizar um grupo de ativação de pós-falha automática (no-pré-visualização) (passo 1). custo em curso do Olá da configuração de recuperação de desastre Olá neste cenário de é igual toohello custo total de bases de dados secundária Olá. Esta configuração é ilustrada no diagrama seguinte Olá.

![Figura 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Se ocorrer uma falha na região primária Olá, Olá toobring de passos de recuperação online a sua aplicação são ilustrados por diagrama seguinte Olá.

* grupo de ativação pós-falha de Olá inicia a ativação pós-falha automática da região de DR toohello do Olá gestão da base de dados. aplicação Olá é automaticamente ligação restabelecida toohello novas principal e todas as novas contas e bases de dados de inquilino são criados na região de DR Olá. os clientes existentes do Olá veem os dados temporariamente indisponíveis.
* Criar conjunto elástico Olá com Olá mesma configuração como conjunto de Olá original (2).
* Utilize georrestauro toocreate cópias das bases de dados do inquilino de Olá (3). Pode considerar a acionar restauros individuais Olá pelas ligações de utilizador final Olá ou utilize outra esquema de prioridade específicas da aplicação.


Neste momento a aplicação estiver novamente online na região de DR Olá, mas alguns clientes experiência atraso quando aceder aos respetivos dados.

![Figura 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Se a falha de Olá foi temporária, é possível que nessa região primária Olá é recuperada do Azure antes de todos os restauros de base de dados de Olá concluídos na região de Olá DR. Neste caso, orquestrar o movimento Olá aplicação back toohello região primária. processo de Olá executa os passos de Olá ilustrados no diagrama seguinte Olá.

* Cancele a todos os pedidos de georrestauro pendentes.   
* Ativação pós-falha Olá gestão bases de dados toohello região primária (5). Após a recuperação da região de Olá, primaries antigo Olá automaticamente ficou secundárias. Agora, mudar funções novamente. 
* Altere ligação cadeia toopoint back toohello região primária da aplicação Olá. Agora todas as novas contas e bases de dados de inquilino são criados na região primária Olá. Alguns clientes existentes veem os dados temporariamente indisponíveis.   
* Defina todas as bases de dados em Olá DR agrupamento apenas de tooread tooensure que não podem ser modificadas na região de DR Olá (6). 
* Para cada base de dados no Olá DR conjunto que foi alterada desde a recuperação de Olá, mude o nome ou eliminar Olá correspondente as bases de dados no conjunto de principais de Olá (7). 
* Olá cópia atualizada bases de dados de Olá conjunto principal do DR conjunto toohello (8). 
* Eliminar conjunto de DR Olá (9)

Neste momento a sua aplicação está online na região primária de Olá com todos os inquilinos bases de dados disponível no agrupamento principal Olá.

![Figura 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

chave de Olá **beneficiar** desta estratégia é baixo custo em curso para a redundância de camada de dados. São efetuadas automaticamente cópias de segurança por Olá serviço de base de dados SQL com nenhuma aplicação reescrever e sem custos adicionais.  custo de Olá quando apenas quando as bases de dados elásticas Olá são restauradas. Olá **compromisso** é que a recuperação completa de Olá de todas as bases de dados do inquilino demora muito tempo. Olá período de tempo depende do número total de Olá de restauros iniciar no Olá DR região e o tamanho geral do Olá bases de dados de inquilino. Mesmo que atribuir prioridades restauros dos inquilinos, alguns através de outros utilizadores, estão a competir com Olá todos os outros restauros que sejam iniciados na Olá mesma região que o serviço de Olá arbitrates e acelera toominimize Olá impacto geral em bases de dados dos clientes Olá existentes. Além disso, recuperação Olá das bases de dados do Olá inquilino não consegue iniciar até que o novo conjunto elástico Olá na região de DR Olá é criado.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Cenário 2. Aplicação madura com o serviço em camadas
<i>Sou uma aplicação SaaS madura com ofertas de serviço em camadas e SLAs diferentes para os clientes de avaliação e pagar com clientes. Para clientes de avaliação Olá, tenho de Olá tooreduce custo quanto possível. Os clientes de avaliação podem demorar um período de indisponibilidade, mas pretendo tooreduce a probabilidade. Para Olá pagar com os clientes, qualquer período de inatividade é um risco de voo. Para que pretendo toomake se de que os clientes pagar sempre tooaccess capaz dos seus dados.</i> 

toosupport neste cenário, separado Olá inquilinos avaliação de paga inquilinos colocando-los em conjuntos elásticos separados. os clientes de avaliação de Olá têm inferior eDTU por inquilino e inferior SLA com mais tempo de recuperação. os clientes de pagar Olá estão num conjunto com superior eDTU por inquilino e um SLA mais elevado. tooguarantee Olá menor tempo de recuperação, bases de dados de inquilino de Olá pagar clientes estão a georreplicação. Esta configuração é ilustrada no diagrama seguinte Olá. 

![Figura 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Como no cenário de primeiro Olá, bases de dados de gestão de Olá são bastante Active Directory para utilizar uma única base de dados georreplicação para o mesmo (1). Isto assegura um desempenho previsível Olá novas subscrições de cliente, atualizações de perfil e outras operações de gestão. Olá região na qual residem primaries Olá das bases de dados de gestão de Olá é região primária Olá e região Olá na qual residem secundárias Olá das bases de dados de gestão de Olá é a região de Olá DR.

Olá bases de dados de inquilino de pagar clientes tem bases de dados ativas Olá "paga" agrupamento aprovisionado na região primária Olá. Aprovisione um conjunto com o mesmo nome na região de Olá DR de Olá secundário. Cada inquilino é toohello de georreplicação secundária conjunto (2). Isto permite uma recuperação rápida de todas as bases de dados inquilino através de ativação pós-falha. 

Se ocorrer uma falha na região primária Olá, Olá toobring de passos de recuperação online a sua aplicação são ilustrado no diagrama seguinte Olá:

![figura 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Efetuar imediatamente a ativação pós-falha de região de DR do toohello de bases de dados de gestão de Olá (3).
* Altere a região de toohello DR de toopoint de cadeia de ligação da aplicação Olá. Agora todas as novas contas e bases de dados de inquilino são criados na região de DR Olá. os clientes de avaliação existente Olá ver os dados temporariamente indisponíveis.
* Ativação pós-falha Olá paga agrupamento de toohello de bases de dados do inquilino na Olá DR região tooimmediately restaurar a respetiva disponibilidade (4). Uma vez que a ativação pós-falha de Olá é uma alteração do nível de metadados rápido, considere uma otimização onde Olá as ativações pós-falha individuais são acionadas a pedido por ligações de utilizador final Olá. 
* Se o tamanho de eDTU do conjunto secundária foi inferior ao hello primário porque Olá secundário bases de dados apenas Olá necessária capacidade tooprocess Olá alteração registos ao foram réplicas secundárias, imediatamente aumentar a capacidade do agrupamento Olá agora tooaccommodate Olá completa carga de trabalho de todos os inquilinos (5). 
* Criar novo conjunto elástico Olá com Olá mesmo nome e Olá mesmo configuração na região de Olá DR para bases de dados dos clientes Olá avaliação (6). 
* Assim que for criado o conjunto de Olá avaliação clientes, utilize georrestauro toorestore Olá inquilino de avaliação individual as bases de dados para o novo agrupamento de Olá (7). Considere a acionar restauros individuais Olá pelas ligações de utilizador final Olá ou utilize outra esquema de prioridade específicas da aplicação.

Neste momento a sua aplicação estiver novamente online na região de DR Olá. Todos os clientes de pagar têm acesso tootheir dados enquanto os clientes de avaliação Olá experiência atraso quando aceder aos respetivos dados.

Quando a região primária Olá for recuperada pelo Azure *depois* restaurou aplicação Olá na região de Olá DR pode continuar a execução da aplicação Olá nessa região ou pode decidir região primária do toofail toohello anterior. Se for recuperada região primária Olá *antes* conclusão do processo de ativação pós-falha de Olá, considere a falhar back imediato. reativação pós-falha da Olá demora passos Olá ilustrados no diagrama seguinte Olá: 

![figura 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Cancele a todos os pedidos de georrestauro pendentes.   
* Efetuar a ativação pós-falha de bases de dados de gestão Olá (8). Após a recuperação da região de Olá, hello primário antigo automaticamente ficar Olá secundário. Agora, torna-se Olá primário novamente.  
* Ativação pós-falha Olá paga bases de dados do inquilino (9). De igual modo, após a recuperação da região de Olá, primaries antigo Olá automaticamente tornar-se secundárias Olá. Agora que se tornem primaries Olá novamente. 
* Conjunto Olá restaurada avaliação bases de dados que foram alterados na região de DR Olá só tooread (10).
* Para cada base de dados no agrupamento de DR de clientes avaliação Olá alterados desde a recuperação de Olá, mude o nome ou eliminar Olá correspondente da base de dados no agrupamento de primário Olá clientes avaliação (11). 
* Olá cópia atualizada bases de dados de Olá conjunto principal do DR conjunto toohello (12). 
* Eliminar conjunto de DR Olá (13) 

> [!NOTE]
> a operação de ativação pós-falha do Olá é assíncrona. toominimize hora da recuperação Olá é importante que executar o comando de ativação pós-falha dos Olá inquilino bases de dados em lotes de, pelo menos, 20 bases de dados. 
> 
> 

chave de Olá **beneficiar** desta estratégia é que proporciona SLA mais elevado de Olá Olá pagar com clientes. Esta ação garante também que avaliações novo Olá estiverem desbloqueadas, assim como Olá avaliação DR conjunto for criado. Olá **compromisso** é que esta configuração aumenta o custo total Olá das bases de dados do Olá inquilino ao custo de Olá do conjunto de secundário DR Olá para paga clientes. Além disso, se o agrupamento secundário Olá tem um tamanho diferente, os clientes de pagar Olá experiência de desempenho inferior após a ativação pós-falha até hello conjunto conclusão da atualização na região de Olá DR. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Cenário 3. Aplicação distribuída geograficamente com o serviço em camadas
<i>Tenho uma aplicação SaaS madura com ofertas de serviço em camadas. Posso pretende toooffer um toomy SLA muito agressiva paga clientes e minimizar o risco de Olá de impacto quando ocorrem falhas porque interrupção breve mesmo pode causar insatisfação de cliente. É fundamental que Olá pagar com os clientes pode sempre aceder aos respetivos dados. avaliações de Olá são gratuitas e um SLA não é oferecido durante o período de avaliação de Olá.</i> 

toosupport neste cenário, utilize separado do três conjuntos elásticos. Aprovisionar conjuntos de tamanho igual dois com elevada eDTUs por base de dados em dois Olá de toocontain regiões diferentes paga inquilino as bases de dados dos clientes. o conjunto de terceiro Olá com inquilinos avaliação Olá pode ter inferior eDTUs por base de dados e aprovisionamento de uma das duas regiões de Olá.

tooguarantee Olá menor tempo de recuperação durante a falhas, bases de dados de inquilino de Olá pagar clientes são georreplicação com 50% das bases de dados primária Olá em cada uma das regiões Olá dois. Da mesma forma, cada região tem 50% das bases de dados secundária Olá. Desta forma, se uma região estiver offline, os apenas 50% do Olá paga bases de dados de clientes são afetados e têm toofail sobre. Olá outras bases de dados permanecem intactas. Esta configuração é ilustrada no Olá diagrama a seguir:

![Figura 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Como em cenários de anterior Olá, bases de dados de gestão de Olá são bastante Active Directory, por isso, configurá-las como único georreplicação bases de dados (1). Isto assegura um desempenho previsível Olá de subscrições de cliente novo Olá, atualizações de perfil e outras operações de gestão. Região A região primária de Olá para bases de dados de gestão de Olá e região Olá B é utilizada para recuperação de bases de dados de gestão de Olá.

inquilino as bases de dados Olá pagar clientes são também georreplicação mas com primaries e bases de dados secundárias divididas entre região A e região B (2). Desta forma, Olá inquilino principal bases de dados afetados pela indisponibilidade de Olá podem efetuar a ativação pós-falha toohello outra região e fique disponível. Olá outro metade das bases de dados de inquilino de Olá não são ser afetado de todo. 

diagrama seguinte Olá ilustra tootake de passos de recuperação Olá se ocorrer uma falha na região A.

![figura 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Efetuar imediatamente a ativação pós-falha tooregion de bases de dados de gestão de Olá B (3).
* Alterar ligação cadeia toopoint toohello gestão bases de dados da aplicação Olá numa região B. Modifique Olá gestão bases de dados toomake se novas contas de Olá e bases de dados de inquilino são criados na região B e Olá existente inquilino as bases de dados encontram-se não existe como bem. os clientes de avaliação existente Olá ver os dados temporariamente indisponíveis.
* Ativação pós-falha Olá paga toopool de bases de dados do inquilino 2 na região B tooimmediately restaurar a respetiva disponibilidade (4). Uma vez que a ativação pós-falha de Olá é uma alteração do nível de metadados rápido, pode considerar otimização onde Olá as ativações pós-falha individuais são acionadas a pedido por ligações de utilizador final Olá. 
* Desde agora conjunto 2 contém apenas as bases de dados primárias, Olá carga de trabalho total no Olá conjunto aumenta e imediatamente pode aumentar o tamanho de eDTU (5). 
* Criar novo conjunto elástico Olá com Olá mesmo nome e Olá mesmo configuração na região de Olá B para bases de dados dos clientes Olá avaliação (6). 
* Uma vez Olá é criado conjunto utilize georrestauro toorestore Olá individuais inquilino de avaliação da base de dados num agrupamento de Olá (7). Pode considerar a acionar restauros individuais Olá pelas ligações de utilizador final Olá ou utilize outra esquema de prioridade específicas da aplicação.

> [!NOTE]
> a operação de ativação pós-falha do Olá é assíncrona. tempo de recuperação do toominimize Olá, é importante que executar o comando de ativação pós-falha dos Olá inquilino bases de dados em lotes de, pelo menos, 20 bases de dados. 
> 

Neste momento a aplicação estiver novamente online na região B. Todos os clientes de pagar têm acesso tootheir dados enquanto os clientes de avaliação Olá experiência atraso quando aceder aos respetivos dados.

Quando a região A for recuperada terá de toodecide se pretender toouse região B para clientes de avaliação ou a reativação pós-falha toousing Olá um conjunto de clientes avaliação na região A. Um critério pode ser Olá % das bases de dados do inquilino de avaliação modificada uma vez que a recuperação de Olá. Independentemente desse decisão, terá de toore balancear Olá paga inquilinos entre dois conjuntos. diagrama seguinte Olá ilustra o processo de Olá bases de dados de inquilino de avaliação de Olá falharem tooregion back-a.  

![figura 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Cancele a todo o agrupamento de tootrial DR pedidos pendentes georrestauro.   
* Efetuar a ativação pós-falha da base de dados de gestão Olá (8). Após a recuperação da região de Olá, o principal anterior Olá ficou automaticamente Olá secundário. Agora, torna-se Olá primário novamente.  
* Selecione as bases de dados do inquilino paga falharem back toopool 1 e iniciar ativação pós-falha tootheir secundárias (9). Após a recuperação da região de Olá, todas as bases de dados no conjunto 1 automaticamente deixou de estar bases de dados secundárias. Agora a 50% deles ficar primaries novamente. 
* Reduza o tamanho de Olá de eDTU do conjunto 2 toohello original (10).
* Conjunto de todos os restaurar bases de dados de avaliação numa região de Olá B só tooread (11).
* Para cada base de dados no agrupamento DR avaliação Olá que tenha sido alterado desde a recuperação de Olá, mude o nome ou eliminar Olá correspondente da base de dados no agrupamento principal avaliação Olá (12). 
* Olá cópia atualizada bases de dados de Olá conjunto principal do DR conjunto toohello (13). 
* Eliminar conjunto de DR Olá (14) 

chave de Olá **vantagens** desta estratégia são:

* Suporta SLA mais agressiva Olá para Olá pagar com os clientes, porque garante que uma falha não pode afetar mais de 50% das bases de dados do Olá inquilino. 
* Garante que avaliações novo Olá estiverem desbloqueadas, assim que o registo de Olá DR conjunto é criado durante a recuperação de Olá. 
* Permite uma utilização mais eficiente da capacidade de agrupamento de Olá como 50% das bases de dados secundárias no conjunto 1 e conjunto 2 garantidos toobe menos ativas que bases de dados primária Olá.

Olá principal **compromissos** são:

* as operações CRUD Olá bases de dados de gestão de Olá têm uma latência inferior para Olá os utilizadores finais ligados tooregion A que para os utilizadores finais ligados de Olá tooregion B, tal como que são executadas contra Olá primária do bases de dados de gestão de Olá.
* Requer mais complexa conceção da base de dados de gestão de Olá. Por exemplo, cada registo de inquilino tem uma tag de localização que tem toobe foi alterado durante a ativação pós-falha e a reativação pós-falha.  
* Olá pagar com os clientes pode ter um desempenho inferior do que o habitual até hello conjunto conclusão da atualização na região B. 

## <a name="summary"></a>Resumo
Este artigo incida no estratégias de recuperação de desastre Olá para a camada de base de dados de Olá utilizado por uma aplicação de multi-inquilino de SaaS ISV. Olá estratégia escolher baseia-se nas necessidades de Olá da aplicação Olá, tais como o modelo de negócio Olá, Olá SLA pretender que os clientes do toooffer tooyour, budget restrição etc. Cada descrito estratégia destaca Olá benefícios e compromisso pelo que pode tomar uma decisão informada. Além disso, a aplicação específica provável inclui outros componentes do Azure. Assim, reveja as orientações de continuidade de negócio e orquestrar recuperação Olá da camada de base de dados de Olá com os mesmos. toolearn mais sobre a gestão de recuperação de aplicações de base de dados no Azure, consulte demasiado[estruturar soluções de nuvem de recuperação após desastre](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre cópias de segurança automatizada de SQL Database do Azure, consulte [cópias de segurança automatizadas de base de dados SQL](sql-database-automated-backups.md).
* Para cenários e uma descrição geral de continuidade de negócio, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).
* toolearn sobre a utilização de cópias de segurança automatizadas para recuperação, consulte [restaurar uma base de dados de cópias de segurança de iniciou o serviço Olá](sql-database-recovery-using-backups.md).
* toolearn sobre as opções de recuperação mais rápidas, consulte [georreplicação ativa](sql-database-geo-replication-overview.md).
* toolearn sobre a utilização de cópias de segurança automatizadas para arquivar, consulte [cópia da base de dados](sql-database-copy.md).

