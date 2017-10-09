---
title: "desempenho de aaaMonitor de muitas bases de dados SQL do Azure numa aplicação SaaS multi-inquilino | Microsoft Docs"
description: "Monitorizar e gerir o desempenho de bases de dados e agrupamentos de aplicações do Azure SQL da base de dados Wingtip SaaS de Olá"
keywords: tutorial de base de dados sql
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Monitorizar o desempenho de Olá aplicação Wingtip SaaS

Neste tutorial, são explorou vários cenários de gestão de chave de desempenho utilizados em aplicações SaaS. Utilizar uma atividade de toosimulate do gerador de carga em todas as bases de dados do inquilino, Olá incorporada monitorização e alertas funcionalidades da base de dados SQL e conjuntos elásticos são demonstradas.

aplicações de Wingtip SaaS Olá utilizam um modelo de dados de inquilino único, onde cada venue (inquilino) tem a sua própria base de dados. Como muitas aplicações de SaaS, Olá antecipado padrão de carga de trabalho de inquilino é imprevisível e esporádicas. Por outras palavras, as vendas de bilhetes podem ocorrer em qualquer altura. tootake vantagem deste padrão de utilização de base de dados típicas, inquilino bases de dados são implementadas em agrupamentos de bases de dados elásticas. Conjuntos elásticos otimizam os custos de Olá de uma solução, partilhar recursos em muitas bases de dados. Com este tipo de padrão, é importante toomonitor base de dados e tooensure de utilização de recursos de agrupamento carrega razoavelmente são equilibrados entre conjuntos. Também precisa de tooensure que bases de dados individuais tem recursos adequados e de que os conjuntos são não atingir os seus [eDTU](sql-database-what-is-a-dtu.md) limites. Este tutorial explicar toomonitor formas e gerir bases de dados e agrupamentos e como uma ação corretiva tootake na resposta toovariations numa carga de trabalho.

Neste tutorial, ficará a saber como:

> [!div class="checklist"]

> * Simular a utilização de bases de dados do Olá inquilino ao executar um gerador de carga fornecido
> * Inquilino do monitor Olá as bases de dados como estes respondem toohello aumento de carga
> * Aumentar verticalmente Olá conjunto elástico em resposta toohello da base de dados de aumento de carga
> * Aprovisionar uma segunda atividade de base de dados de balanceamento do tooload conjunto elástico


toocomplete neste tutorial, Olá se disponibilizar os seguintes pré-requisitos estão concluídas:

* Olá Wingtip SaaS aplicação é implementada. toodeploy em menos de cinco minutos, consulte [implementar e explorar aplicações de Wingtip SaaS Olá](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter mais detalhes, veja [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toosaas-performance-management-patterns"></a>Padrões de gestão de desempenho de tooSaaS de introdução

Gerir o desempenho de base de dados consiste em compilar e analisar dados de desempenho e, em seguida, agir os dados de toothis ao ajustar os parâmetros toomaintain um tempo de resposta aceitável para a sua aplicação. Quando alojam vários inquilinos, conjuntos de bases de dados elásticas estão tooprovide uma forma económica e gerir os recursos para um grupo de bases de dados com cargas de trabalho imprevisíveis. Com determinados padrões de carga de trabalho, um mínimo de duas bases de dados S3 pode beneficiar ao serem geridas num conjunto.

![suporte de dados](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Os conjuntos e bases de dados de Olá em conjuntos, devem ser tooensure monitorizado, ficam nos intervalos aceitáveis de desempenho. Otimizar Olá conjunto configuração toomeet Olá às necessidades da carga de trabalho de agregação Olá de todas as bases de dados, assegurar que os eDTUs de conjunto de Olá estão adequados para Olá carga de trabalho geral. Ajuste Olá por base de dados por base de dados e mínima de eDTU máxima valores tooappropriate os valores para os seus requisitos de aplicação específica.

### <a name="performance-management-strategies"></a>Estratégias da gestão do desempenho

* tooavoid ter toomanually monitorizar o desempenho, é mais eficaz demasiado**definir alertas acionam quando ou agrupamentos de bases de dados stray fora do normais intervalos**.
* Olá, flutuações de tooshort termo toorespond de nível de desempenho agregado de Olá de um agrupamento, **nível de eDTU do conjunto pode ser escalado para cima ou para baixo**. Se esta flutuação ocorre de forma normal ou previsível, **dimensionamento conjunto Olá pode ser agendada toooccur automaticamente**. Por exemplo, reduza verticalmente quando sabe que a carga de trabalho é leve, talvez durante a noite ou durante os fins de semana.
* Olá, flutuações de toolonger termo toorespond ou alterações ao número de bases de dados, **bases de dados individuais podem ser movidos para outros conjuntos**.
* os aumentos toorespond tooshort termo *individuais* carga de base de dados **bases de dados individuais podem ser efetuadas fora de um conjunto e atribuídos um nível de desempenho individuais**. Assim que a carga de Olá é reduzida, base de dados de Olá pode, em seguida, ser devolvido toohello agrupamento. Quando isto é conhecido seguinte com antecedência, bases de dados podem ser movidos pre-emptively tooensure Olá base de dados sempre tem recursos Olá necessita e tooavoid impacto nas outras bases de dados no agrupamento de Olá. Se este requisito é previsível, tais como um venue experienciar uma rush de vendas de pedido de suporte para um evento popular, este comportamento de gestão pode ser integrado na aplicação Olá.

Olá [portal do Azure](https://portal.azure.com) fornece monitorização incorporada e os alertas na maioria dos recursos. Na Base de Dados SQL, a monitorização e os alertas estão disponíveis nas bases de dados e nos conjuntos. Este incorporado monitorização e alertas é específico de recursos, é conveniente toouse para pequenas quantidades de recursos, mas não é muito conveniente ao trabalhar com muitos recursos.

Para cenários de elevado volume onde está a trabalhar com muitos reources, [análise de registos (OMS)](sql-database-saas-tutorial-log-analytics.md) pode ser utilizado. Este é um serviço Azure separado que fornece análises através de registos de diagnóstico emitidos e telemetria recolhidos numa área de trabalho de análise de registo. Análise de registos pode recolher telemetria a partir de vários serviços e ser utilizado tooquery e definir alertas.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Obter o código fonte da aplicação Wingtip Olá e scripts

Olá Wingtip SaaS scripts e código fonte da aplicação estão disponíveis no Olá [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório do github. [Os passos scripts de Wingtip SaaS toodownload Olá](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Aprovisionar inquilinos adicionais

Enquanto agrupamentos podem ser económicos com apenas dois bases de dados de S3, hello mais bases de dados que estão a ser Olá de conjunto de Olá mais económica Olá média, menos efeito torna-se. Para uma boa compreensão de como funciona a monitorização e a gestão do desempenho à escala, este tutorial requer que tenha, pelo menos, 20 bases de dados implementadas.

Se já um lote de inquilinos que aprovisionou um tutorial anterior, avance toohello [simular utilização em todas as bases de dados do inquilino](#simulate-usage-on-all-tenant-databases) secção.

1. Abra... \\Learning módulos\\monitorização de desempenho e gestão\\*demonstração PerformanceMonitoringAndManagement.ps1* no Olá *ISE do PowerShell*. Mantenha este script aberto, uma vez que vai executar vários cenários durante este tutorial.
1. Defina **$DemoScenario** = **1**, **Aprovisionar um lote de inquilinos**
1. Prima **F5** script de Olá toorun.

script de Olá irá implementar 17 inquilinos em menos de cinco minutos.

Olá *New-TenantBatch* script utiliza um conjunto aninhado ou ligado de [Resource Manager](../azure-resource-manager/index.md) modelos que criam um lote de inquilinos, que, por predefinição, copia a base de dados de Olá **basetenantdb** no Olá catálogo toocreate Olá novo inquilino bases de dados, em seguida, regista estes no catálogo de Olá e, finalmente, inicializa-los com o tipo de nome e venue do inquilino de Olá. Isto é consistente com a forma de Olá aplicação Olá aprovisiona um novo inquilino. Todas as alterações efetuadas demasiado*basetenantdb* é aplicado tooany novos inquilinos aprovisionados após essa data. Consulte Olá [tutorial de gestão de esquema](sql-database-saas-tutorial-schema-management.md) toosee como esquema de toomake alterações demasiado*existente* inquilino bases de dados (incluindo Olá *basetenantdb* base de dados).

## <a name="simulate-usage-on-all-tenant-databases"></a>Simular a utilização em todas as bases de dados de inquilinos

Olá *demonstração PerformanceMonitoringAndManagement.ps1* script é fornecida que simula uma carga de trabalho em execução em todas as bases de dados do inquilino. carga de Olá é gerada utilizando uma das situações de carga disponíveis Olá:

| Demonstração | Cenário |
|:--|:--|
| 2 | Gerar carga de intensidade normal (aprox. 40 DTUs) |
| 3 | Gerar carga com picos mais demorados e mais frequentes por base de dados|
| 4 | Gerar carga com picos de DTU mais altos por base de dados (aprox. 80 DTUs)|
| 5 | Gerar uma carga normal + uma carga elevada num inquilino individual (aprox. 95 DTUs)|
| 6 | Gerar carga desequilibrada em vários conjuntos|

gerador de carga Olá aplica-se um *sintético* base de dados do carregamento só de CPU tooevery inquilino. gerador de Olá inicia uma tarefa para cada base de dados do inquilino que chama um procedimento armazenado de uma só periodicamente o que gera carga Olá. níveis de carga Olá (nas eDTUs), a duração e o intervalos são diversificados em todas as bases de dados, simulando atividade inquilino imprevisível.

1. Abra... \\Learning módulos\\monitorização de desempenho e gestão\\*demonstração PerformanceMonitoringAndManagement.ps1* no Olá *ISE do PowerShell*. Mantenha este script aberto, uma vez que vai executar vários cenários durante este tutorial.
1. Definir **$DemoScenario** = **2**, *carga normal intensidade de gerar*.
1. Prima **F5** tooapply tooall uma carga as bases de dados do inquilino.

Wingtip é uma aplicação SaaS e carga do mundo real Olá numa aplicação SaaS é normalmente esporádicas e imprevisíveis. toosimulate isto, Olá carga gerador produz uma carga aleatório distribuída a todos os inquilinos. Necessários alguns minutos para Olá carga padrão tooemerge, por isso, executar o gerador de carga Olá durante 3 a 5 minutos antes de repetir o carregamento de Olá toomonitor em Olá secções a seguir.

> [!IMPORTANT]
> gerador de carga Olá está em execução como uma série de tarefas na sua sessão do PowerShell local. Manter Olá *demonstração PerformanceMonitoringAndManagement.ps1* separador abra! Se fechar o separador de Olá ou suspender o seu computador, deixa de gerador de carga Olá. gerador de carga Olá permanece num *invocar a tarefa* Estado onde gera carga de quaisquer novos inquilinos aprovisionados após o início do gerador de Olá. Utilize *Ctrl-C* toostop invocar as novas tarefas e saída Olá script. gerador de carga Olá continuará toorun, mas apenas nos inquilinos existentes.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Monitorizar a utilização de recursos com Olá portal do Azure

toomonitor Olá a utilização de recursos que carregamento de resultados de Olá que está a ser aplicada, abra o conjunto de portal toohello de Olá que contêm bases de dados do Olá inquilino:

1. Abra Olá [portal do Azure](https://portal.azure.com) e procurar toohello *tenants1 -&lt;utilizador&gt;*  servidor.
1. Desloque-se para baixo, localize os conjuntos elásticos e clique em **Pool1**. Este conjunto contém todos os Olá inquilino bases de dados criadas até ao momento.

Observar Olá **monitorização do conjunto elástico** e **monitorização de base de dados elástica** gráficos.

Olá a utilização de recursos do conjunto é utilização de base de dados de agregação de Olá para todas as bases de dados no agrupamento de Olá. gráfico de base de dados de Olá mostra Olá cinco hottest bases de dados:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Porque existem bases de dados adicionais no agrupamento de Olá além Olá cinco superior, utilização de conjunto de Olá mostra atividade que não será refletida no gráfico de bases de dados de cinco superior Olá. Para obter mais detalhes, clique em **utilização de recursos de base de dados**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Definir alertas de desempenho Olá agrupamento

Defina um alerta num conjunto de Olá que aciona no \>75% de utilização da seguinte forma:

1. Abra *Pool1* (no Olá *tenants1 -\<utilizador\>*  servidor) no Olá [portal do Azure](https://portal.azure.com).
1. Clique em **Regras de Alerta**e, em seguida, clique em **+ Adicionar alerta**:

   ![adicionar alerta](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Forneça um nome, tal como **DTU elevada**,
1. Definir Olá os seguintes valores:
   * **Métrica = percentagem de eDTU**
   * **Condição = maior que**.
   * **Limiar = 75**.
   * **Período = através de Olá últimos 30 minutos**.
1. Adicionar um toohello de endereço de correio eletrónico *administrador adicionais email(s)* caixa e clique em **OK**.

   ![alerta de definição](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Aumentar verticalmente um conjunto ocupado

Se o nível de carga agregado Olá aumenta num ponto de toohello conjunto que maxes saída conjunto Olá e atingir a utilização de eDTU de 100%, em seguida, o desempenho de base de dados individuais é afetado, potencialmente abrandamento tempos de resposta de consulta para todas as bases de dados no agrupamento de Olá.

**A curto prazo**, considere como aumentar verticalmente a recursos adicionais do Olá conjunto tooprovide ou remover bases de dados do conjunto de Olá (movê-los tooother agrupamentos, ou fora do escalão de serviço autónomo Olá conjunto tooa).

**Termo mais**, considere a possibilidade de otimizar as consultas ou índice de desempenho de base de dados de tooimprove de utilização. Consoante Olá tooperformance de sensibilidade da aplicação emite o tooscale prática melhor um conjunto de cópias de segurança antes de atingir a utilização de eDTU de 100%. Utilize um alerta toowarn que antecipadamente.

Pode simular um conjunto ocupado ao aumento da carga Olá produzido pelo gerador de dimensões Olá. A causar Olá tooburst de bases de dados mais frequentemente e para a carga agregado Olá maior, aumentar no conjunto de Olá sem alterar os requisitos de Olá das bases de dados individuais Olá. Como aumentar verticalmente conjunto Olá facilmente é efetuada no portal de Olá ou a partir do PowerShell. Neste exercício utiliza o portal de Olá.

1. Definir *$DemoScenario* = **3**, _carga gerar com maiores e mais frequentes bursts por base de dados_ intensidade de Olá tooincrease de carga de agregação Olá conjunto de Olá sem alterar Olá pico de carga necessário para cada base de dados.
1. Prima **F5** tooapply tooall uma carga as bases de dados do inquilino.

1. Aceda demasiado**Pool1** no Olá portal do Azure.

Olá monitor aumenta a utilização de eDTU do conjunto no gráfico superior Olá. Demora alguns minutos para tookick carga superior novo por Olá, mas rapidamente deverá ver o conjunto de Olá iniciar toohit de utilização máxima e como carga Olá steadies para padrão de nova Olá, sobrecarrega rapidamente conjunto Olá.

1. tooscale segurança agrupamento Olá, clique em **configurar conjunto** , Olá parte superior do Olá **Pool1** página.
1. Ajustar Olá **eDTU do conjunto** definição demasiado**100**. A alteração de eDTU do conjunto de Olá não alterar as definições de por base de dados de Olá (que é ainda 50 eDTU máxima por base de dados). Pode ver as definições do Olá por base de dados no lado direito de Olá de Olá **configurar conjunto** página.
1. Clique em **guardar** agrupamento de Olá toosubmit Olá pedido tooscale.

Voltar atrás demasiado**Pool1** > **descrição geral** Olá tooview gráficos de monitorização. Monitorizar o efeito de Olá de fornecer o conjunto de Olá com mais recursos (embora com algumas bases de dados e uma carga aleatório não seja sempre toosee fácil conclusively até ser executado há algum tempo). Enquanto está a visualizar Olá gráficos tenha em atenção que a 100% no Olá superior agora gráfico representa 100 eDTUs, enquanto no Olá inferior gráfico 100% ainda 50 eDTUs como Olá por base de dados máximo ainda 50 eDTUs.

Bases de dados permanecerem online e totalmente disponíveis ao longo do processo de Olá. Em Olá último neste momento dado que cada base de dados é toobe pronto, ativada com Olá novo eDTU de agrupamento, quaisquer ligações ativas sejam interrompidas. Código da aplicação sempre deve ser escrito tooretry ignorado ligações e para a ligação será restabelecida toohello base de dados no agrupamento de expandidos Olá.

## <a name="load-balance-between-pools"></a>Balanceamento de carga entre conjuntos

Como uma alternativa tooscaling segurança agrupamento Olá, crie um segundo conjunto e mover bases de dados para a mesma toobalance Olá carregar entre Olá dois conjuntos. toodo este novo conjunto de Olá deve estar criado no Olá mesmo servidor que Olá primeiro.

1. No Olá [portal do Azure](https://portal.azure.com), abra Olá **tenants1 -&lt;utilizador&gt;**  servidor.
1. Clique em **+ novo conjunto** toocreate um agrupamento de servidor atual Olá.
1. No Olá **conjunto de bases de dados elásticas** modelo:

    1. Definir **nome** demasiado*Pool2*.
    1. Deixe Olá preços camada como **conjunto Standard**.
    1. Clique em **Configurar conjunto**.
    1. Definir **eDTU do conjunto** demasiado*50 eDTU*.
    1. Clique em **adicionar bases de dados** toosee uma lista de bases de dados no servidor de Olá que podem ser adicionados demasiado*Pool2*.
    1. Selecione qualquer toomove 10 bases de dados estes toohello novo agrupamento e, em seguida, clique em **selecione**. Se tiver sido a executar o gerador de carga Olá, o serviço de Olá já sabe que o seu perfil de desempenho necessita de um conjunto maior do que o tamanho predefinido da 50 eDTU Olá e recomenda a começar com uma definição de eDTU 100.

    ![Recomendação](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Para este tutorial, deixe a predefinição de Olá 50 eDTUs e clique em **selecione** novamente.
    1. Selecione **OK** toocreate Olá novo agrupamento e toomove Olá selecionado bases de dados para a mesma.

Criar conjunto de Olá e mover bases de dados de Olá demora alguns minutos. Como as bases de dados são movidos permanecem online e acessível a totalmente até Olá último muito pouco, altura em que todas as ligações abertas são fechadas. Desde que tenham algumas lógica de repetição, os clientes, em seguida, irão ligar toohello base de dados no novo conjunto de Olá.

Procurar demasiado**Pool2** (no Olá *tenants1* servidor) tooopen Olá agrupamento e monitorizar o desempenho dele. Se não o vir, aguarde que o aprovisionamento de Olá novo conjunto toocomplete.

Verá então que a utilização de recursos no *Pool1* interrompeu e que *Pool2* da mesma forma já foi carregadas.

## <a name="manage-performance-of-a-single-database"></a>Gerir o desempenho de uma base de dados

Se uma base de dados individual num conjunto sofre uma carga elevada constante, consoante a configuração do agrupamento de Olá, poderá tendem a recursos de Olá toodominate no agrupamento de Olá e afetar outras bases de dados. Se a atividade de Olá toocontinue provável durante algum tempo, base de dados de Olá pode ser movido temporariamente fora do conjunto de Olá. Isto permite Olá de toohave de base de dados de Olá recursos adicionais necessita e isola de Olá outras bases de dados.

Neste exercício simula o efeito de Olá da Contoso Concert Hall experienciar uma elevada carga quando acede bilhetes de venda para um concert popular.

1. Abra Olá... \\ *Demonstração PerformanceMonitoringAndManagement.ps1* script.
1. Defina **$DemoScenario = 5, Gerar uma carga normal mais uma carga elevada num inquilino individual (aprox. 95 DTUs).**
1. Defina **$SingleTenantDatabaseName = contosoconcerthall**
1. Executar através do script de Olá **F5**.


1. No Olá [portal do Azure](https://portal.azure.com) abrir **Pool1**.
1. Inspecione Olá **monitorização do conjunto elástico** gráfico e procure a utilização de eDTU do conjunto de Olá aumentada. Depois de um minuto ou dois, uma carga maior Olá deve começar tookick em e, deverá ver rapidamente o conjunto de Olá chega a utilização de 100%.
1. Inspecione Olá **monitorização de base de dados elástica** ecrã que mostra as bases de dados hottest Olá Olá horas anteriores. Olá *contosoconcerthall* base de dados em breve deve aparecer como uma das bases de dados hottest Olá cinco.
1. **Clique em monitorização de base de dados elástica Olá** **gráfico** e abre-se Olá **utilização de recursos de base de dados** página onde é possível monitorizar qualquer uma das bases de dados de Olá. Isto permite-lhe isolar apresentar Olá para Olá *contosoconcerthall* base de dados.
1. Na lista de Olá das bases de dados, clique em **contosoconcerthall**.
1. Clique em **escalão de preço (dimensionamento DTUs)** tooopen Olá **Configurar desempenho** página onde pode definir um nível de desempenho autónomo da base de dados de Olá.
1. Clique em Olá **padrão** separador Opções de dimensionamento de Olá tooopen no escalão Standard Olá.
1. Deslize Olá **controlo de deslize DTU** tooright tooselect **100** DTUs. Note que este corresponde ao objetivo de serviço toohello, **S3**.
1. Clique em **aplicar** toomove Olá da base de dados fora do conjunto de Olá e torná-lo um *Standard S3* base de dados.
1. Assim que o dimensionamento é concluída, monitor Olá efeito na base de dados do Olá contosoconcerthall e Pool1 no painéis de agrupamento e da base de dados elásticos no Olá.

Assim que a carga elevada do Olá na base de dados do Olá contosoconcerthall subsides deve retomadas rapidamente regressar-toohello conjunto tooreduce o custo. Se não é claro quando que irá acontecer pode configurar um alerta na base de dados de Olá que é acionado quando a utilização da DTU descerem abaixo Olá por base de dados máximo no conjunto de Olá. Veja o exercício 5, para saber como mover uma base de dados para um conjunto.

## <a name="other-performance-management-patterns"></a>Outros Padrões de Gestão do Desempenho

**Dimensionamento preventivas** exercício de Olá acima onde, explorou como tooscale uma base de dados isolado, souberem que toolook de base de dados para. Se a gestão de Olá da Contoso Concert Hall tinha informado Wingtips de venda de permissão iminente Olá, base de dados de Olá foi terem sido movido fora do conjunto de Olá pre-emptively. Caso contrário, é provável que necessitaria um alerta no conjunto de Olá ou Olá toospot de base de dados que estava a acontecer. Não pretende toolearn sobre esta de Olá outros inquilinos na Olá conjunto complaining de degradação do desempenho. E se o inquilino Olá pode prever quanto terão de recursos adicionais pode configurar uma automatização do Azure runbook toomove Olá base de dados fora do conjunto de Olá e, em seguida, fazer uma cópia no novo com base numa agenda definida.

**Dimensionamento de self-service de inquilino** porque o dimensionamento é uma tarefa facilmente chamada através de API de gestão de Olá, pode facilmente criar capacidade Olá tooscale inquilino as bases de dados na sua aplicação destinado ao inquilino e oferecem-la como uma funcionalidade do seu serviço de SaaS. Por exemplo, permitir que os inquilinos self-administer aumentar e reduzir verticalmente, talvez ligado diretamente tootheir faturação!

**Aumentar um conjunto e reduzir verticalmente nos padrões de utilização de toomatch agenda**

Em que a utilização de agregação inquilino segue padrões de utilização previsíveis, pode utilizar tooscale de automatização do Azure um agrupamento de cima e baixo com base numa agenda. Por exemplo, reduza verticalmente um conjunto após as 18:00 e aumente-o verticalmente antes das 06:00 nos dias da semana quando sabe que existe uma quebra nos requisitos de recursos.



## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Simular a utilização de bases de dados do Olá inquilino ao executar um gerador de carga fornecido
> * Inquilino do monitor Olá as bases de dados como estes respondem toohello aumento de carga
> * Aumentar verticalmente Olá conjunto elástico em resposta toohello da base de dados de aumento de carga
> * Aprovisionar uma segundo conjunto elástico tooload saldo Olá atividade base de dados

[Tutorial Restaurar um inquilino individual](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais baseiam Olá implementação de aplicação Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Conjuntos elásticos SQL](sql-database-elastic-pool.md)
* [Automatização do Azure](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) – Tutorial de configuração e utilização do Log Analytics
