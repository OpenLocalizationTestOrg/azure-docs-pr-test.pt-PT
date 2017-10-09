---
title: "aaaCreate um serviço fiável de Service Fabric do Azure com c#"
description: "Crie, implemente e depure uma aplicação Reliable Service compilada no Azure Service Fabric com o Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Criar a sua primeira aplicação Reliable Services sem monitorização de estado do Service Fabric em C#

Saiba como toodeploy sua primeira aplicação de Service Fabric para .NET no Windows em apenas alguns minutos. Quando tiver terminado, terá um cluster local em execução com uma aplicação do Reliable Services.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que [configurou o seu ambiente de desenvolvimento](service-fabric-get-started.md). Isto inclui a instalação Olá SDK de Service Fabric e Visual Studio 2017 ou 2015.

## <a name="create-hello-application"></a>Criar aplicação Olá

Inicie o Visual Studio como **administrador**.

Criar um projeto com `CTRL`+`SHIFT`+`N`

No Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicação de Service Fabric**.

Nome da aplicação Olá **MinhaAplicação** e prima **OK**.

   
![Caixa de diálogo de novo projeto no Visual Studio][1]

Pode criar qualquer tipo de aplicação de Service Fabric da caixa de diálogo seguinte Olá. Neste Início Rápido, escolha **Serviço Com Estado** .

Nome do serviço de Olá **MyStatefulService** e prima **OK**.

![Caixa de diálogo novo serviço no Visual Studio][2]


Visual Studio cria o projeto de aplicação Olá e projeto de serviço com estado Olá e apresenta-os no Explorador de soluções.

![Explorador de Soluções a seguir a criação da aplicação com o serviço com estado][3]

projeto de aplicação Olá (**MinhaAplicação**) não contém qualquer código diretamente. Em vez disso, referencia um conjunto de projetos de serviço. Além disso, contém outros três tipos de conteúdo:

* **Perfis de publicação**  
Perfis para a implementação de ambientes de toodifferent.

* **Scripts**  
Script do PowerShell para implementar/atualizar a sua aplicação.

* **Definição da aplicação**  
Inclui o ficheiro de ApplicationManifest.xml Olá em *ApplicationPackageRoot* que descreve a composição da sua aplicação. Os ficheiros de parâmetro de aplicação associada são em *ApplicationParameters*, que pode ser utilizado toospecify parâmetros específico do ambiente. Perfil de publicação Visual seleciona de Studio associado a um ficheiro de parâmetros de aplicação que é especificado no Olá durante ambiente específico de tooa de implementação.
    
Para obter uma descrição geral do conteúdo de Olá do projeto de serviço Olá, consulte [introdução a Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Implementar e depurar a aplicação Olá

Agora que tem uma aplicação, execute-a.

No Visual Studio, prima `F5` aplicação de Olá toodeploy de depuração.

>[!NOTE]
>Olá pela primeira vez, executar e implementar a aplicação de Olá localmente, Visual Studio cria um cluster local para a depuração. Esta operação pode demorar algum tempo. o estado de criação do cluster Olá é apresentado na janela de saída do Visual Studio Olá.

Quando Olá cluster estiver pronto, receberá uma notificação de Olá local cluster sistema tabuleiro a aplicação do manager incluída com Olá SDK.
   
![Notificação do tabuleiro de sistema do cluster local][4]

Uma vez iniciado o aplicação Olá, Visual Studio automaticamente aparece Olá **Visualizador de eventos de diagnóstico**, onde pode ver os resultados de rastreio do seu serviços.
   
![Visualizador de eventos de diagnóstico][5]

Olá modelo de serviço com estado utilizámos simplesmente mostra um valor de contador incrementando no Olá `RunAsync` método **MyStatefulService.cs**.

Expanda um dos Olá eventos toosee mais detalhes, incluindo o nó de olá onde código Olá está em execução. Neste caso, é \_Nó\_, embora possa ser diferente no seu computador.
   
![Detalhe do visualizador de eventos de diagnóstico][6]

cluster local Olá contém cinco nós alojados num único computador. Num ambiente de produção, cada nó é alojada num computador físico ou virtual diferente. perda de Olá toosimulate de uma máquina ao exercising Olá Visual Studio debugger em Olá mesmo tempo, desativemos um de nós de Olá no cluster local Olá.

No Olá **Explorador de soluções** janela, abra **MyStatefulService.cs**. 

Determinar Olá `RunAsync` método e o conjunto de um ponto de interrupção na linha de primeiro Olá do método Olá.

![Método RunAsync com ponto de interrupção do serviço com estado ][7]

Iniciar Olá **Service Fabric Explorer** ferramenta clicando no Olá **Gestor de clusters locais** aplicação de tabuleiro de sistema e escolha **gerir Cluster Local**.

![Iniciar o Explorador de recursos de infraestrutura de serviço de Olá Gestor de clusters locais][systray-launch-sfx]

O [**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) oferece uma representação visual de um cluster. Inclui o conjunto de Olá de aplicações implementadas tooit e conjunto de Olá nós físicos que o constituem.

No painel esquerdo Olá, expanda **Cluster > nós** e localizar Olá nó onde o código está em execução.

Clique em **ações > desativar (reiniciar)** toosimulate um reinício do computador.

![Parar um nó no Service Fabric Explorer][sfx-stop-node]

Momentaneamente, deverá ver o ponto de interrupção atingido no Visual Studio, como o cálculo de Olá que estava a fazer num nó totalmente integrada a ativação pós-falha tooanother.


Em seguida, devolver toohello Visualizador de eventos de diagnóstico e observe mensagens hello. contador Olá tem continuou incrementando, apesar de eventos de Olá, na verdade, provenientes de um nó diferente.

![Visualizador de eventos de diagnóstico após falha][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>A limpar cluster local Olá (opcional)

Lembre-se de que este cluster local é real. Parar o depurador Olá remove a instância da aplicação e tipo de aplicação Olá anula o registo. No entanto, o cluster de Olá continua toorun em segundo plano de Olá. Quando tiver um cluster local do toostop pronto Olá, existem algumas opções.

### <a name="keep-application-and-trace-data"></a>Manter os dados da aplicação e de rastreio

Encerrar o cluster de Olá clicando no Olá **Gestor de clusters locais** aplicação de tabuleiro de sistema e, em seguida, escolha **parar Cluster Local**.

### <a name="delete-hello-cluster-and-all-data"></a>Eliminar cluster Olá e todos os dados

Remover cluster Olá clicando no Olá **Gestor de clusters locais** aplicação de tabuleiro de sistema e, em seguida, escolha **remover Cluster Local**. 

Se escolher esta opção, o Visual Studio irá Reimplementar Olá de cluster Olá próxima vez que a execução Olá aplicação. Selecione esta opção se não tenciona cluster local do toouse Olá durante algum tempo ou se precisar de tooreclaim recursos.

## <a name="next-steps"></a>Passos seguintes
Leia mais sobre o [Reliable Services](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
