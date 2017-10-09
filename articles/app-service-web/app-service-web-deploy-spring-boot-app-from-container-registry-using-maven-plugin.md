---
title: "aaaHow toouse Olá Plug-in do Maven para Web Apps do Azure toodeploy uma aplicação de arranque de mola no registo de contentor do Azure tooAzure do serviço de aplicações"
description: "Este tutorial irá guiá-lo embora Olá passos toodeploy uma aplicação de arranque de mola no registo de contentor do Azure tooAzure tooAzure do serviço de aplicações através da utilização de um plug-in do Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="06254-103">Como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy uma aplicação de arranque de mola no registo de contentor do Azure tooAzure do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="06254-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="06254-104">Olá  **[mola Framework]**  é uma arquitetura de open source popular, que ajuda os programadores de Java criar web, móveis e aplicações API.</span><span class="sxs-lookup"><span data-stu-id="06254-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="06254-105">Este tutorial utiliza uma aplicação de exemplo criada utilizando [mola arranque], uma abordagem condicionada por Convenção para utilizar mola tooget a trabalhar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="06254-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="06254-106">Este artigo demonstra como toodeploy tooAzure de aplicação de arranque a um exemplo registo de contentor e, em seguida, utilize hello Plug-in do Maven para Web Apps do Azure toodeploy tooAzure a aplicação do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="06254-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="06254-107">Olá Plug-in do Maven para Web Apps do Azure está atualmente disponível como uma pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="06254-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="06254-108">Por agora, a publicação de FTP só é suportada, embora as funcionalidades adicionais estejam planeadas para Olá futura.</span><span class="sxs-lookup"><span data-stu-id="06254-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="06254-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="06254-109">Prerequisites</span></span>

<span data-ttu-id="06254-110">Ordem toocomplete Olá passos deste tutorial, terá de Olá toohave os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="06254-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="06254-111">Uma subscrição do Azure; Se ainda não tiver uma subscrição do Azure, pode ativar o [benefícios de subscritor do MSDN] ou inscrever-se um [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="06254-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="06254-112">Olá [Interface de linha de comandos do Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="06254-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="06254-113">Um atualizados [Java Development Kit (JDK)], versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06254-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="06254-114">Do Apache [Maven] criar ferramenta (versão 3).</span><span class="sxs-lookup"><span data-stu-id="06254-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="06254-115">A [Git] cliente.</span><span class="sxs-lookup"><span data-stu-id="06254-115">A [Git] client.</span></span>
* <span data-ttu-id="06254-116">A [Docker] cliente.</span><span class="sxs-lookup"><span data-stu-id="06254-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="06254-117">Devido a requisitos de Virtualização toohello deste tutorial, não pode seguir passos descritos neste artigo Olá numa máquina virtual; tem de utilizar um computador físico com funcionalidades de Virtualização ativadas.</span><span class="sxs-lookup"><span data-stu-id="06254-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="06254-118">Exemplo de Olá clone mola arranque na aplicação web de Docker</span><span class="sxs-lookup"><span data-stu-id="06254-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="06254-119">Nesta secção, clonar uma de aplicação de arranque de mola e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="06254-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="06254-120">Abra uma linha de comandos ou janela de terminal e criar um diretório local toohold da aplicação de arranque de mola e alteração toothat diretório; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="06254-121">- ou -</span><span class="sxs-lookup"><span data-stu-id="06254-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="06254-122">Olá clone [arranque mola no Docker introdução] projeto de exemplo para o diretório de Olá criou; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="06254-123">Altere o projeto do diretório toohello concluída; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="06254-124">Criar o ficheiro JAR de Olá com o Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="06254-125">Quando tiver sido criada a aplicação web de Olá, iniciar a aplicação de web de Olá com o Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="06254-126">Testar a aplicação web de Olá navegando tooit localmente utilizando um browser.</span><span class="sxs-lookup"><span data-stu-id="06254-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="06254-127">Por exemplo, pode utilizar Olá se tiver o curl disponível os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="06254-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="06254-128">Deverá ver Olá seguir a mensagem apresentada: **Olá, mundo Docker**</span><span class="sxs-lookup"><span data-stu-id="06254-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Procure a aplicação de exemplo localmente][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="06254-130">Criar um Azure principal de serviço</span><span class="sxs-lookup"><span data-stu-id="06254-130">Create an Azure service principal</span></span>

<span data-ttu-id="06254-131">Nesta secção, vai criar um Azure principal de serviço que Olá utiliza de plug-in do Maven quando implementar a sua tooAzure de contentor.</span><span class="sxs-lookup"><span data-stu-id="06254-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="06254-132">Abra uma linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="06254-132">Open a command prompt.</span></span>

1. <span data-ttu-id="06254-133">Inicie sessão na sua conta do Azure utilizando Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="06254-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="06254-134">Siga Olá instruções toocomplete Olá início de sessão no processo.</span><span class="sxs-lookup"><span data-stu-id="06254-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="06254-135">Crie um Azure principal de serviço:</span><span class="sxs-lookup"><span data-stu-id="06254-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="06254-136">Onde `uuuuuuuu` é o nome de utilizador de Olá e `pppppppp` é Olá palavra-passe para o principal de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="06254-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="06254-137">Azure responde com JSON que se assemelha Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-137">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="06254-138">Irá utilizar valores de Olá desta resposta JSON quando configurar Olá Maven Plug-in toodeploy tooAzure seu contentor.</span><span class="sxs-lookup"><span data-stu-id="06254-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="06254-139">Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de marcador de posição, o que são utilizados em toomake este exemplo-lo mais fácil toomap estes valores tootheir respetivos elementos quando configura o Maven `settings.xml` ficheiros Olá seguinte secção.</span><span class="sxs-lookup"><span data-stu-id="06254-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="06254-140">Criar um registo de contentor do Azure utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06254-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="06254-141">Abra uma linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="06254-141">Open a command prompt.</span></span>

1. <span data-ttu-id="06254-142">Inicie sessão no tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="06254-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="06254-143">Crie um grupo de recursos para Olá recursos do Azure que irá utilizar este artigo:</span><span class="sxs-lookup"><span data-stu-id="06254-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="06254-144">Substitua `wingtiptoysresources` neste exemplo, com um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="06254-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="06254-145">Crie um registo de contentor do Azure privado no grupo de recursos de Olá para a sua aplicação de arranque de mola:</span><span class="sxs-lookup"><span data-stu-id="06254-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="06254-146">Substitua `wingtiptoysregistry` neste exemplo, com um nome exclusivo para o registo de contentor.</span><span class="sxs-lookup"><span data-stu-id="06254-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="06254-147">Obter Olá palavra-passe para o registo do contentor:</span><span class="sxs-lookup"><span data-stu-id="06254-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="06254-148">Azure irá responder com a palavra-passe; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="06254-149">Adicionar o registo de contentor do Azure e as definições de Maven principal tooyour de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="06254-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="06254-150">Abra o Maven `settings.xml` ficheiro num editor de texto; este ficheiro pode ser um caminho como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="06254-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="06254-151">Adicionar as definições de acesso do registo de contentor do Azure na secção anterior do Olá da toohello artigo `<servers>` coleção no Olá *settings.xml* ficheiro; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="06254-152">Em que:</span><span class="sxs-lookup"><span data-stu-id="06254-152">Where:</span></span>
   <span data-ttu-id="06254-153">Elemento</span><span class="sxs-lookup"><span data-stu-id="06254-153">Element</span></span> | <span data-ttu-id="06254-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="06254-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="06254-155">Contém o nome de Olá do seu registo de contentor do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="06254-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="06254-156">Contém o nome de Olá do seu registo de contentor do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="06254-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="06254-157">Contém a palavra-passe de Olá que obteve na secção anterior do Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="06254-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="06254-158">Adicionar as definições de principal de serviço do Azure a partir de uma secção anterior deste artigo toohello `<servers>` coleção no Olá *settings.xml* ficheiro; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="06254-159">Em que:</span><span class="sxs-lookup"><span data-stu-id="06254-159">Where:</span></span>
   <span data-ttu-id="06254-160">Elemento</span><span class="sxs-lookup"><span data-stu-id="06254-160">Element</span></span> | <span data-ttu-id="06254-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="06254-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="06254-162">Especifica um nome exclusivo que Maven utiliza toolook configurar as definições de segurança quando implementa o tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06254-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="06254-163">Contém Olá `appId` valor do seu principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="06254-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="06254-164">Contém Olá `tenant` valor do seu principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="06254-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="06254-165">Contém Olá `password` valor do seu principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="06254-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="06254-166">Define o ambiente de nuvem do Azure do Olá destino, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="06254-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="06254-167">(Uma lista completa dos ambientes está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação)</span><span class="sxs-lookup"><span data-stu-id="06254-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="06254-168">Guarde e feche Olá *settings.xml* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="06254-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="06254-169">Compilar o Docker imagem do contentor e enviá-lo tooyour registo de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="06254-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="06254-170">Navegue (por exemplo, o diretório de projeto toohello concluída para a sua aplicação de arranque de mola "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra Olá *pom.xml* ficheiro com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="06254-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="06254-171">Olá atualização `<properties>` coleção no Olá *pom.xml* ficheiro com o valor de início de sessão hello do servidor para o registo de contentor do Azure na secção anterior do Olá deste tutorial; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="06254-172">Em que:</span><span class="sxs-lookup"><span data-stu-id="06254-172">Where:</span></span>
   <span data-ttu-id="06254-173">Elemento</span><span class="sxs-lookup"><span data-stu-id="06254-173">Element</span></span> | <span data-ttu-id="06254-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="06254-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="06254-175">Especifica o nome de Olá do seu registo de contentor do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="06254-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="06254-176">Especifica o URL de Olá do seu registo de contentor do Azure privado, que é derivado acrescentando ". azurecr.io" toohello nome do seu registo de contentor privada.</span><span class="sxs-lookup"><span data-stu-id="06254-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="06254-177">Certifique-se de que `<plugin>` de plug-in de Olá Docker no seu *pom.xml* ficheiro contém propriedades correto do Olá Olá início de sessão e registo de endereço do nome de servidor do passo anterior Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="06254-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="06254-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="06254-179">Em que:</span><span class="sxs-lookup"><span data-stu-id="06254-179">Where:</span></span>
   <span data-ttu-id="06254-180">Elemento</span><span class="sxs-lookup"><span data-stu-id="06254-180">Element</span></span> | <span data-ttu-id="06254-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="06254-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="06254-182">Especifica a propriedade de Olá que contém o nome do seu registo de contentor do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="06254-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="06254-183">Especifica a propriedade de Olá que contém o URL de Olá do seu registo de contentor do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="06254-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="06254-184">Navegue toohello concluída o diretório de projeto para a sua aplicação de arranque de mola e executar Olá seguintes aplicações do comando toorebuild Olá e push Olá contentor tooyour registo de contentor do Azure:</span><span class="sxs-lookup"><span data-stu-id="06254-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="06254-185">OPCIONAL: Procurar toohello [portal do Azure] e verifique se existe com o nome de imagem do contentor de Docker **gs-mola arranque docker** no seu registo de contentor.</span><span class="sxs-lookup"><span data-stu-id="06254-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Certifique-se contentor no portal do Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="06254-187">Personalizar a sua pom.xml, em seguida, criar e implementar tooAzure o contentor</span><span class="sxs-lookup"><span data-stu-id="06254-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="06254-188">Abra Olá `pom.xml` de ficheiros para a sua aplicação de arranque de mola num editor de texto e, em seguida, localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="06254-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="06254-189">Este elemento deve assemelhar-se Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="06254-190">Existem vários valores que pode modificar para o plug-in do Maven Olá e uma descrição detalhada para cada um destes elementos está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação.</span><span class="sxs-lookup"><span data-stu-id="06254-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="06254-191">Que a ser consiga aceder tal, existem vários valores, realçando neste artigo:</span><span class="sxs-lookup"><span data-stu-id="06254-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="06254-192">Elemento</span><span class="sxs-lookup"><span data-stu-id="06254-192">Element</span></span> | <span data-ttu-id="06254-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="06254-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="06254-194">Especifica uma versão de Olá Olá [Plug-in do Maven para Web Apps do Azure].</span><span class="sxs-lookup"><span data-stu-id="06254-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="06254-195">Deve verificar a versão de Olá listada no Olá [Respository Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que está a utilizar Olá versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="06254-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="06254-196">Especifica as informações de autenticação de Olá do Azure, que, neste exemplo, contém um `<serverId>` elemento que contenha `azure-auth`; Maven utiliza toolook esse valor dos valores de principal de serviço do Azure Olá no seu Maven *settings.xml* ficheiro, que é definida uma secção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="06254-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="06254-197">Especifica o grupo de recursos do Olá destino, que é `wingtiptoysresources` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="06254-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="06254-198">grupo de recursos de Olá será criado durante a implementação, se já existir.</span><span class="sxs-lookup"><span data-stu-id="06254-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="06254-199">Especifica o nome de destino Olá para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06254-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="06254-200">Neste exemplo, é o nome de destino Olá `maven-linux-app-${maven.build.timestamp}`, em que hello `${maven.build.timestamp}` é acrescentado um sufixo neste conflito de tooavoid de exemplo.</span><span class="sxs-lookup"><span data-stu-id="06254-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="06254-201">(Olá timestamp é opcional; pode especificar qualquer cadeia exclusiva para o nome da aplicação Olá).</span><span class="sxs-lookup"><span data-stu-id="06254-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="06254-202">Especifica a região de destino Olá, que, neste exemplo, é `westus`.</span><span class="sxs-lookup"><span data-stu-id="06254-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="06254-203">(Uma lista completa está a ser Olá [Plug-in do Maven para Web Apps do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="06254-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="06254-204">Especifica as propriedades de Olá que contêm o nome de Olá e o URL do seu contentor.</span><span class="sxs-lookup"><span data-stu-id="06254-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="06254-205">Especifica as definições de exclusivas para Maven toouse quando implementar a sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="06254-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="06254-206">Neste exemplo, um `<property>` elemento contém um par nome/valor de elementos subordinados que especifique a porta de Olá para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="06254-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="06254-207">número de porta do Olá definições toochange Olá neste exemplo, apenas são necessários quando está a alterar a porta de Olá da predefinição de Olá.</span><span class="sxs-lookup"><span data-stu-id="06254-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="06254-208">Olá linha de comandos ou janela de terminal que estava a utilizar anteriormente, reconstrua o ficheiro JAR de Olá com o Maven se tiver efetuado quaisquer alterações toohello *pom.xml* ficheiro; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="06254-209">Implementar o tooAzure de aplicação web com o Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="06254-210">Maven irá implementar a sua tooAzure de aplicação web; Se a aplicação web de Olá ainda não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="06254-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="06254-211">Se região Olá que especificou nas Olá `<region>` elemento do seu *pom.xml* ficheiro não tem suficiente servidores disponíveis quando iniciar a implementação, poderá ver um erro toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="06254-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="06254-212">Se isto acontecer, pode especificar que outra região e volte a executar Olá toodeploy de comando Maven a aplicação.</span><span class="sxs-lookup"><span data-stu-id="06254-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="06254-213">Quando a web tiver sido implementada, será capaz de toomanage-lo utilizando Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="06254-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="06254-214">A aplicação web será listada no **serviços aplicacionais**:</span><span class="sxs-lookup"><span data-stu-id="06254-214">Your web app will be listed in **App Services**:</span></span>

   ![Aplicação Web listada no portal do Azure serviços aplicacionais][AP01]

* <span data-ttu-id="06254-216">E Olá URL para a sua aplicação web será listada no Olá **descrição geral** para a sua aplicação web:</span><span class="sxs-lookup"><span data-stu-id="06254-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinar o URL de Olá para a sua aplicação web][AP02]

## <a name="next-steps"></a><span data-ttu-id="06254-218">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06254-218">Next steps</span></span>

<span data-ttu-id="06254-219">Para obter mais informações sobre Olá várias tecnologias abordadas neste artigo, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="06254-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="06254-220">[Plug-in do Maven para Web Apps do Azure]</span><span class="sxs-lookup"><span data-stu-id="06254-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="06254-221">Inicie sessão no tooAzure de Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06254-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="06254-222">Criar um Azure principal de serviço com o Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="06254-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="06254-223">Referência de definições do maven</span><span class="sxs-lookup"><span data-stu-id="06254-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="06254-224">[Plug-in do docker para Maven]</span><span class="sxs-lookup"><span data-stu-id="06254-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Interface de linha de comandos do Azure (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Plug-in do Maven para Web Apps do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in do docker para Maven]: https://github.com/spotify/docker-maven-plugin
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefícios de subscritor do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[mola arranque]: http://projects.spring.io/spring-boot/
[arranque mola no Docker introdução]: https://github.com/spring-guides/gs-spring-boot-docker
[mola Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
