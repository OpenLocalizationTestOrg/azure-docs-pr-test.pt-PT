---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em c# | Microsoft Docs"
description: "Este tutorial orienta-o pelos passos de Olá da criação, depurar e implementar um serviço baseado em ator simple utilizando o serviço de recursos de infraestrutura Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Introdução a Reliable Actors
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-actors-get-started.md)
> * [Java em Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Este artigo explica Olá Noções básicas do Azure Service Fabric Reliable Actors e explica-lhe como criar, depurar e implementar uma aplicação simples de Ator fiável no Visual Studio.

## <a name="installation-and-setup"></a>Instalação e configuração
Antes de começar, certifique-se de que tem o ambiente de desenvolvimento do Service Fabric Olá que configurar no seu computador.
Se precisar de tooset-lo, consulte instruções detalhadas sobre [como tooset configurar o ambiente de desenvolvimento de Olá](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Conceitos básicos
tooget começar Reliable Actors, apenas é necessário toounderstand alguns conceitos básicos:

* **Serviço de atores**. Reliable Actors são reunidas em Reliable Services que podem ser implementados numa infraestrutura de Service Fabric Olá. Instâncias de ator são ativadas numa instância de serviço com nome.
* **Registo de ator**. Como com Reliable Services, um serviço de Atores fiável tem toobe registado com o tempo de execução do Olá Service Fabric. Além disso, o tipo de ator Olá deve toobe registado com o tempo de execução do Olá Ator.
* **Interface de ator**. interface de ator Olá é utilizado toodefine uma interface pública com tipo seguro de um ator. Na terminologia de modelo de Ator fiável Olá, a interface de ator Olá define Olá tipos de mensagens hello ator podem compreender e processar. interface de ator Olá é utilizado por outros atores e aplicações cliente demasiado "de envio" (no modo assíncrono) ator toohello de mensagens. Reliable Actors podem implementar várias interfaces.
* **Classe de ActorProxy**. Olá ActorProxy classe é utilizada pelo cliente aplicações tooinvoke Olá métodos expostos através da interface de ator Olá. Olá ActorProxy classe fornece duas funcionalidades importantes:
  
  * Resolução de nomes: é capaz de toolocate actor de Olá num cluster de Olá (localizar Olá nó de cluster olá onde está alojado).
  * Processamento de falhas: pode repetir invocações de método e novamente resolver a localização de atores de Olá depois, por exemplo, uma falha de que necessita de Olá ator toobe relocalizada tooanother de nó no cluster de Olá.

Olá seguintes regras que dizem respeito tooactor interfaces é mencionar:

* Métodos de interface de ator não podem estar sobrecarregados.
* Interface de ator métodos não pode ter out, ref ou parâmetros opcionais.
* Interfaces genéricas não são suportadas.

## <a name="create-a-new-project-in-visual-studio"></a>Criar um novo projeto no Visual Studio
Inicie o Visual Studio 2015 ou Visual Studio 2017 como administrador e criar um novo projeto de aplicação de Service Fabric:

![Ferramentas do Service Fabric para Visual Studio – novo projeto][1]

Na caixa de diálogo seguinte Olá, pode escolher tipo de Olá do projeto que pretende que o toocreate.

![Modelos de projeto de Service Fabric][5]

Para o projeto de Olámundo Olá, vamos a utilizar o serviço de Service Fabric Reliable Actors Olá.

Depois de ter criado solução Olá, deverá ver Olá seguir a estrutura:

![Estrutura do projeto de Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a>Fiáveis blocos modulares básicos Actors
Uma solução de Reliable Actors típica é composta por três projetos:

* **projeto de aplicação Olá (MyActorApplication)**. Este é o projeto de Olá que todos os serviços de Olá em conjunto para a implementação de pacotes. Contém Olá *ApplicationManifest.xml* e scripts do PowerShell para gerir a aplicação Olá.
* **o projeto de interface de Olá (MyActor.Interfaces)**. Este é o projeto de Olá que contém uma definição de interface de Olá para ator Olá. No projeto de MyActor.Interfaces Olá, pode definir interfaces de Olá que serão utilizadas pelo atores Olá na solução de Olá. As interfaces de ator podem ser definidas em qualquer projeto com qualquer nome, no entanto, a interface Olá define o contrato de ator Olá que é partilhado por clientes de Olá chamar ator Olá, pelo que, normalmente, faz sentido toodefine e de implementação de ator Olá-la numa assemblagem que é separar da implementação de ator Olá e pode ser partilhado por vários outros projetos.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **projeto de serviço de atores Olá (MyActor)**. Isto é Olá projeto utilizado toodefine Olá Service Fabric serviço actor de Olá de toohost contínuo. Implementação de Olá de ator Olá nele contidos. Uma implementação de atores é uma classe que deriva de um tipo base Olá `Actor` e implementa Olá interfaces que estão definidas no projeto de MyActor.Interfaces Olá. Uma classe de ator também tem de implementar um construtor que aceite um `ActorService` instância e um `ActorId` e transmite-os toohello base `Actor` classe. Isto permite a inserção de dependências de construtor de dependências de plataforma.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

serviço de atores Olá tem de ser registado com um tipo de serviço no tempo de execução do Olá Service Fabric. Na ordem de Olá toorun do serviço de Atores as instâncias de ator, o tipo de ator também tem de ser registado com Olá serviço de Atores. Olá `ActorRuntime` método de registo efetua este trabalho de atores.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Se iniciar a partir de um novo projeto no Visual Studio e tiver apenas uma definição de ator, registo Olá é incluído por predefinição no código Olá que gera o Visual Studio. Se definir outros atores no serviço de Olá, terá de registo de ator tooadd Olá utilizando:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Olá Atores do Service Fabric runtime emite algumas [eventos e contadores de desempenho relacionados com métodos tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Estes são úteis em diagnóstico e monitorização do desempenho.
> 
> 

## <a name="debugging"></a>Depuração
ferramentas do Service Fabric Olá para Visual Studio suportam a depuração no seu computador local. Pode iniciar uma sessão de depuração, atingir Olá tecla F5. Visual Studio cria (se necessário) pacotes. Também implementa a aplicação Olá no cluster de Service Fabric local Olá e anexa depurador Olá.

Durante o processo de implementação de Olá, pode ver o progresso de Olá na Olá **saída** janela.

![Janela de saída de depuração Service Fabric][3]

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [como Reliable Actors utilizar plataforma de Service Fabric Olá](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
