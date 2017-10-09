---
title: "aaaSeparating a telemetria de desenvolvimento, teste e da versão no Azure Application Insights | Microsoft Docs"
description: "Recursos de toodifferent telemetria direto para os carimbos de desenvolvimento, teste e produção."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Separação de telemetria de desenvolvimento, teste e produção

Quando estiver a desenvolver versão seguinte do Olá de uma aplicação web, que não pretende toomix segurança Olá [Application Insights](app-insights-overview.md) telemetria da nova versão de Olá e a versão de Olá já foi libertado. tooavoid confusão, envie a telemetria de Olá de desenvolvimento diferentes prepara tooseparate recursos do Application Insights, com chaves de instrumentação separados (ikeys). toomake-lo mais fácil toochange de chave de instrumentação de Olá como uma versão move de uma fase tooanother, pode ser útil tooset Olá ikey no código em vez de no ficheiro de configuração de Olá. 

(Se o sistema é um serviço de nuvem do Azure, há [outro método de configuração separadas ikeys](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Sobre recursos e chaves de instrumentação

Quando configurar a monitorização do Application Insights para a sua aplicação web, cria um Application Insights *recursos* no Microsoft Azure. Abrir este recurso no portal do Azure na ordem toosee de Olá e analisar telemetria Olá recolhida da sua aplicação. recurso de Olá é identificado por um *chave de instrumentação* (ikey). Quando instala Olá toomonitor de pacote de Application Insights, a aplicação, pode configurá-lo com a chave de instrumentação Olá, para que o se sabe onde toosend Olá telemetria.

Normalmente, escolher recursos separados toouse ou um único recurso partilhado diferentes cenários:

* Aplicações diferentes, independentes - utilize um recurso individual e ikey para cada aplicação.
* Utilizar vários componentes ou funções da aplicação de um negócio - um [único recurso partilhado](app-insights-monitor-multi-role-apps.md) para Olá todos os componentes de aplicações. Pode ser filtrada ou segmentada pela propriedade de cloud_RoleName Olá a telemetria.
* Desenvolvimento, teste e versão - utilizam um recurso individual e ikey para versões do sistema de Olá 'Carimbo' ou a fase de produção.
* A | Testar B - utilizar um único recurso. Crie um tooadd TelemetryInitializer telemetria de toohello uma propriedade que identifica variantes Olá.


## <a name="dynamic-ikey"></a>Chave de instrumentação dinâmica

toomake facilitam toochange Olá ikey como código de Olá move entre fases de produção, defini-lo no código em vez de no ficheiro de configuração de Olá.

Defina a chave de Olá um método de inicialização, tais como global.aspx.cs num serviço ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

Neste exemplo, Olá ikeys para recursos diferentes Olá são colocadas em diferentes versões do ficheiro de configuração web Olá. Trocar Olá ficheiro de configuração web - que pode fazê-lo como parte do script de libertação de Olá - será trocar o recurso de destino Olá.

### <a name="web-pages"></a>Páginas Web
Olá iKey também é utilizado na web páginas sua aplicação, Olá [script que recebeu do painel de início rápido Olá](app-insights-javascript.md). Em vez de codificação-literalmente no script de Olá, gerá-la a partir do Estado do servidor Olá. Por exemplo, numa aplicação ASP.NET:

*JavaScript em Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Criar recursos adicionais do Application Insights
telemetria de tooseparate para os componentes da aplicação diferente ou para diferentes carimbos de data / (dev/teste/produção) de Olá mesmo componente, então poderá terá toocreate um novo recurso do Application Insights.

No Olá [portal.azure.com](https://portal.azure.com), adicione um recurso do Application Insights:

![Clicar em Novo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* **Tipo de aplicação** afeta o que vê no painel de descrição geral de Olá e propriedades de Olá disponíveis no [explorer métrica](app-insights-metrics-explorer.md). Se não vir o seu tipo de aplicação, escolha um dos tipos de web de Olá para páginas web.
* **Grupo de recursos** está para efeitos práticos para a gestão de propriedades, como [controlo de acesso](app-insights-resources-roles-access-control.md). Pode utilizar grupos de recursos separado para o desenvolvimento, teste e produção.
* **Subscrição** é a sua conta de pagamento no Azure.
* **Localização** é onde iremos manter os seus dados. Atualmente não pode ser alterada. 
* **Adicionar toodashboard** coloca um mosaico de acesso de leitura rápida para o seu recurso na sua página de home page do Azure. 

Criar recurso Olá demora alguns segundos. Verá um alerta quando terminar.

(Pode escrever um [script do PowerShell](app-insights-powershell-script-create-resource.md) toocreate um recurso automaticamente.)

### <a name="getting-hello-instrumentation-key"></a>Obter a chave de instrumentação Olá
chave de instrumentação Olá identifica recursos de Olá que criou. 

![Clique em Essentials, clique em Olá chave de instrumentação, CTRL + C](./media/app-insights-separate-resources/02-props.png)

Precisa de chaves de instrumentação Olá de todos os toowhich de recursos de Olá a aplicação irá enviar dados.

## <a name="filter-on-build-number"></a>Filtrar por número de compilação
Quando publica uma nova versão da sua aplicação, poderá ser útil toobe telemetria de Olá tooseparate capaz de diferentes compilações.

Pode definir a propriedade de versão da aplicação de Olá, de modo a que pode filtrar [pesquisa](app-insights-diagnostic-search.md) e [explorer métrica](app-insights-metrics-explorer.md) resultados.

![Uma propriedade de filtragem](./media/app-insights-separate-resources/050-filter.png)

Existem vários métodos diferentes da definição da propriedade Olá versão da aplicação.

* Defina diretamente:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Moldar essa linha num [inicializador de telemetria](app-insights-api-custom-events-metrics.md#defaults) tooensure que todas as instâncias de TelemetryClient estão definidas de forma consistente.
* [ASP.NET] Definir Olá versão no `BuildInfo.config`. o módulo Olá web selecionará versão Olá a partir do nó de BuildLabel Olá. Incluir este ficheiro no seu projeto e não se esqueça tooset Olá cópia sempre propriedade no Explorador de soluções.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] Gere automaticamente BuildInfo.config no MSBuild. toodo, adicionar alguns linhas tooyour `.csproj` ficheiro:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Isto gera um ficheiro chamado *Nomedoprojeto*. BuildInfo.config. Olá processo de publicação lhe mude o nome tooBuildInfo.config.

    etiqueta de compilação de Olá contém um marcador de posição (AutoGen _) quando criar com o Visual Studio. Mas, quando criadas com MSBuild, este é preenchido com Olá número de versão correta.

    números de versão do MSBuild toogenerate tooallow, definir Olá versão como `1.0.*` no AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Versão e controlo de versão
versão da aplicação Olá tootrack, certifique-se `buildinfo.config` é gerado pelo processo do motor de compilação da Microsoft. No ficheiro .csproj, adicione:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Quando tem informações de compilação de Olá, adiciona automaticamente o módulo de web do Application Insights Olá **versão da aplicação** como um item de tooevery de propriedade de telemetria. Que lhe permite toofilter por versão ao executar [pesquisas de diagnóstico](app-insights-diagnostic-search.md), ou quando a [explorar métricas](app-insights-metrics-explorer.md).

No entanto, tenha em atenção que o número de versão de compilação Olá é gerado apenas pelo Olá Microsoft criar motor não pelo programador Olá compilar no Visual Studio.

### <a name="release-annotations"></a>Anotações da versão
Se utilizar o Visual Studio Team Services, pode [obter um marcador de anotação](app-insights-annotations.md) adicionado tooyour gráficos sempre que a versão uma nova versão. Olá imagem a seguir mostra como esta marcador é apresentada.

![Captura de ecrã de um exemplo de anotação de versão num gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Passos seguintes

* [Recursos partilhados de várias funções](app-insights-monitor-multi-role-apps.md)
* [Criar um toodistinguish de inicializador de telemetria A | Variantes B](app-insights-api-filtering-sampling.md#add-properties)
