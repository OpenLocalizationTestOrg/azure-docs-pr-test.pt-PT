---
title: Exportar tooSQL do Azure Application Insights | Microsoft Docs
description: Exporte continuamente tooSQL de dados do Application Insights com o Stream Analytics.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Instruções: Exportar tooSQL do Application Insights com o Stream Analytics
Este artigo mostra como toomove os dados de telemetria [Azure Application Insights] [ start] para uma base de dados SQL do Azure utilizando [exportação contínua] [ export] e [do Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). 

A exportação contínua move os dados de telemetria para o armazenamento do Azure no formato JSON. Vamos analisar os objetos JSON Olá utilizando o Azure Stream Analytics e criar linhas numa tabela da base de dados.

(Mais geralmente, a exportação contínua está Olá forma toodo o seus próprios análise de telemetria de Olá as suas aplicações enviar tooApplication Insights. A foi adaptar este toodo de exemplo de código outras coisas com a telemetria de Olá exportado, tais como a agregação de dados.)

Iremos começar com pressuposto Olá que já tenha aplicação Olá pretende toomonitor.

Neste exemplo, vamos utilizar dados de vista de página Olá, mas hello mesmo padrão pode facilmente ser expandido tooother tipos de dados, tais como exceções e eventos personalizados. 

## <a name="add-application-insights-tooyour-application"></a>Adicionar Application Insights tooyour aplicação
tooget iniciado:

1. [Configurar o Application Insights para as suas páginas web](app-insights-javascript.md). 
   
    (Neste exemplo, iremos irá focar-se no processamento de dados de vista de página browsers do cliente de Olá, mas também pode configurar Application Insights para o lado do servidor de Olá sua [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) aplicação e o processo de pedido dependência e outra telemetria do servidor.)
2. Publicar a aplicação e ver os dados de telemetria no recurso do Application Insights.

## <a name="create-storage-in-azure"></a>Criar armazenamento no Azure
A exportação contínua produz sempre a conta de armazenamento do Azure tooan de dados, pelo que necessita de armazenamento de Olá toocreate primeiro.

1. Criar uma conta de armazenamento na sua subscrição no Olá [portal do Azure][portal].
   
    ![No portal do Azure, escolha novo, dados, de armazenamento. Selecione clássico, escolha o criar. Forneça um nome de armazenamento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Criar um contentor
   
    ![No novo armazenamento Olá, selecionar contentores, clique em mosaico de contentores Olá e, em seguida, adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Copie a chave de acesso de armazenamento Olá
   
    Irá precisar das mesmas em breve tooset Olá toohello entrada stream analytics serviço.
   
    ![No armazenamento de Olá, abra as definições, as chaves e efetuar uma cópia da chave de acesso primária de Olá](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Iniciar a exportação contínua tooAzure armazenamento
1. No portal do Azure Olá, procure o recurso do Application Insights toohello que criou para a sua aplicação.
   
    ![Escolha procurar, Application Insights, a aplicação](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Crie uma exportação contínua.
   
    ![Escolha as definições, a exportação contínua, adicione](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Selecione a conta de armazenamento de Olá que criou anteriormente:

    ![Definir o destino de exportação de Olá](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Defina os tipos de evento Olá que pretende toosee:

    ![Escolha tipos de evento](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Permitir que alguns dados a acumularem. Manter-se novamente e permitir que as pessoas a utilizar a aplicação de tempo. Telemetria ficará e irá ver gráficos análises [explorer métrica](app-insights-metrics-explorer.md) e eventos individuais no [pesquisa de diagnóstico](app-insights-diagnostic-search.md). 
   
    Além disso, os dados de Olá serão de exportação e tooyour armazenamento. 
2. Inspecione Olá exportada dados, no portal de Olá - escolher **procurar**, selecione a sua conta de armazenamento e, em seguida, **contentores** - ou no Visual Studio. No Visual Studio, selecione **ver / nuvem Explorer**e a abrir Azure / armazenamento. (Se não tiver esta opção de menu, terá de tooinstall Olá SDK do Azure: Abra a caixa de diálogo do Olá novo projeto e abra Visual c# / nuvem / obter o Microsoft Azure SDK para .NET.)
   
    ![No Visual Studio, abra o Browser do servidor, o Azure, o armazenamento](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Tome nota da parte comuns de Olá de nome de caminho de Olá, que é derivado de chave de instrumentação e o nome de aplicação de Olá. 

eventos de Olá são escritos tooblob ficheiros no formato JSON. Cada ficheiro pode conter um ou mais eventos. Por isso, gostaríamos dados de eventos de Olá tooread e filtrar os campos de Olá que queremos. Existem todos os tipos de coisas que pode efetuar com dados Olá, mas a nossa plano é hoje toouse Stream Analytics toomove Olá dados tooa base de dados SQL. Que tornarão toorun fácil muitas das consultas interessantes.

## <a name="create-an-azure-sql-database"></a>Criar uma base de dados SQL do Azure
Novamente a partir da sua subscrição no [portal do Azure][portal], criar base de dados de Olá (e um novo servidor, a menos que já já tem um) toowhich irá escrever dados Olá.

![Novo, dados, o SQL Server](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Certifique-se de que o servidor da base de dados Olá permite o acesso tooAzure serviços:

![Procurar, servidores, o servidor, definições, Firewall, tooAzure permitir acesso](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Criar uma tabela na BD SQL do Azure
Ligar a base de dados de toohello criada na secção anterior do Olá com a ferramenta de gestão preferenciais. Esta explicação passo a passo, vamos utilizar [ferramentas de gestão do SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Criar uma nova consulta e execute Olá seguinte T-SQL:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

Neste exemplo, estamos a utilizar dados a partir de vistas de página. toosee Olá outros dados disponíveis, Inspecione a saída JSON e consulte Olá [exportar o modelo de dados](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Criar uma instância do Azure Stream Analytics
De Olá [Portal clássico do Azure](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics Olá e criar uma nova tarefa de Stream Analytics:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Quando é criada a nova tarefa de Olá, expanda os respectivos detalhes:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Definir localização de blob
Entrada de tootake a partir do seu blob exportação contínua de defini-lo:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Agora, terá Olá chave de acesso primária da sua conta de armazenamento, que anotou anteriormente. Defina esta opção como Olá chave da conta de armazenamento.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Padrão de prefixo do caminho de conjunto
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Ser demasiado se tooset Olá formato de data**aaaa-MM-DD** (com **traços**).

Olá caminho prefixo padrão Especifica como o Stream Analytics localiza os ficheiros de entrada Olá no armazenamento de Olá. Terá de tooset-toohow toocorrespond exportação contínua armazena dados Olá. Defina-o como esta:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Neste exemplo:

* `webapplication27`é o nome Olá Olá recurso do Application Insights, **todo em minúsculas**. 
* `1234...`é a chave de instrumentação Olá de Olá recurso do Application Insights **com traços removidos**. 
* `PageViews`é Olá tipo de dados queremos tooanalyze. tipos disponíveis Olá dependem de filtro de Olá definido na exportação contínua. Examine Olá de toosee Olá dados exportados outros tipos disponíveis e consulte Olá [exportar o modelo de dados](app-insights-export-data-model.md).
* `/{date}/{time}`um padrão é escrito literalmente.

nome de Olá tooget e iKey do recurso do Application Insights, abra Essentials na sua página de descrição geral ou abra definições.

#### <a name="finish-initial-setup"></a>Concluir a configuração inicial
Confirme o formato de serialização Olá:

![Confirmar e fechar o Assistente](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Feche o assistente Olá e aguarde Olá toocomplete de configuração.

> [!TIP]
> Utilize toocheck de função de exemplo de Olá que definiu caminho entrada Olá corretamente. Se não conseguir: Verifique se há dados no armazenamento de Olá para o intervalo de tempo do exemplo Olá que escolheu. Editar definição de entrada Olá e verificar definir a conta do storage Olá, prefixo do caminho e data corretamente formato.
> 
> 

## <a name="set-query"></a>Consulta de conjunto
Abra a secção de consulta Olá:

![Do stream analytics, selecione a consulta](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Substitua a consulta predefinida de Olá com:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Tenha em atenção que o primeiro Olá algumas propriedades são toopage específico ver dados. Exportações de outros tipos de telemetria tem propriedades diferentes. Consulte Olá [detalhadas referência de modelo de dados para tipos de propriedade Olá e valores.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Configurar toodatabase de saída
Selecione o SQL Server como saída Olá.

![Do stream analytics, selecione saídas](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Especifique Olá SQL da base de dados.

![Preencha os detalhes de Olá da base de dados](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Fechar o Assistente de Olá e aguarde que uma notificação que saída Olá tiver sido configurada.

## <a name="start-processing"></a>Iniciar o processamento
Inicie a tarefa de Olá a partir da barra de ação de Olá:

![Do stream analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Pode escolher se o processamento de toostart Olá dados a partir de agora ou toostart com dados anteriores. Olá esta última opção é útil se tiver tido a exportação contínua já em execução para um pouco.

![Do stream analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Após alguns minutos, volte atrás tooSQL ferramentas de gestão de servidor e veja Olá dados fluir em. Por exemplo, utilize uma consulta como esta:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Artigos relacionados
* [Exportar tooPowerBI utilizando o Stream Analytics](app-insights-export-power-bi.md)
* [Referência para os tipos de propriedade de Olá e valores de modelo de dados de detalhado.](app-insights-export-data-model.md)
* [Exportação contínua no Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

