---
title: "informações acerca do desempenho de aaaQuery para a SQL Database do Azure | Microsoft Docs"
description: "Monitorização do desempenho de consulta identifica Olá mais CPU consome consultas para uma base de dados do SQL do Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>SQL do Azure da base de dados desempenho das consultas
Gerir e otimização de desempenho de Olá das bases de dados relacionais são uma tarefa um desafio que requer conhecimentos significativos e o investimento de tempo. Desempenho das consultas permite-lhe toospend menos tempo de resolução de problemas de desempenho de base de dados, fornecendo seguinte Olá:

* Mais aprofundadas sobre o seu consumo de recursos (DTU) de bases de dados. 
* consultas de Olá superiores por contagem de CPU/duração/execução que potencialmente podem ser otimizados para um melhor desempenho.
* Olá toodrill de capacidade para baixo para detalhes de Olá de uma consulta, ver o texto e o histórico de utilização de recursos. 
* As anotações que mostram as ações executadas de otimização do desempenho [Advisor de base de dados SQL do Azure](sql-database-advisor.md)  



## <a name="prerequisites"></a>Pré-requisitos
* Consulta Performance Insight requer que [arquivo de consultas](https://msdn.microsoft.com/library/dn817826.aspx) está ativo na base de dados. Se o arquivo de consultas não está em execução, o portal de Olá pede-lhe tooturn-lo na.

## <a name="permissions"></a>Permissões
seguinte Olá [controlo de acesso baseado em funções](../active-directory/role-based-access-control-what-is.md) permissões são necessária toouse Query Performance Insight: 

* **Leitor**, **proprietário**, **contribuinte**, **contribuinte da BD SQL**, ou **contribuinte de servidor de SQL** são permissões necessário tooview Olá principais recursos consumir consultas e gráficos. 
* **Proprietário**, **contribuinte**, **contribuinte da BD SQL**, ou **contribuinte de servidor de SQL** permissões são necessárias tooview texto da consulta.

## <a name="using-query-performance-insight"></a>Utilizar o desempenho das consultas
Desempenho das consultas é fácil toouse:

* Abra [portal do Azure](https://portal.azure.com/) e localizar base de dados que pretende que o tooexamine. 
  * No menu do lado esquerdo, em suporte e resolução de problemas, selecione "Query Performance Insight".
* No separador de primeiro Olá, reveja a lista de Olá de consultas de consumo de recursos principais.
* Selecione uma consulta individual tooview os respetivos detalhes.
* Abra [Advisor de base de dados do SQL Azure](sql-database-advisor.md) e verifique se as recomendações estarão disponíveis.
* Utilizar controlos de deslize ou toochange ícones observado o intervalo de zoom.
  
    ![dashboard de desempenho](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Horas de alguns dos dados tem toobe capturado pelo arquivo de consultas para o query performance Insight para base de dados SQL tooprovide. Se a base de dados de Olá não tem nenhuma atividade ou o arquivo de consultas não esteve ativo durante um determinado período de tempo, os gráficos de Olá estará vazios quando se apresenta esse período de tempo. Se não está em execução, pode ativar o arquivo de consultas em qualquer altura.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Reveja principal da CPU de consultas de consumo
No Olá [portal](http://portal.azure.com) Olá a seguir:

1. Procurar tooa SQL da base de dados e clique em **todas as definições** > **suporte + resolução de problemas** > **nas informações de desempenho de consulta**. 
   
    ![Query Performance Insight][1]
   
    Abre a vista de consultas superiores Olá e as principais consultas consumo de CPU de Olá estão listadas.
2. Clique em torno do gráfico de Olá para obter mais detalhes.<br>Olá linha superior mostra % geral de DTU para base de dados de Olá, enquanto as barras de Olá mostram % de CPU consumido por consultas Olá selecionado durante o intervalo selecionado Olá (por exemplo, se **passado semana** está selecionado cada barra representa um dia).
   
    ![consultas superiores][2]
   
    grelha de inferior Olá representa a informação agregada para consultas visível Olá.
   
   * ID de consulta - o identificador exclusivo da consulta no interior da base de dados.
   * CPU por consulta durante o intervalo de observable (depende da função de agregação).
   * Duração por consulta (depende da função de agregação).
   * Número total de execuções de uma consulta específica.
     
     Selecione ou desmarque tooinclude consultas individuais ou excluir da gráfico Olá com caixas de verificação.
3. Se os dados torna-se obsoleta, clique em Olá **atualizar** botão.
4. Pode utilizar controlos de deslize e o intervalo de observação de toochange de botões de zoom e investigar picos: ![definições](./media/sql-database-query-performance/zoom.png)
5. Opcionalmente, se pretender uma vista diferente, pode selecionar **personalizada** separador e definir:
   
   * Métrica (CPU, duração, a contagem de execução)
   * Intervalo de tempo (últimas 24 horas, após uma semana, passado mês). 
   * Número de consultas.
   * Função de agregação.
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Detalhes de consulta individuais de visualização
detalhes de consulta tooview:

1. Clique em qualquer consulta na lista de Olá de consultas superiores.
   
    ![Detalhes](./media/sql-database-query-performance/details.png)
2. Abre a vista de detalhes de Olá e contagem de consumo/duração/execução Olá consultas CPU é reduzida ao longo do tempo.
3. Clique em torno do gráfico de Olá para obter mais detalhes.
   
   * Principal gráfico mostra a linha de base de dados DTU % geral e as barras de Olá são consumida pela consulta selecionada Olá de CPU de %.
   * Segundo gráfico mostra a duração total pela consulta selecionada Olá.
   * Gráfico de inferior mostra o número total de execuções pela consulta selecionada Olá.
     
     ![detalhes de consulta][3]
4. Opcionalmente, utilize os controlos de deslize, zoom botões ou clique em **definições** toocustomize como consultar dados são apresentados ou toopick um período de hora diferente.

## <a name="review-top-queries-per-duration"></a>Reveja as consultas superiores por duração
A atualização recente Olá de desempenho das consultas, introduzimos duas métricas novo que podem ajudar a identificar potenciais congestionamentos: contagem de duração e a execução.<br>

As consultas de execução longa ter possibilidade de maior Olá de bloqueio mais recursos, bloquear a outros utilizadores e limitar a escalabilidade. Também são candidatos a melhor Olá para otimização.<br>

tooidentify execução longa consultas:

1. Abra **personalizada** separador no desempenho das consultas de base de dados selecionada
2. Alterar as métricas toobe **duração**
3. Selecione o número de consultas e o intervalo de observação
4. Selecione a função de agregação
   
   * **Soma** adiciona todos os tempo de execução da consulta durante o intervalo de observação todo.
   * **Máx.** localiza consultas que tempo de execução estava máximo no intervalo de observação todo.
   * **Média** encontra tempo médio de execução de todas as execuções de consulta e mostrar-lhe Olá superior fora destes médias. 
     
     ![duração de consulta][4]

## <a name="review-top-queries-per-execution-count"></a>Reveja as consultas superiores por contagem de execução
Número elevado de execuções poderá não ser que afetam a própria base de dados e a utilização de recursos pode ser reduzida, mas global da aplicação poderá obter lenta.

Em alguns casos, contagem de execução muito elevado pode levar tooincrease da rede de ida e volta. Ida e volta afetar significativamente o desempenho. São latência de toonetwork do requerente e toodownstream latência de servidor. 

Por exemplo, muitos sites Web condicionada por dados fortemente aceder Olá base de dados para cada pedido de utilizador. Enquanto a ligação agrupamento ajuda-o, hello maior tráfego de rede e a carga de processamento no servidor de base de dados de Olá negativamente pode afeta o desempenho.  Conselhos geral é tookeep arredondar viagens tooan mínimo.

tooidentify executada com frequência consultas de ("chatty") de consultas:

1. Abra **personalizada** separador no desempenho das consultas de base de dados selecionada
2. Alterar as métricas toobe **contagem de execução**
3. Selecione o número de consultas e o intervalo de observação
   
    ![Contagem de execução da consulta][5]

## <a name="understanding-performance-tuning-annotations"></a>Noções sobre anotações de otimização de desempenho
Enquanto a explorar a carga de trabalho no desempenho das consultas, é possível que repare ícones com linha vertical por cima do gráfico Olá.<br>

Estes ícones são anotações; representam o desempenho que afetam a ações realizadas por [Advisor de base de dados do SQL Azure](sql-database-advisor.md). Por hovering anotação, obter informações básicas sobre a ação de Olá:

![anotação de consulta][6]

Se pretender mais tooknow ou aplicar a recomendação do advisor, clique no ícone Olá. Detalhes de ação é aberto. Se for uma recomendação de Active Directory, pode aplicá-la diretamente ausente utilizando o comando.

![detalhes de anotação de consulta][7]

### <a name="multiple-annotations"></a>Vários anotações.
É possível que, devido ao nível de zoom, irão obter fechadas anotações são tooeach fechar outros numa só. Isto será representado por ícone especial, clicar nela irá abrir novo painel onde a lista de agrupadas anotações será apresentado.
Correlacionar consultas e ações de otimização do desempenho pode ajudar toobetter compreender a sua carga de trabalho. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Otimizar a configuração do arquivo de consultas de Olá para o Query Performance Insight
Durante a utilização do desempenho das consultas, que poderá encontrar Olá seguintes mensagens de arquivo de consultas:

* "Arquivo de consultas não está devidamente configurado nesta base de dados. Clique aqui toolearn mais."
* "Arquivo de consultas não está devidamente configurado nesta base de dados. Clique aqui definições toochange." 

Estas mensagens são apresentados normalmente quando o arquivo de consultas não consegue toocollect novos dados. 

Primeiro caso acontece quando o arquivo de consultas está no estado só de leitura e os parâmetros estão definidos de forma ideal. Para corrigir este problema, aumente o tamanho do arquivo de consultas ou limpar o arquivo de consultas.

![botão de qds][8]

Segundo caso acontece quando o arquivo de consultas está desligado ou com parâmetros não se encontram definidos de forma ideal. <br>Pode alterar Olá retenção e a captura de política e ativar o arquivo de consultas ao executar comandos abaixo ou diretamente a partir do portal:

![botão de qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Política de retenção e a captura recomendada
Existem dois tipos de políticas de retenção:

* Tamanho baseia - se for atingida a tooAUTO conjunto irá limpar dados automaticamente quando perto de tamanho máximo.
* Hora com base - por predefinição será o definimos too30 dias, que significa que, se o arquivo de consultas irá ficar sem espaço, serão eliminadas consultar informações com mais de 30 dias

Captura de política pode ser definida como:

* **Todos os** -captura todas as consultas.
* **Auto** -influxo consultas e consultas com a duração de compilação e execução insignificant são ignoradas. Limiares de duração de execução contagem, compilação e tempo de execução são determinados internamente. Esta é a opção predefinida de Olá.
* **Nenhum** -arquivo de consultas deixa de captura nova consultas, no entanto, as estatísticas de tempo de execução de consultas já capturadas são ainda recolhidas.

Recomendamos que defina todas as políticas tooAUTO e limpar política too30 dias:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Aumente o tamanho do arquivo de consultas. Isto pode ser efetuada pela base de dados de tooa ligação e a emitir a seguinte consulta:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Aplicar estas definições, eventualmente, faz com que o arquivo de consultas recolher novas consultas, no entanto, se não quiser toowait pode limpar o arquivo de consultas. 

> [!NOTE]
> Executar consulta seguinte irá eliminar todas as informações atuais Olá arquivo de consultas. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Resumo
Desempenho das consultas ajuda-o a compreender o impacto de Olá da sua carga de trabalho de consulta e como se relaciona com toodatabase consumo de recursos. Com esta funcionalidade, irá saber mais sobre melhores Olá consultas de consumo e identificar facilmente Olá aqueles toofix antes de ficarem um problema.

## <a name="next-steps"></a>Passos seguintes
Para obter recomendações adicionais sobre como melhorar o desempenho de Olá da sua base de dados do SQL Server, clique em [recomendações](sql-database-advisor.md) no Olá **Query Performance Insight** painel.

![Advisor de desempenho](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

