---
title: "aaaCreate um novo relatório de um conjunto de dados no Azure Power BI Embedded | Microsoft Docs"
description: "Relatórios de Power BI Embedded agora podem ser criados a partir de um conjunto de dados na sua própria aplicação."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="68891-103">Criar um novo relatório a partir de um conjunto de dados no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="68891-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="68891-104">Relatórios de Power BI Embedded agora podem ser criados a partir de um conjunto de dados na sua própria aplicação.</span><span class="sxs-lookup"><span data-stu-id="68891-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="68891-105">Olá método de autenticação é semelhante incorporar toothat do relatório.</span><span class="sxs-lookup"><span data-stu-id="68891-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="68891-106">Se basear em tokens de acesso que são específicas tooa conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="68891-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="68891-107">Tokens utilizados para PowerBI.com são emitidos pelo Azure Active Directory (AAD) e o Power BI Embedded tokens emitidos pelo seu próprio serviço.</span><span class="sxs-lookup"><span data-stu-id="68891-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="68891-108">Quando createing um relatório incorporados, hello são tokens emitidos para um conjunto de dados específico.</span><span class="sxs-lookup"><span data-stu-id="68891-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="68891-109">Tokens devem ser associados com Olá incorporar URL Olá mesmo elemento tooensure, cada tem um token exclusivo.</span><span class="sxs-lookup"><span data-stu-id="68891-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="68891-110">Na ordem toocreate um relatório incorporados, *Dataset.Read e Workspace.Report.Create* âmbitos tem de ser fornecidos no token de acesso de Olá.</span><span class="sxs-lookup"><span data-stu-id="68891-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="68891-111">Criar novo relatório do acesso token toocreate necessários</span><span class="sxs-lookup"><span data-stu-id="68891-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="68891-112">Step-by-Power BI Embedded utilizam de token de incorporação que HMAC iniciada JSON Web Tokens.</span><span class="sxs-lookup"><span data-stu-id="68891-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="68891-113">tokens de Olá são assinados com a chave de acesso de Olá da sua coleção de área de trabalho Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="68891-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="68891-114">Incorpore tokens, por predefinição, são utilizado tooprovide ler apenas acesso tooa relatório tooembed numa aplicação.</span><span class="sxs-lookup"><span data-stu-id="68891-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="68891-115">Incorpore tokens emitidos para um relatório específico e deve estar associados um URL de incorporação.</span><span class="sxs-lookup"><span data-stu-id="68891-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="68891-116">Tokens de acesso devem ser criados no servidor de Olá como chaves de acesso de Olá são tokens de Olá toosign/encriptar utilizados.</span><span class="sxs-lookup"><span data-stu-id="68891-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="68891-117">Para obter informações sobre como toocreate um token de acesso, consulte [Authenticating e autorização com Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="68891-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="68891-118">Também pode rever Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método.</span><span class="sxs-lookup"><span data-stu-id="68891-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="68891-119">Eis um exemplo de como isto iria aspeto utilizando Olá .NET SDK para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="68891-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="68891-120">Neste exemplo, temos de id nosso conjunto de dados que pretendemos novo relatório do toocreat Olá no.</span><span class="sxs-lookup"><span data-stu-id="68891-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="68891-121">É também necessário âmbitos de Olá tooadd para *Dataset.Read e Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="68891-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="68891-122">Olá *PowerBIToken classe* necessita da instalação Olá [pacote do Power BI Core NuGut](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="68891-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="68891-123">**Instalação de pacotes NuGet**</span><span class="sxs-lookup"><span data-stu-id="68891-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="68891-124">**Código c#**</span><span class="sxs-lookup"><span data-stu-id="68891-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="68891-125">Criar um novo relatório em branco</span><span class="sxs-lookup"><span data-stu-id="68891-125">Create a new blank report</span></span>

<span data-ttu-id="68891-126">Ordem toocreate um novo relatório, Olá criar configuração deve ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="68891-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="68891-127">Isto deve incluir o token de acesso de Olá, Olá embedURL e Olá datasetID que queremos relatório de Olá toocreate contra.</span><span class="sxs-lookup"><span data-stu-id="68891-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="68891-128">Isto requer que instalar nuget Olá [pacote do Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="68891-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="68891-129">Olá embedUrl apenas será https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="68891-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="68891-130">Pode utilizar Olá [exemplo de incorporar o relatório de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="68891-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="68891-131">Também fornece exemplos de código para operações de diferentes Olá que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="68891-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="68891-132">**Instalação de pacotes NuGet**</span><span class="sxs-lookup"><span data-stu-id="68891-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="68891-133">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="68891-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="68891-134">Chamar *powerbi.createReport()* fará com que uma tela em branco no modo de edição aparecem dentro de Olá *div* elemento.</span><span class="sxs-lookup"><span data-stu-id="68891-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="68891-135">Guardar os novos relatórios</span><span class="sxs-lookup"><span data-stu-id="68891-135">Save new reports</span></span>

<span data-ttu-id="68891-136">relatório de Olá não serão realmente criado até chamar Olá **guardar como** operação.</span><span class="sxs-lookup"><span data-stu-id="68891-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="68891-137">Isto pode ser feito a partir do menu de ficheiro ou de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="68891-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="68891-138">É criado um novo relatório apenas após **guardar como** é chamado.</span><span class="sxs-lookup"><span data-stu-id="68891-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="68891-139">Depois de guardar, tela Olá mostrará ainda Olá conjunto de dados no relatório de modo e não Olá de edição.</span><span class="sxs-lookup"><span data-stu-id="68891-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="68891-140">Precisa de novo relatório do tooreload Olá, tal como faria com qualquer outro tipo de relatório.</span><span class="sxs-lookup"><span data-stu-id="68891-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="68891-141">Carga Olá novo relatório</span><span class="sxs-lookup"><span data-stu-id="68891-141">Load hello new report</span></span>

<span data-ttu-id="68891-142">Toointeract de ordem com o novo relatório de Olá precisa de tooembed incorporá-lo na Olá mesma forma que aplicação Olá o atacante incorpora um relatório regular, significado, um novo token tem de ser emitida especificamente para Olá novo relatório e, em seguida, Olá de chamada de método.</span><span class="sxs-lookup"><span data-stu-id="68891-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="68891-143">Automatizar guardar e carregar de um novo relatório utilizando Olá "guardada" eventos</span><span class="sxs-lookup"><span data-stu-id="68891-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="68891-144">No processo de Olá tooautomate ordem de "Guardar como" e, em seguida, ao carregar o novo relatório de Olá pode tornar a utilização de Olá "Guardar" eventos.</span><span class="sxs-lookup"><span data-stu-id="68891-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="68891-145">Este evento é desencadeado quando Olá operação de gravação e devolve um objeto Json que contém reportId novo Olá, o nome do relatório, reportId antigo Olá (se tiver ocorrido um) e se a operação de Olá foi saveAs ou guardar.</span><span class="sxs-lookup"><span data-stu-id="68891-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="68891-146">processo de Olá tooAutomate pode escutar eventos Olá "guardada", tome reportId novo Olá, criar o novo token de Olá e incorporar relatório novo Olá com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="68891-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="68891-147">Consultar também</span><span class="sxs-lookup"><span data-stu-id="68891-147">See also</span></span>

[<span data-ttu-id="68891-148">Introdução com exemplo</span><span class="sxs-lookup"><span data-stu-id="68891-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="68891-149">Guardar relatórios</span><span class="sxs-lookup"><span data-stu-id="68891-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="68891-150">Incorporar um relatório</span><span class="sxs-lookup"><span data-stu-id="68891-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="68891-151">Autenticação e autorização no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="68891-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="68891-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="68891-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="68891-153">Exemplo de Incorporação de JavaScript</span><span class="sxs-lookup"><span data-stu-id="68891-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="68891-154">Pacote de NuGut do Power BI Core</span><span class="sxs-lookup"><span data-stu-id="68891-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="68891-155">Pacote do Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="68891-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="68891-156">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="68891-156">More questions?</span></span> [<span data-ttu-id="68891-157">Tente Olá da Comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="68891-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
