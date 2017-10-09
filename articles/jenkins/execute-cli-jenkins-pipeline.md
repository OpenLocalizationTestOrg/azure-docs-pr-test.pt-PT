---
title: "Olá aaaExecute CLI do Azure com Jenkins | Microsoft Docs"
description: "Saiba como toouse CLI do Azure toodeploy um Java web tooAzure de aplicação no Pipeline de Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Implementar tooAzure do serviço de aplicações com Jenkins e Olá CLI do Azure
toodeploy um tooAzure de aplicação web Java, pode utilizar a CLI do Azure no [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/). Neste tutorial, vai criar um pipeline de CI/CD numa VM do Azure incluindo como:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Configurar Jenkins
> * Criar uma aplicação web no Azure
> * Preparar um repositório do GitHub
> * Criar Jenkins pipeline
> * Executar o pipeline de Olá e certifique-se a aplicação web de Olá

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. versão de Olá toofind, execute `az --version`. Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Criar e configurar Jenkins instância
Se ainda não tiver um mestre Jenkins, comece por Olá [modelo de solução](install-jenkins-solution-template.md), que inclui Olá necessário [credenciais do Azure](https://plugins.jenkins.io/azure-credentials) Plug-in por predefinição. 

Plug-in do Olá credencial do Azure permite-lhe credenciais principais de serviço do Microsoft Azure de toostore no Jenkins. Na versão 1.2, iremos Olá suporte adicionado nesse Jenkins Pipeline pode obter Olá credenciais do Azure. 

Certifique-se de que tem a versão 1.2 ou posterior:
* No dashboard de Jenkins Olá, clique em **Jenkins gerir -> Gestor de plug-in ->** e procure **credencial do Azure**. 
* Atualize o plug-in de Olá se a versão de Olá é anterior ao 1.2.

Também é necessário no mestre de Jenkins Olá Java JDK e Maven. tooinstall, inicie sessão no mestre de tooJenkins ao utilizar o SSH e execute Olá os seguintes comandos:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Adicionar credencial principal tooJenkins de serviço do Azure

Uma credencial do Azure é necessário tooexecute CLI do Azure.

* No dashboard de Jenkins Olá, clique em **credenciais -> sistema ->**. Clique em **Global credentials(unrestricted)**.
* Clique em **adicionar credenciais** tooadd um [principal de serviço do Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ao preencher Olá ID de subscrição, o ID de cliente, o segredo do cliente e o ponto final de tokens do OAuth 2.0. Forneça um ID para utilização num passo subsequente.

![Adicione as credenciais](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Criar um serviço de aplicações do Azure para implementar a aplicação de web de Java Olá

Criar um plano do App Service do Azure com Olá **livres** utilizando Olá do escalão de preço [criar plano de serviço aplicacional az](/cli/azure/appservice/plan#create) comando da CLI. plano de serviço aplicacional Olá define Olá recursos físicos utilizados toohost as suas aplicações. Todas as aplicações atribuídas o plano de serviço aplicacional tooan partilham destes recursos, permitindo-lhe toosave custo quando várias aplicações de alojamento. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Quando estiver pronto o plano de Olá, Olá que CLI do Azure mostra semelhante saída toohello seguinte exemplo:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Criar uma aplicação Web do Azure

 Olá utilize [az webapp criar](/cli/azure/appservice/web#create) CLI comando toocreate uma definição de aplicação web no Olá `myAppServicePlan` plano do App Service. definição da aplicação web Olá fornece tooaccess um URL da aplicação com e configura várias opções toodeploy tooAzure seu código. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Olá Substitute `<app_name>` marcador de posição com o seu próprio nome de aplicação único. Este nome exclusivo faz parte de nome de domínio Olá predefinido para a aplicação web de Olá, pelo nome de Olá tem toobe exclusivo em todas as aplicações no Azure. Pode mapear uma aplicação de web toohello de entrada de nome de domínio personalizado antes de expor tooyour utilizadores.

Quando a definição da aplicação web Olá estiver pronta, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Configurar o Java 

Definir a configuração de tempo de execução de Java Olá que precisa da aplicação com Olá [atualização az da configuração de web de serviço aplicacional](/cli/azure/appservice/web/config#update) comando.

Olá seguinte comando configura Olá web app toorun um 8 JDK recentes do Java e [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>Preparar um repositório do GitHub
Abra Olá [simples aplicação de Web de Java do Azure](https://github.com/azure-devops/javawebappsample) repositório. toofork Olá repositório tooyour ser proprietário da conta do GitHub, clique em Olá **bifurcação** botão no canto superior direito Olá.

* Na IU do GitHub web, abra **Jenkinsfile** ficheiro. Clique em tooedit de ícone de lápis Olá este grupo de recursos do ficheiro tooupdate Olá e o nome da sua aplicação web na linha 20 e 21, respetivamente.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Alterar linha 23 tooupdate credencial ID na sua instância Jenkins

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Criar Jenkins pipeline
Abra Jenkins num browser, clique em **Novo Item**. 

* Forneça um nome para a tarefa de Olá e selecione **Pipeline**. Clique em **OK**.
* Clique em Olá **Pipeline** separador seguinte. 
* Para **definição**, selecione **de Pipeline de script no SCM**.
* Para **SCM**, selecione **Git**.
* Introduza Olá GitHub URL para o repositório forked: https:\<seu repositório forked\>.git
* Clique em **guardar**

## <a name="test-your-pipeline"></a>Testar o pipeline
* Aceda pipeline toohello que criou, clique em **compilar agora**
* Uma compilação deve ter êxito dentro de alguns segundos e pode ir toohello compilação e clique em **resultado da consola** detalhes de Olá toosee

## <a name="verify-your-web-app"></a>Certifique-se a sua aplicação web
ficheiro WAR tooverify Olá é implementado com êxito tooyour web app. Abra um browser:

* Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/ping  
Consulte:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substituir &lt;x > e &lt;y > com os números) tooget soma Olá x e y

![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Implementar tooAzure aplicação Web no Linux
Agora que já sabe como toouse CLI do Azure na sua Jenkins pipeline, pode modificar Olá script toodeploy tooan aplicação de Web do Azure no Linux.

Web App no Linux suporta uma implementação de Olá de toodo de forma diferente, que é toouse Docker. toodeploy, terá de tooprovide um Dockerfile que a aplicação web com o tempo de execução do serviço de pacotes para uma imagem de Docker. Plug-in de Olá, em seguida, irá criar a imagem de Olá, enviá-lo de registo de Docker tooa e implementar Olá imagem tooyour web app.

* Siga os passos de Olá [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate uma aplicação de Web do Azure em execução no Linux.
* Instalar Docker na sua instância Jenkins seguindo as instruções de Olá deste [artigo](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Criar um registo de contentor no Olá portal do Azure, utilizando os passos de Olá [aqui](/azure/container-registry/container-registry-get-started-azure-cli).
* No Olá mesmo [simples aplicação de Web de Java do Azure](https://github.com/azure-devops/javawebappsample) repositório escolhido, editar Olá **Jenkinsfile2** ficheiro:
    * Linha 18 21, atualizar toohello nomes do seu grupo de recursos, a aplicação web e o ACR respetivamente. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Linha 24, atualizar \<azsrvprincipal\> tooyour credencial ID
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Criar um novo pipeline Jenkins como fez quando implementar a aplicação de web tooAzure no Windows, apenas neste momento, utilize **Jenkinsfile2** em vez disso.
* Execute a tarefa de novo.
* tooverify, na CLI do Azure, execute:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Obter Olá seguinte resultado:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/ping. Verá uma mensagem de saudação: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substituir &lt;x > e &lt;y > com os números) tooget soma Olá x e y
    
## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou um pipeline de Jenkins que verifica o código de origem Olá no repositório do GitHub. Executa Maven toobuild um ficheiro war e, em seguida, utiliza a CLI do Azure toodeploy tooAzure do serviço de aplicações. Aprendeu a:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Configurar Jenkins
> * Criar uma aplicação web no Azure
> * Preparar um repositório do GitHub
> * Criar Jenkins pipeline
> * Executar o pipeline de Olá e certifique-se a aplicação web de Olá
