---
title: "aaaEnabling as métricas do storage no portal do Azure de Olá | Microsoft Docs"
description: "Como as métricas do storage tooenable para Olá serviços Blob, fila, tabela e ficheiro"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="514d0-103">Ativar as métricas do Storage do Azure e visualizar dados de métricas</span><span class="sxs-lookup"><span data-stu-id="514d0-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="514d0-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="514d0-104">Overview</span></span>
<span data-ttu-id="514d0-105">As métricas do Storage está ativada por predefinição quando cria uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="514d0-106">Pode configurar a monitorização através de Olá [portal do Azure](https://portal.azure.com) ou o Windows PowerShell, ou através de programação através de uma das bibliotecas de cliente do armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="514d0-107">Pode configurar um período de retenção de dados de métricas de Olá: este período determina para armazenamento de Olá quanto serviço mantém métricas Olá e eventuais encargos lhe Olá espaço necessário toostore-los.</span><span class="sxs-lookup"><span data-stu-id="514d0-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="514d0-108">Normalmente, deve utilizar um período de retenção mais curto minuto com base nas métricas que métricas horárias devido a Olá significativas extra o espaço necessário para as métricas de minutos.</span><span class="sxs-lookup"><span data-stu-id="514d0-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="514d0-109">Deverá escolher um período de retenção de forma a que tem suficiente vez tooanalyze Olá que os dados e transferir quaisquer métricas desejar tookeep para fins de relatórios ou de análise offline.</span><span class="sxs-lookup"><span data-stu-id="514d0-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="514d0-110">Lembre-se de que será também faturado para transferência de dados de métricas da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="514d0-111">Como métricas de tooenable utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="514d0-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="514d0-112">Siga estes passos tooenable nas métricas nas Olá [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="514d0-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="514d0-113">Navegue tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="514d0-114">Selecione **diagnóstico** no Olá **Menu** painel</span><span class="sxs-lookup"><span data-stu-id="514d0-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="514d0-115">Certifique-se de que **estado** estiver definido demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="514d0-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="514d0-116">Selecione Olá as métricas para os serviços de Olá desejar toomonitor.</span><span class="sxs-lookup"><span data-stu-id="514d0-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="514d0-117">Especifique um tooindicate de política de retenção quanto tooretain métricas e registo de dados.</span><span class="sxs-lookup"><span data-stu-id="514d0-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="514d0-118">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="514d0-118">Select **Save**.</span></span>

<span data-ttu-id="514d0-119">Tenha em atenção que Olá [portal do Azure](https://portal.azure.com) não atualmente permitem-lhe tooconfigure métricas minuto na sua conta de armazenamento; tem de ativar as métricas minutos com o PowerShell ou através de programação.</span><span class="sxs-lookup"><span data-stu-id="514d0-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="514d0-120">Como métricas de tooenable através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="514d0-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="514d0-121">Pode utilizar o PowerShell no seu computador local de tooconfigure as métricas do Storage na sua conta de armazenamento utilizando Olá Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Olá definições atuais e Olá cmdlet Conjunto AzureStorageServiceMetricsProperty toochange Olá definições atuais.</span><span class="sxs-lookup"><span data-stu-id="514d0-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="514d0-122">cmdlets de Olá que controlam as métricas do Storage utilizam Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="514d0-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="514d0-123">MetricsType: os valores possíveis são horas e minutos.</span><span class="sxs-lookup"><span data-stu-id="514d0-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="514d0-124">ServiceType: os valores possíveis são tabela, fila e Blob.</span><span class="sxs-lookup"><span data-stu-id="514d0-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="514d0-125">MetricsLevel: os valores possíveis são None, serviço e ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="514d0-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="514d0-126">Por exemplo, hello seguinte comando muda num minuto métricas para o serviço de Blob Olá na sua conta de armazenamento predefinido com um período de retenção de Olá definir toofive dias:</span><span class="sxs-lookup"><span data-stu-id="514d0-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="514d0-127">Olá seguinte comando obtém Olá atuais por hora métricas e retenção de nível de dias para o serviço de blob Olá na sua conta do storage predefinida:</span><span class="sxs-lookup"><span data-stu-id="514d0-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="514d0-128">Para obter informações sobre como tooconfigure Olá Azure PowerShell cmdlets toowork com a sua subscrição do Azure e como tooselect Olá armazenamento predefinido toouse de contas, consulte: [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="514d0-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="514d0-129">Como tooenable as métricas do Storage através de programação</span><span class="sxs-lookup"><span data-stu-id="514d0-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="514d0-130">Olá c# fragmento a seguir mostra como tooenable métricas e registo de utilização de serviço Blob do Olá hello a biblioteca de clientes de armazenamento para .NET:</span><span class="sxs-lookup"><span data-stu-id="514d0-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="514d0-131">Ver as métricas do Storage</span><span class="sxs-lookup"><span data-stu-id="514d0-131">Viewing Storage metrics</span></span>
<span data-ttu-id="514d0-132">Depois de configurar toomonitor de métricas da análise de armazenamento a conta do storage, análise de armazenamento regista métricas Olá num conjunto de tabelas bem conhecidas na sua conta do storage.</span><span class="sxs-lookup"><span data-stu-id="514d0-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="514d0-133">Pode configurar métricas de hora a hora de tooview de gráficos na Olá [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="514d0-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="514d0-134">Navegue tooyour a conta de armazenamento no Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="514d0-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="514d0-135">Selecione **métricas** no Olá **Menu** painel Olá service cujas métricas pretende tooview.</span><span class="sxs-lookup"><span data-stu-id="514d0-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="514d0-136">Selecione **editar** no gráfico de Olá pretende tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="514d0-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="514d0-137">No Olá **editar gráfico** painel, selecione de Olá **intervalo de tempo**, **tipo de gráfico**e métricas de Olá que pretende apresentar no gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="514d0-138">Selecione **OK**</span><span class="sxs-lookup"><span data-stu-id="514d0-138">Select **OK**</span></span>

<span data-ttu-id="514d0-139">Se pretender que as métricas de Olá toodownload para armazenamento de longa duração ou tooanalyze-los localmente, precisa de:</span><span class="sxs-lookup"><span data-stu-id="514d0-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="514d0-140">Utilize uma ferramenta que está ciente destas tabelas e permitem-lhe tooview e transferi-los.</span><span class="sxs-lookup"><span data-stu-id="514d0-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="514d0-141">Escrever um tooread de aplicação ou script personalizado e armazenar tabelas Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="514d0-142">Muitas ferramentas de navegação de armazenamento de terceiros estão cientes estas tabelas e permitem-lhe tooview-los diretamente.</span><span class="sxs-lookup"><span data-stu-id="514d0-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="514d0-143">Consulte [ferramentas de cliente de armazenamento do Azure](storage-explorers.md) para obter uma lista das ferramentas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="514d0-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="514d0-144">Começando com a versão 0.8.0 de Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/), pode ver e transferir a tabelas de métricas de análise Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="514d0-145">Na análise de Olá ordem tooaccess tabelas programaticamente, tenha em atenção que as tabelas de análise Olá não são apresentados se lista todas as tabelas de Olá na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="514d0-146">Pode aceder às mesmas diretamente pelo nome, ou utilizar Olá [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) no Olá .NET cliente biblioteca tooquery Olá os nomes das tabelas.</span><span class="sxs-lookup"><span data-stu-id="514d0-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="514d0-147">Métricas por hora</span><span class="sxs-lookup"><span data-stu-id="514d0-147">Hourly metrics</span></span>
* <span data-ttu-id="514d0-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="514d0-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="514d0-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="514d0-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="514d0-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="514d0-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="514d0-151">Métricas de minutos</span><span class="sxs-lookup"><span data-stu-id="514d0-151">Minute metrics</span></span>
* <span data-ttu-id="514d0-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="514d0-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="514d0-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="514d0-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="514d0-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="514d0-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="514d0-155">Capacidade</span><span class="sxs-lookup"><span data-stu-id="514d0-155">Capacity</span></span>
* <span data-ttu-id="514d0-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="514d0-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="514d0-157">Pode encontrar detalhes completos de esquemas Olá para estas tabelas em [armazenamento esquema da tabela de métricas de análise](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="514d0-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="514d0-158">linhas de exemplo de Olá abaixo mostram apenas um subconjunto de colunas de Olá disponíveis, mas ilustram algumas funcionalidades importantes de forma Olá que as métricas do Storage guarda estas métricas:</span><span class="sxs-lookup"><span data-stu-id="514d0-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="514d0-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="514d0-159">PartitionKey</span></span> | <span data-ttu-id="514d0-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="514d0-160">RowKey</span></span> | <span data-ttu-id="514d0-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="514d0-161">Timestamp</span></span> | <span data-ttu-id="514d0-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="514d0-162">TotalRequests</span></span> | <span data-ttu-id="514d0-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="514d0-163">TotalBillableRequests</span></span> | <span data-ttu-id="514d0-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="514d0-164">TotalIngress</span></span> | <span data-ttu-id="514d0-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="514d0-165">TotalEgress</span></span> | <span data-ttu-id="514d0-166">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="514d0-166">Availability</span></span> | <span data-ttu-id="514d0-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="514d0-167">AverageE2ELatency</span></span> | <span data-ttu-id="514d0-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="514d0-168">AverageServerLatency</span></span> | <span data-ttu-id="514d0-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="514d0-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="514d0-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="514d0-170">20140522T1100</span></span> |<span data-ttu-id="514d0-171">utilizador; Todos os</span><span class="sxs-lookup"><span data-stu-id="514d0-171">user;All</span></span> |<span data-ttu-id="514d0-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="514d0-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="514d0-173">7</span><span class="sxs-lookup"><span data-stu-id="514d0-173">7</span></span> |<span data-ttu-id="514d0-174">7</span><span class="sxs-lookup"><span data-stu-id="514d0-174">7</span></span> |<span data-ttu-id="514d0-175">4003</span><span class="sxs-lookup"><span data-stu-id="514d0-175">4003</span></span> |<span data-ttu-id="514d0-176">46801</span><span class="sxs-lookup"><span data-stu-id="514d0-176">46801</span></span> |<span data-ttu-id="514d0-177">100</span><span class="sxs-lookup"><span data-stu-id="514d0-177">100</span></span> |<span data-ttu-id="514d0-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="514d0-178">104.4286</span></span> |<span data-ttu-id="514d0-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="514d0-179">6.857143</span></span> |<span data-ttu-id="514d0-180">100</span><span class="sxs-lookup"><span data-stu-id="514d0-180">100</span></span> |
| <span data-ttu-id="514d0-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="514d0-181">20140522T1100</span></span> |<span data-ttu-id="514d0-182">utilizador; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="514d0-182">user;QueryEntities</span></span> |<span data-ttu-id="514d0-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="514d0-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="514d0-184">5</span><span class="sxs-lookup"><span data-stu-id="514d0-184">5</span></span> |<span data-ttu-id="514d0-185">5</span><span class="sxs-lookup"><span data-stu-id="514d0-185">5</span></span> |<span data-ttu-id="514d0-186">2694</span><span class="sxs-lookup"><span data-stu-id="514d0-186">2694</span></span> |<span data-ttu-id="514d0-187">45951</span><span class="sxs-lookup"><span data-stu-id="514d0-187">45951</span></span> |<span data-ttu-id="514d0-188">100</span><span class="sxs-lookup"><span data-stu-id="514d0-188">100</span></span> |<span data-ttu-id="514d0-189">143.8</span><span class="sxs-lookup"><span data-stu-id="514d0-189">143.8</span></span> |<span data-ttu-id="514d0-190">7.8</span><span class="sxs-lookup"><span data-stu-id="514d0-190">7.8</span></span> |<span data-ttu-id="514d0-191">100</span><span class="sxs-lookup"><span data-stu-id="514d0-191">100</span></span> |
| <span data-ttu-id="514d0-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="514d0-192">20140522T1100</span></span> |<span data-ttu-id="514d0-193">utilizador; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="514d0-193">user;QueryEntity</span></span> |<span data-ttu-id="514d0-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="514d0-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="514d0-195">1</span><span class="sxs-lookup"><span data-stu-id="514d0-195">1</span></span> |<span data-ttu-id="514d0-196">1</span><span class="sxs-lookup"><span data-stu-id="514d0-196">1</span></span> |<span data-ttu-id="514d0-197">538</span><span class="sxs-lookup"><span data-stu-id="514d0-197">538</span></span> |<span data-ttu-id="514d0-198">633</span><span class="sxs-lookup"><span data-stu-id="514d0-198">633</span></span> |<span data-ttu-id="514d0-199">100</span><span class="sxs-lookup"><span data-stu-id="514d0-199">100</span></span> |<span data-ttu-id="514d0-200">3</span><span class="sxs-lookup"><span data-stu-id="514d0-200">3</span></span> |<span data-ttu-id="514d0-201">3</span><span class="sxs-lookup"><span data-stu-id="514d0-201">3</span></span> |<span data-ttu-id="514d0-202">100</span><span class="sxs-lookup"><span data-stu-id="514d0-202">100</span></span> |
| <span data-ttu-id="514d0-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="514d0-203">20140522T1100</span></span> |<span data-ttu-id="514d0-204">utilizador; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="514d0-204">user;UpdateEntity</span></span> |<span data-ttu-id="514d0-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="514d0-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="514d0-206">1</span><span class="sxs-lookup"><span data-stu-id="514d0-206">1</span></span> |<span data-ttu-id="514d0-207">1</span><span class="sxs-lookup"><span data-stu-id="514d0-207">1</span></span> |<span data-ttu-id="514d0-208">771</span><span class="sxs-lookup"><span data-stu-id="514d0-208">771</span></span> |<span data-ttu-id="514d0-209">217</span><span class="sxs-lookup"><span data-stu-id="514d0-209">217</span></span> |<span data-ttu-id="514d0-210">100</span><span class="sxs-lookup"><span data-stu-id="514d0-210">100</span></span> |<span data-ttu-id="514d0-211">9</span><span class="sxs-lookup"><span data-stu-id="514d0-211">9</span></span> |<span data-ttu-id="514d0-212">6</span><span class="sxs-lookup"><span data-stu-id="514d0-212">6</span></span> |<span data-ttu-id="514d0-213">100</span><span class="sxs-lookup"><span data-stu-id="514d0-213">100</span></span> |

<span data-ttu-id="514d0-214">Dados de métricas minuto neste exemplo, a chave de partição Olá utiliza a hora de Olá na resolução minuto.</span><span class="sxs-lookup"><span data-stu-id="514d0-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="514d0-215">chave de linha de Olá identifica o tipo de Olá de informações que são armazenadas na linha de Olá e isto é composto por duas partes de informações, o tipo de acesso de Olá e o tipo de pedido de Olá:</span><span class="sxs-lookup"><span data-stu-id="514d0-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="514d0-216">tipo de acesso de Olá é utilizador ou sistema, onde o utilizador refere-se o serviço de armazenamento do tooall utilizador pedidos toohello e sistema refere-se toorequests graças à análise de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="514d0-217">tipo de pedido de Olá é tudo caso em que é uma linha de resumo, ou identifica Olá API específica, como QueryEntity ou UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="514d0-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="514d0-218">dados de exemplo de Olá acima mostra que todos os Olá regista para um único minuto (começando às 11:00), por isso, Olá número de pedidos de QueryEntities plus hello número de pedidos de QueryEntity mais o número de Olá de pedidos de UpdateEntity adicionados até tooseven, que é Olá total apresentado no linha de utilizador: All Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="514d0-219">Da mesma forma, podem derivar Olá latência média de ponto a ponto 104.4286 na linha de utilizador: All Olá calculando ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="514d0-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="514d0-220">Alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="514d0-220">Metrics alerts</span></span>
<span data-ttu-id="514d0-221">Deve considerar como configurar alertas no Olá [portal do Azure](https://portal.azure.com) para as métricas do Storage pode automaticamente notificá-lo de alterações importantes no comportamento de Olá dos seus serviços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="514d0-222">Se utilizar um toodownload de ferramenta do Explorador de armazenamento estes dados de métricas num formato delimitado, pode utilizar os dados do Microsoft Excel tooanalyze Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="514d0-223">Consulte [ferramentas de cliente de armazenamento do Azure](storage-explorers.md) para obter uma lista das ferramentas do Explorador de armazenamento disponível.</span><span class="sxs-lookup"><span data-stu-id="514d0-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="514d0-224">Pode configurar alertas no Olá **regras de alerta** painel, acessível com **monitorização** no painel de menu da conta de armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="514d0-225">Pode haver um atraso entre um evento de armazenamento e quando é registada Olá correspondente dados de métricas de hora a hora ou minuto.</span><span class="sxs-lookup"><span data-stu-id="514d0-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="514d0-226">No caso de Olá das métricas minutos, vários minutos de dados podem ser escritos em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="514d0-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="514d0-227">Isto pode levar tootransactions de minutos anteriores a ser agregados numa transação Olá para Olá minuto atual.</span><span class="sxs-lookup"><span data-stu-id="514d0-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="514d0-228">Quando isto acontecer, o alerta de Olá serviço pode não ter todos os dados de métricas disponíveis para Olá configurado intervalo de alerta, que pode levar tooalerts acionando inesperadamente.</span><span class="sxs-lookup"><span data-stu-id="514d0-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="514d0-229">Aceder aos dados de métricas programaticamente</span><span class="sxs-lookup"><span data-stu-id="514d0-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="514d0-230">Olá listagem seguinte mostra c# código de exemplo que acede ao métricas de minuto Olá para um intervalo de minutos e apresenta os resultados de Olá numa janela de consola.</span><span class="sxs-lookup"><span data-stu-id="514d0-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="514d0-231">Utiliza Olá biblioteca de armazenamento do Azure versão 4, que inclui Olá CloudAnalyticsClient classe que simplifica a tabelas de métricas de Olá ao aceder no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="514d0-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="514d0-232">Cobra o que pode implicar ao ativar as métricas do storage?</span><span class="sxs-lookup"><span data-stu-id="514d0-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="514d0-233">Escreva as entidades da tabela de toocreate pedidos com base nas métricas são cobradas às operações de armazenamento do Azure Olá taxas padrão tooall aplicável.</span><span class="sxs-lookup"><span data-stu-id="514d0-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="514d0-234">Pedidos de leitura e eliminar por um toometrics de dados de cliente também são facturável às taxas padrão.</span><span class="sxs-lookup"><span data-stu-id="514d0-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="514d0-235">Se tiver configurado uma política de retenção de dados, não lhe serem cobrados ao Storage do Azure elimina dados antigos de métricas.</span><span class="sxs-lookup"><span data-stu-id="514d0-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="514d0-236">No entanto, se eliminar dados de análise, a sua conta é cobrada para operações de eliminação de Olá.</span><span class="sxs-lookup"><span data-stu-id="514d0-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="514d0-237">capacidade de Olá utilizada pelo tabelas de métricas de Olá também é facturável: pode utilizar Olá quantidade de Olá tooestimate utilizada para armazenar dados de métricas de capacidade de os seguintes:</span><span class="sxs-lookup"><span data-stu-id="514d0-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="514d0-238">Se a cada hora um serviço utiliza a cada API em cada serviço, aproximadamente 148KB de dados é armazenado nas tabelas de transação Olá métricas a cada hora se tiver ativado o serviço e o nível da API resumo.</span><span class="sxs-lookup"><span data-stu-id="514d0-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="514d0-239">Se a cada hora um serviço utiliza a cada API em cada serviço, aproximadamente 12KB de dados é armazenado nas tabelas de transação Olá métricas a cada hora se tiver ativado apenas nível de serviço resumo.</span><span class="sxs-lookup"><span data-stu-id="514d0-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="514d0-240">Olá tabela de capacidade para os blobs tem duas linhas adicionadas por dia (fornecidos pelo utilizador foi optada ativamente por participar para os registos): Isto implica que cada tamanho de Olá dia desta tabela aumenta em segurança tooapproximately 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="514d0-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="514d0-241">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="514d0-241">Next steps</span></span>
[<span data-ttu-id="514d0-242">Ativar o armazenamento de registo e aceder aos dados de registo</span><span class="sxs-lookup"><span data-stu-id="514d0-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
