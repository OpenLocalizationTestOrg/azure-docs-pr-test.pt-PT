---
title: "aaaWindows Phone Silverlight alcançar integração do SDK"
description: "Como tooIntegrate do Azure Mobile Engagement alcançar com aplicações do Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Integração do SDK de alcance do Silverlight do Windows Phone
Tem de seguir o procedimento de integração de Olá descrito em Olá [integração do Windows Phone Silverlight Engagement SDK](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir este guia.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Incorporar Olá SDK alcance do Engagement no seu projeto Windows Phone Silverlight
Não tem nada tooadd. `EngagementReach`as referências e recursos já estão no seu projeto.

> [!TIP]
> Pode personalizar as imagens localizadas em Olá `Resources` pasta do projeto, especialmente Olá marca ícone (que ícone de envolvimento predefinido do toohello).
> 
> 

## <a name="add-hello-capabilities"></a>Adicionar capacidades do Olá
Olá SDK alcance do Engagement tem algumas capacidades adicionais.

Abra o `WMAppManifest.xml` de ficheiros e certifique-se de que Olá seguintes capacidades declarados:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Olá primeiro um é utilizado por Olá MPNS serviço tooallow Olá de apresentação de notificação de alerta. Olá segundo é utilizado tooembed uma tarefa do browser para Olá SDK.

Editar Olá `WMAppManifest.xml` de ficheiros e adicionar dentro Olá `<Capabilities />` etiquetas:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Ativar Olá serviço de notificação Push da Microsoft
No Olá toouse de ordem **serviço de notificação Push da Microsoft** (referido como MPNS) sua `WMAppManifest.xml` ficheiro tem de ter um `<App />` tag com um `Publisher` atributo definido toohello nome do seu projeto.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inicializar Olá SDK alcance do Engagement
### <a name="engagement-configuration"></a>Configuração de envolvimento
configuração de envolvimento Olá é centralizada em Olá `Resources\EngagementConfiguration.xml` ficheiro do seu projeto.

Edite esta configuração de alcance do ficheiro toospecify:

* *Opcional*, indicar se o push nativo do Olá (MPNS) está ativado ou não entre `<enableNativePush>` e `</enableNativePush>` etiquetas, (`true` por predefinição).
* *Opcional*, indicar o nome de Olá do canal de push Olá entre `<channelName>` e `</channelName>` etiquetas, fornecer Olá mesmo que a aplicação pode atualmente utilizar ou deixe em branco.

Se quiser toospecify-la no tempo de execução em vez disso, pode chamar seguinte Olá método antes da inicialização de agente do Engagement Olá:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Pode especificar o nome de Olá do canal de push Olá MPNS da sua aplicação. Por predefinição, o Engagement cria um nome com base no ID da aplicação Olá. Possui sem necessidade de toospecify Olá nome por si, exceto se planear o canal de push de Olá toouse fora o Engagement.
> 
> 

### <a name="engagement-initialization"></a>Inicialização do engagement
Modificar Olá `App.xaml.cs`:

* Adicionar tooyour `using` instruções:
  
      using Microsoft.Azure.Engagement;
* Inserir `EngagementReach.Instance.Init` apenas após `EngagementAgent.Instance.Init` no `Application_Launching` :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Inserir `EngagementReach.Instance.OnActivated` no Olá `Application_Activated` método:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Olá `EngagementReach.Instance.Init` é executado num thread dedicado. Não dispõe de toodo-lo por si.
> 
> 

## <a name="app-store-submission-considerations"></a>Considerações de submissão de arquivo de aplicação
Microsoft impõe algumas regras ao utilizar notificações de push Olá:

De Olá Microsoft [políticas de aplicações] documentação, secção 2.9:

1) Tem de pedir ao hello tooaccept tooreceive push as notificações de utilizador. Em seguida, as definições, adicione notificações de push uma forma toodisable Olá.

objeto de EngagementReach Olá fornece dois métodos toomanage Olá na/optar ativamente por participar-ativamente, `EnableNativePush()` e `DisableNativePush()`. Por exemplo, pode criar uma opção nas definições de Olá com um toodisable Ativar/desativar ou ativar MPNS.

Também pode decidir toodeactivate MPNS através da configuração de envolvimento Olá\<windows phone-sdk-alcance-configuração\>.

> 2.9.1) aplicação Olá primeiro tem de descrever Olá notificações toobe fornecida e **obter hello do express permissão do utilizador (optar ativamente por participar-em)**, e **tem de fornecer um mecanismo através do qual Olá utilizador pode optar ativamente por participar fora de receção notificações push**. Todas as notificações fornecidas a utilizar Olá serviço de notificação Push da Microsoft tem de ser consistentes com o utilizador de toohello Olá descrição fornecida e tem de cumprir todos os aplicável [políticas de aplicações] [ Content Policies]e [requisitos adicionais para tipos de aplicação específica].
> 
> 

2) Não deve utilizar demasiados notificações push. Engagement processará as notificações por si.

> 2.9.2) aplicação Olá e a sua utilização de Olá serviço de notificação Push da Microsoft tem excessivamente não utilizar a capacidade de rede ou de largura de banda de Olá serviço de notificação Push da Microsoft ou caso contrário unduly burden Windows Phone ou outros dispositivos Microsoft ou o serviço excessivo com notificações push, conforme determinado pela Microsoft à sua discrição razoável e não pode prejudicar ou interferir com a quaisquer redes da Microsoft ou servidores ou quaisquer servidores de terceiros ou redes ligados toohello serviço notificação Push da Microsoft.
> 
> 

3) Não dependem das informações do MPNS toosend criticals. Engagement utiliza MPNS, pelo que também se aplica esta regra de campanhas de Olá criadas dentro de Olá o Engagement front-end.

> 2.9.3) Olá serviço de notificação Push da Microsoft não pode ser utilizado toosend notificações que são o missão críticos ou, caso contrário pode afetar é importante de vida ou death, incluindo sem dispositivo médicas do limitação críticas notificações tooa relacionados ou condição. MICROSOFT expressamente exclui quaisquer garantias que Olá utilização de Olá MICROSOFT PUSH notificação serviço ou entrega de MICROSOFT PUSH notificação serviço notificações irá ser interrompido, erro livre, ou caso contrário garantida tooOCCUR ON A em tempo real base.
> 
> 

**Não podemos garantir que a aplicação passará o processo de validação de Olá se não respeitem estas recomendações.**

## <a name="handle-data-push-optional"></a>Processar o push de dados (opcional)
Se pretender que o seu pushes de dados do application toobe tooreceive capaz de alcance, tiver tooimplement dois eventos de Olá EngagementReach classe:

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

Pode ver essa chamada de retorno Olá de cada método de devolve um valor booleano. Engagement envia um comentários tooits back-end após a emissão de push de dados de Olá. Se a chamada de retorno Olá devolve false, Olá `exit` comentários serão envio. Caso contrário, será `action`. Não se for definida nenhum chamada de retorno para eventos de Olá, Olá `drop` comentários serão devolvido tooEngagement.

> [!WARNING]
> Não o engagement é capaz de tooreceive comentários de múltiplos para um push de dados. Se pretender tooset vários processadores um evento, lembre-se de que o comentários de Olá serão correspondem toohello uma última enviada. Neste caso, recomendamos tooalways devolve Olá mesmo tooavoid de valor ter confuso comentários nos Olá front-end.
> 
> 

## <a name="customize-ui-optional"></a>Personalizar IU (opcional)
### <a name="first-step"></a>Primeiro passo
Iremos permitem-lhe alcance de Olá toocustomize IU.

toodo por isso, ter toocreate uma subclasse de Olá `EngagementReachHandler` classe.

**Código de exemplo:**

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

Em seguida, definir o conteúdo de Olá de Olá `EngagementReach.Instance.Handler` campo com o seu objeto personalizado no seu `App.xaml.cs` classe no Olá `Application_Launching` método.

**Código de exemplo:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Por predefinição, o Engagement utiliza a suas próprias implementação `EngagementReachHandler`. Não tem toocreate os seus próprios, e se o fizer, não é necessário toooverride cada método. comportamento predefinido de Olá é o objeto de base do Engagement tooselect Olá.
> 
> 

### <a name="layouts"></a>Esquemas
Por predefinição, o alcance irá utilizar Olá incorporado recursos de notificações do Olá DLL toodisplay Olá e páginas.

No entanto, pode decidir toouse tooreflect os seus próprios recursos sua marca destes componentes.

Pode substituir `EngagementReachHandler` métodos no seu toouse de envolvimento tootell subclasse as esquemas de:

**Código de exemplo:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Olá `CreateNotification` método pode devolver um valor nulo. notificação de Olá não irá ser apresentada e campanhas de alcance Olá serão ignoradas.
> 
> 

toosimplify a implementação de esquema, também fornecemos nosso própria xaml que possa servir como base para o seu código. Onde estão localizados num arquivo de SDK do Engagement Olá (/ src/alcance /).

> [!WARNING]
> origens de Olá que fornecemos são Olá exato mesmo que utilizamos. Por isso, se quiser toomodify-los diretamente, não se esqueça de espaço de nomes do toochange Olá e Olá nome.
> 
> 

### <a name="notification-position"></a>Posição de notificação
Por predefinição, é apresentada uma notificação na aplicação no lado esquerdo de inferior Olá da aplicação Olá. Pode alterar este comportamento através da substituição Olá `GetNotificationPosition` método de Olá `EngagementReachHandler` objeto.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Atualmente, pode escolher entre Olá `BOTTOM` (predefinição) e `TOP` posições.

### <a name="launch-message"></a>Inicie a mensagem
Quando um utilizador clica numa notificação do sistema (um alerta), inicia Engagement Olá aplicação, a carga Olá conteúdo de Olá push mensagens e apresentar a página Olá Olá correspondente campanha.

Não há um atraso entre a execução de Olá da apresentação de aplicação e Olá Olá da página Olá (dependendo da velocidade Olá da sua rede).

utilizador de toohello tooindicate que algo está a carregar, deve fornecer informações de um visual, como uma barra de progresso ou um indicador de progresso. Engagement não consegue processar que ela própria, mas fornece alguns processadores para si.

tooimplement Olá chamada de retorno, efetue:

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Pode definir a chamada de retorno de Olá na sua `Application_Launching` método de sua `App.xaml.cs` ficheiro, preferencialmente, antes de Olá `EngagementReach.Instance.Init()` chamada.

> [!TIP]
> Cada processador é designado por Olá Thread de IU. Não dispõe de tooworry quando utilizar uma MessageBox ou algo relacionadas com a IU.
> 
> 

[políticas de aplicações]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisitos adicionais para tipos de aplicação específica]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

