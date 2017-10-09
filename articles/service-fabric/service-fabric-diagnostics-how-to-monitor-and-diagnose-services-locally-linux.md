---
title: "aaaDebug micro-serviços do Azure no Linux | Microsoft Docs"
description: "Saiba como toomonitor e diagnosticar os serviços escritos utilizando o Microsoft Azure Service Fabric numa máquina de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="6b3fb-103">Monitorizar e diagnosticar os serviços de uma configuração de desenvolvimento do computador local</span><span class="sxs-lookup"><span data-stu-id="6b3fb-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b3fb-104">Windows</span><span class="sxs-lookup"><span data-stu-id="6b3fb-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="6b3fb-105">Linux</span><span class="sxs-lookup"><span data-stu-id="6b3fb-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="6b3fb-106">Monitorização, detetar, diagnosticar e resolver problemas permitem serviços toocontinue mínima interrupção toohello experiência de utilização.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="6b3fb-107">Monitorização e diagnóstico é crítico num ambiente de produção implementado real.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="6b3fb-108">Adotar um modelo semelhante durante o desenvolvimento de serviços garante que nesse pipeline diagnóstico Olá funciona quando move tooa ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="6b3fb-109">Service Fabric torna mais fácil para tooimplement de diagnóstico de programadores de serviço que funciona na perfeição entre setups única máquina de desenvolvimento local e setups de cluster de produção do mundo real.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="6b3fb-110">A depuração de aplicações Java de recursos de infraestrutura de serviço</span><span class="sxs-lookup"><span data-stu-id="6b3fb-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="6b3fb-111">Para aplicações de Java, [várias arquiteturas de registo](http://en.wikipedia.org/wiki/Java_logging_framework) estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="6b3fb-112">Uma vez que `java.util.logging` é a opção predefinida de Olá com Olá JRE, também é utilizado para Olá [exemplos em github de código](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="6b3fb-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="6b3fb-113">Olá debate seguinte explica como tooconfigure Olá `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="6b3fb-114">Utilizar Util pode redirecionar a aplicação regista toomemory, fluxos de saída, ficheiros de consola ou sockets.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="6b3fb-115">Para cada uma destas opções, existem processadores predefinidos já são fornecidos no framework Olá.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="6b3fb-116">Pode criar um `app.properties` processador de ficheiros do ficheiro tooconfigure Olá para sua tooredirect aplicação todos os registos de ficheiros local tooa.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="6b3fb-117">Olá seguinte fragmento de código contém uma configuração de exemplo:</span><span class="sxs-lookup"><span data-stu-id="6b3fb-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="6b3fb-118">Olá do Olá pasta tooby apontado `app.properties` ficheiro tem de existir.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="6b3fb-119">Depois de Olá `app.properties` ficheiro é criado, tem de tooalso modificar o script de ponto de entrada, `entrypoint.sh` no Olá `<applicationfolder>/<servicePkg>/Code/` propriedade do pasta tooset Olá `java.util.logging.config.file` demasiado`app.propertes` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="6b3fb-120">entrada de Olá deve aspeto Olá seguinte fragmento:</span><span class="sxs-lookup"><span data-stu-id="6b3fb-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="6b3fb-121">Esta configuração resulta em registos estão a ser recolhidos de forma rotating em `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="6b3fb-122">ficheiro de registo Olá neste caso é denominado mysfapp%u.%g.log onde:</span><span class="sxs-lookup"><span data-stu-id="6b3fb-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="6b3fb-123">**%u** é um tooresolve número exclusivo conflitos entre processos simultâneos de Java.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="6b3fb-124">**%g** é Olá geração número toodistinguish entre a rotação dos registos.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="6b3fb-125">Por predefinição se nenhuma rotina de tratamento explicitamente estiver configurada, o processador de consola Olá está registado.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="6b3fb-126">Um pode ver os registos de Olá do syslog em /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="6b3fb-127">Para obter mais informações, consulte Olá [exemplos em github de código](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="6b3fb-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="6b3fb-128">Depurar aplicações de Service Fabric c#</span><span class="sxs-lookup"><span data-stu-id="6b3fb-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="6b3fb-129">Várias estruturas estão disponíveis para rastreio CoreCLR aplicações no Linux.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="6b3fb-130">Para obter mais informações, consulte [GitHub: registo](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="6b3fb-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="6b3fb-131">Uma vez que é de EventSource familiar tooC # programadores,' Este artigo utiliza EventSource para o rastreio nos exemplos CoreCLR no Linux.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="6b3fb-132">Step-by-Olá primeiro passo é tooinclude System.Diagnostics.Tracing para que pode escrever o seu toomemory de registos, os fluxos de saída ou ficheiros da consola.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="6b3fb-133">Para o registo através de EventSource, adicione Olá projeto tooyour project.json os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6b3fb-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="6b3fb-134">Pode utilizar um toolisten EventListener personalizado para o evento de serviço Olá e, em seguida, adequadamente redirecioná-los tootrace ficheiros.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="6b3fb-135">Olá fragmento de código seguinte mostra uma implementação de exemplo de início de sessão através de EventSource e um EventListener personalizado:</span><span class="sxs-lookup"><span data-stu-id="6b3fb-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="6b3fb-136">Olá fragmento anterior produz Olá registos tooa ficheiro `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="6b3fb-137">Este nome de ficheiro necessita de toobe corretamente atualizado.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="6b3fb-138">No caso de pretender tooredirect Olá registos tooconsole, utilize Olá seguinte fragmento na sua classe EventListener personalizado:</span><span class="sxs-lookup"><span data-stu-id="6b3fb-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="6b3fb-139">Olá exemplos em [amostras de c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utilizar EventSource e um ficheiro de tooa eventos de toolog do personalizado EventListener.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6b3fb-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6b3fb-140">Next steps</span></span>
<span data-ttu-id="6b3fb-141">Olá mesmo código de rastreio adicionado tooyour aplicação também funciona com diagnóstico Olá da sua aplicação num cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="6b3fb-142">Modificação nestes artigos que aborda Olá opções diferentes para as ferramentas de Olá e descrevem como tooset-las a cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="6b3fb-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="6b3fb-143">Modo de registo de toocollect com diagnósticos do Azure</span><span class="sxs-lookup"><span data-stu-id="6b3fb-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
