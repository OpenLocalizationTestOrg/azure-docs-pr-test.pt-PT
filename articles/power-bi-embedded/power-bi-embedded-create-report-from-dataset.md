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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Criar um novo relatório a partir de um conjunto de dados no Power BI Embedded

Relatórios de Power BI Embedded agora podem ser criados a partir de um conjunto de dados na sua própria aplicação. 

Olá método de autenticação é semelhante incorporar toothat do relatório. Se basear em tokens de acesso que são específicas tooa conjunto de dados. Tokens utilizados para PowerBI.com são emitidos pelo Azure Active Directory (AAD) e o Power BI Embedded tokens emitidos pelo seu próprio serviço.

Quando createing um relatório incorporados, hello são tokens emitidos para um conjunto de dados específico. Tokens devem ser associados com Olá incorporar URL Olá mesmo elemento tooensure, cada tem um token exclusivo. Na ordem toocreate um relatório incorporados, *Dataset.Read e Workspace.Report.Create* âmbitos tem de ser fornecidos no token de acesso de Olá.

## <a name="create-access-token-needed-toocreate-new-report"></a>Criar novo relatório do acesso token toocreate necessários

Step-by-Power BI Embedded utilizam de token de incorporação que HMAC iniciada JSON Web Tokens. tokens de Olá são assinados com a chave de acesso de Olá da sua coleção de área de trabalho Azure Power BI Embedded. Incorpore tokens, por predefinição, são utilizado tooprovide ler apenas acesso tooa relatório tooembed numa aplicação. Incorpore tokens emitidos para um relatório específico e deve estar associados um URL de incorporação.

Tokens de acesso devem ser criados no servidor de Olá como chaves de acesso de Olá são tokens de Olá toosign/encriptar utilizados. Para obter informações sobre como toocreate um token de acesso, consulte [Authenticating e autorização com Power BI Embedded](power-bi-embedded-app-token-flow.md). Também pode rever Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método. Eis um exemplo de como isto iria aspeto utilizando Olá .NET SDK para o Power BI.

Neste exemplo, temos de id nosso conjunto de dados que pretendemos novo relatório do toocreat Olá no. É também necessário âmbitos de Olá tooadd para *Dataset.Read e Workspace.Report.Create*.

Olá *PowerBIToken classe* necessita da instalação Olá [pacote do Power BI Core NuGut](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalação de pacotes NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Código c#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Criar um novo relatório em branco

Ordem toocreate um novo relatório, Olá criar configuração deve ser fornecida. Isto deve incluir o token de acesso de Olá, Olá embedURL e Olá datasetID que queremos relatório de Olá toocreate contra. Isto requer que instalar nuget Olá [pacote do Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Olá embedUrl apenas será https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Pode utilizar Olá [exemplo de incorporar o relatório de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidade. Também fornece exemplos de código para operações de diferentes Olá que estão disponíveis.

**Instalação de pacotes NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Código JavaScript**

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

Chamar *powerbi.createReport()* fará com que uma tela em branco no modo de edição aparecem dentro de Olá *div* elemento.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Guardar os novos relatórios

relatório de Olá não serão realmente criado até chamar Olá **guardar como** operação. Isto pode ser feito a partir do menu de ficheiro ou de JavaScript.

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
> É criado um novo relatório apenas após **guardar como** é chamado. Depois de guardar, tela Olá mostrará ainda Olá conjunto de dados no relatório de modo e não Olá de edição. Precisa de novo relatório do tooreload Olá, tal como faria com qualquer outro tipo de relatório.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Carga Olá novo relatório

Toointeract de ordem com o novo relatório de Olá precisa de tooembed incorporá-lo na Olá mesma forma que aplicação Olá o atacante incorpora um relatório regular, significado, um novo token tem de ser emitida especificamente para Olá novo relatório e, em seguida, Olá de chamada de método.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Automatizar guardar e carregar de um novo relatório utilizando Olá "guardada" eventos

No processo de Olá tooautomate ordem de "Guardar como" e, em seguida, ao carregar o novo relatório de Olá pode tornar a utilização de Olá "Guardar" eventos. Este evento é desencadeado quando Olá operação de gravação e devolve um objeto Json que contém reportId novo Olá, o nome do relatório, reportId antigo Olá (se tiver ocorrido um) e se a operação de Olá foi saveAs ou guardar.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

processo de Olá tooAutomate pode escutar eventos Olá "guardada", tome reportId novo Olá, criar o novo token de Olá e incorporar relatório novo Olá com o mesmo.

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

## <a name="see-also"></a>Consultar também

[Introdução com exemplo](power-bi-embedded-get-started-sample.md)  
[Guardar relatórios](power-bi-embedded-save-reports.md)  
[Incorporar um relatório](power-bi-embedded-embed-report.md)  
[Autenticação e autorização no Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemplo de Incorporação de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Pacote de NuGut do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Pacote do Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Mais perguntas? [Tente Olá da Comunidade do Power BI](http://community.powerbi.com/)
