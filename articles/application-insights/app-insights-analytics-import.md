---
title: aaaImport tooAnalytics os dados no Azure Application Insights | Microsoft Docs
description: "Importar dados estáticos toojoin com a telemetria da aplicação ou importe um tooquery de fluxo de dados separada Analytics."
services: application-insights
keywords: "Abra o esquema, a importação de dados"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="e3b65-104">Importar dados para análise</span><span class="sxs-lookup"><span data-stu-id="e3b65-104">Import data into Analytics</span></span>

<span data-ttu-id="e3b65-105">Importar dados de tabela para [análise](app-insights-analytics.md), qualquer toojoin com [Application Insights](app-insights-overview.md) telemetria da sua aplicação, ou pode analisá-lo como uma sequência separada.</span><span class="sxs-lookup"><span data-stu-id="e3b65-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="e3b65-106">A análise é fluxos de elevado volume timestamped uma consulta poderosa idioma tooanalyzing adequada de telemetria.</span><span class="sxs-lookup"><span data-stu-id="e3b65-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="e3b65-107">Pode importar dados para análise ao utilizar o seu próprio esquema.</span><span class="sxs-lookup"><span data-stu-id="e3b65-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="e3b65-108">Não tem esquemas de Application Insights de padrão de Olá do toouse como pedido ou rastreio.</span><span class="sxs-lookup"><span data-stu-id="e3b65-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="e3b65-109">Pode importar JSON ou DSV (delimitador de valores separados por - ponto e vírgula, vírgula ou por separador) ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e3b65-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="e3b65-110">Existem três situações em que a importação tooAnalytics é útil:</span><span class="sxs-lookup"><span data-stu-id="e3b65-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="e3b65-111">**Associe-se com a telemetria da aplicação.**</span><span class="sxs-lookup"><span data-stu-id="e3b65-111">**Join with app telemetry.**</span></span> <span data-ttu-id="e3b65-112">Por exemplo, pode importar uma tabela que mapeia os URLs de títulos de página legível de toomore o Web site.</span><span class="sxs-lookup"><span data-stu-id="e3b65-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="e3b65-113">Análise, pode criar um relatório de gráfico do dashboard que mostra Olá dez páginas mais populares no seu Web site.</span><span class="sxs-lookup"><span data-stu-id="e3b65-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="e3b65-114">Agora, pode mostrar Olá títulos de página em vez de Olá URLs.</span><span class="sxs-lookup"><span data-stu-id="e3b65-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="e3b65-115">**Correlacionar a telemetria da sua aplicação** com outras origens, como o tráfego de rede, os dados do servidor ou CDN ficheiros de registo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="e3b65-116">**Aplica o fluxo de dados separada do tooa de análise.**</span><span class="sxs-lookup"><span data-stu-id="e3b65-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="e3b65-117">Application Insights Analytics é uma ferramenta poderosa, o que funciona bem com dispersa, timestamped fluxos - muito melhores do que o SQL Server em muitos casos.</span><span class="sxs-lookup"><span data-stu-id="e3b65-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="e3b65-118">Se tiver essa um fluxo de alguns outra origem, pode analisá-lo com a análise.</span><span class="sxs-lookup"><span data-stu-id="e3b65-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="e3b65-119">Enviar dados de origem de dados de tooyour é fácil.</span><span class="sxs-lookup"><span data-stu-id="e3b65-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="e3b65-120">(Uma vez) Defina o esquema de Olá dos seus dados numa "origem de dados'.</span><span class="sxs-lookup"><span data-stu-id="e3b65-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="e3b65-121">(Periodicamente) Carregar o armazenamento de tooAzure de dados e chame Olá REST API toonotify-nos que novos dados está a aguardar ingestão.</span><span class="sxs-lookup"><span data-stu-id="e3b65-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="e3b65-122">Dentro de alguns minutos, os dados de Olá estão disponíveis para consulta na análise.</span><span class="sxs-lookup"><span data-stu-id="e3b65-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="e3b65-123">Olá frequência de carregamento de Olá é definida por si e a rapidez pretende que o seu toobe dados disponível para consultas.</span><span class="sxs-lookup"><span data-stu-id="e3b65-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="e3b65-124">É mais eficientes dados de tooupload segmentos maior, mas não superior a 1GB.</span><span class="sxs-lookup"><span data-stu-id="e3b65-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="e3b65-125">*Obteve muitos tooanalyze de origens de dados?*</span><span class="sxs-lookup"><span data-stu-id="e3b65-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="e3b65-126">*Considere a utilização de* logstash *tooship os dados no Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="e3b65-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="e3b65-127">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="e3b65-127">Before you start</span></span>

<span data-ttu-id="e3b65-128">É necessário:</span><span class="sxs-lookup"><span data-stu-id="e3b65-128">You need:</span></span>

1. <span data-ttu-id="e3b65-129">Um recurso do Application Insights no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b65-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="e3b65-130">Se quiser tooanalyze os dados separadamente a partir de qualquer outra telemetria [criar um novo recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e3b65-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="e3b65-131">Se estiver a adesão ou comparar os seus dados com a telemetria a partir de uma aplicação que já está definida com o Application Insights, em seguida, pode utilizar recursos Olá para essa aplicação.</span><span class="sxs-lookup"><span data-stu-id="e3b65-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="e3b65-132">Recurso de toothat de acesso contribuinte ou proprietário.</span><span class="sxs-lookup"><span data-stu-id="e3b65-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="e3b65-133">Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b65-133">Azure storage.</span></span> <span data-ttu-id="e3b65-134">Carregar tooAzure armazenamento e análise obtém os dados a partir daí.</span><span class="sxs-lookup"><span data-stu-id="e3b65-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="e3b65-135">Recomendamos que crie uma conta de armazenamento dedicado para os blobs.</span><span class="sxs-lookup"><span data-stu-id="e3b65-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="e3b65-136">Se os blobs são partilhados com outros processos, demora mais longo para o nosso tooread processos os blobs.</span><span class="sxs-lookup"><span data-stu-id="e3b65-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="e3b65-137">Definir o esquema</span><span class="sxs-lookup"><span data-stu-id="e3b65-137">Define your schema</span></span>

<span data-ttu-id="e3b65-138">Antes de importar dados, tem de definir um *origem de dados,* que especifica o esquema de Olá dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="e3b65-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="e3b65-139">Pode ter segurança too50 origens de dados num único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="e3b65-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="e3b65-140">Inicie o Assistente de origem de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-140">Start hello data source wizard.</span></span> <span data-ttu-id="e3b65-141">Utilize o botão "Adicionar nova origem de dados".</span><span class="sxs-lookup"><span data-stu-id="e3b65-141">Use "Add new data source" button.</span></span> <span data-ttu-id="e3b65-142">Em alternativa - clique no botão de definições no canto superior direito e selecione "Origens de dados" no menu pendente.</span><span class="sxs-lookup"><span data-stu-id="e3b65-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Adicionar nova origem de dados](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="e3b65-144">Forneça um nome para a nova origem de dados.</span><span class="sxs-lookup"><span data-stu-id="e3b65-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="e3b65-145">Defina o formato de ficheiros de Olá que irá carregar.</span><span class="sxs-lookup"><span data-stu-id="e3b65-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="e3b65-146">Pode definir o formato de Olá manualmente ou carregar um ficheiro de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="e3b65-147">Se os dados de Olá estão num formato CSV, Olá primeira linha exemplo Olá pode ser cabeçalhos de coluna.</span><span class="sxs-lookup"><span data-stu-id="e3b65-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="e3b65-148">Pode alterar os nomes de campos de Olá no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="e3b65-149">exemplo de Olá deve incluir pelo menos 10 linhas ou registos de dados.</span><span class="sxs-lookup"><span data-stu-id="e3b65-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="e3b65-150">Os nomes de coluna ou o campo devem ter nomes alfanuméricos (sem espaços ou pontuação).</span><span class="sxs-lookup"><span data-stu-id="e3b65-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Carregar um ficheiro de exemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="e3b65-152">Esquema de Olá de revisão que Olá assistente foi obtido.</span><span class="sxs-lookup"><span data-stu-id="e3b65-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="e3b65-153">Se este inferir tipos de Olá a partir de uma amostra, poderá ter de tipos de Olá inferido tooadjust de colunas de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Esquema de Olá inferido de revisão](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="e3b65-155">(Opcional.) Carregue uma definição de esquema.</span><span class="sxs-lookup"><span data-stu-id="e3b65-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="e3b65-156">Consulte o formato de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-156">See hello format below.</span></span>

 * <span data-ttu-id="e3b65-157">Selecione um carimbo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-157">Select a Timestamp.</span></span> <span data-ttu-id="e3b65-158">Todos os dados na análise tem de ter um campo de carimbo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="e3b65-159">Tem de ter tipo `datetime`, mas não tem toobe com o nome 'timestamp'.</span><span class="sxs-lookup"><span data-stu-id="e3b65-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="e3b65-160">Se os seus dados têm uma coluna que contém uma data e hora no formato ISO, escolha tal como coluna de carimbo de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="e3b65-161">Caso contrário, escolha "como dados chegou" e o processo de importação de Olá irá adicionar um campo de carimbo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="e3b65-162">Crie origem de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="e3b65-163">Formato de ficheiro de definição de esquema</span><span class="sxs-lookup"><span data-stu-id="e3b65-163">Schema definition file format</span></span>

<span data-ttu-id="e3b65-164">Em vez de editar o esquema de Olá na IU, pode carregar a definição de esquema de Olá de um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e3b65-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="e3b65-165">formato de definição de esquema Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3b65-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="e3b65-166">Formato delimitado</span><span class="sxs-lookup"><span data-stu-id="e3b65-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="e3b65-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="e3b65-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="e3b65-168">Cada coluna é identificada por nome e tipo de localização de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="e3b65-169">Localização – para o formato de ficheiro delimitado-lo é posição Olá do valor de Olá mapeado.</span><span class="sxs-lookup"><span data-stu-id="e3b65-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="e3b65-170">Para o formato JSON, é Olá jpath da chave de Olá mapeado.</span><span class="sxs-lookup"><span data-stu-id="e3b65-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="e3b65-171">Nome – Olá apresentado o nome da coluna de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="e3b65-172">Tipo – Olá dados dessa coluna.</span><span class="sxs-lookup"><span data-stu-id="e3b65-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="e3b65-173">No caso de dados de exemplo foi utilizados e é delimitado formato de ficheiro, definição de esquema Olá tem de mapear todas as colunas e adicionar novas colunas no fim de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="e3b65-174">JSON permite um mapeamento parcial de dados de Olá, portanto hello definição de esquema no formato JSON não tem toomap cada chave que não foi encontrado nos dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e3b65-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="e3b65-175">-Também é possível mapear colunas que não façam parte de dados de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3b65-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="e3b65-176">Importar dados</span><span class="sxs-lookup"><span data-stu-id="e3b65-176">Import data</span></span>

<span data-ttu-id="e3b65-177">dados tooimport, carregue-o armazenamento de tooAzure, criar uma chave de acesso para o mesmo e, em seguida, efetuar uma chamada de REST API.</span><span class="sxs-lookup"><span data-stu-id="e3b65-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Adicionar nova origem de dados](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="e3b65-179">Pode efetuar Olá seguindo o processo manualmente ou configurar um toodo automatizado do sistema-lo em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="e3b65-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="e3b65-180">Terá de toofollow estes passos para cada bloco de dados pretende tooimport.</span><span class="sxs-lookup"><span data-stu-id="e3b65-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="e3b65-181">Carregar dados de Olá demasiado[blob storage do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="e3b65-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="e3b65-182">Os BLOBs podem ser qualquer dimensão se too1GB descomprimidos.</span><span class="sxs-lookup"><span data-stu-id="e3b65-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="e3b65-183">Os blobs grande de centenas de MB são ideais de uma perspetiva de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e3b65-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="e3b65-184">Pode comprimi-los com o tempo de carregamento de tooimprove Gzip e latência para Olá dados toobe disponível para consulta.</span><span class="sxs-lookup"><span data-stu-id="e3b65-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="e3b65-185">Olá utilize `.gz` extensão de nome de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e3b65-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="e3b65-186">É melhor toouse uma conta de armazenamento separada para esta finalidade, chamadas de tooavoid provenientes de diferentes serviços abrandamento desempenho.</span><span class="sxs-lookup"><span data-stu-id="e3b65-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="e3b65-187">Quando o envio de dados de alta frequência, cada alguns segundos, é recomendado toouse mais do que uma conta de armazenamento, por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e3b65-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="e3b65-188">[Criar uma chave de assinatura de acesso partilhado de blob Olá](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="e3b65-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="e3b65-189">chave de Olá deve ter um período de expiração de um dia e fornecer acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="e3b65-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="e3b65-190">Efetuar uma toonotify de chamada REST Application Insights que está a aguardar a dados.</span><span class="sxs-lookup"><span data-stu-id="e3b65-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="e3b65-191">Ponto final:`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="e3b65-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="e3b65-192">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="e3b65-192">HTTP method: POST</span></span>
 * <span data-ttu-id="e3b65-193">Payload:</span><span class="sxs-lookup"><span data-stu-id="e3b65-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="e3b65-194">marcadores de posição de Olá são:</span><span class="sxs-lookup"><span data-stu-id="e3b65-194">hello placeholders are:</span></span>

* <span data-ttu-id="e3b65-195">`Blob URI with Shared Access Key`: Pode obter esta do procedimento de Olá para criar uma chave.</span><span class="sxs-lookup"><span data-stu-id="e3b65-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="e3b65-196">É blob toohello específico.</span><span class="sxs-lookup"><span data-stu-id="e3b65-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="e3b65-197">`Schema ID`: Olá ID do esquema gerado para o esquema definido.</span><span class="sxs-lookup"><span data-stu-id="e3b65-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="e3b65-198">dados Olá este blob devem estar em conformidade toohello esquema.</span><span class="sxs-lookup"><span data-stu-id="e3b65-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="e3b65-199">`DateTime`: tempo de Olá no qual Olá pedido ser submetido, UTC.</span><span class="sxs-lookup"><span data-stu-id="e3b65-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="e3b65-200">Podemos aceitar estes formatos: ISO8601 (como "2016-01-01 13:45:01"); Rfc822 ("Qua, 14 16 de Dec 14:57:01 + 0000"); RFC850 ("Quarta-feira, 14-Dec-16 UTC de 57:14:00"); RFC1123 ("Qua, 14 de Dec de 2016 57:14:00 + 0000").</span><span class="sxs-lookup"><span data-stu-id="e3b65-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="e3b65-201">`Instrumentation key`de recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e3b65-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="e3b65-202">dados de Olá estão disponíveis no Analytics após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e3b65-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="e3b65-203">Respostas de erro</span><span class="sxs-lookup"><span data-stu-id="e3b65-203">Error responses</span></span>

* <span data-ttu-id="e3b65-204">**pedido incorreto 400**: indica que o payload de pedido Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="e3b65-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="e3b65-205">Verifique:</span><span class="sxs-lookup"><span data-stu-id="e3b65-205">Check:</span></span>
 * <span data-ttu-id="e3b65-206">Chave de instrumentação correto.</span><span class="sxs-lookup"><span data-stu-id="e3b65-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="e3b65-207">Valor de hora válido.</span><span class="sxs-lookup"><span data-stu-id="e3b65-207">Valid time value.</span></span> <span data-ttu-id="e3b65-208">Deve ser tempo Olá agora em UTC.</span><span class="sxs-lookup"><span data-stu-id="e3b65-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="e3b65-209">Está em conformidade com o JSON do evento de Olá toohello esquema.</span><span class="sxs-lookup"><span data-stu-id="e3b65-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="e3b65-210">**403 Proibido**: blob Olá que enviou não está acessível.</span><span class="sxs-lookup"><span data-stu-id="e3b65-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="e3b65-211">Certifique-se de que essa chave de acesso partilhado Olá é válido e não expirou.</span><span class="sxs-lookup"><span data-stu-id="e3b65-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="e3b65-212">**404 não encontrado**:</span><span class="sxs-lookup"><span data-stu-id="e3b65-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="e3b65-213">blob Olá não existe.</span><span class="sxs-lookup"><span data-stu-id="e3b65-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="e3b65-214">sourceId Olá está errada.</span><span class="sxs-lookup"><span data-stu-id="e3b65-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="e3b65-215">Estão disponíveis na mensagem de erro de resposta de Olá informações mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="e3b65-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="e3b65-216">Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="e3b65-216">Sample code</span></span>

<span data-ttu-id="e3b65-217">Este código utiliza Olá [newtonsoft](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="e3b65-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="e3b65-218">Classes</span><span class="sxs-lookup"><span data-stu-id="e3b65-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="e3b65-219">Ingerir dados</span><span class="sxs-lookup"><span data-stu-id="e3b65-219">Ingest data</span></span>

<span data-ttu-id="e3b65-220">Utilize este código para cada blob.</span><span class="sxs-lookup"><span data-stu-id="e3b65-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="e3b65-221">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e3b65-221">Next steps</span></span>

* [<span data-ttu-id="e3b65-222">Apresentação de Olá idioma de consulta de análise de registos</span><span class="sxs-lookup"><span data-stu-id="e3b65-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="e3b65-223">Utilize *Logstash* toosend dados tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="e3b65-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
