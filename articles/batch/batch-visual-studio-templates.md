---
title: "aaaStart criar soluções do Batch com modelos de projeto do Visual Studio - Azure | Microsoft Docs"
description: "Saiba como modelos de projeto do Visual Studio podem ajudá-lo de implementar e executar as cargas de trabalho intensivas de computação do Azure batch."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Utilizar as soluções do Batch de toojump start modelos do Visual Studio projeto

Olá **Gestor de tarefas** e **modelos de tarefas processador Visual Studio** Batch proporcionam toohelp de código tooimplement e execute as cargas de trabalho intensivas de computação no Batch com menos Olá quantidade de esforço. Este documento descreve estes modelos e fornece orientações para como toouse-los.

> [!IMPORTANT]
> Este artigo descreve apenas modelos de toothese aplicáveis dois de informações e parte do princípio de que está familiarizado com o serviço de Batch de Olá e tooit relacionados conceitos-chave: conjuntos, nós de computação, trabalhos e tarefas, tarefas do Gestor, variáveis de ambiente e outros informações relevantes. Pode encontrar mais informações em [Noções básicas do Azure Batch](batch-technical-overview.md), [descrição geral da funcionalidade Batch para programadores](batch-api-basics.md), e [introdução à biblioteca do Azure Batch Olá para .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Descrição geral de alto nível
modelos de Gestor de tarefas e tarefas processador Olá podem ser utilizado toocreate dois componentes úteis:

* Uma tarefa do Gestor de tarefas que implementa o divisor uma tarefa que pode dividir uma tarefa em várias tarefas que podem ser executadas de forma independente, em paralelo.
* Um processador de tarefas que pode ser utilizados tooperform pré- processamento de e pós-processamento em torno de uma linha de comandos de aplicação.

Por exemplo, num cenário de composição de filmes, Divisor da tarefa de Olá seria ativar uma tarefa de filmes único para centenas ou milhares de tarefas separadas que seriam processam frames individuais separadamente. Proporcionalmente, processadores de tarefa Olá seriam invocar Olá compor a aplicação e todos os processos dependentes que são necessário toorender cada moldura, bem como realizar quaisquer ações adicionais (por exemplo, copiar Olá composto moldura tooa localização de armazenamento).

> [!NOTE]
> modelos de Gestor de tarefas e tarefas processador Olá são independentes entre si, para que possa escolher toouse ambos ou apenas um deles, consoante os requisitos de Olá do seu trabalho de computação e nas suas preferências.
> 
> 

Como é mostrado no diagrama de Olá abaixo, uma tarefa de computação que utiliza estes modelos passarão três fases:

1. código de cliente Olá (por exemplo, aplicações, serviço web, etc.) submete uma tarefa toohello serviço Batch no Azure, especificando como respectivo programa de tarefa de Gestor do tarefa manager tarefas Olá.
2. serviço de Batch de Olá Olá tarefa do Gestor de tarefas é executada num nó de computação e hello tarefa divisor inicia Olá especificado diversas tarefas de processador de tarefas, na como muitas nós de computação conforme necessário, com base nos parâmetros de Olá e especificações no código do Olá tarefa divisor.
3. Olá tarefas processador tarefas são executadas de forma independente, em paralelo, tooprocess dados de entrada Olá e geram Olá dados de saída.

![Diagrama que mostra como o código de cliente interage com Olá serviço Batch][diagram01]

## <a name="prerequisites"></a>Pré-requisitos
modelos de Batch de Olá toouse, terá de seguinte Olá:

* Um computador com o Visual Studio 2015, instalado. Os modelos de lote são atualmente suportados apenas para o Visual Studio 2015.
* modelos de Batch de Olá, que estão disponíveis no Olá [galeria do Visual Studio] [ vs_gallery] como extensões de Visual Studio. Existem duas formas modelos de Olá tooget:
  
  * Instalar os modelos de Olá utilizando Olá **extensões e atualizações** caixa de diálogo no Visual Studio (para obter mais informações, consulte [a localizar e utilizar extensões de Visual Studio][vs_find_use_ext]). No Olá **extensões e atualizações** caixa de diálogo, procurar e transferir Olá duas extensões os seguintes:
    
    * Gestor de tarefas de lote do Azure com o divisor da tarefa
    * Processador de tarefa de lote do Azure
  * Transferir os modelos de Olá da Galeria online Olá para Visual Studio: [modelos de projeto do Microsoft Azure Batch][vs_gallery_templates]
* Se planear toouse Olá [pacotes de aplicações](batch-application-packages.md) nós de computação do Gestor de tarefas do funcionalidade toodeploy Olá e tarefas processador toohello Batch, tem de toolink um tooyour de conta de armazenamento conta do Batch.

## <a name="preparation"></a>Preparação
Recomendamos a criação de uma solução que pode conter o seu Gestor de tarefas, bem como o processador de tarefa, porque esta pode tornar mais fácil tooshare código entre o Gestor de tarefas e programas de processador de tarefas. toocreate nesta solução, siga estes passos:

1. Abra o Visual Studio e selecione **ficheiro** > **novo** > **projeto**.
2. Em **modelos**, expanda **outros tipos de projeto**, clique em **soluções do Visual Studio**e, em seguida, selecione **solução em branco**.
3. Escreva um nome que descreva o objetivo de aplicação e Olá desta solução (por exemplo, "LitwareBatchTaskPrograms").
4. toocreate Olá nova solução, clique em **OK**.

## <a name="job-manager-template"></a>Modelo de Gestor de tarefas
modelo de tarefa do Gestor de Olá ajuda tooimplement uma tarefa do Gestor de tarefas que pode realizar Olá seguintes ações:

* Divida uma tarefa em várias tarefas.
* Submeta toorun essas tarefas no Batch.

> [!NOTE]
> Para mais informações sobre o Gestor de tarefas, consulte [descrição geral da funcionalidade Batch para programadores](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Criar um Gestor de tarefas utilizando o modelo de Olá
tooadd uma solução de toohello do Gestor de tarefas que criou anteriormente, siga estes passos:

1. Abra a solução existente no Visual Studio.
2. No Explorador de soluções, solução de Olá rato, clique em **adicionar** > **novo projeto**.
3. Em **Visual c#**, clique em **nuvem**e, em seguida, clique em **Gestor de tarefas de lote do Azure com a tarefa divisor**.
4. Escreva um nome que descreve a aplicação e identifica este projeto como Gestor de tarefas Olá (por exemplo "LitwareJobManager").
5. projeto de Olá toocreate, clique em **OK**.
6. Por fim, referenciado de compilação Olá projeto tooforce Visual Studio tooload todos os pacotes NuGet e tooverify Olá projeto é válido antes de começar a modificá-lo.

### <a name="job-manager-template-files-and-their-purpose"></a>Ficheiros de modelo de Gestor de tarefas e respetivo objetivo
Quando cria um projeto com o modelo de tarefa do Gestor de Olá, gera três grupos de ficheiros de código:

* ficheiros de programa principal Olá (Program.cs). Contém o ponto de entrada do programa Olá e processamento de exceções de nível superior. Não deve normalmente terá toomodify isto.
* diretório de Framework Olá. Contém os ficheiros de Olá responsáveis pelo trabalho de 'automático' Olá efetuado pelo programa de Gestor de tarefas Olá – unpacking parâmetros, a adição de um trabalho do Batch toohello tarefas, etc. Normalmente, não deverá ser preciso toomodify estes ficheiros.
* Olá tarefa divisor o ficheiro (JobSplitter.cs). Esta é a localização onde irá colocar a lógica de aplicação específicos para dividir uma tarefa para tarefas.

Obviamente pode adicionar ficheiros adicionais conforme necessário toosupport código divisor tarefa, consoante a complexidade de Olá da tarefa de Olá dividir lógica.

o modelo de Olá também gera ficheiros de projeto .NET padrão, tais como um ficheiro. csproj, App. config, Packages, etc.

rest Olá desta secção descreve os diferentes ficheiros de Olá e respetiva estrutura de código e explica o que faz cada classe.

![Visual Studio Solution Explorer que mostra a solução de modelo de tarefa do Gestor de Olá][solution_explorer01]

**Ficheiros de Framework**

* `Configuration.cs`: Encapsula carregamento Olá tarefa dos dados de configuração, tais como os detalhes da conta do Batch, as credenciais da conta de armazenamento ligado, tarefas e informações e parâmetros da tarefa. Também fornece acesso variáveis de ambiente definidas pelo tooBatch (consulte as definições de ambiente para tarefas, na documentação de Batch de Olá) através de classe de Configuration.EnvironmentVariable Olá.
* `IConfiguration.cs`: Deduz Olá a implementação de Olá classe de configuração, para que possa unidade testar o divisor de tarefa com um objeto de configuração falsificados ou mock.
* `JobManager.cs`: Os componentes de Olá do programa de Gestor de tarefas Olá orquestra. É responsável pela Olá inicializar divisor de tarefa Olá, invocar divisor da tarefa de Olá, e emissão tarefas Olá devolvido por Olá tarefa divisor toohello submissor da tarefa de.
* `JobManagerException.cs`: Representa um erro que exige Olá tarefa manager tooterminate. JobManagerException é utilizado toowrap 'era esperado' erros onde as informações de diagnóstico específicas podem ser fornecidas como parte de terminação.
* `TaskSubmitter.cs`: Esta classe é tarefas tooadding responsável devolvidas pelo Olá tarefa divisor toohello um trabalho do Batch. classe de JobManager Olá agrega sequência Olá das tarefas em lotes para a tarefa de toohello adição eficiente mas atempada, em seguida, chama TaskSubmitter.SubmitTasks no thread de segundo plano para cada lote.

**Tarefa divisor**

`JobSplitter.cs`: Esta classe contém específicas da aplicação lógica para dividir a tarefa de Olá para tarefas. Olá framework invoca Olá JobSplitter.Split método tooobtain uma sequência de tarefas, que adiciona toohello tarefa como método de Olá devolve-os. Esta é a classe de olá onde irá inserir lógica Olá da tarefa. Implemente Olá divisão método tooreturn uma sequência de instâncias de CloudTask que representa as tarefas de Olá na qual pretende que a tarefa de Olá toopartition.

**Ficheiros de projeto de linha de comandos do padrão .NET**

* `App.config`: Ficheiro de configuração da aplicação .NET padrão.
* `Packages.config`: Ficheiro de dependência de pacote NuGet padrão.
* `Program.cs`: Contém o ponto de entrada do programa de Olá e processamento de exceções de nível superior.

### <a name="implementing-hello-job-splitter"></a>Implementar o divisor da tarefa de Olá
Quando abrir projeto de modelo de tarefa do Gestor de Olá, projeto Olá terá ficheiros de JobSplitter.cs Olá abrir por predefinição. Pode implementar Olá dividir lógica para tarefas de Olá na sua carga de trabalho utilizando mostrar de método de Split() Olá abaixo:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Olá anotado secção Olá `Split()` método é a secção apenas Olá Olá código de modelo de Gestor de tarefas que foi concebido para lhe toomodify adicionando Olá lógica toosplit as tarefas para tarefas diferentes. Se quiser toomodify secção diferente do modelo de Olá, certifique-se são familiarized com como funciona o Batch e experimente algumas das Olá [exemplos de código do Batch][github_samples].
> 
> 

A implementação de Split() tem acesso ao:

* Olá parâmetros da tarefa, através de Olá `_parameters` campo.
* Olá CloudJob objeto que representa Olá tarefa através de Olá `_job` campo.
* Olá CloudTask objeto que representa Olá tarefa do Gestor de tarefas, através de Olá `_jobManagerTask` campo.

O `Split()` implementação não precisa de tarefa de toohello tooadd tarefas diretamente. Em vez disso, o código deverá devolver uma sequência de objetos de CloudTask e estes serão adicionados toohello tarefa automaticamente por classes de estrutura de Olá invocam divisor da tarefa de Olá. É comum toouse do # iterator (`yield return`) funcionalidade splitters de tarefa tooimplement como isto permite Olá toostart de tarefas em execução logo que possível, em vez de aguardar que todas as tarefas toobe calculado.

**Falha da tarefa divisor**

Se o divisor da tarefa encontra um erro, quer devia:

* Terminar a sequência de Olá utilizando Olá c# `yield break` declaração, em que o Gestor de tarefas Olá maiúsculas e será tratado como êxito; ou
* Gerar uma exceção, em que o Gestor de tarefas Olá maiúsculas será tratado como falhado e pode ser repetido dependendo de como cliente Olá configurou-lo).

Em ambos os casos, todas as tarefas já devolvidos pelo divisor da tarefa de Olá e tarefa de lote toohello adicionada será toorun elegível. Se não pretender que esta toohappen, em seguida, pode:

* Terminar a tarefa de Olá antes da devolução do divisor da tarefa de Olá
* Formular a coleção de tarefas todo Olá antes de o devolver (ou seja, devolver um `ICollection<CloudTask>` ou `IList<CloudTask>` em vez de implementar o divisor tarefa utilizando um iterator c#)
* Utilizar toomake de dependências de tarefas todas as tarefas dependem após a conclusão com êxito Olá do Gestor de tarefas Olá

**Tentativas de Gestor de tarefas**

Se o Gestor de tarefas Olá falhar, pode ser repetida pelo serviço de Batch de Olá dependendo das definições de repetição do cliente Olá. Em geral, isto é seguro, porque quando o framework Olá adiciona uma tarefa de toohello de tarefas, ignora todas as tarefas que já existem. No entanto, esteja calcular tarefas dispendiosas, poderá não pretende custo Olá tooincur recalcular as tarefas que já foram adicionadas toohello tarefa; por outro lado, se Olá volte a executar é toogenerate não garantida Olá mesmos IDs de tarefas, em seguida, o comportamento de 'Ignorar duplicados' Olá não irá iniciar. Nestes casos deve conceber a sua tarefa divisor toodetect Olá trabalho já foi executado e repita-lo, por exemplo, efetuando uma CloudJob.ListTasks antes de iniciar tooyield tarefas.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Sair códigos e exceções no modelo de tarefa do Gestor de Olá
Códigos de saída e exceções de fornecem um mecanismo toodetermine Olá resultado executarem um programa e podem ajudar tooidentify quaisquer problemas com a execução de Olá do programa de Olá. modelo de tarefa do Gestor de Olá implementa códigos de saída Olá e exceções descritas nesta secção.

Uma tarefa do Gestor de tarefas que é implementado com o modelo de tarefa do Gestor de Olá pode devolver as três códigos de saída possíveis:

| Código | Descrição |
| --- | --- |
| 0 |Gestor de tarefas de Olá foi concluído com êxito. Código do divisor da tarefa foi executada toocompletion e todas as tarefas foram adicionadas toohello tarefa. |
| 1 |Olá tarefa do Gestor de tarefas falhou com uma exceção numa parte do programa de Olá 'esperada'. Exceção de Olá foi traduzida tooa JobManagerException com informações de diagnóstico e, sempre que possível, sugestões para resolver Olá falha. |
| 2 |Olá tarefa do Gestor de tarefas falhou com uma exceção 'inesperada'. Olá exceção foi iniciada toostandard de saída, mas o Gestor de tarefas Olá foi tooadd não é possível quaisquer informações de diagnóstico ou remediação adicionais. |

No caso de Olá de falha de tarefa do Gestor de tarefas, algumas tarefas poderão ainda ter sido adicionadas toohello serviço antes de Olá erro. Estas tarefas serão executadas como normais. Consulte "Falha de divisor da tarefa" acima para debate deste caminho de código.

Todas as informações de Olá devolvidas pelo exceções são escritas em ficheiros stdout.txt e stderr.txt. Para obter mais informações, consulte [erro processamento](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Considerações de cliente
Esta secção descreve alguns requisitos de implementação do cliente ao invocar um Gestor de tarefas com base neste modelo. Consulte [como toopass parâmetros e variáveis de ambiente de código de cliente Olá](#pass-environment-settings) para obter detalhes sobre a transmitir parâmetros e definições de ambiente.

**Credenciais obrigatórias**

Tarefa de ordem tooadd tarefas toohello do Azure Batch, Olá tarefa do Gestor de tarefas requer o URL da conta do Azure Batch e a chave. Tem de passar estes nas variáveis de ambiente com o nome YOUR_BATCH_URL e YOUR_BATCH_KEY. Pode definir estas no Gestor de tarefas de Olá definições de ambiente de tarefas. Por exemplo, num c# cliente:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Credenciais do armazenamento**

Normalmente, Olá cliente não precisa de tooprovide Olá armazenamento ligado conta credenciais toohello tarefa do Gestor de tarefas porque (a) a maioria dos gestores de tarefa não é necessário acesso de tooexplicitly Olá ligado conta de armazenamento e (b) hello conta de armazenamento ligado é frequentemente fornecida tarefas de tooall como uma definição de ambiente comuns para a tarefa de Olá. Se não está a fornecer Olá ligado a conta de armazenamento através de definições de ambiente comuns Olá e o Gestor de tarefas Olá requer acesso toolinked armazenamento, em seguida, deve fornecer as credenciais do armazenamento de Olá ligado da seguinte forma:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Definições de tarefa do Gestor de tarefas**

cliente de Olá deve definir o Gestor de tarefas Olá *killJobOnCompletion* sinalizador demasiado**falso**.

É normalmente seguro para Olá cliente tooset *runExclusive* demasiado**falso**.

cliente de Olá deve utilizar Olá *resourceFiles* ou *applicationPackageReferences* coleção toohave Olá Gestor de tarefas executável (e respetivas DLLs necessários) implementado o nó de computação toohello.

Por predefinição, o Gestor de tarefas Olá não será repetido se falhar. Consoante a lógica de Gestor de tarefas, cliente Olá poderá pretender tooenable tentativas através de *restrições*/*maxTaskRetryCount*.

**Definições da tarefa**

Se o divisor da tarefa de Olá emite tarefas com as dependências, cliente Olá tem de definir tootrue de usesTaskDependencies da tarefa de Olá.

No modelo de divisor da tarefa Olá, é pouco usual clientes toowish tooadd tarefas toojobs over and above divisor de tarefa que Olá cria. cliente de Olá, por conseguinte, deve definir normalmente da tarefa de Olá *onAllTasksComplete* demasiado**terminatejob**.

## <a name="task-processor-template"></a>Modelo de processador de tarefas
Um modelo de processador de tarefas ajuda-o a tooimplement um processador de tarefas que pode realizar Olá seguintes ações:

* Configure informações de Olá necessárias por cada toorun de tarefa do Batch.
* Execute todas as ações de cada tarefa do Batch.
* Guarde as saídas da tarefa toopersistent armazenamento.

Embora um processador de tarefas não é necessário toorun tarefas do batch, Olá das principais vantagens da utilização de um processador de tarefas é que fornece um wrapper tooimplement todas as ações de execução de tarefas numa única localização. Por exemplo, se precisar de toorun várias aplicações no contexto de Olá de cada tarefa, ou se precisar de toocopy o armazenamento de dados toopersistent depois de concluir cada tarefa.

as ações de Olá efetuadas pelo processador de tarefa Olá podem ser como simples ou complexas e como muitas ou poucos, conforme necessário, a carga de trabalho. Além disso, ao implementar todas as ações de tarefas para um processador de tarefas, pode prontamente atualizar ou adicionar ações com base nos requisitos de carga de trabalho ou tooapplications de alterações. No entanto, em alguns casos um processador de tarefas pode não ser solução ideal de Olá da implementação que pode adicionar complexidade desnecessária, por exemplo quando tarefas em execução que podem ser rapidamente iniciadas a partir de uma linha de comandos simple.

### <a name="create-a-task-processor-using-hello-template"></a>Criar um processador de tarefas utilizando o modelo de Olá
tooadd uma solução de toohello de processador de tarefas que criou anteriormente, siga estes passos:

1. Abra a solução existente no Visual Studio.
2. No Explorador de soluções, solução de Olá rato, clique em **adicionar**e, em seguida, clique em **novo projeto**.
3. Em **Visual c#**, clique em **nuvem**e, em seguida, clique em **processador de tarefa de lote do Azure**.
4. Escreva um nome que descreve a aplicação e identifica este projeto como Olá (por exemplo, o processador de tarefas "LitwareTaskProcessor").
5. projeto de Olá toocreate, clique em **OK**.
6. Por fim, referenciado de compilação Olá projeto tooforce Visual Studio tooload todos os pacotes NuGet e tooverify Olá projeto é válido antes de começar a modificá-lo.

### <a name="task-processor-template-files-and-their-purpose"></a>Ficheiros de modelo de processador de tarefa e respetivo objetivo
Quando cria um projeto com o modelo de processador de tarefa Olá, gera três grupos de ficheiros de código:

* ficheiros de programa principal Olá (Program.cs). Contém o ponto de entrada do programa Olá e processamento de exceções de nível superior. Não deve normalmente terá toomodify isto.
* diretório de Framework Olá. Contém os ficheiros de Olá responsáveis pelo trabalho de 'automático' Olá efetuado pelo programa de Gestor de tarefas Olá – unpacking parâmetros, a adição de um trabalho do Batch toohello tarefas, etc. Normalmente, não deverá ser preciso toomodify estes ficheiros.
* ficheiro de processador de tarefa de Olá (TaskProcessor.cs). Esta é a localização onde irá colocar a lógica de aplicação específicos para executar uma tarefa (normalmente por prós tooan executável de existente). Código de pré e pós-processamento, tal como a transferência de dados adicionais ou carregar ficheiros de resultado, também aqui.

Obviamente pode adicionar ficheiros adicionais conforme necessário toosupport o código de processador de tarefas, dependendo da complexidade Olá da tarefa de Olá dividir lógica.

o modelo de Olá também gera ficheiros de projeto .NET padrão, tais como um ficheiro. csproj, App. config, Packages, etc.

rest Olá desta secção descreve os diferentes ficheiros de Olá e respetiva estrutura de código e explica o que faz cada classe.

![Visual Studio Solution Explorer que mostra a solução de modelo de processador de tarefa Olá][solution_explorer02]

**Ficheiros de Framework**

* `Configuration.cs`: Encapsula carregamento Olá tarefa dos dados de configuração, tais como os detalhes da conta do Batch, as credenciais da conta de armazenamento ligado, tarefas e informações e parâmetros da tarefa. Também fornece acesso variáveis de ambiente definidas pelo tooBatch (consulte as definições de ambiente para tarefas, na documentação de Batch de Olá) através de classe de Configuration.EnvironmentVariable Olá.
* `IConfiguration.cs`: Deduz Olá a implementação de Olá classe de configuração, para que possa unidade testar o divisor de tarefa com um objeto de configuração falsificados ou mock.
* `TaskProcessorException.cs`: Representa um erro que exige Olá tarefa manager tooterminate. TaskProcessorException é utilizado toowrap 'era esperado' erros onde as informações de diagnóstico específicas podem ser fornecidas como parte de terminação.

**Processador de tarefas**

* `TaskProcessor.cs`: Executa tarefas de Olá. arquitetura de Olá invoca o método de TaskProcessor.Run Olá. Esta é a classe de olá onde irá inserir lógica de específicas da aplicação Olá da sua tarefa. Implemente o método de execução de Olá para:
  * Analisar e validar os parâmetros da tarefa
  * Componha Olá linha de comandos para qualquer programa externo pretende tooinvoke
  * Inicie sessão quaisquer informações de diagnóstico que precisa para fins de depuração
  * Iniciar um processo com essa linha de comandos
  * Aguarde Olá processo tooexit
  * Capturar o código de saída de Olá de Olá processo toodetermine se esta foi concluída com êxito ou falha
  * Guardar os ficheiros de saída que pretende tookeep toopersistent armazenamento

**Ficheiros de projeto de linha de comandos do padrão .NET**

* `App.config`: Ficheiro de configuração da aplicação .NET padrão.
* `Packages.config`: Ficheiro de dependência de pacote NuGet padrão.
* `Program.cs`: Contém o ponto de entrada do programa de Olá e processamento de exceções de nível superior.

## <a name="implementing-hello-task-processor"></a>Implementar o processador de tarefa Olá
Quando abrir projeto de modelo de processador de tarefa Olá, projeto Olá terá ficheiros de TaskProcessor.cs Olá abrir por predefinição. Pode implementar a lógica de Olá executar tarefas de Olá na sua carga de trabalho utilizando o método de Run() Olá mostrado abaixo:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Olá anotada secção Olá Run() método é secção apenas Olá código do modelo de processador de tarefa Olá que foi concebida para lhe toomodify adicionando lógica Olá executar tarefas de Olá na sua carga de trabalho. Se quiser toomodify secção diferente do modelo de Olá,. primeiro familiarizar-se com como funciona o Batch ao rever Olá Batch documentação e experimentar alguns dos exemplos de código do Batch Olá.
> 
> 

Olá Run() método é responsável por iniciar Olá linha de comandos, a partir de um ou mais processos, a aguardar que todos os processos toocomplete, guardar resultados de Olá e, finalmente, devolvendo com um código de saída. Olá Run() método é onde implementar Olá lógica para as suas tarefas de processamento. arquitetura de processador de tarefa Olá invoca o método de Run() Olá para si; Não é necessário toocall-lo por si.

A implementação de Run() tem acesso ao:

* Olá parâmetros da tarefa, através de Olá `_parameters` campo.
* Olá ids de tarefas e, através de Olá `_jobId` e `_taskId` campos.
* configuração da tarefa Olá, através de Olá `_configuration` campo.

**Falha de tarefa**

Em caso de falha, pode sair o método de Run() Olá ao gerar uma exceção, mas esta opção deixa o processador de excepções de nível superior de Olá no controlo de código de saída de tarefas Olá. Se precisar de código de saída do toocontrol Olá, de modo a que poder diferenciar os diferentes tipos de falha, por exemplo para fins de diagnóstico ou porque algumas modos de falha devem terminar tarefa Olá e outros não devem, em seguida, deve sair o método de Run() Olá devolvendo um código de saída diferente de zero. Isto torna-se o código de saída de tarefas Olá.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Sair códigos e exceções no modelo de processador de tarefa Olá
Códigos de saída e exceções de fornecem um mecanismo toodetermine Olá resultado executarem um programa e pode ajudar a identificar quaisquer problemas com a execução de Olá do programa de Olá. modelo de processador de tarefa Olá implementa códigos de saída Olá e exceções descritas nesta secção.

Uma tarefa do processador de tarefas que é implementada com o modelo de processador de tarefa Olá pode devolver as três códigos de saída possíveis:

| Código | Descrição |
| --- | --- |
| [Process.ExitCode][process_exitcode] |processador de tarefa Olá ficou toocompletion. Tenha em atenção que isto não implica desse programa Olá que é invocado foi concluída com êxito – apenas esse processador de tarefa Olá invocado-lo com êxito e efetuar qualquer processamento posterior sem exceções. significado Olá do código de saída Olá depende do programa de Olá invocado – o código de saída 0 significa habitualmente programa Olá foi concluída com êxito e outro código de saída significa Olá programa tenha falhado. |
| 1 |processador de tarefa Olá falhou com uma exceção numa parte do programa de Olá 'esperada'. Olá exceção foi tooa traduzida `TaskProcessorException` com informações de diagnóstico e, sempre que possível, sugestões para resolver Olá falha. |
| 2 |processador de tarefa Olá falhou com uma exceção 'inesperada'. Olá exceção foi iniciada toostandard de saída, mas o processador de tarefa Olá foi tooadd não é possível quaisquer informações de diagnóstico ou remediação adicionais. |

> [!NOTE]
> Se o programa Olá que invocar utiliza saída códigos 1 e 2 tooindicate falha específica modos, em seguida, utilizar códigos de saída a 1 e 2 para erros de processador de tarefas é ambígua. Pode alterar estas tarefas processador códigos toodistinctive saída códigos de erro de editando casos de exceção Olá no ficheiro Program.cs de Olá.
> 
> 

Todas as informações de Olá devolvidas pelo exceções são escritas em ficheiros stdout.txt e stderr.txt. Para obter mais informações, consulte o erro processar, no Olá documentação do Batch.

### <a name="client-considerations"></a>Considerações de cliente
**Credenciais do armazenamento**

Se o processador de tarefas utiliza saídas de toopersist ao armazenamento de Blobs do Azure, por exemplo utilizando a biblioteca de programa auxiliar de convenções de ficheiro Olá, em seguida, necessita de acesso demasiado*ou* Olá credenciais de conta de armazenamento de nuvem *ou* um URL de contentor do blob que inclui uma assinatura de acesso partilhado (SAS). modelo de Olá inclui suporte para fornecer credenciais através de variáveis de ambiente comuns. O cliente pode passar as credenciais do armazenamento de Olá da seguinte forma:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

conta de armazenamento Olá, em seguida, está disponível no Olá TaskProcessor classe através de Olá `_configuration.StorageAccount` propriedade.

Se preferir toouse um URL de contentor com SAS, também pode transmitir este através de uma definição de ambiente comuns de tarefa, mas o modelo de processador de tarefa Olá não atualmente inclui suporte incorporado para este.

**Configuração de armazenamento**

Recomenda-se que Olá cliente ou a tarefa do Gestor de tarefas criar quaisquer contentores necessários pelas tarefas antes de adicionar a tarefa de toohello Olá tarefas. Isto é obrigatório que se utilizar um URL de contentor com SAS, tal como um URL não inclui contentor de Olá toocreate de permissão. Recomenda-se, mesmo que se passa credenciais da conta de armazenamento, como ela guarda cada tarefa ter toocall CloudBlobContainer.CreateIfNotExistsAsync no contentor de Olá.

## <a name="pass-parameters-and-environment-variables"></a>Transmita os parâmetros e variáveis de ambiente
### <a name="pass-environment-settings"></a>Transmita as definições de ambiente
Um cliente pode transmitir informações toohello tarefa do Gestor de tarefas no formulário de Olá das definições de ambiente. Esta informação, em seguida, pode ser utilizada por Olá tarefa do Gestor de tarefas quando a tarefa de computação de gerar Olá tarefas processador as tarefas que serão executado como parte da Olá. Exemplos de informações de Olá que podem passar como definições de ambiente são:

* Chaves de conta e o nome de conta de armazenamento
* URL da conta de batch
* Chave de conta do batch

Olá serviço Batch tem um mecanismo simples toopass ambiente definições tooa tarefa do Gestor de tarefas utilizando Olá `EnvironmentSettings` propriedade no [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Por exemplo, tooget Olá `BatchClient` instância para uma conta do Batch, pode passar como variáveis de ambiente de cliente de Olá Olá URL de código e partilhados as credenciais da chave Olá conta de Batch. Da mesma forma, a conta de armazenamento de Olá tooaccess que está ligado a conta do Batch toohello, pode passar o nome de conta do storage Olá e chave de conta do storage Olá como variáveis de ambiente.

### <a name="pass-parameters-toohello-job-manager-template"></a>Passar o modelo de tarefa do Gestor de toohello parâmetros
Em muitos casos, é útil toopass por tarefa parâmetros toohello tarefa de gestão, a tarefa de Olá toocontrol dividir o processo ou tarefas de Olá tooconfigure para Olá tarefa. Pode fazê-lo através do carregamento de um ficheiro JSON com o nome Parameters. JSON como um ficheiro de recursos para Olá tarefa do Gestor de tarefas. parâmetros de Olá, em seguida, podem ficar disponíveis na Olá `JobSplitter._parameters` campo no modelo de tarefa do Gestor de Olá.

> [!NOTE]
> processador de parâmetro incorporada Olá suporta apenas dicionários de cadeia-cadeia. Se quiser toopass valores JSON complexos, como os valores de parâmetros, será necessário toopass como cadeias e analisá-los no divisor da tarefa de Olá ou modificar do framework Olá `Configuration.GetJobParameters` método.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Passar o modelo de processador de tarefa toohello de parâmetros
Pode também passar os parâmetros tooindividual tarefas implementadas utilizando o modelo de processador de tarefa Olá. Tal como com modelos do Gestor de tarefas de Olá, modelo de processador de tarefa Olá procura um ficheiro de recursos com o nome

Parameters. JSON e se encontrar esta carrega-o como o dicionário de parâmetros de Olá. Existem duas opções para como toopass parâmetros toohello tarefas tarefas de processador:

* Reutilize os parâmetros da tarefa Olá JSON. Isto funciona bem se parâmetros apenas Olá são ao nível da tarefa (por exemplo, uma composição altura e largura). toodo, quando criar um CloudTask no divisor da tarefa de Olá, adicionar um objeto de ficheiro de recursos do referência toohello Parameters. JSON de ResourceFiles do Olá tarefa do Gestor (`JobSplitter._jobManagerTask.ResourceFiles`) coleção ResourceFiles do toohello CloudTask.
* Gerar e carregar um documento de Parameters. JSON de específicas de tarefas como parte da execução da tarefa divisor para fazer referência a esse blob na coleção de ficheiros de recursos da tarefa de Olá. Isto é necessário se diferentes tarefas possuem parâmetros diferentes. Um exemplo pode ser um cenário de composição 3D onde o índice de moldura Olá é transmitido toohello tarefas como um parâmetro.

> [!NOTE]
> processador de parâmetro incorporada Olá suporta apenas dicionários de cadeia-cadeia. Se quiser toopass valores JSON complexos, como os valores de parâmetros, será necessário toopass como cadeias e analisá-los no processador de tarefa Olá ou modificar do framework Olá `Configuration.GetTaskParameters` método.
> 
> 

## <a name="next-steps"></a>Passos seguintes
### <a name="persist-job-and-task-output-tooazure-storage"></a>Manter a tarefa e tarefas da saída tooAzure armazenamento
Outra ferramenta útil no desenvolvimento de solução do Batch é [convenções de ficheiro do Azure Batch][nuget_package]. Utilizar esta biblioteca de classe do .NET (atualmente em pré-visualização) no arquivo de tooeasily de aplicações de .NET do Batch e obter tooand saídas de tarefa do armazenamento do Azure. [Manter a saída de tarefas e do Azure Batch](batch-task-output.md) contém um debate completo da biblioteca de Olá e a sua utilização.

### <a name="batch-forum"></a>Fórum do batch
Olá [fórum do Azure Batch] [ forum] no MSDN é ótimo colocar toodiscuss Batch e colocar questões sobre serviço Olá. HEAD na ativação pós-falha para mensagens "temporária" úteis e publique as suas perguntas que possam surgir ao criar as soluções do Batch.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
