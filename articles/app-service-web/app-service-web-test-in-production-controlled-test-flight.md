---
title: "implementação de aaaFlighting (beta teste) no App Service do Azure"
description: "Saiba como tooflight novas funcionalidades na sua aplicação ou beta testar as atualizações neste tutorial ponto-a-ponto. -Reúne as funcionalidades do serviço de aplicações como publicação contínua, ranhuras, o encaminhamento de tráfego e a integração do Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Implementação de distribuição de pacotes piloto (beta teste) no App Service do Azure
Este tutorial mostra como toodo *implementações de distribuição de pacotes piloto* através da integração Olá diversas capacidades de [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) e [Azure Application Insights](/services/application-insights/).

*Distribuição de pacotes piloto* é um processo de implementação que valida a uma nova funcionalidade ou altere com um número limitado de clientes reais e é um teste principais no cenário de produção. É akin toobeta testar e é por vezes conhecida como "teste controlada voo". Muitas empresas de grandes dimensão com uma presença na web, utilize esta abordagem para obter validação antecipada sobre as atualizações de aplicações na respetiva prática de [desenvolvimento seja ágil](https://en.wikipedia.org/wiki/Agile_software_development). App Service do Azure permite-lhe toointegrate teste em produção com a publicação contínua e Application Insights tooimplement Olá mesmo cenário de DevOps. Vantagens desta abordagem incluem:

* **Obter comentários real *antes* atualizações são publicada tooproduction** -Olá só coisa melhor do que obtenham comentários, assim que a versão é obter comentários antes de a versão. Pode testar as atualizações com o tráfego de utilizador reais e comportamentos antecipadamente que desejar no ciclo de vida do produto Olá.
* **Melhorar [desenvolvimento contínuo condicionada no teste (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - através da integração teste em produção com a integração contínua e instrumentação com o Application Insights, validação de utilizador acontece numa fase inicial e automaticamente no seu ciclo de vida do produto. Isto ajuda a reduzir os investimentos de tempo na execução do teste manual.
* **Otimizar o fluxo de trabalho de teste** -ao automatizar teste em produção com instrumentação de monitorização contínua, pode potencialmente realizar objetivos Olá dos vários tipos de testes num único processo, tal como [integração](https://en.wikipedia.org/wiki/Integration_testing), [regressão](https://en.wikipedia.org/wiki/Regression_testing), [usabilidade](https://en.wikipedia.org/wiki/Usability_testing), acessibilidade, localização, [desempenho](https://en.wikipedia.org/wiki/Software_performance_testing), [segurança](https://en.wikipedia.org/wiki/Security_testing), e [ aceitação](https://en.wikipedia.org/wiki/Acceptance_testing).

Não é de uma implementação flighting encaminhamento praticamente tráfego em direto. Neste tipo de implementação que pretende toogain insight mais rapidamente possível, se este ser um erro inesperado, degradação do desempenho, problemas de experiência de utilizador. Lembre-se de que estão a lidar com os clientes reais. Por isso, toodo-lo à direita, tem de se certificar que configurou o toogather implementação flighting todos os dados de Olá que necessita na ordem toomake uma decisão informada para o próximo passo. Este tutorial mostra como toocollect dados com o Application Insights, mas podem utilizar New Relic ou outras tecnologias que se adequa aos seus cenário.

## <a name="what-you-will-do"></a>O que irá fazer
Neste tutorial, ficará a saber como toobring Olá, os seguintes cenários de tootest em conjunto, a aplicação de serviço de aplicações na produção:

* [Encaminhar o tráfego de produção](app-service-web-test-in-production-get-start.md) tooyour beta aplicação
* [Instrumente a sua aplicação](../application-insights/app-insights-web-track-usage.md) métricas úteis tooobtain
* Continuamente implementar a sua aplicação beta e monitorizar as métricas da aplicação em direto
* Métricas de comparação entre Olá aplicação de produção e Olá beta aplicação toosee como alterações de código traduzir tooresults

## <a name="what-you-will-need"></a>O que precisa
* Uma conta do Azure
* A [GitHub](https://github.com/) conta
* Visual Studio 2015 - pode transferir Olá [edição Community](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Shell do Git (instalado com [GitHub para Windows](https://windows.github.com/))-permite toorun ambos os comandos de Git e PowerShell Olá no Olá mesma sessão
* Mais recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits
* Compreensão básica do seguinte Olá:
  * [O Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) implementação do modelo (consulte [implementar uma aplicação complexa previsibilidade no Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Precisa de uma conta do Azure toocomplete neste tutorial:
>
> * Pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -receberá créditos pode utilizar tootry saída paga serviços do Azure e, mesmo depois cópias de segurança, pode manter Olá conta e utilizar serviços gratuitos do Azure, tais como Web Apps.
> * Pode [ativar os benefícios de subscritor do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -o Visual Studio subscrição dá-lhe créditos todos os meses que pode utilizar para serviços pagos do Azure.
>
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
>
>

## <a name="set-up-your-production-web-app"></a>Configurar a sua aplicação web de produção
> [!NOTE]
> script de Olá utilizado neste tutorial automaticamente irá configurar a publicação contínua do seu repositório do GitHub. Isto requer que as suas credenciais de GitHub já são armazenados no Azure, caso contrário, a implementação de Olá convertidos em script falhará quando tentar tooconfigure definições de controlo de origem para aplicações web de Olá.
>
> toostore o GitHub credenciais no Azure, criar uma aplicação web no Olá [Portal do Azure](https://portal.azure.com/) e [configurar a implementação de GitHub](app-service-continuous-deployment.md). Basta toodo numa vez.
>
>

Um cenário típico de DevOps, que tem uma aplicação que está em execução no Azure e pretender toomake alterações tooit através da publicação contínua. Neste cenário, irá implementar tooproduction um modelo que tenha desenvolvidas e testado.

1. Criar a suas próprias bifurcação de Olá [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositório. Para obter informações sobre como criar o repositório de cópia, consulte [Bifurcar um repositório](https://help.github.com/articles/fork-a-repo/). Assim que o repositório de cópia for criado, pode vê-lo no seu browser.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Abra uma sessão de Shell de Git. Se ainda não tiver a Shell de Git, instale [GitHub para Windows](https://windows.github.com/) agora.
3. Crie um clone local da sua bifurcação executando Olá os seguintes comandos:

     Git clone https://github.com/<your_fork>/ToDoApp.git
4. Assim que tiver o clone local, navegue até demasiado*&lt;repository_root >*\ARMTemplates e execução Olá deploy.ps1 script com um sufixo exclusivo, como mostrado abaixo:

     .\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix >
5. Quando lhe for pedido, o tipo de Olá pretendido nome de utilizador e palavra-passe para acesso de base de dados. Lembre-se de que as credenciais da base de dados porque precisa de toospecify-las novamente quando a atualização Olá grupo de recursos.

   Deverá ver Olá aprovisionamento progresso de vários recursos do Azure. Quando tiver concluído a implementação, o script de Olá iniciar aplicação Olá no browser Olá e dão-lhe um beep amigável.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Novamente na sua sessão do Git Shell, execute:

     . \swap – nome ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Quando o script de Olá é concluída, volte atrás endereço do toobrowse toohello front-end (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) aplicações de Olá toosee em execução na produção.
8. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/) e observe o que é criado.

   Deve ser capaz de toosee dois web apps no Olá mesmo grupo de recursos, uma com Olá `Api` sufixo no nome de Olá. Se observar a vista de grupo de recursos de Olá, também verá Olá base de dados do SQL Server e servidor, Olá plano do App Service e ranhuras de teste de Olá para aplicações web de Olá. Procurar através de recursos diferentes Olá e compará-los com  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json como estão configuradas no modelo de Olá.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Configurou a aplicação de produção Olá.  Agora, Vamos imaginar que receber comentários que a facilidade de utilização é fraca para a aplicação Olá. Para decidir tooinvestigate. Vai tooinstrument toogive sua aplicação, comentários.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Investigar: Instrumente a sua aplicação de cliente de monitorização/com base nas métricas
1. Abra  *&lt;repository_root >*\src\MultiChannelToDo.sln no Visual Studio.
2. Restaurar todos os pacotes de Nuget clicando solução > **gerir pacotes NuGet para solução** > **restaurar**.
3. Clique com botão direito **MultiChannelToDo.Web** > **adicionar telemetria do Application Insights** > **configurar definições de** > grupo de recursos de alteração tooToDoApp*&lt;your_suffix >* > **tooProject de adicionar o Application Insights**.
4. No Portal do Azure Olá, abra o painel Olá Olá **MultiChannelToDo.Web** recurso do Application Insight. Em seguida, no Olá **estado de funcionamento da aplicação** parte, clique em **saber como a página de browser toocollect carregar dados** > copiar o código.
5. Adicionar Olá copiados código de instrumentação JS demasiado*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, imediatamente antes de fecho de Olá `<heading>` etiquetas. Esta deve conter a chave de instrumentação exclusivo de Olá do seu recurso do Application Insight.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Envie eventos personalizados tooApplication Insights para cliques do rato adicionando Olá parte inferior do toohello de código do corpo os seguintes:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Este fragmento do JavaScript envia um evento personalizado tooApplication Insights sempre que um utilizador clica em qualquer parte na aplicação web de Olá.
7. Na Shell de Git, consolide e emita o repositório de cópia de tooyour alterações no GitHub. Em seguida, aguarde browser toorefresh de clientes.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Comutação Olá implementado tooproduction de alterações de aplicação:

     . \swap – nome ToDoApp < your_suffix >
9. Procure o recurso do Application Insights toohello que configurou. Clique em Personalizar eventos.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Se não vir métricas para eventos personalizados, aguarde alguns minutos e clique em **atualizar**.

Suponha que vê um gráfico, conforme mostrado abaixo:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

E Olá grelha de eventos abaixo do mesmo:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

De acordo com código da aplicação tooyour ToDoApp, Olá **botão** eventos corresponde toohello botão para submeter e Olá **entrada** eventos corresponde toohello caixa de texto. Até ao momento, coisas fazem sentido. No entanto, esta parece não haver uma quantidade boa de cliques e muito poucos cliques nos itens de tarefas Olá (Olá **LI** eventos).

Com base neste, formulário sua hipótese que alguns utilizadores sejam confundido que parte da Olá IU é clicável e porque cursor Olá é escovado para selecção de texto quando se passa em itens de lista de Olá e os respetivos ícones.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Esta situação pode ser um exemplo contrived. Contudo, está a toomake do uma aplicação de tooyour melhoramento e, em seguida, execute um flighting comentários de Facilidade de utilização de tooget de implementação de clientes em direto.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumente a sua aplicação de servidor de monitorização/com base nas métricas
Este é um tangente, uma vez que o cenário de Olá demonstrado neste tutorial apenas lida com a aplicação de cliente Olá. No entanto, por questões de exaustividade, irá configurar aplicação do lado do servidor de Olá.

1. Clique com botão direito **MultiChannelToDo** > **adicionar telemetria do Application Insights** > **configurar definições de** > grupo de recursos de alteração tooToDoApp*&lt;your_suffix >* > **tooProject de adicionar o Application Insights**.
2. Na Shell de Git, consolide e emita o repositório de cópia de tooyour alterações no GitHub. Em seguida, aguarde browser toorefresh de clientes.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Comutação Olá implementado tooproduction de alterações de aplicação:

     . \swap – nome ToDoApp < your_suffix >

Já está!

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Investigar: Adicionar métricas de aplicação de cliente de tooyour etiquetas específicos da ranhura
Nesta secção, irá configurar Olá implementação diferentes ranhuras toosend específicos da ranhura de telemetria toohello mesmo recurso do Application Insights. Desta forma, pode comparar a telemetria de dados entre o tráfego de ranhuras diferente (ambientes de implementação) tooeasily Consulte efeito Olá das alterações de aplicação. AT Olá mesmo tempo, pode a separar o tráfego de produção Olá de rest de Olá para poder continuar toomonitor a aplicação de produção conforme necessário.

Uma vez que está a recolher dados sobre o comportamento do cliente, terá de [adicionar um tooyour de inicializador de telemetria código JavaScript](../application-insights/app-insights-api-filtering-sampling.md) no Index. cshtml. Se pretender que o desempenho do lado do servidor de tootest, por exemplo, também pode fazer da mesma forma no seu código de servidor (consulte [API do Application Insights para as métricas e eventos personalizados](../application-insights/app-insights-api-custom-events-metrics.md).

1. Primeiro, adicione Olá de bewteen Olá código dois `//` comentários abaixo no bloco de JavaScript Olá que adicionou toohello `<heading>` tag anteriormente.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Este código de inicializador faz com que Olá `appInsights` objeto tooadd Olá uma propriedade personalizada denominada `Environment` tooevery peça de telemetria que envia.
2. Em seguida, adicione a propriedade personalizada como um [espaço definição](web-sites-staged-publishing.md#AboutConfiguration) para a sua aplicação web no Azure. toodo, Olá execute os seguintes comandos na sessão do Git Shell.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Olá Web. config no seu projeto já define Olá `environment` definição de aplicação. Com esta definição, quando o testar localmente, a aplicação Olá métricas serão etiquetadas com `VS Debugger`. No entanto, quando enviar o tooAzure de alterações, Azure irá localizar e utilizar Olá `environment` na configuração da aplicação web Olá em vez disso, a definição de aplicação e as métricas serão etiquetadas com `Production`.
3. Consolidar push sua bifurcação de tooyour de alterações de código no GitHub e, em seguida, aguarde que os utilizadores toouse Olá nova aplicação (necessidade toorefresh Olá browser). Demora cerca de 15 minutos para Olá nova propriedade tooshow cópias de segurança no seu Application Insights `MultiChannelToDo.Web` recursos.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Agora, visite toohello **personalizar eventos** painel novamente e filtrar Olá métricas no `Environment=Production`. Agora deve ser capaz de toosee todos os Olá novos eventos personalizados na produção Olá espaço com este filtro.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Clique em Olá **Favoritos** como o botão toosave Olá atual Explorador de métricas definições toosomething **eventos personalizados: produção**. Pode facilmente mudar entre esta vista e uma vista de ranhura de implementação mais tarde.

   > [!TIP]
   > Para a análise ainda mais poderoso, considere [integrar o recurso do Application Insights com o Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Adicione as métricas de aplicação do servidor de tooyour etiquetas específicos da ranhura
Novamente, por questões de exaustividade, irá configurar aplicação do lado do servidor de Olá. Ao contrário Olá as aplicações cliente que estão instrumentada em JavaScript, etiquetas específicos da ranhura de aplicação de servidor Olá está instrumentada com o código de .NET.

1. Abra  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Adicione bloco de código Olá abaixo, imediatamente antes da Olá Fechar chaveta de espaço de nomes.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Corrija os erros de resolução de nomes de Olá adicionando Olá `using` as instruções abaixo toohello início do ficheiro de Olá:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Adicione o código de Olá abaixo início toohello Olá `Application_Start()` método:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Consolidar push sua bifurcação de tooyour de alterações de código no GitHub e, em seguida, aguarde que os utilizadores toouse Olá nova aplicação (necessidade toorefresh Olá browser). Demora cerca de 15 minutos para Olá nova propriedade tooshow cópias de segurança no seu Application Insights `MultiChannelToDo` recursos.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Atualização: Configurar a sua sucursal beta
1. Abra  *&lt;repository_root >*Olá \ARMTemplates\ProdAndStagetest.json e localizar `appsettings` recursos (procure `"name": "appsettings"`). Existem 4 deles, um para cada bloco.
2. Para cada `appsettings` recursos, adicione um `"environment": "[parameters('slotName')]"` final toohello de definição de aplicação de Olá `properties` matriz. Não se esqueça tooend linha anterior de Olá com uma vírgula.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Acabou de adicionar Olá `environment` definição tooall ranhuras Olá no modelo de Olá de aplicação.
3. No mesmo ficheiro de Olá, determinar Olá `slotconfignames` recursos (procure `"name": "slotconfignames"`). Existem 2 deles, um para cada aplicação.
4. Para cada `slotconfignames` recursos, adicione `"environment"` final toohello Olá `appSettingNames` matriz. Não se esqueça tooend linha anterior de Olá com uma vírgula.

    Apenas efetuou Olá `environment` aplicação definição pen tooits respetivos ranhura de implementação para ambas as aplicações.  
5. Na sua sessão do Git Shell, seguinte Olá executar os comandos com Olá mesmo sufixo do grupo de recursos que usou antes.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Quando lhe for pedido, especifique Olá as mesmas credenciais de base de dados do SQL Server como anteriormente. Em seguida, quando lhe for perguntado tooupdate Olá grupo de recursos tipo `Y`, em seguida, `ENTER`.

    Assim que o script de Olá é concluída, todos os recursos no grupo de recursos original Olá são mantidos, mas uma nova ranhura denominada "beta" é criada no mesmo com Olá mesmo configuração como ranhura de "Transição" Olá que foi criada no início de Olá.

   > [!NOTE]
   > Este método de criação de ambientes de implementação diferentes é diferente do método Olá [desenvolvimento de software seja ágil App Service do Azure](app-service-agile-software-development.md). Aqui, pode criar ambientes de implementação com as ranhuras de implementação, onde existe como criar ambientes de implementação com grupos de recursos. Gerir ambientes de implementação com grupos de recursos permite-lhe toodevelopers de ambiente de produção Olá do tookeep off-limits, mas não é fácil toodo na produção, que pode fazê-lo facilmente com ranhuras de teste.
   >
   >

Se assim o desejar, também pode criar uma aplicação alfa executando

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Para este tutorial, que será apenas manter a utilizar a aplicação de beta.

## <a name="update-push-your-updates-toohello-beta-app"></a>Atualização: Push a aplicação de beta toohello atualizações
Criar uma aplicação tooyour que pretende que o tooimprove.

1. Certifique-se de que está agora no seu ramo beta

        git checkout beta
2. No  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, localizar Olá `<li>` assinalar e adicionar Olá `style="cursor:pointer"` atributo, conforme mostrado abaixo.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. Consolide e emita tooAzure.
4. Certifique-se de que a alteração de Olá agora é refletida na ranhura de beta Olá navegando toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Se não vir Olá alterar ainda, atualize o browser tooget Olá novo no código javascript.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Agora que configurou a sua alteração em execução na ranhura de beta Olá, está pronto tooperform uma implementação flighting.

## <a name="validate-route-traffic-toohello-beta-app"></a>Validar: Encaminhar o tráfego toohello beta aplicação
Nesta secção, irá encaminhar tráfego toohello beta aplicação. For sake of efeitos de clareza de demonstração, vai tooroute uma parte significativa de Olá utilizador tráfego tooit. Na realidade, Olá quantidade de tráfego que pretende tooroute dependerá da sua situação específica. Por exemplo, se o site é à escala Olá de microsoft.com, em seguida, poderá ter menos de uma percentagem do tráfego total de dados úteis de toogain de ordem.

1. Na sua sessão do Git Shell, execute Olá os seguintes comandos tooroute metade da ranhura de beta do Olá produção tráfego toohello:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Olá `ReroutePercentage=50` propriedade especifica que a 50% do tráfego de produção Olá será URL da aplicação de beta toohello encaminhadas (especificado pelo Olá `ActionHostName` propriedade).
2. Agora navegar toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% do tráfego de Olá deve ser redirecionada toohello ranhura de beta.
3. No recurso do Application Insights, filtrar as métricas de Olá pelo ambiente = "beta".

   > [!NOTE]
   > Se guardar esta vista filtrada como favorito outro, em seguida, pode facilmente inverte vistas do Explorador de métrica de Olá entre a produção e vistas de beta.
   >
   >

Suponha no Application Insights, verá algo semelhante toohello seguinte:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Não só é isto que mostra que existem muitos cliques mais no Olá `<li>` etiquetas, mas parece toobe com um aumento de cliques nos `<li>` etiquetas. Em seguida, pode concluir que pessoas tenham detetados Olá novo `<li>` etiquetas são clicáveis e são agora limpar todas as suas tarefas anteriormente concluída na aplicação Olá.

Com base nos dados de Olá da sua implementação flighting, decidir que a nova IU está pronta para produção.

## <a name="go-live-move-your-new-code-into-production"></a>Vá em direto: mover o novo código em produção
Está agora pronto toomove tooproduction a atualização. O que é uma grande é que, agora que sabe que a atualização já foi validada *antes* é feita tooproduction. Por isso, agora, pode implementar com confidencialidade-lo. Uma vez que efetuou uma aplicação de cliente do atualização toohello AngularJS, apenas validada código do lado do cliente de Olá. Se as alterações de toomake toohello aplicações de Web API de back-end, foi possível validar as alterações da mesma forma e fácil.

1. Na Shell de Git, remova a regra de encaminhamento de tráfego de Olá executando Olá os seguintes comandos:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Execute os comandos de Git Olá:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Aguarde alguns minutos para Olá novo código toohello toobe implementado ranhura de teste, em seguida, iniciar http://ToDoApp*&lt;your_suffix >*-tooverify staging.azurewebsites.net que Olá nova atualização é preparada no modo de transição de Olá ranhura. Lembre-se de que Olá ramo principal o repositório de cópia é ligado toohello transição ranhura da sua aplicação.
4. Agora, comutação Olá ranhura de teste em produção

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Resumo
App Service do Azure torna mais fácil para empresas pequena toomedium-tamanho tootest as suas aplicações direcionadas para o cliente na produção, algo que tiver sido realizada tradicionalmente em grandes empresas. Hopefully, este tutorial lhe forneceu Olá conhecimento terá toobring em conjunto do serviço de aplicações e o Application Insights toomake distribuição de pacotes piloto implementação possível e mesmo a outros cenários de teste em produção, no seu mundo de DevOps.

## <a name="more-resources"></a>Mais recursos
* [Desenvolvimento de software seja ágil App Service do Azure](app-service-agile-software-development.md)
* [Configurar ambientes para web apps no App Service do Azure de teste](web-sites-staged-publishing.md)
* [Implementar uma aplicação complexa previsibilidade no Azure](app-service-deploy-complex-application-predictably.md)
* [Criação de modelos Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Olá validador JSON](http://jsonlint.com/)
* [A ramificação Git – básico ramificação e intercalação](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Wiki do Kudu projeto](https://github.com/projectkudu/kudu/wiki)
