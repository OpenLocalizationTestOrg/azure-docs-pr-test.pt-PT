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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorizar e diagnosticar os serviços de uma configuração de desenvolvimento do computador local


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Monitorização, detetar, diagnosticar e resolver problemas permitem serviços toocontinue mínima interrupção toohello experiência de utilização. Monitorização e diagnóstico é crítico num ambiente de produção implementado real. Adotar um modelo semelhante durante o desenvolvimento de serviços garante que nesse pipeline diagnóstico Olá funciona quando move tooa ambiente de produção. Service Fabric torna mais fácil para tooimplement de diagnóstico de programadores de serviço que funciona na perfeição entre setups única máquina de desenvolvimento local e setups de cluster de produção do mundo real.


## <a name="debugging-service-fabric-java-applications"></a>A depuração de aplicações Java de recursos de infraestrutura de serviço

Para aplicações de Java, [várias arquiteturas de registo](http://en.wikipedia.org/wiki/Java_logging_framework) estão disponíveis. Uma vez que `java.util.logging` é a opção predefinida de Olá com Olá JRE, também é utilizado para Olá [exemplos em github de código](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Olá debate seguinte explica como tooconfigure Olá `java.util.logging` framework.

Utilizar Util pode redirecionar a aplicação regista toomemory, fluxos de saída, ficheiros de consola ou sockets. Para cada uma destas opções, existem processadores predefinidos já são fornecidos no framework Olá. Pode criar um `app.properties` processador de ficheiros do ficheiro tooconfigure Olá para sua tooredirect aplicação todos os registos de ficheiros local tooa.

Olá seguinte fragmento de código contém uma configuração de exemplo:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Olá do Olá pasta tooby apontado `app.properties` ficheiro tem de existir. Depois de Olá `app.properties` ficheiro é criado, tem de tooalso modificar o script de ponto de entrada, `entrypoint.sh` no Olá `<applicationfolder>/<servicePkg>/Code/` propriedade do pasta tooset Olá `java.util.logging.config.file` demasiado`app.propertes` ficheiro. entrada de Olá deve aspeto Olá seguinte fragmento:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Esta configuração resulta em registos estão a ser recolhidos de forma rotating em `/tmp/servicefabric/logs/`. ficheiro de registo Olá neste caso é denominado mysfapp%u.%g.log onde:
* **%u** é um tooresolve número exclusivo conflitos entre processos simultâneos de Java.
* **%g** é Olá geração número toodistinguish entre a rotação dos registos.

Por predefinição se nenhuma rotina de tratamento explicitamente estiver configurada, o processador de consola Olá está registado. Um pode ver os registos de Olá do syslog em /var/log/syslog.

Para obter mais informações, consulte Olá [exemplos em github de código](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Depurar aplicações de Service Fabric c#


Várias estruturas estão disponíveis para rastreio CoreCLR aplicações no Linux. Para obter mais informações, consulte [GitHub: registo](http:/github.com/aspnet/logging).  Uma vez que é de EventSource familiar tooC # programadores,' Este artigo utiliza EventSource para o rastreio nos exemplos CoreCLR no Linux.

Step-by-Olá primeiro passo é tooinclude System.Diagnostics.Tracing para que pode escrever o seu toomemory de registos, os fluxos de saída ou ficheiros da consola.  Para o registo através de EventSource, adicione Olá projeto tooyour project.json os seguintes:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Pode utilizar um toolisten EventListener personalizado para o evento de serviço Olá e, em seguida, adequadamente redirecioná-los tootrace ficheiros. Olá fragmento de código seguinte mostra uma implementação de exemplo de início de sessão através de EventSource e um EventListener personalizado:


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


Olá fragmento anterior produz Olá registos tooa ficheiro `/tmp/MyServiceLog.txt`. Este nome de ficheiro necessita de toobe corretamente atualizado. No caso de pretender tooredirect Olá registos tooconsole, utilize Olá seguinte fragmento na sua classe EventListener personalizado:

```csharp
public static TextWriter Out = Console.Out;
```

Olá exemplos em [amostras de c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utilizar EventSource e um ficheiro de tooa eventos de toolog do personalizado EventListener.



## <a name="next-steps"></a>Passos seguintes
Olá mesmo código de rastreio adicionado tooyour aplicação também funciona com diagnóstico Olá da sua aplicação num cluster do Azure. Modificação nestes artigos que aborda Olá opções diferentes para as ferramentas de Olá e descrevem como tooset-las a cópia de segurança.
* [Modo de registo de toocollect com diagnósticos do Azure](service-fabric-diagnostics-how-to-setup-lad.md)
