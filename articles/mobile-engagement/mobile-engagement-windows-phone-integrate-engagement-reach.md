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
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="30636-103">Integração do SDK de alcance do Silverlight do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="30636-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="30636-104">Tem de seguir o procedimento de integração de Olá descrito em Olá [integração do Windows Phone Silverlight Engagement SDK](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="30636-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="30636-105">Incorporar Olá SDK alcance do Engagement no seu projeto Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="30636-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="30636-106">Não tem nada tooadd.</span><span class="sxs-lookup"><span data-stu-id="30636-106">You do not have anything tooadd.</span></span> <span data-ttu-id="30636-107">`EngagementReach`as referências e recursos já estão no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="30636-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="30636-108">Pode personalizar as imagens localizadas em Olá `Resources` pasta do projeto, especialmente Olá marca ícone (que ícone de envolvimento predefinido do toohello).</span><span class="sxs-lookup"><span data-stu-id="30636-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="30636-109">Adicionar capacidades do Olá</span><span class="sxs-lookup"><span data-stu-id="30636-109">Add hello capabilities</span></span>
<span data-ttu-id="30636-110">Olá SDK alcance do Engagement tem algumas capacidades adicionais.</span><span class="sxs-lookup"><span data-stu-id="30636-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="30636-111">Abra o `WMAppManifest.xml` de ficheiros e certifique-se de que Olá seguintes capacidades declarados:</span><span class="sxs-lookup"><span data-stu-id="30636-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="30636-112">Olá primeiro um é utilizado por Olá MPNS serviço tooallow Olá de apresentação de notificação de alerta.</span><span class="sxs-lookup"><span data-stu-id="30636-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="30636-113">Olá segundo é utilizado tooembed uma tarefa do browser para Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="30636-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="30636-114">Editar Olá `WMAppManifest.xml` de ficheiros e adicionar dentro Olá `<Capabilities />` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="30636-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="30636-115">Ativar Olá serviço de notificação Push da Microsoft</span><span class="sxs-lookup"><span data-stu-id="30636-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="30636-116">No Olá toouse de ordem **serviço de notificação Push da Microsoft** (referido como MPNS) sua `WMAppManifest.xml` ficheiro tem de ter um `<App />` tag com um `Publisher` atributo definido toohello nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="30636-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="30636-117">Inicializar Olá SDK alcance do Engagement</span><span class="sxs-lookup"><span data-stu-id="30636-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="30636-118">Configuração de envolvimento</span><span class="sxs-lookup"><span data-stu-id="30636-118">Engagement configuration</span></span>
<span data-ttu-id="30636-119">configuração de envolvimento Olá é centralizada em Olá `Resources\EngagementConfiguration.xml` ficheiro do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="30636-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="30636-120">Edite esta configuração de alcance do ficheiro toospecify:</span><span class="sxs-lookup"><span data-stu-id="30636-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="30636-121">*Opcional*, indicar se o push nativo do Olá (MPNS) está ativado ou não entre `<enableNativePush>` e `</enableNativePush>` etiquetas, (`true` por predefinição).</span><span class="sxs-lookup"><span data-stu-id="30636-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="30636-122">*Opcional*, indicar o nome de Olá do canal de push Olá entre `<channelName>` e `</channelName>` etiquetas, fornecer Olá mesmo que a aplicação pode atualmente utilizar ou deixe em branco.</span><span class="sxs-lookup"><span data-stu-id="30636-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="30636-123">Se quiser toospecify-la no tempo de execução em vez disso, pode chamar seguinte Olá método antes da inicialização de agente do Engagement Olá:</span><span class="sxs-lookup"><span data-stu-id="30636-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

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
> <span data-ttu-id="30636-124">Pode especificar o nome de Olá do canal de push Olá MPNS da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="30636-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="30636-125">Por predefinição, o Engagement cria um nome com base no ID da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="30636-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="30636-126">Possui sem necessidade de toospecify Olá nome por si, exceto se planear o canal de push de Olá toouse fora o Engagement.</span><span class="sxs-lookup"><span data-stu-id="30636-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="30636-127">Inicialização do engagement</span><span class="sxs-lookup"><span data-stu-id="30636-127">Engagement initialization</span></span>
<span data-ttu-id="30636-128">Modificar Olá `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="30636-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="30636-129">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="30636-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="30636-130">Inserir `EngagementReach.Instance.Init` apenas após `EngagementAgent.Instance.Init` no `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="30636-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="30636-131">Inserir `EngagementReach.Instance.OnActivated` no Olá `Application_Activated` método:</span><span class="sxs-lookup"><span data-stu-id="30636-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="30636-132">Olá `EngagementReach.Instance.Init` é executado num thread dedicado.</span><span class="sxs-lookup"><span data-stu-id="30636-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="30636-133">Não dispõe de toodo-lo por si.</span><span class="sxs-lookup"><span data-stu-id="30636-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="30636-134">Considerações de submissão de arquivo de aplicação</span><span class="sxs-lookup"><span data-stu-id="30636-134">App store submission considerations</span></span>
<span data-ttu-id="30636-135">Microsoft impõe algumas regras ao utilizar notificações de push Olá:</span><span class="sxs-lookup"><span data-stu-id="30636-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="30636-136">De Olá Microsoft [políticas de aplicações] documentação, secção 2.9:</span><span class="sxs-lookup"><span data-stu-id="30636-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="30636-137">Tem de pedir ao hello tooaccept tooreceive push as notificações de utilizador.</span><span class="sxs-lookup"><span data-stu-id="30636-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="30636-138">Em seguida, as definições, adicione notificações de push uma forma toodisable Olá.</span><span class="sxs-lookup"><span data-stu-id="30636-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="30636-139">objeto de EngagementReach Olá fornece dois métodos toomanage Olá na/optar ativamente por participar-ativamente, `EnableNativePush()` e `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="30636-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="30636-140">Por exemplo, pode criar uma opção nas definições de Olá com um toodisable Ativar/desativar ou ativar MPNS.</span><span class="sxs-lookup"><span data-stu-id="30636-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="30636-141">Também pode decidir toodeactivate MPNS através da configuração de envolvimento Olá\<windows phone-sdk-alcance-configuração\>.</span><span class="sxs-lookup"><span data-stu-id="30636-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="30636-142">2.9.1) aplicação Olá primeiro tem de descrever Olá notificações toobe fornecida e **obter hello do express permissão do utilizador (optar ativamente por participar-em)**, e **tem de fornecer um mecanismo através do qual Olá utilizador pode optar ativamente por participar fora de receção notificações push**.</span><span class="sxs-lookup"><span data-stu-id="30636-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="30636-143">Todas as notificações fornecidas a utilizar Olá serviço de notificação Push da Microsoft tem de ser consistentes com o utilizador de toohello Olá descrição fornecida e tem de cumprir todos os aplicável [políticas de aplicações] [ Content Policies]e [requisitos adicionais para tipos de aplicação específica].</span><span class="sxs-lookup"><span data-stu-id="30636-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="30636-144">Não deve utilizar demasiados notificações push.</span><span class="sxs-lookup"><span data-stu-id="30636-144">You should not use too many push notifications.</span></span> <span data-ttu-id="30636-145">Engagement processará as notificações por si.</span><span class="sxs-lookup"><span data-stu-id="30636-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="30636-146">2.9.2) aplicação Olá e a sua utilização de Olá serviço de notificação Push da Microsoft tem excessivamente não utilizar a capacidade de rede ou de largura de banda de Olá serviço de notificação Push da Microsoft ou caso contrário unduly burden Windows Phone ou outros dispositivos Microsoft ou o serviço excessivo com notificações push, conforme determinado pela Microsoft à sua discrição razoável e não pode prejudicar ou interferir com a quaisquer redes da Microsoft ou servidores ou quaisquer servidores de terceiros ou redes ligados toohello serviço notificação Push da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30636-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="30636-147">Não dependem das informações do MPNS toosend criticals.</span><span class="sxs-lookup"><span data-stu-id="30636-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="30636-148">Engagement utiliza MPNS, pelo que também se aplica esta regra de campanhas de Olá criadas dentro de Olá o Engagement front-end.</span><span class="sxs-lookup"><span data-stu-id="30636-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="30636-149">2.9.3) Olá serviço de notificação Push da Microsoft não pode ser utilizado toosend notificações que são o missão críticos ou, caso contrário pode afetar é importante de vida ou death, incluindo sem dispositivo médicas do limitação críticas notificações tooa relacionados ou condição.</span><span class="sxs-lookup"><span data-stu-id="30636-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="30636-150">MICROSOFT expressamente exclui quaisquer garantias que Olá utilização de Olá MICROSOFT PUSH notificação serviço ou entrega de MICROSOFT PUSH notificação serviço notificações irá ser interrompido, erro livre, ou caso contrário garantida tooOCCUR ON A em tempo real base.</span><span class="sxs-lookup"><span data-stu-id="30636-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="30636-151">**Não podemos garantir que a aplicação passará o processo de validação de Olá se não respeitem estas recomendações.**</span><span class="sxs-lookup"><span data-stu-id="30636-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="30636-152">Processar o push de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="30636-152">Handle data push (optional)</span></span>
<span data-ttu-id="30636-153">Se pretender que o seu pushes de dados do application toobe tooreceive capaz de alcance, tiver tooimplement dois eventos de Olá EngagementReach classe:</span><span class="sxs-lookup"><span data-stu-id="30636-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="30636-154">Pode ver essa chamada de retorno Olá de cada método de devolve um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="30636-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="30636-155">Engagement envia um comentários tooits back-end após a emissão de push de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="30636-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="30636-156">Se a chamada de retorno Olá devolve false, Olá `exit` comentários serão envio.</span><span class="sxs-lookup"><span data-stu-id="30636-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="30636-157">Caso contrário, será `action`.</span><span class="sxs-lookup"><span data-stu-id="30636-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="30636-158">Não se for definida nenhum chamada de retorno para eventos de Olá, Olá `drop` comentários serão devolvido tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="30636-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="30636-159">Não o engagement é capaz de tooreceive comentários de múltiplos para um push de dados.</span><span class="sxs-lookup"><span data-stu-id="30636-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="30636-160">Se pretender tooset vários processadores um evento, lembre-se de que o comentários de Olá serão correspondem toohello uma última enviada.</span><span class="sxs-lookup"><span data-stu-id="30636-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="30636-161">Neste caso, recomendamos tooalways devolve Olá mesmo tooavoid de valor ter confuso comentários nos Olá front-end.</span><span class="sxs-lookup"><span data-stu-id="30636-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="30636-162">Personalizar IU (opcional)</span><span class="sxs-lookup"><span data-stu-id="30636-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="30636-163">Primeiro passo</span><span class="sxs-lookup"><span data-stu-id="30636-163">First step</span></span>
<span data-ttu-id="30636-164">Iremos permitem-lhe alcance de Olá toocustomize IU.</span><span class="sxs-lookup"><span data-stu-id="30636-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="30636-165">toodo por isso, ter toocreate uma subclasse de Olá `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="30636-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="30636-166">**Código de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="30636-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="30636-167">Em seguida, definir o conteúdo de Olá de Olá `EngagementReach.Instance.Handler` campo com o seu objeto personalizado no seu `App.xaml.cs` classe no Olá `Application_Launching` método.</span><span class="sxs-lookup"><span data-stu-id="30636-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="30636-168">**Código de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="30636-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="30636-169">Por predefinição, o Engagement utiliza a suas próprias implementação `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="30636-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="30636-170">Não tem toocreate os seus próprios, e se o fizer, não é necessário toooverride cada método.</span><span class="sxs-lookup"><span data-stu-id="30636-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="30636-171">comportamento predefinido de Olá é o objeto de base do Engagement tooselect Olá.</span><span class="sxs-lookup"><span data-stu-id="30636-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="30636-172">Esquemas</span><span class="sxs-lookup"><span data-stu-id="30636-172">Layouts</span></span>
<span data-ttu-id="30636-173">Por predefinição, o alcance irá utilizar Olá incorporado recursos de notificações do Olá DLL toodisplay Olá e páginas.</span><span class="sxs-lookup"><span data-stu-id="30636-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="30636-174">No entanto, pode decidir toouse tooreflect os seus próprios recursos sua marca destes componentes.</span><span class="sxs-lookup"><span data-stu-id="30636-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="30636-175">Pode substituir `EngagementReachHandler` métodos no seu toouse de envolvimento tootell subclasse as esquemas de:</span><span class="sxs-lookup"><span data-stu-id="30636-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="30636-176">**Código de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="30636-176">**Sample Code :**</span></span>

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
> <span data-ttu-id="30636-177">Olá `CreateNotification` método pode devolver um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="30636-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="30636-178">notificação de Olá não irá ser apresentada e campanhas de alcance Olá serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="30636-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="30636-179">toosimplify a implementação de esquema, também fornecemos nosso própria xaml que possa servir como base para o seu código.</span><span class="sxs-lookup"><span data-stu-id="30636-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="30636-180">Onde estão localizados num arquivo de SDK do Engagement Olá (/ src/alcance /).</span><span class="sxs-lookup"><span data-stu-id="30636-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="30636-181">origens de Olá que fornecemos são Olá exato mesmo que utilizamos.</span><span class="sxs-lookup"><span data-stu-id="30636-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="30636-182">Por isso, se quiser toomodify-los diretamente, não se esqueça de espaço de nomes do toochange Olá e Olá nome.</span><span class="sxs-lookup"><span data-stu-id="30636-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="30636-183">Posição de notificação</span><span class="sxs-lookup"><span data-stu-id="30636-183">Notification position</span></span>
<span data-ttu-id="30636-184">Por predefinição, é apresentada uma notificação na aplicação no lado esquerdo de inferior Olá da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="30636-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="30636-185">Pode alterar este comportamento através da substituição Olá `GetNotificationPosition` método de Olá `EngagementReachHandler` objeto.</span><span class="sxs-lookup"><span data-stu-id="30636-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="30636-186">Atualmente, pode escolher entre Olá `BOTTOM` (predefinição) e `TOP` posições.</span><span class="sxs-lookup"><span data-stu-id="30636-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="30636-187">Inicie a mensagem</span><span class="sxs-lookup"><span data-stu-id="30636-187">Launch message</span></span>
<span data-ttu-id="30636-188">Quando um utilizador clica numa notificação do sistema (um alerta), inicia Engagement Olá aplicação, a carga Olá conteúdo de Olá push mensagens e apresentar a página Olá Olá correspondente campanha.</span><span class="sxs-lookup"><span data-stu-id="30636-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="30636-189">Não há um atraso entre a execução de Olá da apresentação de aplicação e Olá Olá da página Olá (dependendo da velocidade Olá da sua rede).</span><span class="sxs-lookup"><span data-stu-id="30636-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="30636-190">utilizador de toohello tooindicate que algo está a carregar, deve fornecer informações de um visual, como uma barra de progresso ou um indicador de progresso.</span><span class="sxs-lookup"><span data-stu-id="30636-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="30636-191">Engagement não consegue processar que ela própria, mas fornece alguns processadores para si.</span><span class="sxs-lookup"><span data-stu-id="30636-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="30636-192">tooimplement Olá chamada de retorno, efetue:</span><span class="sxs-lookup"><span data-stu-id="30636-192">tooimplement hello callback, do:</span></span>

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

<span data-ttu-id="30636-193">Pode definir a chamada de retorno de Olá na sua `Application_Launching` método de sua `App.xaml.cs` ficheiro, preferencialmente, antes de Olá `EngagementReach.Instance.Init()` chamada.</span><span class="sxs-lookup"><span data-stu-id="30636-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="30636-194">Cada processador é designado por Olá Thread de IU.</span><span class="sxs-lookup"><span data-stu-id="30636-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="30636-195">Não dispõe de tooworry quando utilizar uma MessageBox ou algo relacionadas com a IU.</span><span class="sxs-lookup"><span data-stu-id="30636-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[políticas de aplicações]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisitos adicionais para tipos de aplicação específica]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

