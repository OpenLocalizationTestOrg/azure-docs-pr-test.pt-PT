---
title: "aaaDeploy uma aplicação de Service Fabric do Azure com a integração contínua (Team Services) | Microsoft Docs"
description: "Saiba como tooset integração contínua e implementação para uma aplicação de Service Fabric com o Visual Studio Team Services.  Implemente um cluster do Service Fabric tooa aplicação no Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Implementar uma aplicação com o cluster do Service Fabric CI/CD tooa
Este tutorial faz parte três de uma série e descreve como tooset integração contínua e implementação para uma aplicação de Service Fabric do Azure utilizando o Visual Studio Team Services.  É necessária uma aplicação de Service Fabric existente, a aplicação Olá criado no [compilar uma aplicação .NET](service-fabric-tutorial-create-dotnet-app.md) é utilizada como exemplo.

Na parte três série Olá, saiba como:

> [!div class="checklist"]
> * Adicione o projeto de tooyour de controlo de origem
> * Criar uma definição de compilação nos serviços de equipa
> * Criar uma definição de versão no Team Services
> * Implementar e atualizar uma aplicação automaticamente

Este tutorial série, a saber como:
> [!div class="checklist"]
> * [Criar uma aplicação .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * [Implementar Olá aplicação tooa remoto cluster](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Configurar CI/CD utilizando o Visual Studio Team Services

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial:
- Se não tiver uma subscrição do Azure, crie um [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Instalar Visual Studio 2017](https://www.visualstudio.com/) e instalar Olá **programação do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.
- [Instalar Olá SDK de Service Fabric](service-fabric-get-started.md)
- Criar uma aplicação de Service Fabric, por exemplo, [seguir este tutorial](service-fabric-tutorial-create-dotnet-app.md). 
- Criar um cluster do Windows Service Fabric no Azure, por exemplo, [seguir este tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)
- Criar um [conta Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Transferir a aplicação de exemplo Olá voto
Se não criar aplicação de exemplo Olá voto [parte de um desta série tutorial](service-fabric-tutorial-create-dotnet-app.md), poderá transferi-lo. Numa janela de comandos, execute Olá os seguintes comandos tooclone Olá exemplo aplicação repositório tooyour computador local.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Preparar um perfil de publicação
Agora que já [criado uma aplicação](service-fabric-tutorial-create-dotnet-app.md) e ter [implementado Olá aplicação tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), está pronto tooset a integração contínua.  Em primeiro lugar, prepare um perfil de publicação na sua aplicação para utilização pelo processo de implementação de Olá que é executada num Team Services.  perfil de publicação de Olá deve ser o cluster de Olá tootarget configurado que criou anteriormente.  Inicie o Visual Studio e abrir um projeto de aplicação de Service Fabric existente.  No **Explorador de soluções**, aplicação Olá com o botão direito e selecione **publicar...** .

Escolha um perfil de destino dentro da sua toouse do projeto de aplicação para o fluxo de trabalho de integração contínua, por exemplo na nuvem.  Especifique o ponto final de ligação de cluster Olá.  Verifique Olá **Olá atualização aplicação** caixa de verificação para que a aplicação atualiza para cada implementação nos serviços de equipa.  Clique em Olá **guardar** hyperlink toosave Olá definições toohello perfil de publicação e, em seguida, clique em **Cancelar** caixa de diálogo de Olá tooclose.  

![Perfil de push][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Partilhar o Visual Studio solução tooa nova equipa serviços repositório do Git
Partilhe os ficheiros de origem da aplicação tooa o projeto de equipa no Team Services, pelo que pode gerar baseia-se.  

Criar um novo repositório de Git local para o seu projeto, selecionando **adicionar tooSource controlo** -> **Git** na barra de estado de Olá no canto direito inferior Olá do Visual Studio. 

No Olá **Push** ver no **equipa Explorer**, selecione Olá **publicar repositório de Git** botão em **Push tooVisual Studio Team Services**.

![Repositório de Git de push][push-git-repo]

Verifique o seu e-mail e selecione a sua conta em Olá **equipa dos serviços de domínio** pendente. Introduza o nome do seu repositório e selecione **publicar repositório**.

![Repositório de Git de push][publish-code]

Publicar o repositório de Olá cria um novo projeto de equipa na sua conta com o mesmo nome como repositório local Olá de Olá. repositório de Olá toocreate num projeto de equipa existente, clique em **avançadas** seguinte demasiado**repositório** nome e selecione um projeto de equipa. Pode ver o código na web Olá, selecionando **vê-la na web Olá**.

## <a name="configure-continuous-delivery-with-vsts"></a>Configurar a entrega contínua com VSTS
Uma definição de compilação Team Services descreve um fluxo de trabalho é composto por um conjunto de passos de compilação que são executados sequencialmente. Crie uma definição de compilação que produz um pacote de aplicação de Service Fabric e outros artefactos, o cluster do Service Fabric toodeploy tooa. Saiba mais sobre [Team Services criar definições](https://www.visualstudio.com/docs/build/define/create). 

Uma definição de versão Team Services descreve um fluxo de trabalho que implementa um cluster de tooa do pacote de aplicação. Quando utilizado em conjunto, Olá Criar definição e executar a definição da versão Olá fluxo de trabalho completo começadas tooending de ficheiros de origem com uma aplicação em execução no seu cluster. Saiba mais sobre os serviços da equipa [versão definições](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-build-definition"></a>Criar uma definição de compilação
Abra um browser e navegue tooyour novo projeto de equipa em: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Selecione Olá **compilar & versão** separador, em seguida, **baseia-se**, em seguida, **+ nova definição**.  No **selecionar um modelo**, selecione Olá **aplicação do Azure Service Fabric** modelo e clique em **aplicar**. 

![Escolha o modelo de compilação][select-build-template] 

Olá votar aplicação contém um projeto de .NET Core, por isso, adicione uma tarefa que restaura dependências Olá. No Olá **tarefas** visualizar, selecione **+ adicionar tarefa** na parte inferior de Olá à esquerda. Procurar em tarefas de linha de comandos "Linha de comandos" toofind Olá, em seguida, clique em **adicionar**. 

![Adicionar tarefa][add-task] 

Tarefa de novo Olá, introduza "Executar dotnet.exe" **nome a apresentar**, "dotnet.exe" no **ferramenta**e "restaurar" na **argumentos**. 

![Nova tarefa][new-task] 

No Olá **Acionadores** ver, clique em Olá **ativar este acionador** comutador em **integração contínua**. 

Selecione **Guardar & fila** e introduza "VS2017 alojado" como Olá **fila agente**. Selecione **fila** toomanually iniciar uma compilação.  Baseia-se também acionadores na emissão ou entrada.

toocheck o progresso de compilação, o comutador toohello **compilações** separador.  Depois de verificar que a compilação de Olá executa com êxito, defina uma definição de versão que implementa o cluster de tooa de aplicação. 

### <a name="create-a-release-definition"></a>Criar uma definição de versão  

Selecione Olá **compilar & versão** separador, em seguida, **versões**, em seguida, **+ nova definição**.  No **criar versão definição**, selecione Olá **implementação de recursos de infraestrutura do serviço de Azure** modelo na lista de Olá e clique em **seguinte**.  Selecione Olá **criar** de origem, verifique Olá **a implementação contínua** caixa e clique em **criar**. 

No Olá **ambientes** ver, clique em **adicionar** toohello à direita dos **ligação de Cluster**.  Especifique um nome de ligação de "mysftestcluster", um ponto final de cluster do "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" e Olá do Azure Active Directory ou credenciais de certificado para o cluster de Olá. Para as credenciais do Azure Active Directory, definir credenciais Olá pretende toouse tooconnect toohello cluster Olá **Username** e **palavra-passe** campos. Para autenticação baseada em certificado, defina Olá Base64 codificação de ficheiro de certificado de cliente Olá no Olá **certificado de cliente** campo.  Consulte o menu de pop-up Olá ajuda sobre esse campo para informações sobre como tooget valor.  Se o certificado é protegido por palavra-passe, definir palavra-passe de Olá Olá **palavra-passe** campo.  Clique em **guardar** definição de versão de Olá toosave.

![Adicionar ligação de cluster][add-cluster-connection] 

Clique em **executar no agente**, em seguida, selecione **alojado VS2017** para **fila implementação**. Clique em **guardar** definição de versão de Olá toosave.

![Executar no agente][run-on-agent]

Selecione **+ versão** -> **criar versão** -> **criar** toomanually de criar uma versão.  Certifique-se de que implementação de Olá concluída com êxito e aplicação Olá está em execução no cluster de Olá.  Abra um browser e navegue demasiado[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Tenha em atenção a versão da aplicação Olá, neste exemplo é "1.0.0.20170616.3". 

## <a name="commit-and-push-changes-trigger-a-release"></a>Consolide e emita consolidações de alterações, acionar uma versão
tooverify Olá pipeline de integração contínua está a funcionar, verificando em algumas alterações de código tooTeam serviços.    

À medida que escreve o seu código, as alterações são automaticamente registadas pelo Visual Studio. Consolidar alterações tooyour repositório local do Git selecionando Olá pendentes (de ícone de alterações![Pendente][pending]) a partir da barra de estado de Olá na parte inferior do Olá à direita.

No Olá **alterações** ver no Explorador de equipa, adicione uma mensagem que descrevem a atualização e consolidar as alterações.

![Consolidar todas][changes]

Ícone de barra de estado das alterações não publicadas Olá selecione (![anulou a publicação de alterações][unpublished-changes]) ou Olá vista de sincronização no Explorador de equipa. Selecione **Push** tooupdate código na equipa de serviços/do TFS.

![Envie as alterações][push]

Enviar Olá alterações tooTeam serviços automaticamente acionadores uma compilação.  Quando a definição de compilação de Olá concluir com êxito, uma versão é criada automaticamente e inicia a atualizar a aplicação Olá no cluster de Olá.

toocheck o progresso de compilação, o comutador toohello **compilações** separador **equipa Explorer** no Visual Studio.  Depois de verificar que a compilação de Olá executa com êxito, defina uma definição de versão que implementa o cluster de tooa de aplicação.

Certifique-se de que implementação de Olá concluída com êxito e aplicação Olá está em execução no cluster de Olá.  Abra um browser e navegue demasiado[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Tenha em atenção a versão da aplicação Olá, neste exemplo é "1.0.0.20170815.3".

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Atualizar aplicação Olá
Efetue alterações de código na aplicação Olá.  Guarde e consolidar alterações de Olá, seguindo os passos anteriores Olá.

Depois de atualizar o Olá Olá aplicação começar, pode ver o progresso da atualização no Service Fabric Explorer Olá:

![Service Fabric Explorer][sfx2]

atualização da aplicação Olá poderá demorar vários minutos. Quando a atualização de Olá estiver concluída, Olá aplicação será executada versão seguinte Olá.  Neste exemplo, "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Adicione o projeto de tooyour de controlo de origem
> * Criar uma definição de compilação
> * Criar uma definição de versão
> * Implementar e atualizar uma aplicação automaticamente

Agora que implementou uma aplicação e configurar a integração contínua, experimente o seguinte Olá:
- [Atualizar uma aplicação](service-fabric-application-upgrade.md)
- [Testar uma aplicação](service-fabric-testability-overview.md) 
- [Monitorizar e diagnosticar](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png