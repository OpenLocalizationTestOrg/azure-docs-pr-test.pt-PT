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
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="9fb73-103">Implementar tooAzure do serviço de aplicações com Jenkins e Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9fb73-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="9fb73-104">toodeploy um tooAzure de aplicação web Java, pode utilizar a CLI do Azure no [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="9fb73-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="9fb73-105">Neste tutorial, vai criar um pipeline de CI/CD numa VM do Azure incluindo como:</span><span class="sxs-lookup"><span data-stu-id="9fb73-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9fb73-106">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="9fb73-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="9fb73-107">Configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="9fb73-107">Configure Jenkins</span></span>
> * <span data-ttu-id="9fb73-108">Criar uma aplicação web no Azure</span><span class="sxs-lookup"><span data-stu-id="9fb73-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="9fb73-109">Preparar um repositório do GitHub</span><span class="sxs-lookup"><span data-stu-id="9fb73-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="9fb73-110">Criar Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="9fb73-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="9fb73-111">Executar o pipeline de Olá e certifique-se a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="9fb73-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="9fb73-112">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9fb73-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9fb73-113">versão de Olá toofind, execute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="9fb73-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="9fb73-114">Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9fb73-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="9fb73-115">Criar e configurar Jenkins instância</span><span class="sxs-lookup"><span data-stu-id="9fb73-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="9fb73-116">Se ainda não tiver um mestre Jenkins, comece por Olá [modelo de solução](install-jenkins-solution-template.md), que inclui Olá necessário [credenciais do Azure](https://plugins.jenkins.io/azure-credentials) Plug-in por predefinição.</span><span class="sxs-lookup"><span data-stu-id="9fb73-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="9fb73-117">Plug-in do Olá credencial do Azure permite-lhe credenciais principais de serviço do Microsoft Azure de toostore no Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9fb73-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="9fb73-118">Na versão 1.2, iremos Olá suporte adicionado nesse Jenkins Pipeline pode obter Olá credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb73-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="9fb73-119">Certifique-se de que tem a versão 1.2 ou posterior:</span><span class="sxs-lookup"><span data-stu-id="9fb73-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="9fb73-120">No dashboard de Jenkins Olá, clique em **Jenkins gerir -> Gestor de plug-in ->** e procure **credencial do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="9fb73-121">Atualize o plug-in de Olá se a versão de Olá é anterior ao 1.2.</span><span class="sxs-lookup"><span data-stu-id="9fb73-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="9fb73-122">Também é necessário no mestre de Jenkins Olá Java JDK e Maven.</span><span class="sxs-lookup"><span data-stu-id="9fb73-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="9fb73-123">tooinstall, inicie sessão no mestre de tooJenkins ao utilizar o SSH e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9fb73-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="9fb73-124">Adicionar credencial principal tooJenkins de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="9fb73-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="9fb73-125">Uma credencial do Azure é necessário tooexecute CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb73-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="9fb73-126">No dashboard de Jenkins Olá, clique em **credenciais -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="9fb73-127">Clique em **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="9fb73-128">Clique em **adicionar credenciais** tooadd um [principal de serviço do Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ao preencher Olá ID de subscrição, o ID de cliente, o segredo do cliente e o ponto final de tokens do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="9fb73-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="9fb73-129">Forneça um ID para utilização num passo subsequente.</span><span class="sxs-lookup"><span data-stu-id="9fb73-129">Provide an ID for use in subsequent step.</span></span>

![Adicione as credenciais](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="9fb73-131">Criar um serviço de aplicações do Azure para implementar a aplicação de web de Java Olá</span><span class="sxs-lookup"><span data-stu-id="9fb73-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="9fb73-132">Criar um plano do App Service do Azure com Olá **livres** utilizando Olá do escalão de preço [criar plano de serviço aplicacional az](/cli/azure/appservice/plan#create) comando da CLI.</span><span class="sxs-lookup"><span data-stu-id="9fb73-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="9fb73-133">plano de serviço aplicacional Olá define Olá recursos físicos utilizados toohost as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="9fb73-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="9fb73-134">Todas as aplicações atribuídas o plano de serviço aplicacional tooan partilham destes recursos, permitindo-lhe toosave custo quando várias aplicações de alojamento.</span><span class="sxs-lookup"><span data-stu-id="9fb73-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="9fb73-135">Quando estiver pronto o plano de Olá, Olá que CLI do Azure mostra semelhante saída toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fb73-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="9fb73-136">Criar uma aplicação Web do Azure</span><span class="sxs-lookup"><span data-stu-id="9fb73-136">Create an Azure Web app</span></span>

 <span data-ttu-id="9fb73-137">Olá utilize [az webapp criar](/cli/azure/appservice/web#create) CLI comando toocreate uma definição de aplicação web no Olá `myAppServicePlan` plano do App Service.</span><span class="sxs-lookup"><span data-stu-id="9fb73-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="9fb73-138">definição da aplicação web Olá fornece tooaccess um URL da aplicação com e configura várias opções toodeploy tooAzure seu código.</span><span class="sxs-lookup"><span data-stu-id="9fb73-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="9fb73-139">Olá Substitute `<app_name>` marcador de posição com o seu próprio nome de aplicação único.</span><span class="sxs-lookup"><span data-stu-id="9fb73-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="9fb73-140">Este nome exclusivo faz parte de nome de domínio Olá predefinido para a aplicação web de Olá, pelo nome de Olá tem toobe exclusivo em todas as aplicações no Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb73-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="9fb73-141">Pode mapear uma aplicação de web toohello de entrada de nome de domínio personalizado antes de expor tooyour utilizadores.</span><span class="sxs-lookup"><span data-stu-id="9fb73-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="9fb73-142">Quando a definição da aplicação web Olá estiver pronta, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fb73-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="9fb73-143">Configurar o Java</span><span class="sxs-lookup"><span data-stu-id="9fb73-143">Configure Java</span></span> 

<span data-ttu-id="9fb73-144">Definir a configuração de tempo de execução de Java Olá que precisa da aplicação com Olá [atualização az da configuração de web de serviço aplicacional](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="9fb73-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="9fb73-145">Olá seguinte comando configura Olá web app toorun um 8 JDK recentes do Java e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="9fb73-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="9fb73-146">Preparar um repositório do GitHub</span><span class="sxs-lookup"><span data-stu-id="9fb73-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="9fb73-147">Abra Olá [simples aplicação de Web de Java do Azure](https://github.com/azure-devops/javawebappsample) repositório.</span><span class="sxs-lookup"><span data-stu-id="9fb73-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="9fb73-148">toofork Olá repositório tooyour ser proprietário da conta do GitHub, clique em Olá **bifurcação** botão no canto superior direito Olá.</span><span class="sxs-lookup"><span data-stu-id="9fb73-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="9fb73-149">Na IU do GitHub web, abra **Jenkinsfile** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="9fb73-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="9fb73-150">Clique em tooedit de ícone de lápis Olá este grupo de recursos do ficheiro tooupdate Olá e o nome da sua aplicação web na linha 20 e 21, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="9fb73-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="9fb73-151">Alterar linha 23 tooupdate credencial ID na sua instância Jenkins</span><span class="sxs-lookup"><span data-stu-id="9fb73-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="9fb73-152">Criar Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="9fb73-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="9fb73-153">Abra Jenkins num browser, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="9fb73-154">Forneça um nome para a tarefa de Olá e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="9fb73-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-155">Click **OK**.</span></span>
* <span data-ttu-id="9fb73-156">Clique em Olá **Pipeline** separador seguinte.</span><span class="sxs-lookup"><span data-stu-id="9fb73-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="9fb73-157">Para **definição**, selecione **de Pipeline de script no SCM**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="9fb73-158">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="9fb73-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="9fb73-159">Introduza Olá GitHub URL para o repositório forked: https:\<seu repositório forked\>.git</span><span class="sxs-lookup"><span data-stu-id="9fb73-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="9fb73-160">Clique em **guardar**</span><span class="sxs-lookup"><span data-stu-id="9fb73-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="9fb73-161">Testar o pipeline</span><span class="sxs-lookup"><span data-stu-id="9fb73-161">Test your pipeline</span></span>
* <span data-ttu-id="9fb73-162">Aceda pipeline toohello que criou, clique em **compilar agora**</span><span class="sxs-lookup"><span data-stu-id="9fb73-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="9fb73-163">Uma compilação deve ter êxito dentro de alguns segundos e pode ir toohello compilação e clique em **resultado da consola** detalhes de Olá toosee</span><span class="sxs-lookup"><span data-stu-id="9fb73-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="9fb73-164">Certifique-se a sua aplicação web</span><span class="sxs-lookup"><span data-stu-id="9fb73-164">Verify your web app</span></span>
<span data-ttu-id="9fb73-165">ficheiro WAR tooverify Olá é implementado com êxito tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="9fb73-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="9fb73-166">Abra um browser:</span><span class="sxs-lookup"><span data-stu-id="9fb73-166">Open a web browser:</span></span>

* <span data-ttu-id="9fb73-167">Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="9fb73-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="9fb73-168">Consulte:</span><span class="sxs-lookup"><span data-stu-id="9fb73-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="9fb73-169">Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substituir &lt;x > e &lt;y > com os números) tooget soma Olá x e y</span><span class="sxs-lookup"><span data-stu-id="9fb73-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="9fb73-171">Implementar tooAzure aplicação Web no Linux</span><span class="sxs-lookup"><span data-stu-id="9fb73-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="9fb73-172">Agora que já sabe como toouse CLI do Azure na sua Jenkins pipeline, pode modificar Olá script toodeploy tooan aplicação de Web do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="9fb73-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="9fb73-173">Web App no Linux suporta uma implementação de Olá de toodo de forma diferente, que é toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="9fb73-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="9fb73-174">toodeploy, terá de tooprovide um Dockerfile que a aplicação web com o tempo de execução do serviço de pacotes para uma imagem de Docker.</span><span class="sxs-lookup"><span data-stu-id="9fb73-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="9fb73-175">Plug-in de Olá, em seguida, irá criar a imagem de Olá, enviá-lo de registo de Docker tooa e implementar Olá imagem tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="9fb73-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="9fb73-176">Siga os passos de Olá [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate uma aplicação de Web do Azure em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="9fb73-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="9fb73-177">Instalar Docker na sua instância Jenkins seguindo as instruções de Olá deste [artigo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="9fb73-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="9fb73-178">Criar um registo de contentor no Olá portal do Azure, utilizando os passos de Olá [aqui](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9fb73-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="9fb73-179">No Olá mesmo [simples aplicação de Web de Java do Azure](https://github.com/azure-devops/javawebappsample) repositório escolhido, editar Olá **Jenkinsfile2** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="9fb73-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="9fb73-180">Linha 18 21, atualizar toohello nomes do seu grupo de recursos, a aplicação web e o ACR respetivamente.</span><span class="sxs-lookup"><span data-stu-id="9fb73-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="9fb73-181">Linha 24, atualizar \<azsrvprincipal\> tooyour credencial ID</span><span class="sxs-lookup"><span data-stu-id="9fb73-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="9fb73-182">Criar um novo pipeline Jenkins como fez quando implementar a aplicação de web tooAzure no Windows, apenas neste momento, utilize **Jenkinsfile2** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="9fb73-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="9fb73-183">Execute a tarefa de novo.</span><span class="sxs-lookup"><span data-stu-id="9fb73-183">Run your new job.</span></span>
* <span data-ttu-id="9fb73-184">tooverify, na CLI do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="9fb73-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="9fb73-185">Obter Olá seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="9fb73-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="9fb73-186">Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="9fb73-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="9fb73-187">Verá uma mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="9fb73-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="9fb73-188">Aceda toohttp: / /&lt;APP_NAME>.azurewebsites.NET >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substituir &lt;x > e &lt;y > com os números) tooget soma Olá x e y</span><span class="sxs-lookup"><span data-stu-id="9fb73-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="9fb73-189">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9fb73-189">Next steps</span></span>
<span data-ttu-id="9fb73-190">Neste tutorial, configurou um pipeline de Jenkins que verifica o código de origem Olá no repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9fb73-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="9fb73-191">Executa Maven toobuild um ficheiro war e, em seguida, utiliza a CLI do Azure toodeploy tooAzure do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="9fb73-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="9fb73-192">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="9fb73-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9fb73-193">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="9fb73-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="9fb73-194">Configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="9fb73-194">Configure Jenkins</span></span>
> * <span data-ttu-id="9fb73-195">Criar uma aplicação web no Azure</span><span class="sxs-lookup"><span data-stu-id="9fb73-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="9fb73-196">Preparar um repositório do GitHub</span><span class="sxs-lookup"><span data-stu-id="9fb73-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="9fb73-197">Criar Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="9fb73-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="9fb73-198">Executar o pipeline de Olá e certifique-se a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="9fb73-198">Run hello pipeline and verify hello web app</span></span>
