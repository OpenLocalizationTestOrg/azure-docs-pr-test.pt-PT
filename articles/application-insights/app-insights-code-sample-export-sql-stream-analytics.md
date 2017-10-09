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
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="cbe08-103">Instruções: Exportar tooSQL do Application Insights com o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbe08-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="cbe08-104">Este artigo mostra como toomove os dados de telemetria [Azure Application Insights] [ start] para uma base de dados SQL do Azure utilizando [exportação contínua] [ export] e [do Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="cbe08-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="cbe08-105">A exportação contínua move os dados de telemetria para o armazenamento do Azure no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cbe08-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="cbe08-106">Vamos analisar os objetos JSON Olá utilizando o Azure Stream Analytics e criar linhas numa tabela da base de dados.</span><span class="sxs-lookup"><span data-stu-id="cbe08-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="cbe08-107">(Mais geralmente, a exportação contínua está Olá forma toodo o seus próprios análise de telemetria de Olá as suas aplicações enviar tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="cbe08-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="cbe08-108">A foi adaptar este toodo de exemplo de código outras coisas com a telemetria de Olá exportado, tais como a agregação de dados.)</span><span class="sxs-lookup"><span data-stu-id="cbe08-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="cbe08-109">Iremos começar com pressuposto Olá que já tenha aplicação Olá pretende toomonitor.</span><span class="sxs-lookup"><span data-stu-id="cbe08-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="cbe08-110">Neste exemplo, vamos utilizar dados de vista de página Olá, mas hello mesmo padrão pode facilmente ser expandido tooother tipos de dados, tais como exceções e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="cbe08-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="cbe08-111">Adicionar Application Insights tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="cbe08-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="cbe08-112">tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="cbe08-112">tooget started:</span></span>

1. <span data-ttu-id="cbe08-113">[Configurar o Application Insights para as suas páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="cbe08-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="cbe08-114">(Neste exemplo, iremos irá focar-se no processamento de dados de vista de página browsers do cliente de Olá, mas também pode configurar Application Insights para o lado do servidor de Olá sua [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) aplicação e o processo de pedido dependência e outra telemetria do servidor.)</span><span class="sxs-lookup"><span data-stu-id="cbe08-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="cbe08-115">Publicar a aplicação e ver os dados de telemetria no recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cbe08-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="cbe08-116">Criar armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="cbe08-116">Create storage in Azure</span></span>
<span data-ttu-id="cbe08-117">A exportação contínua produz sempre a conta de armazenamento do Azure tooan de dados, pelo que necessita de armazenamento de Olá toocreate primeiro.</span><span class="sxs-lookup"><span data-stu-id="cbe08-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="cbe08-118">Criar uma conta de armazenamento na sua subscrição no Olá [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="cbe08-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![No portal do Azure, escolha novo, dados, de armazenamento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="cbe08-122">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="cbe08-122">Create a container</span></span>
   
    ![No novo armazenamento Olá, selecionar contentores, clique em mosaico de contentores Olá e, em seguida, adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="cbe08-124">Copie a chave de acesso de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="cbe08-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="cbe08-125">Irá precisar das mesmas em breve tooset Olá toohello entrada stream analytics serviço.</span><span class="sxs-lookup"><span data-stu-id="cbe08-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![No armazenamento de Olá, abra as definições, as chaves e efetuar uma cópia da chave de acesso primária de Olá](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="cbe08-127">Iniciar a exportação contínua tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="cbe08-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="cbe08-128">No portal do Azure Olá, procure o recurso do Application Insights toohello que criou para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="cbe08-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Escolha procurar, Application Insights, a aplicação](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="cbe08-130">Crie uma exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="cbe08-130">Create a continuous export.</span></span>
   
    ![Escolha as definições, a exportação contínua, adicione](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="cbe08-132">Selecione a conta de armazenamento de Olá que criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="cbe08-132">Select hello storage account you created earlier:</span></span>

    ![Definir o destino de exportação de Olá](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="cbe08-134">Defina os tipos de evento Olá que pretende toosee:</span><span class="sxs-lookup"><span data-stu-id="cbe08-134">Set hello event types you want toosee:</span></span>

    ![Escolha tipos de evento](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="cbe08-136">Permitir que alguns dados a acumularem.</span><span class="sxs-lookup"><span data-stu-id="cbe08-136">Let some data accumulate.</span></span> <span data-ttu-id="cbe08-137">Manter-se novamente e permitir que as pessoas a utilizar a aplicação de tempo.</span><span class="sxs-lookup"><span data-stu-id="cbe08-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="cbe08-138">Telemetria ficará e irá ver gráficos análises [explorer métrica](app-insights-metrics-explorer.md) e eventos individuais no [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="cbe08-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="cbe08-139">Além disso, os dados de Olá serão de exportação e tooyour armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cbe08-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="cbe08-140">Inspecione Olá exportada dados, no portal de Olá - escolher **procurar**, selecione a sua conta de armazenamento e, em seguida, **contentores** - ou no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbe08-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="cbe08-141">No Visual Studio, selecione **ver / nuvem Explorer**e a abrir Azure / armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cbe08-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="cbe08-142">(Se não tiver esta opção de menu, terá de tooinstall Olá SDK do Azure: Abra a caixa de diálogo do Olá novo projeto e abra Visual c# / nuvem / obter o Microsoft Azure SDK para .NET.)</span><span class="sxs-lookup"><span data-stu-id="cbe08-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![No Visual Studio, abra o Browser do servidor, o Azure, o armazenamento](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="cbe08-144">Tome nota da parte comuns de Olá de nome de caminho de Olá, que é derivado de chave de instrumentação e o nome de aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="cbe08-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="cbe08-145">eventos de Olá são escritos tooblob ficheiros no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cbe08-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="cbe08-146">Cada ficheiro pode conter um ou mais eventos.</span><span class="sxs-lookup"><span data-stu-id="cbe08-146">Each file may contain one or more events.</span></span> <span data-ttu-id="cbe08-147">Por isso, gostaríamos dados de eventos de Olá tooread e filtrar os campos de Olá que queremos.</span><span class="sxs-lookup"><span data-stu-id="cbe08-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="cbe08-148">Existem todos os tipos de coisas que pode efetuar com dados Olá, mas a nossa plano é hoje toouse Stream Analytics toomove Olá dados tooa base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbe08-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="cbe08-149">Que tornarão toorun fácil muitas das consultas interessantes.</span><span class="sxs-lookup"><span data-stu-id="cbe08-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="cbe08-150">Criar uma base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="cbe08-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="cbe08-151">Novamente a partir da sua subscrição no [portal do Azure][portal], criar base de dados de Olá (e um novo servidor, a menos que já já tem um) toowhich irá escrever dados Olá.</span><span class="sxs-lookup"><span data-stu-id="cbe08-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Novo, dados, o SQL Server](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="cbe08-153">Certifique-se de que o servidor da base de dados Olá permite o acesso tooAzure serviços:</span><span class="sxs-lookup"><span data-stu-id="cbe08-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Procurar, servidores, o servidor, definições, Firewall, tooAzure permitir acesso](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="cbe08-155">Criar uma tabela na BD SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="cbe08-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="cbe08-156">Ligar a base de dados de toohello criada na secção anterior do Olá com a ferramenta de gestão preferenciais.</span><span class="sxs-lookup"><span data-stu-id="cbe08-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="cbe08-157">Esta explicação passo a passo, vamos utilizar [ferramentas de gestão do SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="cbe08-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="cbe08-158">Criar uma nova consulta e execute Olá seguinte T-SQL:</span><span class="sxs-lookup"><span data-stu-id="cbe08-158">Create a new query, and execute hello following T-SQL:</span></span>

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

<span data-ttu-id="cbe08-159">Neste exemplo, estamos a utilizar dados a partir de vistas de página.</span><span class="sxs-lookup"><span data-stu-id="cbe08-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="cbe08-160">toosee Olá outros dados disponíveis, Inspecione a saída JSON e consulte Olá [exportar o modelo de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="cbe08-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="cbe08-161">Criar uma instância do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbe08-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="cbe08-162">De Olá [Portal clássico do Azure](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics Olá e criar uma nova tarefa de Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="cbe08-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="cbe08-163">Quando é criada a nova tarefa de Olá, expanda os respectivos detalhes:</span><span class="sxs-lookup"><span data-stu-id="cbe08-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="cbe08-164">Definir localização de blob</span><span class="sxs-lookup"><span data-stu-id="cbe08-164">Set blob location</span></span>
<span data-ttu-id="cbe08-165">Entrada de tootake a partir do seu blob exportação contínua de defini-lo:</span><span class="sxs-lookup"><span data-stu-id="cbe08-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="cbe08-166">Agora, terá Olá chave de acesso primária da sua conta de armazenamento, que anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cbe08-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="cbe08-167">Defina esta opção como Olá chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cbe08-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="cbe08-168">Padrão de prefixo do caminho de conjunto</span><span class="sxs-lookup"><span data-stu-id="cbe08-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="cbe08-169">Ser demasiado se tooset Olá formato de data**aaaa-MM-DD** (com **traços**).</span><span class="sxs-lookup"><span data-stu-id="cbe08-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="cbe08-170">Olá caminho prefixo padrão Especifica como o Stream Analytics localiza os ficheiros de entrada Olá no armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="cbe08-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="cbe08-171">Terá de tooset-toohow toocorrespond exportação contínua armazena dados Olá.</span><span class="sxs-lookup"><span data-stu-id="cbe08-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="cbe08-172">Defina-o como esta:</span><span class="sxs-lookup"><span data-stu-id="cbe08-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="cbe08-173">Neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="cbe08-173">In this example:</span></span>

* <span data-ttu-id="cbe08-174">`webapplication27`é o nome Olá Olá recurso do Application Insights, **todo em minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="cbe08-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="cbe08-175">`1234...`é a chave de instrumentação Olá de Olá recurso do Application Insights **com traços removidos**.</span><span class="sxs-lookup"><span data-stu-id="cbe08-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="cbe08-176">`PageViews`é Olá tipo de dados queremos tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="cbe08-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="cbe08-177">tipos disponíveis Olá dependem de filtro de Olá definido na exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="cbe08-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="cbe08-178">Examine Olá de toosee Olá dados exportados outros tipos disponíveis e consulte Olá [exportar o modelo de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="cbe08-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="cbe08-179">`/{date}/{time}`um padrão é escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="cbe08-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="cbe08-180">nome de Olá tooget e iKey do recurso do Application Insights, abra Essentials na sua página de descrição geral ou abra definições.</span><span class="sxs-lookup"><span data-stu-id="cbe08-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="cbe08-181">Concluir a configuração inicial</span><span class="sxs-lookup"><span data-stu-id="cbe08-181">Finish initial setup</span></span>
<span data-ttu-id="cbe08-182">Confirme o formato de serialização Olá:</span><span class="sxs-lookup"><span data-stu-id="cbe08-182">Confirm hello serialization format:</span></span>

![Confirmar e fechar o Assistente](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="cbe08-184">Feche o assistente Olá e aguarde Olá toocomplete de configuração.</span><span class="sxs-lookup"><span data-stu-id="cbe08-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="cbe08-185">Utilize toocheck de função de exemplo de Olá que definiu caminho entrada Olá corretamente.</span><span class="sxs-lookup"><span data-stu-id="cbe08-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="cbe08-186">Se não conseguir: Verifique se há dados no armazenamento de Olá para o intervalo de tempo do exemplo Olá que escolheu.</span><span class="sxs-lookup"><span data-stu-id="cbe08-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="cbe08-187">Editar definição de entrada Olá e verificar definir a conta do storage Olá, prefixo do caminho e data corretamente formato.</span><span class="sxs-lookup"><span data-stu-id="cbe08-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="cbe08-188">Consulta de conjunto</span><span class="sxs-lookup"><span data-stu-id="cbe08-188">Set query</span></span>
<span data-ttu-id="cbe08-189">Abra a secção de consulta Olá:</span><span class="sxs-lookup"><span data-stu-id="cbe08-189">Open hello query section:</span></span>

![Do stream analytics, selecione a consulta](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="cbe08-191">Substitua a consulta predefinida de Olá com:</span><span class="sxs-lookup"><span data-stu-id="cbe08-191">Replace hello default query with:</span></span>

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

<span data-ttu-id="cbe08-192">Tenha em atenção que o primeiro Olá algumas propriedades são toopage específico ver dados.</span><span class="sxs-lookup"><span data-stu-id="cbe08-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="cbe08-193">Exportações de outros tipos de telemetria tem propriedades diferentes.</span><span class="sxs-lookup"><span data-stu-id="cbe08-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="cbe08-194">Consulte Olá [detalhadas referência de modelo de dados para tipos de propriedade Olá e valores.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="cbe08-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="cbe08-195">Configurar toodatabase de saída</span><span class="sxs-lookup"><span data-stu-id="cbe08-195">Set up output toodatabase</span></span>
<span data-ttu-id="cbe08-196">Selecione o SQL Server como saída Olá.</span><span class="sxs-lookup"><span data-stu-id="cbe08-196">Select SQL as hello output.</span></span>

![Do stream analytics, selecione saídas](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="cbe08-198">Especifique Olá SQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="cbe08-198">Specify hello SQL database.</span></span>

![Preencha os detalhes de Olá da base de dados](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="cbe08-200">Fechar o Assistente de Olá e aguarde que uma notificação que saída Olá tiver sido configurada.</span><span class="sxs-lookup"><span data-stu-id="cbe08-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="cbe08-201">Iniciar o processamento</span><span class="sxs-lookup"><span data-stu-id="cbe08-201">Start processing</span></span>
<span data-ttu-id="cbe08-202">Inicie a tarefa de Olá a partir da barra de ação de Olá:</span><span class="sxs-lookup"><span data-stu-id="cbe08-202">Start hello job from hello action bar:</span></span>

![Do stream analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="cbe08-204">Pode escolher se o processamento de toostart Olá dados a partir de agora ou toostart com dados anteriores.</span><span class="sxs-lookup"><span data-stu-id="cbe08-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="cbe08-205">Olá esta última opção é útil se tiver tido a exportação contínua já em execução para um pouco.</span><span class="sxs-lookup"><span data-stu-id="cbe08-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![Do stream analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="cbe08-207">Após alguns minutos, volte atrás tooSQL ferramentas de gestão de servidor e veja Olá dados fluir em.</span><span class="sxs-lookup"><span data-stu-id="cbe08-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="cbe08-208">Por exemplo, utilize uma consulta como esta:</span><span class="sxs-lookup"><span data-stu-id="cbe08-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="cbe08-209">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="cbe08-209">Related articles</span></span>
* [<span data-ttu-id="cbe08-210">Exportar tooPowerBI utilizando o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbe08-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="cbe08-211">Referência para os tipos de propriedade de Olá e valores de modelo de dados de detalhado.</span><span class="sxs-lookup"><span data-stu-id="cbe08-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="cbe08-212">Exportação contínua no Application Insights</span><span class="sxs-lookup"><span data-stu-id="cbe08-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="cbe08-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="cbe08-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

