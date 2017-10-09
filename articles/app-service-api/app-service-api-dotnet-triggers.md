---
title: "acionadores da aplicação API do serviço aaaApp | Microsoft Docs"
description: "Como tooimplement aciona numa aplicação API no App Service do Azure"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="2713d-103">Acionadores da Aplicação API do App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="2713d-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="2713d-104">Esta versão do artigo Olá aplica-se a versão do esquema de pré-visualização 2014-12-01 do tooAPI apps.</span><span class="sxs-lookup"><span data-stu-id="2713d-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="2713d-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="2713d-105">Overview</span></span>
<span data-ttu-id="2713d-106">Este artigo explica como aplicação tooimplement API aciona e aceder aos mesmos a partir de uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2713d-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="2713d-107">Todos os fragmentos de código Olá neste tópico são copiados do Olá [exemplo de código da aplicação de API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="2713d-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="2713d-108">Tenha em atenção que precisa de Olá toodownload seguinte pacote nuget para o código de Olá no toobuild neste artigo e execute: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="2713d-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="2713d-109">Quais são os acionadores da aplicação API?</span><span class="sxs-lookup"><span data-stu-id="2713d-109">What are API app triggers?</span></span>
<span data-ttu-id="2713d-110">É um cenário comum para um toofire de aplicação de API um evento para que os clientes da aplicação de API de Olá podem agir Olá adequada no evento de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="2713d-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="2713d-111">Olá mecanismo de API de REST com base em que suporta este cenário é chamado um acionador de aplicação API.</span><span class="sxs-lookup"><span data-stu-id="2713d-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="2713d-112">Por exemplo, vamos supor que o código de cliente está a utilizar Olá [aplicação API de conector do Twitter](../connectors/connectors-create-api-twitter.md) e o código tem tooperform uma ação com base em novos tweets que contêm palavras específicas.</span><span class="sxs-lookup"><span data-stu-id="2713d-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="2713d-113">Neste caso, pode configurar um toofacilitate de Acionador de consulta ou push esta necessidade.</span><span class="sxs-lookup"><span data-stu-id="2713d-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="2713d-114">Acionador da consulta em comparação com o acionador de push</span><span class="sxs-lookup"><span data-stu-id="2713d-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="2713d-115">Atualmente, são suportados dois tipos de acionadores:</span><span class="sxs-lookup"><span data-stu-id="2713d-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="2713d-116">Acionador da consulta - o cliente consulta Olá aplicação de API para notificação de um evento ter foi acionada</span><span class="sxs-lookup"><span data-stu-id="2713d-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="2713d-117">Acionadores push - cliente é notificado pela aplicação Olá API quando um evento é acionado</span><span class="sxs-lookup"><span data-stu-id="2713d-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="2713d-118">Acionador da consulta</span><span class="sxs-lookup"><span data-stu-id="2713d-118">Poll trigger</span></span>
<span data-ttu-id="2713d-119">Um acionador de consulta é implementado como uma API de REST normal e espera respetivo toopoll de clientes (por exemplo, uma aplicação lógica) na notificação tooget de ordem.</span><span class="sxs-lookup"><span data-stu-id="2713d-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="2713d-120">Enquanto o cliente de Olá pode manter o estado, o acionador de consulta de Olá em si é sem monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="2713d-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="2713d-121">Olá, seguindo as informações relativas a pacotes hello a pedido e resposta ilustrar alguns aspetos fundamentais do contrato de Acionador de consulta Olá:</span><span class="sxs-lookup"><span data-stu-id="2713d-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="2713d-122">Pedir</span><span class="sxs-lookup"><span data-stu-id="2713d-122">Request</span></span>
  * <span data-ttu-id="2713d-123">Método HTTP: introdução</span><span class="sxs-lookup"><span data-stu-id="2713d-123">HTTP method: GET</span></span>
  * <span data-ttu-id="2713d-124">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2713d-124">Parameters</span></span>
    * <span data-ttu-id="2713d-125">triggerState - este parâmetro opcional permite aos clientes toospecify respetivo estado, de modo que Olá acionador de consulta corretamente pode decidir se tooreturn notificação Olá não com base no especificado ou estado.</span><span class="sxs-lookup"><span data-stu-id="2713d-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="2713d-126">Parâmetros de API específica</span><span class="sxs-lookup"><span data-stu-id="2713d-126">API-specific parameters</span></span>
* <span data-ttu-id="2713d-127">Resposta</span><span class="sxs-lookup"><span data-stu-id="2713d-127">Response</span></span>
  * <span data-ttu-id="2713d-128">Código de estado **200** - pedido é válido e que existe uma notificação a partir do acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="2713d-129">conteúdo de Olá de notificação de Olá será o corpo da resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="2713d-130">Um cabeçalho "Tente novamente após" na resposta Olá indica que os dados de notificação adicionais tem de ser obtidos com uma chamada de pedido subsequente.</span><span class="sxs-lookup"><span data-stu-id="2713d-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="2713d-131">Código de estado **202** - pedido é válido, mas não há qualquer notificação nova do acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="2713d-132">Código de estado **4xx** -pedido não é válido.</span><span class="sxs-lookup"><span data-stu-id="2713d-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="2713d-133">cliente de Olá não deverá repetir o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="2713d-134">Código de estado **5xx** -pedido resultou num erro interno do servidor e/ou um problema temporário.</span><span class="sxs-lookup"><span data-stu-id="2713d-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="2713d-135">cliente de Olá deverá repetir o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-135">hello client should retry hello request.</span></span>

<span data-ttu-id="2713d-136">Olá seguinte fragmento de código é um exemplo de como acionar tooimplement uma consulta.</span><span class="sxs-lookup"><span data-stu-id="2713d-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="2713d-137">tootest acionar esta consulta, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="2713d-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="2713d-138">Implementar Olá API aplicação com uma definição de autenticação de **público anónimo**.</span><span class="sxs-lookup"><span data-stu-id="2713d-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="2713d-139">Chamar Olá **touch** operação tootouch um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2713d-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="2713d-140">Olá imagem a seguir mostra um exemplo de pedido através do Postman.</span><span class="sxs-lookup"><span data-stu-id="2713d-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="2713d-141">![Chamar a operação de Touch através do Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="2713d-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="2713d-142">Chamar o acionador de consulta Olá com Olá **triggerState** parâmetro definido tooa tempo carimbo anterior tooStep #2.</span><span class="sxs-lookup"><span data-stu-id="2713d-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="2713d-143">Olá imagem seguinte mostra pedido de exemplo de Olá através do Postman.</span><span class="sxs-lookup"><span data-stu-id="2713d-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="2713d-144">![Chamada de Acionador de consulta através do Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="2713d-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="2713d-145">Acionadores Push</span><span class="sxs-lookup"><span data-stu-id="2713d-145">Push trigger</span></span>
<span data-ttu-id="2713d-146">Um acionador de push é implementado como uma API de REST normal que envia notificações tooclients que registou toobe notificado quando acionados eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="2713d-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="2713d-147">Olá, seguindo as informações relativas a pacotes hello a pedido e resposta ilustrar alguns aspetos fundamentais do contrato de Acionador de push Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="2713d-148">Pedir</span><span class="sxs-lookup"><span data-stu-id="2713d-148">Request</span></span>
  * <span data-ttu-id="2713d-149">Método HTTP: colocar</span><span class="sxs-lookup"><span data-stu-id="2713d-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="2713d-150">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2713d-150">Parameters</span></span>
    * <span data-ttu-id="2713d-151">triggerId: obrigatória - opaco cadeia (por exemplo, um GUID) que representa Olá registo de um acionador de push.</span><span class="sxs-lookup"><span data-stu-id="2713d-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="2713d-152">callbackUrl: obrigatória - URL de Olá tooinvoke de chamada de retorno quando o evento de Olá é acionado.</span><span class="sxs-lookup"><span data-stu-id="2713d-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="2713d-153">invocação de Olá é uma chamada POST HTTP simple.</span><span class="sxs-lookup"><span data-stu-id="2713d-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="2713d-154">Parâmetros de API específica</span><span class="sxs-lookup"><span data-stu-id="2713d-154">API-specific parameters</span></span>
* <span data-ttu-id="2713d-155">Resposta</span><span class="sxs-lookup"><span data-stu-id="2713d-155">Response</span></span>
  * <span data-ttu-id="2713d-156">Código de estado **200** -pedido tooregister cliente com êxito.</span><span class="sxs-lookup"><span data-stu-id="2713d-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="2713d-157">Código de estado **4xx** -pedido não é válido.</span><span class="sxs-lookup"><span data-stu-id="2713d-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="2713d-158">cliente de Olá não deverá repetir o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="2713d-159">Código de estado **5xx** -pedido resultou num erro interno do servidor e/ou um problema temporário.</span><span class="sxs-lookup"><span data-stu-id="2713d-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="2713d-160">cliente de Olá deverá repetir o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="2713d-161">Chamada de retorno</span><span class="sxs-lookup"><span data-stu-id="2713d-161">Callback</span></span>
  * <span data-ttu-id="2713d-162">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="2713d-162">HTTP method: POST</span></span>
  * <span data-ttu-id="2713d-163">Corpo do pedido: conteúdo de notificação.</span><span class="sxs-lookup"><span data-stu-id="2713d-163">Request body: Notification content.</span></span>

<span data-ttu-id="2713d-164">Olá seguinte fragmento de código é um exemplo de como acionar tooimplement um push:</span><span class="sxs-lookup"><span data-stu-id="2713d-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="2713d-165">tootest acionar esta consulta, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="2713d-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="2713d-166">Implementar Olá API aplicação com uma definição de autenticação de **público anónimo**.</span><span class="sxs-lookup"><span data-stu-id="2713d-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="2713d-167">Procurar demasiado[http://requestb.in/](http://requestb.in/) toocreate um RequestBin que irá servir como o seu URL de chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="2713d-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="2713d-168">Chamar o acionador de push Olá com um GUID como **triggerId** e Olá RequestBin URL como **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="2713d-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="2713d-169">![Chamada de Acionador de Push através do Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="2713d-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="2713d-170">Chamar Olá **touch** operação tootouch um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2713d-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="2713d-171">Olá imagem a seguir mostra um exemplo de pedido através do Postman.</span><span class="sxs-lookup"><span data-stu-id="2713d-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="2713d-172">![Chamar a operação de Touch através do Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="2713d-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="2713d-173">Verificação Olá RequestBin tooconfirm que Olá chamada de retorno de Acionador de push é invocado com a saída de propriedade.</span><span class="sxs-lookup"><span data-stu-id="2713d-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="2713d-174">![Chamada de Acionador de consulta através do Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="2713d-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="2713d-175">Descrevem acionadores na definição de API</span><span class="sxs-lookup"><span data-stu-id="2713d-175">Describe triggers in API definition</span></span>
<span data-ttu-id="2713d-176">Após implementar os acionadores de Olá e implementar a sua tooAzure de aplicação API, navegue até toohello **definição da API** painel no portal de pré-visualização do Azure Olá e verá que acionadores são automaticamente reconhecidos no Olá IU, que é controlada por Olá definição de API do Swagger 2.0 da aplicação Olá API.</span><span class="sxs-lookup"><span data-stu-id="2713d-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Painel de definição de API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="2713d-178">Se clicar em Olá **transferir Swagger** botão e ficheiro JSON Olá aberta, verá resultados toohello semelhante, os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2713d-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="2713d-179">propriedade de extensão de Olá **x-ms-schedular-acionador** é como acionadores são descritos na definição de API e é automaticamente adicionada pelo gateway de aplicação Olá API quando solicitar definição Olá API através do gateway de Olá se Olá pedido tooone de Olá os seguintes critérios.</span><span class="sxs-lookup"><span data-stu-id="2713d-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="2713d-180">(Também pode adicionar esta propriedade manualmente.)</span><span class="sxs-lookup"><span data-stu-id="2713d-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="2713d-181">Acionador da consulta</span><span class="sxs-lookup"><span data-stu-id="2713d-181">Poll trigger</span></span>
  * <span data-ttu-id="2713d-182">Se for Olá método HTTP **obter**.</span><span class="sxs-lookup"><span data-stu-id="2713d-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="2713d-183">Se hello **operationId** propriedade contém uma cadeia Olá **acionador**.</span><span class="sxs-lookup"><span data-stu-id="2713d-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="2713d-184">Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida demasiado**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="2713d-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="2713d-185">Acionadores Push</span><span class="sxs-lookup"><span data-stu-id="2713d-185">Push trigger</span></span>
  * <span data-ttu-id="2713d-186">Se for Olá método HTTP **colocar**.</span><span class="sxs-lookup"><span data-stu-id="2713d-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="2713d-187">Se hello **operationId** propriedade contém uma cadeia Olá **acionador**.</span><span class="sxs-lookup"><span data-stu-id="2713d-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="2713d-188">Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida demasiado**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="2713d-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="2713d-189">Utilizar acionadores da aplicação API nas Logic apps</span><span class="sxs-lookup"><span data-stu-id="2713d-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="2713d-190">Listar e configurar acionadores da aplicação API no designer de aplicações de lógica de Olá</span><span class="sxs-lookup"><span data-stu-id="2713d-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="2713d-191">Se criar uma aplicação lógica em Olá mesmo grupo de recursos como Olá aplicação API, será capaz de tooadd-toohello tela estruturador simplesmente clicando nela.</span><span class="sxs-lookup"><span data-stu-id="2713d-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="2713d-192">Olá seguintes imagens ilustrar isto:</span><span class="sxs-lookup"><span data-stu-id="2713d-192">hello following images illustrate this:</span></span>

![Acionadores no Designer de aplicação lógica](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurar o acionador de consulta no Designer de aplicação lógica](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurar o acionador de Push no Designer de aplicação lógica](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="2713d-196">Otimizar acionadores da aplicação API para aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="2713d-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="2713d-197">Depois de adicionar acionadores tooan API aplicação, existem algumas coisas que pode fazer a experiência de Olá tooimprove quando Olá API aplicação uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2713d-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="2713d-198">Por exemplo, Olá **triggerState** parâmetro acionadores de consultas deve ser definido toohello seguintes expressão na aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="2713d-199">Esta expressão deve avaliar a invocação de último Olá do acionador de Olá da aplicação de lógica de Olá e que o valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="2713d-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="2713d-200">Nota: Para obter uma explicação das funções de Olá utilizado numa expressão de Olá acima, consulte a documentação de toohello em [linguagem de definição de fluxo de trabalho de aplicação lógica](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="2713d-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="2713d-201">Os utilizadores de aplicação lógica precisaria de expressão de Olá tooprovide acima para Olá **triggerState** parâmetro durante a utilização de Acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="2713d-202">É possível toohave este valor da configuração predefinido pelo designer de aplicação de lógica de Olá através da propriedade de extensão de Olá **x-ms-agendador-recomendação**.</span><span class="sxs-lookup"><span data-stu-id="2713d-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="2713d-203">Olá **x-ms-visibilidade** tooa valor possível definir a propriedade de extensão *interno* para que o parâmetro de Olá propriamente dito não é apresentado no estruturador de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="2713d-204">Olá fragmento a seguir ilustra que.</span><span class="sxs-lookup"><span data-stu-id="2713d-204">hello following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="2713d-205">Para acionadores push, Olá **triggerId** parâmetro tem de identificar exclusivamente aplicação de lógica de Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="2713d-206">Uma melhor prática recomendada é tooset este nome de toohello de propriedade de fluxo de trabalho Olá utilizando Olá seguintes expressão:</span><span class="sxs-lookup"><span data-stu-id="2713d-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="2713d-207">Utilizar Olá **x-ms-agendador-recomendação** e **x-ms-visibilidade** as propriedades de extensão no respetivo definiton de API, Olá aplicação API podem transmitir defina esta opção toohello lógica aplicação designer tooautomatically expressão para o utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="2713d-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="2713d-208">Adicionar propriedades de extensão do defintion de API</span><span class="sxs-lookup"><span data-stu-id="2713d-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="2713d-209">Informações de metadados adicionais - tais como as propriedades de extensão de Olá **x-ms-agendador-recomendação** e **x-ms-visibilidade** -é possível adicionar defintion Olá API de uma das seguintes formas: estático ou dinâmico.</span><span class="sxs-lookup"><span data-stu-id="2713d-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="2713d-210">Para obter metadados estático, pode editar diretamente Olá */metadata/apiDefinition.swagger.json* de ficheiros no seu projeto e adicionar propriedades de Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="2713d-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="2713d-211">Para API apps através de metadados dinâmico, pode editar tooadd de ficheiro de Swaggerconfig Olá um filtro de operação que pode adicionar estas extensões.</span><span class="sxs-lookup"><span data-stu-id="2713d-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="2713d-212">Olá segue-se um exemplo de como esta classe pode ser o cenário de metadados dinâmico de Olá toofacilitate implementado.</span><span class="sxs-lookup"><span data-stu-id="2713d-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
