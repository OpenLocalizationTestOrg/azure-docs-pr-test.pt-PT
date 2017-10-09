---
title: "aaaHow toouse Olá Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque da mola"
description: "Saiba como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque de mola."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="fef07-103">Como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque da mola</span><span class="sxs-lookup"><span data-stu-id="fef07-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="fef07-104">Olá [Plug-in do Maven para Web Apps do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do App Service do Azure em projetos Maven e simplifica o processo de Olá para os programadores toodeploy web apps tooAzure do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="fef07-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="fef07-105">Este artigo demonstra utilizando Olá Plug-in do Maven para Web Apps do Azure toodeploy tooAzure de aplicação de arranque a um exemplo serviços aplicacionais.</span><span class="sxs-lookup"><span data-stu-id="fef07-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fef07-106">Olá Plug-in do Maven para Web Apps do Azure está atualmente disponível como uma pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="fef07-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="fef07-107">Por agora, a publicação de FTP só é suportada, embora as funcionalidades adicionais estejam planeadas para Olá futura.</span><span class="sxs-lookup"><span data-stu-id="fef07-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="fef07-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fef07-108">Prerequisites</span></span>

<span data-ttu-id="fef07-109">Ordem toocomplete Olá passos deste tutorial, terá de Olá toohave os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="fef07-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="fef07-110">Uma subscrição do Azure; Se ainda não tiver uma subscrição do Azure, pode ativar o [benefícios de subscritor do MSDN] ou inscrever-se um [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="fef07-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="fef07-111">Olá [Interface de linha de comandos do Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="fef07-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="fef07-112">Um atualizados [Java Development Kit (JDK)], versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fef07-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="fef07-113">Do Apache [Maven] criar ferramenta (versão 3).</span><span class="sxs-lookup"><span data-stu-id="fef07-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="fef07-114">A [Git] cliente.</span><span class="sxs-lookup"><span data-stu-id="fef07-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="fef07-115">Aplicação de web de arranque de mola de exemplo de Olá clone</span><span class="sxs-lookup"><span data-stu-id="fef07-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="fef07-116">Nesta secção, clonar uma aplicação de arranque de mola concluída e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="fef07-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="fef07-117">Abra uma linha de comandos ou janela de terminal e criar um diretório local toohold da aplicação de arranque de mola e alteração toothat diretório; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="fef07-118">- ou -</span><span class="sxs-lookup"><span data-stu-id="fef07-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="fef07-119">Olá clone [mola arranque introdução] projeto de exemplo para o diretório de Olá criou; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="fef07-120">Altere o projeto do diretório toohello concluída; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="fef07-121">Criar o ficheiro JAR de Olá com o Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="fef07-122">Quando tiver sido criada a aplicação web de Olá, iniciar a aplicação de web de Olá com o Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="fef07-123">Testar a aplicação web de Olá navegando tooit localmente utilizando um browser.</span><span class="sxs-lookup"><span data-stu-id="fef07-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="fef07-124">Por exemplo, pode utilizar Olá se tiver o curl disponível os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fef07-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="fef07-125">Deverá ver Olá seguir a mensagem apresentada: **saudações de arranque de mola!**</span><span class="sxs-lookup"><span data-stu-id="fef07-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="fef07-126">Criar um Azure principal de serviço</span><span class="sxs-lookup"><span data-stu-id="fef07-126">Create an Azure service principal</span></span>

<span data-ttu-id="fef07-127">Nesta secção, vai criar um Azure principal de serviço que Olá utiliza de plug-in do Maven quando implementar a sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="fef07-128">Abra uma linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="fef07-128">Open a command prompt.</span></span>

1. <span data-ttu-id="fef07-129">Inicie sessão na sua conta do Azure utilizando Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="fef07-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="fef07-130">Siga Olá instruções toocomplete Olá início de sessão no processo.</span><span class="sxs-lookup"><span data-stu-id="fef07-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="fef07-131">Crie um Azure principal de serviço:</span><span class="sxs-lookup"><span data-stu-id="fef07-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="fef07-132">Onde `uuuuuuuu` é o nome de utilizador de Olá e `pppppppp` é Olá palavra-passe para o principal de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="fef07-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="fef07-133">Azure responde com JSON que se assemelha Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="fef07-134">Irá utilizar os valores Olá esta resposta JSON quando configurar Olá Maven Plug-in toodeploy sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="fef07-135">Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de marcador de posição, o que são utilizados em toomake este exemplo-lo mais fácil toomap estes valores tootheir respetivos elementos quando configura o Maven `settings.xml` ficheiros Olá seguinte secção.</span><span class="sxs-lookup"><span data-stu-id="fef07-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="fef07-136">Configurar Maven toouse o principal de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="fef07-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="fef07-137">Nesta secção, utilize os valores de Olá da sua autenticação Olá principal tooconfigure de serviço do Azure que Maven utiliza ao implementar a sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="fef07-138">Abra o Maven `settings.xml` ficheiro num editor de texto; este ficheiro pode ser um caminho como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fef07-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="fef07-139">Adicionar as definições de principal de serviço do Azure na secção anterior do Olá deste tutorial toohello `<servers>` coleção no Olá *settings.xml* ficheiro; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="fef07-140">Em que:</span><span class="sxs-lookup"><span data-stu-id="fef07-140">Where:</span></span>
   <span data-ttu-id="fef07-141">Elemento</span><span class="sxs-lookup"><span data-stu-id="fef07-141">Element</span></span> | <span data-ttu-id="fef07-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="fef07-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="fef07-143">Especifica um nome exclusivo que Maven utiliza toolook configurar as definições de segurança quando implementa o tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="fef07-144">Contém Olá `appId` valor do seu principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="fef07-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="fef07-145">Contém Olá `tenant` valor do seu principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="fef07-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="fef07-146">Contém Olá `password` valor do seu principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="fef07-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="fef07-147">Define o ambiente de nuvem do Azure do Olá destino, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="fef07-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="fef07-148">(Uma lista completa dos ambientes está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação)</span><span class="sxs-lookup"><span data-stu-id="fef07-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="fef07-149">Guarde e feche Olá *settings.xml* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fef07-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="fef07-150">OPCIONAL: Personalizar o pom.xml antes de implementar a sua tooAzure de aplicação web</span><span class="sxs-lookup"><span data-stu-id="fef07-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="fef07-151">Abra Olá `pom.xml` de ficheiros para a sua aplicação de arranque de mola num editor de texto e, em seguida, localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="fef07-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="fef07-152">Este elemento deve assemelhar-se Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-152">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="fef07-153">Existem vários valores que pode modificar para o plug-in do Maven Olá e uma descrição detalhada para cada um destes elementos está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação.</span><span class="sxs-lookup"><span data-stu-id="fef07-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="fef07-154">Que a ser consiga aceder tal, existem vários valores, realçando neste artigo:</span><span class="sxs-lookup"><span data-stu-id="fef07-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="fef07-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="fef07-155">Element</span></span> | <span data-ttu-id="fef07-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="fef07-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="fef07-157">Especifica uma versão de Olá Olá [Plug-in do Maven para Web Apps do Azure].</span><span class="sxs-lookup"><span data-stu-id="fef07-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="fef07-158">Deve verificar a versão de Olá listada no Olá [Respository Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que está a utilizar Olá versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="fef07-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="fef07-159">Especifica as informações de autenticação de Olá do Azure, que, neste exemplo, contém um `<serverId>` elemento que contenha `azure-auth`; Maven utiliza toolook esse valor dos valores de principal de serviço do Azure Olá no seu Maven *settings.xml* ficheiro, que é definida uma secção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="fef07-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="fef07-160">Especifica o grupo de recursos do Olá destino, que é `maven-plugin` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="fef07-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="fef07-161">grupo de recursos de Olá é criado durante a implementação, se já existir.</span><span class="sxs-lookup"><span data-stu-id="fef07-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="fef07-162">Especifica o nome de destino Olá para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="fef07-163">Neste exemplo, é o nome de destino Olá `maven-web-app-${maven.build.timestamp}`, em que hello `${maven.build.timestamp}` é acrescentado um sufixo neste conflito de tooavoid de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fef07-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="fef07-164">(Olá timestamp é opcional; pode especificar qualquer cadeia exclusiva para o nome da aplicação Olá).</span><span class="sxs-lookup"><span data-stu-id="fef07-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="fef07-165">Especifica a região de destino Olá, que, neste exemplo, é `westus`.</span><span class="sxs-lookup"><span data-stu-id="fef07-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="fef07-166">(Uma lista completa está a ser Olá [Plug-in do Maven para Web Apps do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="fef07-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="fef07-167">Especifica a versão de tempo de execução Java Olá para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="fef07-168">(Uma lista completa está a ser Olá [Plug-in do Maven para Web Apps do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="fef07-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="fef07-169">Especifica o tipo de implementação para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="fef07-170">Por agora, apenas `ftp` é suportada, embora suporte para outros tipos de implementação é de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="fef07-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="fef07-171">Especifica os recursos e destinos de destino que utiliza o Maven quando implementar a sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="fef07-172">Neste exemplo, dois `<resource>` elementos especificar que Maven irão implementar o ficheiro JAR de Olá para a sua aplicação web e Olá *Web. config* ficheiros do projeto de arranque de mola Olá.</span><span class="sxs-lookup"><span data-stu-id="fef07-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="fef07-173">Criar e implementar a sua tooAzure de aplicação web</span><span class="sxs-lookup"><span data-stu-id="fef07-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="fef07-174">Assim que tiver configurado o todas as definições de Olá no Olá precedente secções deste artigo, está pronto toodeploy sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fef07-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="fef07-175">toodo por isso, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fef07-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="fef07-176">Olá linha de comandos ou janela de terminal que estava a utilizar anteriormente, reconstrua o ficheiro JAR de Olá com o Maven se tiver efetuado quaisquer alterações toohello *pom.xml* ficheiro; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="fef07-177">Implementar o tooAzure de aplicação web com o Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fef07-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="fef07-178">Maven irá implementar a sua tooAzure de aplicação web; Se a aplicação web de Olá ainda não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="fef07-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="fef07-179">Quando a web tiver sido implementada, será capaz de toomanage-lo utilizando Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="fef07-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="fef07-180">A aplicação web será listada no **serviços aplicacionais**:</span><span class="sxs-lookup"><span data-stu-id="fef07-180">Your web app will be listed in **App Services**:</span></span>

   ![Aplicação Web listada no portal do Azure serviços aplicacionais][AP01]

* <span data-ttu-id="fef07-182">E Olá URL para a sua aplicação web será listada no Olá **descrição geral** para a sua aplicação web:</span><span class="sxs-lookup"><span data-stu-id="fef07-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinar o URL de Olá para a sua aplicação web][AP02]

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="fef07-184">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fef07-184">Next steps</span></span>

<span data-ttu-id="fef07-185">Para obter mais informações sobre Olá várias tecnologias abordadas neste artigo, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="fef07-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="fef07-186">[Plug-in do Maven para Web Apps do Azure]</span><span class="sxs-lookup"><span data-stu-id="fef07-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="fef07-187">Inicie sessão no tooAzure de Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fef07-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="fef07-188">Como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque da mola</span><span class="sxs-lookup"><span data-stu-id="fef07-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="fef07-189">Criar um Azure principal de serviço com o Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fef07-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="fef07-190">Referência de definições do maven</span><span class="sxs-lookup"><span data-stu-id="fef07-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Interface de linha de comandos do Azure (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefícios de subscritor do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[mola arranque introdução]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in do Maven para Web Apps do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
