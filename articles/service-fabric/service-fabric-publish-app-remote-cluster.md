---
title: "aaaPublish cluster remoto de tooa de aplicação com o Visual Studio | Microsoft Docs"
description: "Saiba como toopublish um aplicação tooa serviço remoto dos recursos de infraestrutura de cluster utilizando o Visual Studio."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Implementar e remover aplicações utilizando o Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [APIs FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Olá extensão do Azure Service Fabric para Visual Studio fornece uma forma fácil, repetíveis e passível de ter scripts toopublish um cluster do Service Fabric tooa aplicação.

## <a name="hello-artifacts-required-for-publishing"></a>artefactos Olá necessários para publicação
### <a name="deploy-fabricapplicationps1"></a>FabricApplication.ps1 implementar
Este é um script do PowerShell que utiliza um caminho de perfil de publicação como um parâmetro para publicar aplicações de Service Fabric. Uma vez que este script faz parte da sua aplicação, são toomodify boas-vindas-la conforme for necessário para a sua aplicação.

### <a name="publish-profiles"></a>Perfis de publicação
Uma pasta do projeto de aplicação de Service Fabric Olá chamado **PublishProfiles** contém os ficheiros XML, que armazenam informações essenciais para publicar uma aplicação, tais como:

* Parâmetros de ligação de cluster do Service Fabric
* Ficheiro de parâmetros do caminho tooan aplicação
* Definições de atualização

Por predefinição, a aplicação irá incluir três perfis de publicação: Local.1Node.xml, Local.5Node.xml e Cloud.xml. Pode adicionar mais perfis, copiar e colar um dos ficheiros de predefinidos Olá.

### <a name="application-parameter-files"></a>Ficheiros de parâmetro de aplicação
Uma pasta do projeto de aplicação de Service Fabric Olá chamado **ApplicationParameters** contém os ficheiros XML para os valores de parâmetros de manifesto de aplicação de utilizador especificado. Ficheiros de manifesto de aplicação podem ser parametrizados para que possa utilizar valores diferentes para as definições de implementação. toolearn mais informações sobre parameterizing a sua aplicação, consulte [gerir vários ambientes no Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Para os serviços de atores, deve criar projeto Olá primeiro antes de repetir o ficheiro de Olá tooedit num editor ou através de Olá caixa de diálogo Publicar. Isto acontece porque parte dos ficheiros de manifesto Olá será gerado durante a compilação de Olá.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish uma aplicação utilizando a caixa de diálogo Publicar aplicação do serviço Fabric Olá
Olá passos seguintes demonstram como toopublish utilizando uma aplicação Olá **publicar aplicação do serviço Fabric** caixa de diálogo fornecida pelo Olá ferramentas de recursos de infraestrutura de serviço do Visual Studio.

1. No menu de atalho Olá do projeto de aplicação do serviço Fabric Olá, escolha **publicar...** Olá tooview **publicar aplicação do serviço Fabric** caixa de diálogo.
   
    ![Olá * * caixa de diálogo Publicar Service Fabric aplicação * *][0]
   
    ficheiro Olá selecionado na Olá **destino perfil** caixa de lista pendente é onde todas as definições de Olá, exceto **manifesto versões**, são guardadas. Pode reutilizar um perfil existente ou crie um novo escolhendo **< gerir perfis de... >** no Olá **destino perfil** caixa de lista pendente. Ao escolher um perfil de publicação, são apresentados o respetivo conteúdo em campos de correspondente Olá Olá da caixa de diálogo. toosave as alterações em qualquer altura, escolha Olá **Guardar perfil** ligação.    
2. No Olá **ponto final de ligação** secção, especifique um local ou remoto Service Fabric da publicação ponto final de cluster. tooadd ou alteração Olá ponto final de ligação, clique em Olá **ponto final de ligação** na lista pendente. lista de Olá mostra Olá disponível recursos de infraestrutura do serviço cluster ligação pontos finais toowhich que pode publicar com base nas suas subscrições do Azure. Tenha em atenção que se já não são registados no tooVisual Studio, será pedido toodo por isso.
   
    Utilize Olá toochoose de caixa da caixa de diálogo de seleção de cluster de conjunto de Olá de subscrições disponíveis e clusters.
   
    ![Olá * * caixa de diálogo Selecionar serviço Fabric Cluster * *][1]
   
   > [!NOTE]
   > Se quiser toopublish tooan ponto final arbitrários (por exemplo, um cluster de terceiros), consulte Olá **publicação ponto final de cluster arbitrários tooan** secção abaixo.
   > 
   > 
   
    Depois de escolher um ponto final, o Visual Studio valida cluster do Service Fabric Olá ligação toohello selecionado. Se o cluster de Olá não seguro, Visual Studio podem ligar tooit imediatamente. No entanto, se o cluster de Olá é segura, terá de tooinstall um certificado no computador local antes de continuar. Consulte [como tooconfigure proteger ligações](service-fabric-visualstudio-configure-secure-connections.md) para obter mais informações. Quando tiver terminado, escolha Olá **OK** botão. cluster selecionado Olá aparece no Olá **publicar aplicação do serviço Fabric** caixa de diálogo.
3. No Olá **ficheiro de parâmetros de aplicação** na lista pendente caixa, navegue tooan ficheiro de parâmetros de aplicação. Um ficheiro de parâmetros de aplicação contém valores de utilizador especificado para os parâmetros no ficheiro de manifesto de aplicação Olá. tooadd ou alterar um parâmetro, escolha Olá **editar** botão. Introduza ou altere o valor do parâmetro Olá Olá **parâmetros** grelha. Quando tiver terminado, escolha Olá **guardar** botão.
   
    ![Olá * * caixa de diálogo Editar parâmetros * *][2]
4. Olá utilize **Olá atualização aplicação** toospecify de caixa de verificação se publicar esta ação é uma atualização. Atualização publicar as ações diferem das normal publicar as ações. Consulte [atualizar de aplicação do serviço de recursos de infraestrutura](service-fabric-application-upgrade.md) para obter uma lista das diferenças. definições de atualização de tooconfigure, escolha Olá **configurar definições de atualização** ligação. editor de parâmetro de atualização de Olá aparece. Consulte [configurar Olá a atualização de uma aplicação de Service Fabric](service-fabric-visualstudio-configure-upgrade.md) toolearn mais acerca dos parâmetros de atualização.
5. Escolha Olá **versões Manifest...** Olá do botão tooview **Editar versões** caixa de diálogo. Terá de tooupdate aplicações e versões de serviço para um local de tootake atualização. Consulte [tutorial de atualização de aplicação de Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn como aplicações e versões de manifesto do serviço afetam um processo de atualização.
   
    ![Olá * * caixa de diálogo Editar versões * *][3]
   
    Se aplicação Olá e versões de service usar o controlo de versões semântico como 1.0.0 ou valores de numérico Olá no formato 1.0.0.0, selecione Olá **atualizar automaticamente as aplicações e versões de service** opção. Quando escolher esta opção, o serviço de Olá e números de versão da aplicação são atualizados automaticamente sempre que um código, a configuração ou versão do pacote de dados é atualizado. Se preferir versões de Olá tooedit manualmente, desmarque Olá caixa de verificação toodisable esta funcionalidade.
   
   > [!NOTE]
   > Para todos os tooappear de entradas de pacote para um projeto de ator, primeiro crie Olá projeto toogenerate entradas Olá nos ficheiros de Service Manifest Olá.
   > 
   > 
6. Quando tiver terminado a especificação de todas as definições necessárias Olá, escolha Olá **publicar** botão toopublish toohello a aplicação selecionada cluster do Service Fabric. definições de Olá que especificou são aplicadas toohello publicar processo.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Publicar o ponto final de cluster arbitrários tooan (incluindo clusters de terceiros)
Olá experiência de publicação do Visual Studio está otimizada para a publicação de clusters de tooremote associados uma das suas subscrições do Azure. No entanto, é possível toopublish pontos finais de tooarbitrary (por exemplo, clusters de terceiros de Service Fabric) por diretamente editar Olá publicar o perfil de XML. Como descrito acima, três perfis de publicação são fornecidos por predefinição –**Local.1Node.xml**, **Local.5Node.xml**, e **Cloud.xml**– mas são toocreate boas-vindas perfis adicionais para os diferentes ambientes. Por exemplo, pode pretender toocreate um perfil de publicação tooparty clusters, talvez com o nome **Party.xml**.

Se estiver a ligar tooan protegida cluster, tudo o que é necessário está ponto final com a ligação do cluster Olá, tais como `partycluster1.eastus.cloudapp.azure.com:19000`. Nesse caso, Olá ligação no ponto final em Olá publicar perfil seria algo semelhante ao seguinte:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Se estiver a ligar cluster protegidos tooa, terá também de detalhes de Olá tooprovide do certificado de cliente Olá do Olá arquivo local toobe utilizado para autenticação. Para obter mais detalhes, consulte [cluster do Service Fabric configurar ligações seguras tooa](service-fabric-visualstudio-configure-secure-connections.md).

  Depois do perfil de publicação configurada, pode referenciá-lo no Olá caixa de diálogo Publicar, conforme mostrado abaixo.

  ![Novo perfil de publicação na caixa de diálogo Publicar][4]

  Tenha em atenção que neste caso, Olá novo perfil de publicação pontos tooone dos ficheiros de parâmetro de aplicação do Olá predefinidos. Este é apropriado se quiser toopublish Olá mesmo número de tooa de configuração de aplicação dos ambientes. Por outro lado, casos onde pretende toohave configurações diferentes para cada ambiente que pretende que sejam toopublish para,-iria fazer sentido toocreate um ficheiro de parâmetros de aplicação correspondente.

## <a name="next-steps"></a>Passos seguintes
toolearn como ver o processo de publicação Olá tooautomate num ambiente de integração contínua, [configurar a integração contínua de Service Fabric](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
