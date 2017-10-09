---
title: "análise de aaaUsage para aplicações web com o Azure Application Insights | Documentos da Microsoft"
description: "Compreenda os seus utilizadores e o que fazer com a sua aplicação web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Análise da utilização de aplicações web com o Application Insights

As funcionalidades da sua aplicação web são mais populares? Os seus utilizadores alcançar os seus objetivos com a sua aplicação? De remover estes em determinado pontos e volte mais tarde?  [Azure Application Insights](app-insights-overview.md) ajuda-o a obter informações acerca poderosas como as pessoas utilizam a sua aplicação web. Sempre que atualizar a sua aplicação, pode avaliar o quão bem funciona para os utilizadores. Com este conhecimento, pode efetuar dados orientada por tomar decisões sobre a sua próximas ciclos de desenvolvimento.

## <a name="send-telemetry-from-your-app"></a>Enviar a telemetria da sua aplicação

melhor experiência de Olá é obtida pela instalação do Application Insights no seu código de servidor de aplicação tanto nas suas páginas web. os componentes de cliente e servidor Olá da sua aplicação enviam telemetria back toohello portal do Azure para análise.

1. **Código do servidor:** instalar módulo adequado de Olá para o seu [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), ou [outros](app-insights-platforms.md) aplicação.

    * *Não pretende o código do servidor tooinstall? Apenas [crie um recurso do Azure Application Insights](app-insights-create-new-resource.md).*

2. **Código de página Web:** Olá abra [portal do Azure](https://portal.azure.com), abra o recurso do Application Insights Olá para a sua aplicação e, em seguida, abra **introdução > monitorizar e diagnosticar do lado do cliente**. 

    ![Copie o script Olá para o cabeçalho de Olá da sua página web mestra.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Obter telemetria:** executar o projeto no modo de depuração para alguns minutos e, em seguida, procure os resultados no painel de descrição geral de Olá no Application Insights.

    Publicar a aplicação toomonitor o desempenho da aplicação e saber que os utilizadores estão a fazer com a sua aplicação.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Inclui o ID de utilizador e de sessão na sua telemetria
tootrack utilizadores ao longo do tempo, o Application Insights requer uma forma tooidentify-los. Eventos de Olá ferramenta é Olá única ferramenta de utilização que não requer um ID de utilizador ou um ID de sessão.

Iniciar o envio destes IDs [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Explorar demografia de utilização e estatísticas
Determinar quando as pessoas utilizam a sua aplicação, as páginas que está a mais interessados, onde estão localizados os seus utilizadores, que sistemas operativos e browsers utilizam. 

relatórios de utilizadores e sessões Olá filtre os dados por páginas ou eventos personalizados e segmentá-los por propriedades, tais como a localização e o ambiente e página. Também pode adicionar os seus próprios filtros.

![Utilizadores](./media/app-insights-usage-overview/users.png)  

Conhecimentos aprofundados acerca do Olá direita realçar padrões interessantes no conjunto de Olá de dados.  

* Olá **utilizadores** relatório conta números de Olá de utilizadores exclusivos que aceder às suas páginas na sua períodos de tempo escolhido. (Os utilizadores são contados através da utilização de cookies. Se alguém acede ao seu site com as máquinas de cliente ou browsers diferentes ou limpa os cookies, em seguida, estes serão contados tendo mais do que uma vez.)
* Olá **sessões** relatório conta o número de Olá de sessões de utilizador aceder ao site. Uma sessão é um período de atividade por um utilizador, terminada por um período de inatividade de mais de metade uma hora.

[Mais sobre as ferramentas de utilizadores, sessões e os eventos de Olá](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Vistas de página

No painel de utilização de Olá, clicar Olá vistas de página mosaico tooget uma análise detalhada das suas páginas mais populares:

![No painel de descrição geral de Olá, clique em Olá gráfico de vistas de página](./media/app-insights-usage-overview/05-games.png)

exemplo de Olá acima é de um web site de jogos. De gráficos Olá, pode de forma instantânea, vemos:

* Utilização não melhoradas no Olá na última semana. Talvez é necessário pensar sobre a otimização de motor de pesquisa?
* Tennis é Olá página de jogos mais popular. Vamos concentrar-se na página de toothis mais melhoramentos.
* Em média, visitados a página de Tennis Olá sobre três vezes por semana. (Existem mais de cerca de três vezes sessões que os utilizadores.)
* A maioria dos utilizadores visitam o site de Olá durante a semana do Olá E.U.A. trabalhar e, em horas de trabalho. Talvez deve fornecemos um botão "Ocultar rápido" na página web que Olá.
* Olá [anotações](app-insights-annotations.md) no gráfico de Olá mostrar quando novas versões do Web site de Olá foram implementadas. Nenhuma das implementações recente Olá tinha um efeito considerável na utilização.

E se pretende que tooinvestigate Olá tráfego tooyour site em mais detalhe, como dividir por uma propriedade personalizada, que o site envia na sua telemetria de visualizações de página?

1. Abra Olá **eventos** ferramenta no menu de recurso do Application Insights Olá. Esta ferramenta permite-lhe analisar quantos vistas de página e eventos personalizados foram enviados da sua aplicação, com base numa variedade de opções de filtragem, cohorting e segmentação.
2. Na lista pendente "Quem utilizada" Olá, selecione "Qualquer vista de página".
3. Na lista pendente de "Dividir por" Olá, selecione uma propriedade pela qual toosplit sua página de ver a telemetria.

## <a name="retention---how-many-users-come-back"></a>Retenção - quantos utilizadores voltar?

Retenção ajuda-o a compreender com que frequência os seus utilizadores devolvem toouse as respetivas aplicações, com base no cohorts de utilizadores que efetuar qualquer ação do negócio durante um determinado registo de tempo. 

- Compreender as funcionalidades específicas fazer com que os utilizadores toocome back mais do que outras pessoas 
- Hypotheses de formulário com base nos dados de utilizador reais 
- Determinar se o período de retenção é um problema no seu produto 

![Retenção](./media/app-insights-usage-overview/retention.png) 

controlos de retenção de Olá na parte superior permitem toodefine eventos específicos e retenção de toocalculate de intervalo de tempo. Olá gráfico no meio de Olá proporciona uma representação visual de Olá percentagem de retenção global por Olá intervalo de tempo especificado. gráfico Olá na parte inferior de Olá representa retenção individual num determinado período de tempo. Este nível de detalhe permite-lhe toounderstand que os utilizadores estão a fazer e o que poderá afetar devolvidos utilizadores uma granularidade mais detalhada.  

[Mais informações sobre a ferramenta de retenção de Olá](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Eventos de negócio personalizado

tooget uma compreensão clara dos que os utilizadores não com a sua aplicação web, é útil tooinsert linhas de eventos do código toolog personalizados. Estes eventos podem controlar tudo de ações de utilizador de detalhado como clicar botões específicos, eventos de negócio significativas toomore como efetuar uma compra ou prevalecente um jogo. 

Embora em alguns casos, as vistas de página podem representar eventos úteis, não se encontra verdadeiro em geral. Um utilizador pode abrir uma página de produto, sem comprar produto Olá. 

Com eventos empresariais específicos, pode gráfico progresso dos seus utilizadores através do seu site. Pode saber as respetivas preferências para diferentes opções e em que o se remover out ou tem dificuldades. Com este conhecimento, pode efetuar decisões informadas sobre prioridades Olá no seu registo de segurança de desenvolvimento.

Eventos podem ser registados no Olá web página:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

Ou, no lado do servidor de Olá da aplicação web de Olá:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

Pode anexar eventos de toothese de valores de propriedade, para que possa filtrar ou dividir eventos Olá quando inspecioná-las no portal de Olá. Além disso, um conjunto de propriedades padrão é evento tooeach anexado, por exemplo, o ID de utilizador anónimo, que permite a sequência de Olá tootrace das atividades de um utilizador individual.

Saiba mais sobre [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) e [propriedades](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Eventos dividem e organizam

Nas ferramentas de utilizadores, sessões e os eventos de Olá, pode segmentação e decomposição de eventos personalizados por utilizador, o nome de evento e propriedades.
![Utilizadores](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Design Olá telemetria com aplicação Olá

Ao conceber a cada funcionalidade da sua aplicação, considere como vai toomeasure respetivo êxito com os seus utilizadores. Decida qual iniciar eventos empresariais precisam toorecord e code Olá chamadas para esses eventos de controlo na sua aplicação de Olá.

## <a name="a--b-testing"></a>A | Testar B
Se não souber que a variante de uma funcionalidade que será mais bem sucedida, versão ambas, efetuar cada utilizadores toodifferent acessível. Medir o sucesso de Olá de cada e, em seguida, mova versão unificada tooa.

Para esta técnica, anexar telemetria Olá de tooall de valores de propriedade de diferentes que é enviada por cada versão da sua aplicação. Pode fazê-lo ao definir propriedades na Olá TelemetryContext Active Directory. Estas propriedades predefinidas são adicionadas a mensagem de telemetria de tooevery Olá a aplicação envia - não apenas a mensagens personalizadas, mas Olá padrão telemetria bem.

No portal do Application Insights Olá, filtrar e dividir os dados nos valores de propriedade Olá, assim como versões diferentes do toocompare Olá.

toodo, [configurar um inicializador de telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

No inicializador de aplicação de web de Olá, tais como Global.asax.cs:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

Todos os TelemetryClients novo adicionam automaticamente a especificar o valor da propriedade Olá. Eventos de telemetria individuais podem substituir os valores predefinidos de Olá.

## <a name="next-steps"></a>Passos seguintes
   - [Utilizadores, Sessões, Eventos](app-insights-usage-segmentation.md)
   - [Funis](usage-funnels.md)
   - [Retenção](app-insights-usage-retention.md)
   - [Fluxos do Utilizador](app-insights-usage-flows.md)
   - [Livros](app-insights-usage-workbooks.md)
   - [Adicionar o contexto de utilizador](app-insights-usage-send-user-context.md)
