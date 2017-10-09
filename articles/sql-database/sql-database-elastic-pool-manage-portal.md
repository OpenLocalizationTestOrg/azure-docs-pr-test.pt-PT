---
title: "Portal do Azure: criar e gerir um conjunto elástico da base de dados SQL | Microsoft Docs"
description: "Saiba como toouse Olá portal do Azure e toomanage de intelligence incorporadas da base de dados de SQL, monitor e um desempenho de base de dados do conjunto elástico dimensionável toooptimize dimensionar e gerir custo."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Criar e gerir um conjunto elástico com Olá portal do Azure
Este tópico mostra como toocreate e gerir dimensionável [conjuntos elásticos](sql-database-elastic-pool.md) com Olá portal do Azure. Também pode criar e gerir um conjunto elástico do Azure com [PowerShell](sql-database-elastic-pool-manage-powershell.md), Olá REST API, ou [c#](sql-database-elastic-pool-manage-csharp.md). Também pode criar e mover bases de dados para dentro e fora conjuntos elásticos utilizando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Criar um conjunto elástico 

Existem duas formas de criar um conjunto elástico. Pode fazê-lo a partir do zero se souber o programa de configuração Olá conjunto que pretende ou começa com uma recomendação do serviço de Olá. Base de dados SQL tem intelligence incorporado que recomenda uma configuração de conjunto elástico se é mais económico para si com base nas Olá passado telemetria de utilização para as bases de dados.

Pode criar vários conjuntos num servidor, mas não pode adicionar bases de dados de diferentes servidores ao hello mesmo conjunto. 

> [!NOTE]
> Os conjuntos elásticos estão em disponibilidade geral (GA) em todas as regiões do Azure, exceto na Índia Ocidental, onde se encontra, de momento, em pré-visualização.  A GA dos conjuntos elásticos nesta região vai ocorrer assim que possível.
>

### <a name="step-1-create-an-elastic-pool"></a>Passo 1: Criar um conjunto elástico

Criar um conjunto elástico existente de um **servidor** painel no portal de Olá é Olá mais fácil forma toomove bases de dados existentes para um conjunto elástico.

> [!NOTE]
> Também pode criar um conjunto elástico pesquisando **agrupamento elástico de SQL** no Olá **Marketplace** ou clicar **+ adicionar** no Olá **conjuntos elásticos SQL**procurar painel. São toospecify capaz de um servidor novo ou existente através deste agrupamento de aprovisionamento de fluxo de trabalho.
>
>

1. No Olá [portal do Azure](http://portal.azure.com/), clique em **mais serviços**  **>**  **servidores SQL**e, em seguida, clique em servidor Olá que contém Olá bases de dados que pretende que o agrupamento elástico de tooan tooadd.
2. Clique em **Novo conjunto**.

    ![Adicionar agrupamento tooa servidor](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-OU-**

    Poderá ver uma mensagem a indicar que existem são recomendadas conjuntos elásticos para o servidor de Olá. Clique em Olá toosee mensagem de Olá recomendado conjuntos com base na telemetria de utilização de base de dados históricos e, em seguida, clique Olá camada toosee mais detalhes e personalizar o conjunto de Olá. Consulte [compreender as recomendações de conjunto](#understand-elastic-pool-recommendations) mais adiante neste tópico para saber como a recomendação de Olá é feita.

    ![conjunto recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Olá **conjunto elástico** é apresentado o painel, que é onde especifica as definições de Olá para o seu conjunto. Se clicou em **novo conjunto** no passo anterior Olá, Olá escalão de preço é **padrão** está selecionada por predefinição e não existem bases de dados. Pode criar um conjunto vazio ou especifique um conjunto de bases de dados existentes do toomove servidor para o conjunto de Olá. Se estiver a criar um conjunto de recomendado, Olá recomendada preços camada, as definições de desempenho e são pré-preenchida a lista de bases de dados, mas ainda pode alterá-los.

    ![Configurar o conjunto elástico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Especifique um nome para o conjunto elástico hello, ou deixe-o como predefinição de Olá.

### <a name="step-2-choose-a-pricing-tier"></a>Passo 2: escolher um escalão de preço

Olá escalão de preço do conjunto determina Olá funcionalidades elastics toohello disponível no agrupamento de Olá e Olá número máximo de eDTUs (eDTU máxima) e a base de dados do armazenamento (GBs) disponível tooeach. Para obter detalhes, consulte o Escalões de serviços.

escalão de preço Olá toochange para o conjunto de Olá, clique em **escalão de preço**, clique em Olá pretende e, em seguida, clique em escalão de preço **selecione**.

> [!IMPORTANT]
> Depois de escolher Olá escalão de preço e consolidar as alterações ao clicar em **OK** no último passo Olá, não será Olá toochange capaz de escalão do conjunto de Olá de preço. toochange Olá escalão de preço de um conjunto elástico existente, crie um conjunto elástico no escalão de preço pretendido Olá e migre Olá bases de dados toothis novo agrupamento.
>

![Selecionar um escalão de preço](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Passo 3: Configurar o conjunto de Olá

Depois de definir Olá escalão de preço, clique em Configurar conjunto onde pode adicionar bases de dados, eDTUs de conjunto de conjunto e armazenamento (GBs do conjunto), e definir Olá min e max eDTUs para elastics Olá no agrupamento de Olá.

1. Clique em **Configurar conjunto**
2. Selecione as bases de dados de Olá pretende tooadd toohello agrupamento. Este passo é opcional ao criar o conjunto de Olá. Bases de dados podem ser adicionadas depois do conjunto de Olá ter sido criado.
    tooadd bases de dados, clique em **Adicionar base de dados**, clique em Olá as bases de dados que pretende tooadd e, em seguida, clique em Olá **selecione** botão.

    ![Adicionar bases de dados](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Se as bases de dados de Olá que está a trabalhar tiverem telemetria de histórico de utilização suficiente, Olá **estimado a utilização de GB e eDTU** gráfico e Olá **utilização de eDTU real** toohelp de atualização de gráfico de barras facilitam a configuração decisões. Além disso, Olá serviço poderá apresentar um toohelp de mensagem de recomendação poderá dimensionar Olá agrupamento. Consulte a secção [Recomendações Dinâmicas](#understand-elastic-pool-recommendations).

3. Utilizar controlos Olá Olá **configurar conjunto** página tooexplore definições e configurar o conjunto. Consulte [limites dos conjuntos elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para obter mais detalhes sobre os limites para cada camada de serviço e consulte [considerações sobre preço e desempenho para conjuntos elásticos](sql-database-elastic-pool.md) de detalhado orientações sobre como dimensionar corretamente um conjunto elástico. Para mais informações sobre as definições do conjunto, consulte [propriedades do conjunto elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Configurar o Conjunto Elástico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Clique em **selecione** no Olá **configurar conjunto** painel depois de alterar as definições.
5. Clique em **OK** conjunto de Olá toocreate.

## <a name="understand-elastic-pool-recommendations"></a>Compreender as recomendações de conjunto elástico

Olá serviço de base de dados SQL avalia o histórico de utilização e recomenda um ou mais conjuntos quando é mais rentável do que utilizar bases de dados individuais. Cada recomendação está configurada com um subconjunto exclusivo das bases de dados do servidor de Olá que melhor se adequam ao conjunto de Olá.

![conjunto recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

recomendação de conjunto de Olá é composta por:

- Um escalão de preço para o conjunto de Olá (básica, Standard, Premium ou Premium RS)
- O número adequado de **eDTUs POR CONJUNTO** (também denominado Número máximo de eDTUs por conjunto)
- Olá **número máximo de Edtus** e **número mínimo de Edtus** por base de dados
- lista de Olá de bases de dados recomendadas para o conjunto de Olá

> [!IMPORTANT]
> serviço de Olá tem Olá últimos 30 dias de telemetria em consideração quando recomenda conjuntos. Para um considerada candidata para um conjunto elástico toobe de base de dados, deve existir, pelo menos, 7 dias. As bases de dados que já estão num conjunto elástico não são consideradas candidatas para recomendações de conjunto elástico.
>

serviço de Olá avalia as necessidades de recursos e eficácia de custo de movimento Olá único bases de dados em cada camada de serviço para conjuntos do Olá mesmo escalão. Por exemplo, todas as bases de dados Standard num servidor são avaliadas para determinar a respetiva adequação a um Conjunto Elástico Standard. Isto significa que o serviço de Olá não faz recomendações entre escalões, tal como mover uma base de dados Standard para um conjunto Premium.

Depois de adicionar o conjunto de toohello de bases de dados, as recomendações são geradas dinamicamente com base no histórico de utilização de Olá das bases de dados de Olá que selecionou. Estas recomendações são apresentadas no gráfico de utilização de GB e eDTU Olá e numa faixa de recomendação no topo de Olá da Olá **configurar conjunto** painel. Estas recomendações estão tooassist pretendido na criação de um conjunto elástico otimizada para as bases de dados específicas.

![recomendações dinâmicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Gerir e monitorizar um conjunto elástico

Pode utilizar Olá toomonitor portal do Azure e gerir um conjunto elástico e Olá bases de dados no agrupamento de Olá. No portal de Olá, pode monitorizar a utilização de Olá do conjunto elástico e Olá bases de dados nesse agrupamento. Também pode efetuar um conjunto de alterações de conjunto elástico tooyour e submeter todas as alterações em Olá mesmo tempo. Estas alterações incluem a adição ou remoção de bases de dados, alterar as definições do conjunto elástico ou alterar as definições de base de dados.

Olá gráfico a seguir mostra um agrupamento elástico de exemplo. Vista de Olá inclui:

*  Gráficos para monitorizar a utilização de recursos de agrupamento elástico Olá e bases de dados de Olá contidos no agrupamento de Olá.
*  Olá **configurar** conjunto botão toomake altera o agrupamento elástico toohello.
*  Olá **criar base de dados** botão que cria uma base de dados e adiciona-toohello de conjunto elástico atual.
*  As tarefas elásticas que o ajudam a gerem um grande número de bases de dados através da execução de scripts de Transact SQL em todas as bases de dados numa lista.

![Vista de conjunto][2]

Pode aceder tooa conjunto particular toosee a respetiva utilização de recursos. Por predefinição, o agrupamento de Olá é a utilização de armazenamento e de eDTU tooshow configurado para Olá última hora. gráfico de Olá pode ser métricas diferentes tooshow configurado através de vários intervalos de tempo.

1. Selecione um toowork do conjunto elástico com.
2. Em **monitorização de agrupamento elástico** é um gráfico com a etiqueta **utilização de recursos**. Clique em Olá gráfico.

    ![Monitorização do conjunto elástico][3]

    Olá **métrica** abre painel, que mostra uma vista detalhada do Olá especificado métricas de janela de tempo especificado Olá.   

    ![Painel Métricas][9]

### <a name="toocustomize-hello-chart-display"></a>visualização de gráfico de Olá toocustomize

Pode editar gráfico Olá e Olá painel métrica toodisplay outras métricas, tais como a percentagem de CPU, percentagem de es de dados e a percentagem de es de registo utilizados.

1. No painel de métrica de Olá, clique em **editar**.

    ![Clique em Editar][6]

2. No Olá **editar gráfico** painel, selecione um intervalo de tempo (decorridos desde a hora, hoje em dia, ou últimos semana), ou clique em **personalizado** tooselect qualquer data intervalo no Olá últimas duas semanas. Selecione o tipo de gráfico de Olá (barra ou linha), em seguida, selecione Olá toomonitor de recursos.

   > [!Note]
   > Só as métricas com Olá mesma unidade de medida pode ser apresentada no Olá de gráfico em Olá mesmo tempo. Por exemplo, se selecionar "percentagem de eDTU", em seguida, pode apenas selecionar outras métricas percentagem como unidade de Olá de medida.
   >

    ![Clique em Editar](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Em seguida, clique em **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gerir e monitorizar bases de dados num agrupamento elástico

Bases de dados individuais também podem ser monitorizadas para potenciais problemas.

1. Em **monitorização de base de dados elásticas**, há um gráfico que mostra as métricas das cinco bases de dados. Por predefinição, Olá gráfico mostra Olá superior 5 as bases de dados no agrupamento de Olá pela utilização de eDTU médio no Olá horas anteriores. Clique em Olá gráfico.

    ![Monitorização do conjunto elástico][4]

2. Olá **utilização de recursos de base de dados** é apresentado o painel. Isto fornece uma vista detalhada da utilização de base de dados de Olá no agrupamento de Olá. Utilizar grelha Olá na parte inferior do Olá do painel de Olá, pode selecionar bases de dados no Olá conjunto toodisplay respetiva utilização no gráfico de Olá (segurança de bases de dados too5). Também pode personalizar a janela de métricas e a hora de Olá apresentada no gráfico de Olá clicando **editar gráfico**.

    ![Painel de utilização de recursos de base de dados][8]

### <a name="toocustomize-hello-view"></a>Vista de Olá toocustomize

1. No Olá **base de dados de utilização de recursos** painel, clique em **editar gráfico**.

    ![Clique em Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. No Olá **editar** gráfico painel, selecione um intervalo de tempo (decorridos desde hora ou últimos 24 horas) ou clique em **personalizado** tooselect dia diferentes no Olá passado toodisplay 2 semanas.

    ![Clique em personalizada](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Clique em Olá **comparar bases de dados ao** pendente tooselect um toouse métrica diferentes ao comparar a bases de dados.

    ![Editar gráfico Olá](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor de bases de dados

Na lista de base de dados de Olá do Olá **utilização de recursos de base de dados** painel, pode encontrar bases de dados específicos ao procurar nas páginas de Olá na lista de Olá ou ao escrever Olá nome de uma base de dados. Utilize Olá caixa de verificação tooselect Olá da base de dados.

![Procure toomonitor de bases de dados][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Adicione um recurso de conjunto elástico tooan alerta

Pode adicionar regras tooan conjunto elástico que enviar correio eletrónico toopeople ou alerta pontos finais tooURL de cadeias ao conjunto elástico Olá chega a um limiar de utilização que configurou.

**um recurso de alerta tooany tooadd:**

1. Clique em Olá **utilização de recursos** Olá do gráfico tooopen **métrica** painel, clique em **Adicionar alerta**e, em seguida, preencha as informações de Olá Olá **adicionar um alerta regra** painel (**recursos** automaticamente é configurar o conjunto de Olá de toobe que está a trabalhar com).
2. Escreva um **nome** e **Descrição** que identifica tooyou alerta Olá e destinatários de Olá.
3. Escolha um **métrica** que pretende que o tooalert da lista de Olá.

    gráfico de Olá dinamicamente mostra a utilização de recursos para esse toohelp métrica que escolher um limiar.

4. Escolha um **condição** (superior, inferior, etc.) e um **limiar**.
5. Escolha um **período** de tempo que Olá métrica regra deve ser satisfeita antes de acionadores de alerta de Olá.
6. Clique em **OK**.

Para obter mais informações, consulte [criam alertas de base de dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Mover uma base de dados para um conjunto elástico

Pode adicionar ou remover bases de dados a partir de um conjunto existente. podem estar bases de dados de Olá noutros conjuntos. No entanto, só é possível adicionar bases de dados que estão no Olá mesmo servidor lógico.

1. No painel de Olá para o conjunto de Olá, sob **bases de dados elásticas** clique **configurar conjunto**.

    ![Clique em Configurar conjunto][1]

2. No Olá **configurar conjunto** painel, clique em **adicionar toopool**.

    ![Clique em Adicionar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. No Olá **adicionar bases de dados** painel, base de dados de Olá selecione ou conjunto de toohello tooadd de bases de dados. Em seguida, clique em **selecione**.

    ![Selecione tooadd de bases de dados](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Olá **configurar conjunto** painel agora listas Olá base de dados selecionada toobe adicionado, com o respetivo estado definido demasiado**pendente**.

    ![Adições de agrupamento pendente](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. No Olá **painel do conjunto de configurar**, clique em **guardar**.

    ![Clicar em Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Mover uma base de dados fora de um conjunto elástico

1. No Olá **configurar conjunto** painel, base de dados de Olá selecione ou tooremove de bases de dados.

    ![lista de bases de dados](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Clique em **remover do agrupamento de**.

    ![lista de bases de dados](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Olá **configurar conjunto** painel agora listas Olá base de dados selecionada toobe removido com o respetivo estado definido demasiado**pendente**.

    ![pré-visualização da base de dados adição e remoção](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. No Olá **painel do conjunto de configurar**, clique em **guardar**.

    ![Clicar em Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Alterar as definições de desempenho de um conjunto elástico

Como monitorizar a utilização de recursos de Olá de um conjunto elástico, poderá descobrir que são necessários alguns ajustes. Talvez conjunto Olá necessita de uma alteração na Olá limites de desempenho ou o armazenamento. Possivelmente, pretende que as definições de base de dados de Olá toochange no agrupamento de Olá. Pode alterar a configuração de Olá do conjunto de Olá em qualquer altura tooget Olá melhor equilíbrio de desempenho e o custo. Consulte [quando um conjunto elástico a utilizar?](sql-database-elastic-pool.md) para obter mais informações.

toochange Olá eDTUs ou armazenamento limites por agrupamento e eDTUs por base de dados:

1. Abra Olá **configurar conjunto** painel.

    Em **as definições do conjunto elástico**, utilize o controlo de deslize toochange Olá as definições do conjunto.

    ![Utilização de recursos de agrupamento elástico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Quando altera a definição de Olá, a apresentação de Olá mostra Olá estimado custo mensal de alteração de Olá.

    ![Atualizar um conjunto elástico e o custo mensal novo](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latência de operações do conjunto elástico
* Normalmente, a alteração Olá eDTUs de Mín por base de dados ou o número máximo de eDTUs por base de dados conclui em 5 minutos ou menos.
* Alterar Olá eDTUs por conjunto depende da quantidade total de Olá de espaço utilizado por todas as bases de dados no agrupamento de Olá. Alterações em média 90 minutos ou menos por 100 GB. Por exemplo, se espaço total Olá utilizado por todas as bases de dados no agrupamento de Olá é 200 GB, em seguida, Olá esperado de latência para alterar o conjunto de Olá eDTU por conjunto é 3 horas ou menos.

## <a name="next-steps"></a>Passos seguintes

- toounderstand que um conjunto elástico estiver, consulte [conjunto elástico da base de dados SQL](sql-database-elastic-pool.md).
- Para obter orientações sobre como utilizar conjuntos elásticos, consulte [considerações sobre preço e desempenho para conjuntos elásticos](sql-database-elastic-pool.md).
- scripts de toorun Transact-SQL toouse as tarefas elásticas em qualquer número de bases de dados no agrupamento de Olá, consulte [descrição geral das tarefas elásticas](sql-database-elastic-jobs-overview.md).
- tooquery em qualquer número de bases de dados no agrupamento de Olá, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).
- Para transações qualquer número de bases de dados no agrupamento de Olá, consulte [transações elásticas](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
