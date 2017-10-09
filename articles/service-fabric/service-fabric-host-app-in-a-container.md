---
title: "aaaDeploy uma aplicação .NET no tooAzure contentor Service Fabric | Microsoft Docs"
description: "Informa-o como toopackage uma aplicação .NET no Visual Studio num contentor de Docker. Esta nova aplicação de \"container\", em seguida, for implementada tooa cluster do Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Implementar uma aplicação .NET num tooAzure de contentor do Windows Service Fabric

Este tutorial mostra como toodeploy uma aplicação ASP.NET existente num contentor do Windows no Azure.

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar um projeto de Docker no Visual Studio
> * Containerize uma aplicação existente
> * Configurar a integração contínua com o Visual Studio e VSTS

## <a name="prerequisites"></a>Pré-requisitos

1. Instalar [Docker CE para Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) para que possam executar contentores no Windows 10.
2. Familiarize-se com Olá [início rápido do Windows 10 contentores][link-container-quickstart].
3. Transferir Olá [Fabrikam fibra CallCenter] [ link-fabrikam-github] aplicação de exemplo.
4. Instalar [o Azure PowerShell][link-azure-powershell-install]
5. Instalar Olá [extensão de ferramentas de entrega contínua para Visual Studio 2017][link-visualstudio-cd-extension]
6. Criar um [subscrição do Azure] [ link-azure-subscription] e um [conta Visual Studio Team Services][link-vsts-account]. 
7. [Criar um cluster no Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Containerize aplicação Olá

Agora que tem um [cluster do Service Fabric está em execução no Azure](service-fabric-tutorial-create-cluster-azure-ps.md) são toocreate pronto e implementar uma aplicação de. toostart com a nossa aplicação num contentor, precisamos tooadd **Docker suporte** toohello projeto no Visual Studio. Quando adiciona **suporte Docker** aplicação toohello, duas coisas acontecer. Primeiro, um _Dockerfile_ é adicionada toohello projeto. Este novo ficheiro descreve como a imagem do contentor de Olá é toobe incorporada. Em seguida, segundo, um novo _compor o docker_ projeto é adicionado toohello solução. Olá novo projeto contém alguns ficheiros de compose docker. Ficheiros de compose de docker podem ser utilizado toodescribe como contentor Olá é executado.

Obter mais informações sobre como trabalhar com [ferramentas de contentor do Visual Studio][link-visualstudio-container-tools].

>[!NOTE]
>Se for Olá pela primeira vez que as imagens de contentor do Windows estiver a executar no seu computador, tem obter Docker CE imagens base do Olá para os contentores. imagens de Olá utilizadas neste tutorial são 14 GB. Avançar e execute Olá imagens base do comando terminal toopull Olá os seguintes:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Adicionar suporte de Docker

Abra Olá [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] ficheiro no Visual Studio.

Contexto Olá **FabrikamFiber.Web** projeto > **adicionar** > **Docker suporte**.

### <a name="add-support-for-sql"></a>Adicionar suporte para o SQL Server

Esta aplicação utiliza o SQL Server como fornecedor de dados de Olá, para que um SQL server é necessário toorun Olá aplicação. Referência a uma imagem de contentor do SQL Server no nosso ficheiro docker compose.override.yml.

No Visual Studio, abra **Explorador de soluções**, localizar **compor o docker**e o ficheiro aberto Olá **docker compose.override.yml**.

Navegue toohello `services:` nó, adicionar um nó com o nome `db:` que define a entrada do SQL Server Olá para o contentor de Olá.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Pode utilizar qualquer servidor de SQL que preferir para depuração local, desde que seja acessível a partir do seu anfitrião. No entanto, **localdb** não suporta `container -> host` comunicação.

>[!WARNING]
>Executar o SQL Server num contentor não suporta dados persistentes. Paragem do contentor de Olá, é apagar os dados. Utilize esta configuração para produção.

Navegue toohello `fabrikamfiber.web:` nós e adicionar um nó subordinado com o nome `depends_on:`. Isto garante que Olá `db` início do serviço (contentor de SQL Server Olá) antes da nossa aplicação web (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Atualizar a configuração de web de Olá

Novamente no Olá **FabrikamFiber.Web** projeto, cadeia de ligação Olá atualização Olá **Web. config** toopoint toohello do SQL Server no contentor de Olá, de ficheiros.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Se quiser toouse um SQL Server diferente durante a criação de uma versão de compilação da aplicação web, adicione outra cadeia tooyour web.release.config o ficheiro de ligação.

### <a name="test-your-container"></a>O contentor de teste

Prima **F5** toorun e depuração aplicação Olá no seu contentor.

Limite abre uma página de início definido da sua aplicação utilizando o endereço IP de Olá do contentor de Olá no Olá NAT internos (normalmente 172.x.x.x). toolearn mais informações sobre a depuração de aplicações nos contentores utilizando o Visual Studio 2017, consulte [neste artigo][link-debug-container].

![exemplo de fabrikam num contentor][image-web-preview]

contentor de Olá está agora pronto toobe incorporada e empacotada numa aplicação de Service Fabric. Assim que tiver a imagem de contentor Olá incorporada no seu computador, pode enviá-lo tooany registo de contentor e obtenha-tooany toorun de anfitrião.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Preparar para a nuvem de Olá aplicação Olá

aplicação de Olá tooget pronta para ser executado no Service Fabric no Azure, é preciso toocomplete dois passos:

1. Expor as portas de olá onde queremos tooreach capaz de toobe nossa aplicação web no cluster do Service Fabric Olá.
2. Forneça um produção pronto base de dados SQL para a nossa aplicação.

### <a name="expose-hello-port-for-hello-app"></a>Expor as portas de Olá da aplicação Olá
tem de ter configurámos, de cluster do Service Fabric Olá porta *80* aberta por predefinição no Olá Balanceador de carga do Azure, que equilibra e o cluster de toohello receber tráfego. Pode expomos nosso contentor esta porta através do nosso ficheiro docker-Compose.yml.

No Visual Studio, abra **Explorador de soluções**, localizar **compor o docker**e o ficheiro aberto Olá **docker compose.override.yml**.

Modificar Olá `fabrikamfiber.web:` nó, adicionar um nó subordinado com o nome `ports:`.

Adicionar uma entrada de cadeia `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Utilizar uma base de dados do SQL Server de produção
Quando em execução na produção, precisamos que os nossos dados persistentes na nossa base de dados. Atualmente não existem dados persistentes do tooguarantee de forma num contentor, existe, por conseguinte, não é possível armazenar dados de produção no SQL Server num contentor.

É recomendável que utilizar uma base de dados do SQL do Azure. tooset cópias de segurança e executar um servidor gerido do SQL Server no Azure, visite Olá [inícios rápidos de base de dados do SQL do Azure] [ link-azure-sql] artigo.

>[!NOTE]
>Lembre-se toochange Olá ligação cadeias toohello do SQL Server no Olá **web.release.config** ficheiro Olá **FabrikamFiber.Web** projeto.
>
>Esta aplicação não consegue transições se nenhuma base de dados do SQL Server está acessível. Pode escolher toogo avançar e implementar a aplicação Olá não SQL Server.

## <a name="deploy-with-visual-studio-team-services"></a>Implementar com o Visual Studio Team Services

tooset com a implementação com o Visual Studio Team Services, terá de tooinstall Olá [extensão de ferramentas de entrega contínua para Visual Studio 2017][link-visualstudio-cd-extension]. Esta extensão torna mais fácil toodeploy tooAzure configurando o Visual Studio Team Services e obtenha o seu cluster do Service Fabric tooyour aplicação implementada.

tooget iniciado, o código tem de estar alojado no controlo de origem. parte do princípio de rest de Olá desta secção **git** está a ser utilizado.

### <a name="set-up-a-vsts-repo"></a>Configurar um repositório VSTS
No canto inferior direito de Olá do Visual Studio, clique em **adicionar tooSource controlo** > **Git** (ou qualquer opção que preferir).

![Prima o botão de controlo de origem Olá][image-source-control]

No Olá _equipa Explorer_ painel, prima **publicar repositório de Git**.

Selecione o nome do repositório VSTS e prima **repositório**.

![publicar tooVSTS repositório][image-publish-repo]

Agora que o seu código está sincronizado com um repositório de origem VSTS, pode configurar a integração contínua e entrega contínua.

### <a name="setup-continuous-delivery"></a>Configurar a entrega contínua

No _Explorador de soluções_, contexto Olá **solução** > **configurar contínua entrega**.

Selecione Olá subscrição do Azure.

Definir **tipo de anfitrião** demasiado**Cluster do Service Fabric**.

Definir **anfitrião de destino** que criou na secção anterior Olá de cluster do toohello service fabric.

Escolha um **contentor registo** toopublish o contentor para.

>[!TIP]
>Olá utilize **editar** toocreate de botão de registo do contentor.

Prima **OK**.

![integração contínua de recursos de infraestrutura do serviço de configuração][image-setup-ci]
   
   Depois de concluída a configuração de Olá, o contentor é implementado tooService recursos de infraestrutura. Sempre que push repositório toohello de atualizações é executada uma nova compilação e a versão.
   
   >[!NOTE]
   >As imagens de contentor do edifício Olá demorar cerca de 15 minutos.
   >Olá primeira implementação toohello cluster do Service Fabric faz com que Olá base Windows Server Core contentor imagens toobe transferido. transferência de Olá demora toocomplete adicionais 5-10 minutos.

Procure a aplicação do Centro de atendimento telefónico de Fabrikam toohello utilizando Olá url do cluster: por exemplo, *http://mycluster.westeurope.cloudapp.azure.com*

Agora que tem de e implementar a solução de centro de atendimento telefónico de Fabrikam Olá, pode abrir Olá [portal do Azure] [ link-azure-portal] e ver aplicação Olá em execução no Service Fabric. aplicação de Olá tootry, abra um browser e aceda toohello URL do seu cluster do Service Fabric.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Criar um projeto de Docker no Visual Studio
> * Containerize uma aplicação existente
> * Configurar a integração contínua com o Visual Studio e VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
