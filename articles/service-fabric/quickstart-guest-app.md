---
title: "Implementar rapidamente uma aplicação já existente num cluster do Azure Service Fabric"
description: "Utilize um cluster do Azure Service Fabric para alojar uma aplicação Node.js já existente com o Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 3601b73872bbea4b4e5324382eb97b7384ca6e13
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Alojar uma aplicação Node.js no Azure Service Fabric

Este início rápido ajuda-o a implementar uma aplicação já existente (Node.js, neste exemplo) num cluster do Service Fabric em execução no Azure.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que [configurou o seu ambiente de desenvolvimento](service-fabric-get-started.md). A configuração inclui instalar o Service Fabric SDK e o Visual Studio 2017 ou 2015.

Também precisa de uma aplicação Node.js já existente para implementação. Este início rápido utiliza um Web site Node.js simples, que pode ser transferido [aqui][download-sample]. Extraia este ficheiro para a pasta `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` depois de criar o projeto no passo seguinte.

Se não tiver uma subscrição do Azure, crie uma [conta gratuita][create-account].

## <a name="create-the-service"></a>Criar o serviço

Inicie o Visual Studio como **administrador**.

Criar um projeto com `CTRL`+`SHIFT`+`N`

Na caixa de diálogo **Novo Projeto**, escolha **Cloud > Aplicação do Service Fabric**.

Dê o nome **MyGuestApp** à aplicação e prima **OK**.

>[!IMPORTANT]
>O Node.js consegue exceder facilmente o limite do Windows de 260 carateres para caminhos. Utilize um caminho curto para o projeto, como **c:\code\svc1**.
   
![Caixa de diálogo de novo projeto no Visual Studio][new-project]

Pode criar qualquer tipo de serviço do Service Fabric na caixa de diálogo seguinte. Neste início rápido, escolha **Executável Convidado**.

Dê o nome **MyGuestService** ao serviço e defina as opções à direita com os valores seguintes:

| Definição                   | Valor |
| ------------------------- | ------ |
| Pasta do Pacote de Código       | _&lt;a pasta com a sua aplicação Node.js&gt;_ |
| Comportamento do Pacote de Código     | Copiar os conteúdos da pasta para o projeto |
| Programa                   | node.exe |
| Argumentos                 | server.js |
| Pasta de Trabalho            | CodePackage |

Prima **OK**.

![Caixa de diálogo novo serviço no Visual Studio][new-service]

O Visual Studio cria o projeto de aplicação e o projeto de serviço de ator e apresenta-os no Explorador de Soluções.

O projeto de aplicação (**MyGuestApp**) não contém nenhum código diretamente. Em vez disso, referencia um conjunto de projetos de serviço. Além disso, contém outros três tipos de conteúdo:

* **Perfis de publicação**  
Preferências de ferramentas para diferentes ambientes.

* **Scripts**  
Script do PowerShell para implementar/atualizar a sua aplicação.

* **Definição da aplicação**  
Inclui o manifesto da aplicação em *ApplicationPackageRoot*. Os ficheiros de parâmetro de aplicação associados em *ApplicationParameters*, definem a aplicação e permitem configurá-la especificamente para um determinado ambiente.
    
Para obter uma descrição geral do conteúdo do projeto de serviço, consulte o artigo [Introdução a Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Configurar a rede

A aplicação Node.js de exemplo que estamos a implementar utiliza a porta **80** e temos de dizer ao Service Fabric que esta porta tem de estar exposta.

Abra o ficheiro **ServiceManifest.xml** no projeto. Na parte inferior do manifesto, há um `<Resources> \ <Endpoints>` com uma entrada já definida. Modifique essa entrada para adicionar `Port`, `Protocol` e `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a>Implementar no Azure

Se premir **F5** e executar o projeto, este é implementado no cluster local. No entanto, vamos implementar no Azure.

Clique com o botão direito do rato no projeto e escolha **Publicar...**, o que abre uma caixa de diálogo para publicar no Azure.

![Caixa de diálogo Publicar no Azure para um serviço do Service Fabric][publish]

Selecione o perfil de destino **PublishProfiles\Cloud.xml**.

Se ainda não o tiver feito, escolha uma conta do Azure na qual implementar. Se ainda não tiver uma, [inscreva-se numa][create-account].

Em **Ponto Final da Ligação**, selecione o cluster do Service Fabric no qual implementar. Se não tiver um cluster, selecione **&lt;Criar Novo Cluster...&gt;**, o que abre uma janela do browser para o portal do Azure. Para obter mais informações, veja [Create a cluster in the portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) (Crair um cluster no portal). 

Quando criar o cluster do Service Fabric, confirme que define a definição **Pontos finais personalizados** como **80**.

![Configuração de tipo de nó do Service Fabric com ponto final personalizado][custom-endpoint]

A criação de um cluster do Service Fabric novo demora algum tempo a ser concluída. Quando tiver sido criada, regresse à caixa de diálogo e selecione **&lt;Atualizar&gt;**. O cluster novo é apresentado na caixa pendente; selecione-o.

Prima **publicar** e aguarde pela conclusão da implementação.

Esta operação poderá demorar alguns minutos. Depois de terminar, pode demorar alguns minutos para que a aplicação fique totalmente disponível.

## <a name="test-the-website"></a>Testar o Web site

Depois de o serviço ser publicado, teste-o num browser. 

Em primeiro lugar, abra o portal do Azure e localize o seu serviço do Service Fabric.

Verifique o painel de descrição geral do endereço do serviço. Utilize o nome de domínio da propriedade _Ponto final de ligação do cliente_. Por exemplo, `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Painel de descrição geral do Service Fabric no portal do Azure][overview]

Navegue para este endereço, onde vai ver a resposta `HELLO WORLD`.

## <a name="delete-the-cluster"></a>Eliminar o cluster

Não se esqueça de eliminar todos os recursos que criou para este início rápido, uma vez que lhe são cobrados.

## <a name="next-steps"></a>Passos seguintes
Leia mais sobre os [executáveis convidados](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F