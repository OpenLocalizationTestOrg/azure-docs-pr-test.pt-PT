---
title: "aaaCreate sua primeira aplicação de Service Fabric em c# | Microsoft Docs"
description: "Introdução toocreating uma aplicação do Microsoft Azure Service Fabric com serviços sem monitorização de estado e com monitorização de estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Introdução ao Reliable Services
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-services-quick-start.md)
> * [Java em Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Uma aplicação do Azure Service Fabric contém um ou mais serviços com o seu código. Este guia mostra como toocreate sem monitorização de estado e com monitorização de estado aplicações de Service Fabric com [Reliable Services](service-fabric-reliable-services-introduction.md).  Este vídeo Microsoft Virtual Academy mostra também como toocreate um serviço fiável sem monitorização de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Conceitos básicos
tooget começar Reliable Services, apenas é necessário toounderstand alguns conceitos básicos:

* **Tipo de serviço**: Esta é a implementação de serviço. Está definido por classe de Olá escreve que expande `StatelessService` e quaisquer outras código ou dependências utilizadas nas mesmas, juntamente com um nome e um número de versão.
* **Com o nome de instância de serviço**: toorun seu serviço, criar instâncias nomeadas do seu tipo de serviço, muito como criar instâncias do objecto de um tipo de classe. Uma instância de serviço tem um nome de formato Olá de um URI utilizando Olá "fabric: /" esquema, tal como "fabric: / MyApp/MyService".
* **Anfitrião do serviço**: Olá com o nome de instâncias de serviço criar necessidade toorun dentro de um processo de anfitrião. anfitrião do serviço Olá é apenas um processo em que podem executar instâncias do seu serviço.
* **Serviço de registo**: registo reúne tudo. Olá o tipo de serviço tem de ser registado com Olá Service Fabric runtime num serviço alojem tooallow Service Fabric toocreate instâncias do mesmo toorun.  

## <a name="create-a-stateless-service"></a>Criar um serviço sem monitorização de estado
Um serviço sem monitorização de estado é um tipo de serviço que está atualmente a norma de Olá em aplicações na nuvem. Considera-se sem monitorização de estado porque o serviço de Olá propriamente dito não contém dados que precisam de toobe armazenados de forma fiável ou tornado de elevada. Se uma instância de um serviço sem monitorização de estado foi encerrado, todos os respetivo estado interno é perdido. Este tipo de serviço, estado tem de ser tooan persistente arquivo externo, como tabelas do Azure ou uma base de dados do SQL Server para o mesmo toobe efetuada e de elevada disponibilidade fiável.

Inicie o Visual Studio 2015 ou Visual Studio 2017 como administrador e criar um novo projeto de aplicação de Service Fabric com o nome *Olámundo*:

![Utilizar toocreate de caixa de diálogo Olá novo projeto uma nova aplicação de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Em seguida, criar um projeto de serviço sem monitorização de estado com o nome *HelloWorldStateless*:

![Na caixa de diálogo segundo Olá, crie um projeto de serviço sem monitorização de estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Agora, a sua solução contém dois projetos:

* *Olámundo*. Este é Olá *aplicação* projeto que contém o *serviços*. Também contém o manifesto da aplicação Olá que descreve a aplicação Olá, bem como um número de scripts do PowerShell que o ajudam a toodeploy a aplicação.
* *HelloWorldStateless*. Este é o projeto de serviço Olá. Implementação de serviço sem monitorização de estado de Olá nele contidos.

## <a name="implement-hello-service"></a>Implementar o serviço de Olá
Abra Olá **HelloWorldStateless.cs** ficheiros no projeto de serviço Olá. No Service Fabric, um serviço pode ser executado qualquer lógica empresarial. API do serviço Olá fornece dois pontos de entrada para o seu código:

* Um método de ponto de entrada open-ended, denominado *runasync com*, onde pode começar a executar quaisquer cargas de trabalho, incluindo as cargas de trabalho de computação de execução longa.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Um ponto de entrada de comunicação em que pode plug-in a pilha de comunicação de escolha, tal como ASP.NET Core. Este é onde pode começar a receber pedidos de utilizadores e outros serviços.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

Neste tutorial, iremos irá focar-se no Olá `RunAsync()` o método de ponto de entrada. Este é onde imediatamente pode começar a executar o seu código.
modelo de projeto Olá inclui uma implementação de exemplo de `RunAsync()` que incrementa uma contagem graduais.

> [!NOTE]
> Para obter mais informações sobre como pilha toowork com uma comunicação, consulte [serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>Runasync com
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

plataforma de Olá chama este método quando uma instância de um serviço é tooexecute pronto e colocá-la. Para um serviço sem monitorização de estado, basta que significa quando a instância de serviço Olá é aberta. Um token de cancelamento é fornecido toocoordinate quando a instância de serviço tem toobe fechado. No Service Fabric, este ciclo de abertura/fecho de uma instância de serviço pode ocorrer demasiadas vezes ao longo da duração Olá de serviço Olá como um todo. Esta situação pode ocorrer por vários motivos, incluindo:

* sistema de Olá move as instâncias de serviço para balanceamento de recurso.
* Falhas ocorrerem no seu código.
* aplicação Olá ou do sistema está atualizado.
* hardware subjacente Olá sofre uma falha.

Esta orquestração é gerida pelo Olá sistema tookeep seu serviço altamente disponível e corretamente equilibrado.

`RunAsync()`não deverá bloquear forma síncrona. A implementação de runasync com deve devolver uma tarefa ou await em quaisquer operações demoradas ou bloqueio tooallow Olá runtime toocontinue. Tome nota na Olá `while(true)` ciclo no exemplo anterior Olá, uma tarefa-returning `await Task.Delay()` é utilizado. Se a carga de trabalho tem bloquear de forma síncrona, deve agendar uma nova tarefa com `Task.Run()` no seu `RunAsync` implementação.

O cancelamento da sua carga de trabalho é um esforço cooperative orquestrado por Olá fornecido o token de cancelamento. sistema Olá espera que o tooend de tarefas (por conclusão com êxito, cancelamento ou falhas) antes de se move. É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `RunAsync()` mais rapidamente possível ao sistema de Olá pedidos de cancelamento.

Neste exemplo de serviço sem monitorização de estado, contagem de Olá é armazenada numa variável local. Mas porque se trata de um serviço sem monitorização de estado, o valor de Olá armazenados existe apenas para Olá atual do ciclo de vida da respetiva instância de serviço. Quando move ou reinicia o serviço de Olá, o valor de Olá é perdido.

## <a name="create-a-stateful-service"></a>Criar um serviço com estado
Serviço de recursos de infraestrutura apresenta um novo tipo de serviço que tem o estado monitorizado. Um serviço com estado pode manter o estado Olá próprio serviço, localizado conjuntamente com o código de Olá que está a ser utilizado de forma fiável. Estado é efetuado elevado pelo Service Fabric sem Olá necessidade toopersist tooan externo armazenamento de Estados.

tooconvert um valor de contador de toohighly sem monitorização de estado disponível e persistente, mesmo quando o serviço de Olá move ou reinicia, precisa de um serviço com monitorização de estado.

No Olá mesmo *Olámundo* aplicação, pode adicionar um novo serviço clicando em referências de serviços de Olá no projeto de aplicação Olá e selecionando **adicionar -> novo serviço de recursos de infraestrutura de serviço**.

![Adicionar uma aplicação de Service Fabric de tooyour de serviço](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Selecione **serviço de monitorização de estado** e dê-lhe nome *HelloWorldStateful*. Clique em **OK**.

![Utilizar toocreate de caixa de diálogo Olá novo projeto um novo serviço de monitorização de estado de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

A aplicação deve agora ter dois serviços: Olá sem estado *HelloWorldStateless* e o serviço com estado Olá *HelloWorldStateful*.

Um serviço com estado tem Olá mesmo pontos de entrada como um serviço sem estado. Olá principal diferença é a disponibilidade de Olá de um *fornecedor de estado* que pode armazenar o estado de forma fiável. Service Fabric inclui uma implementação do fornecedor de estado chamada [coleções fiável](service-fabric-reliable-services-reliable-collections.md), que lhe permite criar estruturas de dados replicados através de Olá fiável Gestor de estado. Um serviço fiável com monitorização de estado utiliza este fornecedor de estado por predefinição.

Abra **HelloWorldStateful.cs** no *HelloWorldStateful*, que contém Olá método runasync com os seguintes:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>Runasync com
`RunAsync()`funciona da mesma forma nos serviços de monitorização de estado e sem monitorização de estado. No entanto, num serviço com monitorização de estado, plataforma Olá executa tarefas adicionais em seu nome antes de ser executada `RunAsync()`. Este trabalho pode incluir a garantir que esse Olá fiável Gestor de estado e fiável coleções são toouse pronto.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Fiável coleções e Olá fiável Gestor de estado
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) é uma implementação de dicionário que pode utilizar o estado de arquivo de tooreliably no serviço de Olá. Com o Service Fabric e fiável de coleções, pode armazenar dados diretamente no seu serviço sem necessidade de Olá para um arquivo persistente externo. Coleções fiáveis tornar os dados de elevada disponibilidade. Service Fabric executa esta operação através da criação e gestão de vários *réplicas* do seu serviço para si. Também fornece uma API que deduz complexidades Olá away de gerir as réplicas e os respetivos transições de estado.

Coleções fiáveis podem armazenar qualquer tipo de .NET, incluindo os tipos personalizados, com algumas limitações:

* Recursos de infraestrutura de serviço faz com que o seu estado altamente disponível *replicar* Estado em nós e coleções fiável armazenar o disco de toolocal dados em cada réplica. Isto significa que tudo o que é armazenado em coleções fiável tem de ser *serializável*. Por predefinição, utilize coleções fiável [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para serialização, por isso, é importante toomake se de que os tipos de [suportado pelo serializador de contrato de dados de Olá](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando utilizar a predefinição de Olá serializador.
* Objetos são replicados para elevada disponibilidade ao consolidar transações em coleções fiável. Objetos armazenados em coleções fiável são mantidos na memória local no seu serviço. Isto significa que tem um objeto de toohello de referência local.
  
   É importante que não mutate locais instâncias desses objetos sem efetuar uma operação de atualização na coleção fiável Olá numa transação. Isto acontece porque as alterações toolocal instâncias de objetos não serão replicadas automaticamente. Tem de inserir novamente objeto Olá no dicionário de Olá ou utilize um dos Olá *atualizar* os métodos no dicionário de Olá.

Olá fiável Gestor de estado gere coleções fiável para si. Pode simplesmente colocar Olá fiável Gestor de estado para uma coleção fiável pelo nome em qualquer altura e em qualquer lugar no seu serviço. Olá fiável Gestor de estado garante que obtém uma referência de volta. Não recomendamos que guarde referências tooreliable instâncias de coleção de variáveis de membros de classe ou propriedades. Especial deve ter cuidado tooensure Olá referência está definida tooan instância sempre no ciclo de vida do Olá serviço. Olá fiável Gestor de estado processa este trabalho por si e está otimizado para visitas de repetições.

### <a name="transactional-and-asynchronous-operations"></a>Operações transacionais e assíncronas
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Coleções fiáveis tem muitas das Olá mesmas operações que os respetivos `System.Collections.Generic` e `System.Collections.Concurrent` homólogos, exceto LINQ. As operações em coleções fiável são assíncronas. Isto acontece porque as operações de escrita de coleções fiável efetuar tooreplicate de operações de e/s e manter toodisk de dados.

As operações de coleção fiável *transacional*, para que pode manter estado consistente em vários coleções fiável e operações. Por exemplo, pode anular um item de trabalho a partir de uma fila fiável, efetuar uma operação no mesmo e guardar o resultado de Olá num Dictionary fiável, tudo dentro de uma única transação. Esta é tratada como uma operação Atómica e garante que a operação todo Olá terá êxito ou irá reverter operação todo Olá. Se ocorrer um erro depois de anular o item de Olá, mas antes de guardar o resultado de Olá, transação todo Olá é revertida e item Olá permanece na fila de Olá para processamento.

## <a name="run-hello-application"></a>Executar a aplicação Olá
Vamos voltar agora toohello *Olámundo* aplicação. Agora pode compilar e implementar os seus serviços. Quando prime **F5**, a aplicação será cluster local tooyour criados e implementados.

Após Olá do início em execução, pode ver eventos de rastreio de eventos para o Windows (ETW) Olá gerado por um **eventos de diagnóstico** janela. Tenha em atenção que os eventos de Olá apresentados são de serviço sem estado Olá e o serviço com estado de Olá na aplicação Olá. Pode colocar em pausa o fluxo de Olá clicando Olá **colocar em pausa** botão. Em seguida, pode examinar os detalhes de Olá de uma mensagem expandindo essa mensagem.

> [!NOTE]
> Antes de executar a aplicação Olá, certifique-se de que tem um cluster de desenvolvimento local em execução. Veja Olá [guia de introdução](service-fabric-get-started.md) para obter informações sobre como configurar o ambiente local.
> 
> 

![Ver eventos de diagnóstico no Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Passos seguintes
[Depurar a aplicação de Service Fabric no Visual Studio](service-fabric-debugging-your-application.md)

[Começar a: serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md)

[Saiba mais sobre coleções fiável](service-fabric-reliable-services-reliable-collections.md)

[Implementar uma aplicação](service-fabric-deploy-remove-applications.md)

[Atualização da aplicação](service-fabric-application-upgrade.md)

[Referência para programadores para Reliable Services](https://msdn.microsoft.com/library/azure/dn706529.aspx)

