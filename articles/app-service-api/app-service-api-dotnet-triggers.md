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
# <a name="azure-app-service-api-app-triggers"></a>Acionadores da Aplicação API do App Service do Azure
> [!NOTE]
> Esta versão do artigo Olá aplica-se a versão do esquema de pré-visualização 2014-12-01 do tooAPI apps.
>
>

## <a name="overview"></a>Descrição geral
Este artigo explica como aplicação tooimplement API aciona e aceder aos mesmos a partir de uma aplicação lógica.

Todos os fragmentos de código Olá neste tópico são copiados do Olá [exemplo de código da aplicação de API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Tenha em atenção que precisa de Olá toodownload seguinte pacote nuget para o código de Olá no toobuild neste artigo e execute: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Quais são os acionadores da aplicação API?
É um cenário comum para um toofire de aplicação de API um evento para que os clientes da aplicação de API de Olá podem agir Olá adequada no evento de toohello de resposta. Olá mecanismo de API de REST com base em que suporta este cenário é chamado um acionador de aplicação API.

Por exemplo, vamos supor que o código de cliente está a utilizar Olá [aplicação API de conector do Twitter](../connectors/connectors-create-api-twitter.md) e o código tem tooperform uma ação com base em novos tweets que contêm palavras específicas. Neste caso, pode configurar um toofacilitate de Acionador de consulta ou push esta necessidade.

## <a name="poll-trigger-versus-push-trigger"></a>Acionador da consulta em comparação com o acionador de push
Atualmente, são suportados dois tipos de acionadores:

* Acionador da consulta - o cliente consulta Olá aplicação de API para notificação de um evento ter foi acionada
* Acionadores push - cliente é notificado pela aplicação Olá API quando um evento é acionado

### <a name="poll-trigger"></a>Acionador da consulta
Um acionador de consulta é implementado como uma API de REST normal e espera respetivo toopoll de clientes (por exemplo, uma aplicação lógica) na notificação tooget de ordem. Enquanto o cliente de Olá pode manter o estado, o acionador de consulta de Olá em si é sem monitorização de estado.

Olá, seguindo as informações relativas a pacotes hello a pedido e resposta ilustrar alguns aspetos fundamentais do contrato de Acionador de consulta Olá:

* Pedir
  * Método HTTP: introdução
  * Parâmetros
    * triggerState - este parâmetro opcional permite aos clientes toospecify respetivo estado, de modo que Olá acionador de consulta corretamente pode decidir se tooreturn notificação Olá não com base no especificado ou estado.
    * Parâmetros de API específica
* Resposta
  * Código de estado **200** - pedido é válido e que existe uma notificação a partir do acionador de Olá. conteúdo de Olá de notificação de Olá será o corpo da resposta Olá. Um cabeçalho "Tente novamente após" na resposta Olá indica que os dados de notificação adicionais tem de ser obtidos com uma chamada de pedido subsequente.
  * Código de estado **202** - pedido é válido, mas não há qualquer notificação nova do acionador de Olá.
  * Código de estado **4xx** -pedido não é válido. cliente de Olá não deverá repetir o pedido de Olá.
  * Código de estado **5xx** -pedido resultou num erro interno do servidor e/ou um problema temporário. cliente de Olá deverá repetir o pedido de Olá.

Olá seguinte fragmento de código é um exemplo de como acionar tooimplement uma consulta.

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

tootest acionar esta consulta, siga estes passos:

1. Implementar Olá API aplicação com uma definição de autenticação de **público anónimo**.
2. Chamar Olá **touch** operação tootouch um ficheiro. Olá imagem a seguir mostra um exemplo de pedido através do Postman.
   ![Chamar a operação de Touch através do Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Chamar o acionador de consulta Olá com Olá **triggerState** parâmetro definido tooa tempo carimbo anterior tooStep #2. Olá imagem seguinte mostra pedido de exemplo de Olá através do Postman.
   ![Chamada de Acionador de consulta através do Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Acionadores Push
Um acionador de push é implementado como uma API de REST normal que envia notificações tooclients que registou toobe notificado quando acionados eventos específicos.

Olá, seguindo as informações relativas a pacotes hello a pedido e resposta ilustrar alguns aspetos fundamentais do contrato de Acionador de push Olá.

* Pedir
  * Método HTTP: colocar
  * Parâmetros
    * triggerId: obrigatória - opaco cadeia (por exemplo, um GUID) que representa Olá registo de um acionador de push.
    * callbackUrl: obrigatória - URL de Olá tooinvoke de chamada de retorno quando o evento de Olá é acionado. invocação de Olá é uma chamada POST HTTP simple.
    * Parâmetros de API específica
* Resposta
  * Código de estado **200** -pedido tooregister cliente com êxito.
  * Código de estado **4xx** -pedido não é válido. cliente de Olá não deverá repetir o pedido de Olá.
  * Código de estado **5xx** -pedido resultou num erro interno do servidor e/ou um problema temporário. cliente de Olá deverá repetir o pedido de Olá.
* Chamada de retorno
  * Método HTTP: POST
  * Corpo do pedido: conteúdo de notificação.

Olá seguinte fragmento de código é um exemplo de como acionar tooimplement um push:

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

tootest acionar esta consulta, siga estes passos:

1. Implementar Olá API aplicação com uma definição de autenticação de **público anónimo**.
2. Procurar demasiado[http://requestb.in/](http://requestb.in/) toocreate um RequestBin que irá servir como o seu URL de chamada de retorno.
3. Chamar o acionador de push Olá com um GUID como **triggerId** e Olá RequestBin URL como **callbackUrl**.
   ![Chamada de Acionador de Push através do Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Chamar Olá **touch** operação tootouch um ficheiro. Olá imagem a seguir mostra um exemplo de pedido através do Postman.
   ![Chamar a operação de Touch através do Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Verificação Olá RequestBin tooconfirm que Olá chamada de retorno de Acionador de push é invocado com a saída de propriedade.
   ![Chamada de Acionador de consulta através do Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Descrevem acionadores na definição de API
Após implementar os acionadores de Olá e implementar a sua tooAzure de aplicação API, navegue até toohello **definição da API** painel no portal de pré-visualização do Azure Olá e verá que acionadores são automaticamente reconhecidos no Olá IU, que é controlada por Olá definição de API do Swagger 2.0 da aplicação Olá API.

![Painel de definição de API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Se clicar em Olá **transferir Swagger** botão e ficheiro JSON Olá aberta, verá resultados toohello semelhante, os seguintes:

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

propriedade de extensão de Olá **x-ms-schedular-acionador** é como acionadores são descritos na definição de API e é automaticamente adicionada pelo gateway de aplicação Olá API quando solicitar definição Olá API através do gateway de Olá se Olá pedido tooone de Olá os seguintes critérios. (Também pode adicionar esta propriedade manualmente.)

* Acionador da consulta
  * Se for Olá método HTTP **obter**.
  * Se hello **operationId** propriedade contém uma cadeia Olá **acionador**.
  * Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida demasiado**triggerState**.
* Acionadores Push
  * Se for Olá método HTTP **colocar**.
  * Se hello **operationId** propriedade contém uma cadeia Olá **acionador**.
  * Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida demasiado**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Utilizar acionadores da aplicação API nas Logic apps
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Listar e configurar acionadores da aplicação API no designer de aplicações de lógica de Olá
Se criar uma aplicação lógica em Olá mesmo grupo de recursos como Olá aplicação API, será capaz de tooadd-toohello tela estruturador simplesmente clicando nela. Olá seguintes imagens ilustrar isto:

![Acionadores no Designer de aplicação lógica](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurar o acionador de consulta no Designer de aplicação lógica](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurar o acionador de Push no Designer de aplicação lógica](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Otimizar acionadores da aplicação API para aplicações lógicas
Depois de adicionar acionadores tooan API aplicação, existem algumas coisas que pode fazer a experiência de Olá tooimprove quando Olá API aplicação uma aplicação lógica.

Por exemplo, Olá **triggerState** parâmetro acionadores de consultas deve ser definido toohello seguintes expressão na aplicação de lógica de Olá. Esta expressão deve avaliar a invocação de último Olá do acionador de Olá da aplicação de lógica de Olá e que o valor de retorno.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Nota: Para obter uma explicação das funções de Olá utilizado numa expressão de Olá acima, consulte a documentação de toohello em [linguagem de definição de fluxo de trabalho de aplicação lógica](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Os utilizadores de aplicação lógica precisaria de expressão de Olá tooprovide acima para Olá **triggerState** parâmetro durante a utilização de Acionador de Olá. É possível toohave este valor da configuração predefinido pelo designer de aplicação de lógica de Olá através da propriedade de extensão de Olá **x-ms-agendador-recomendação**.  Olá **x-ms-visibilidade** tooa valor possível definir a propriedade de extensão *interno* para que o parâmetro de Olá propriamente dito não é apresentado no estruturador de Olá.  Olá fragmento a seguir ilustra que.

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

Para acionadores push, Olá **triggerId** parâmetro tem de identificar exclusivamente aplicação de lógica de Olá. Uma melhor prática recomendada é tooset este nome de toohello de propriedade de fluxo de trabalho Olá utilizando Olá seguintes expressão:

    @workflow().name

Utilizar Olá **x-ms-agendador-recomendação** e **x-ms-visibilidade** as propriedades de extensão no respetivo definiton de API, Olá aplicação API podem transmitir defina esta opção toohello lógica aplicação designer tooautomatically expressão para o utilizador Olá.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Adicionar propriedades de extensão do defintion de API
Informações de metadados adicionais - tais como as propriedades de extensão de Olá **x-ms-agendador-recomendação** e **x-ms-visibilidade** -é possível adicionar defintion Olá API de uma das seguintes formas: estático ou dinâmico.

Para obter metadados estático, pode editar diretamente Olá */metadata/apiDefinition.swagger.json* de ficheiros no seu projeto e adicionar propriedades de Olá manualmente.

Para API apps através de metadados dinâmico, pode editar tooadd de ficheiro de Swaggerconfig Olá um filtro de operação que pode adicionar estas extensões.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Olá segue-se um exemplo de como esta classe pode ser o cenário de metadados dinâmico de Olá toofacilitate implementado.

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
