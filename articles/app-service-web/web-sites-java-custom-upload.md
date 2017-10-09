---
title: "aaaUpload um tooAzure de aplicação web de Java personalizada"
description: "Este tutorial mostra como tooupload um Java personalizada web tooAzure de aplicação Web Apps do App Service."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="e13e2-103">Carregar um tooAzure de aplicação web de Java personalizada</span><span class="sxs-lookup"><span data-stu-id="e13e2-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="e13e2-104">Este tópico explica como tooupload um Java personalizada aplicação web demasiado[App Service do Azure] Web Apps.</span><span class="sxs-lookup"><span data-stu-id="e13e2-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="e13e2-105">Incluído é informações que se aplicam tooany site em Java ou aplicação web e também alguns exemplos de aplicações específicas.</span><span class="sxs-lookup"><span data-stu-id="e13e2-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="e13e2-106">Tenha em atenção que o Azure fornece um meio para criar as web apps Java utilizando a IU de configuração do Portal do Azure Olá e Olá Azure Marketplace, conforme documentado no [criar uma aplicação web Java no App Service do Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e13e2-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="e13e2-107">Este tutorial é para cenários nos quais não pretende IU de configuração toouse Olá Portal do Azure ou Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e13e2-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="e13e2-108">Diretrizes de configuração</span><span class="sxs-lookup"><span data-stu-id="e13e2-108">Configuration guidelines</span></span>
<span data-ttu-id="e13e2-109">seguinte Olá descreve definições de Olá esperadas para aplicações web em Java personalizadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="e13e2-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="e13e2-110">porta HTTP de Olá utilizada pelo Olá processo Java é atribuída dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e13e2-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="e13e2-111">processo de Olá tem de utilizar a porta Olá da variável de ambiente de Olá `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="e13e2-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="e13e2-112">Todos os escutam as portas diferentes de escuta HTTP único Olá deve ser desativada.</span><span class="sxs-lookup"><span data-stu-id="e13e2-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="e13e2-113">No Tomcat, que inclui o encerramento de Olá, HTTPS e AJP portas.</span><span class="sxs-lookup"><span data-stu-id="e13e2-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="e13e2-114">contentor de Olá tem toobe configurado para apenas o tráfego IPv4.</span><span class="sxs-lookup"><span data-stu-id="e13e2-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="e13e2-115">Olá **arranque** comando para a aplicação de Olá tem toobe definido na configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="e13e2-116">As aplicações que necessitam da permissão de escrita de diretórios com precisam toobe localizado no diretório conteúdo da aplicação web do Azure Olá, que é **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="e13e2-117">variável de ambiente de Olá `HOME` refere-se tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="e13e2-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="e13e2-118">Pode definir variáveis de ambiente, conforme necessário, no ficheiro Web. config de Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="e13e2-119">configuração do Web. config httpPlatform</span><span class="sxs-lookup"><span data-stu-id="e13e2-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="e13e2-120">Olá informações seguintes descrevem Olá **httpPlatform** formato na Web. config.</span><span class="sxs-lookup"><span data-stu-id="e13e2-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="e13e2-121">**argumentos** (predefinição = "").</span><span class="sxs-lookup"><span data-stu-id="e13e2-121">**arguments** (Default="").</span></span> <span data-ttu-id="e13e2-122">Argumentos toohello executável ou script especificado no Olá **processPath** definição.</span><span class="sxs-lookup"><span data-stu-id="e13e2-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="e13e2-123">Exemplos (mostrada com **processPath** incluídos):</span><span class="sxs-lookup"><span data-stu-id="e13e2-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="e13e2-124">**processPath** -toohello caminho executável ou script que irá iniciar um processo a escutar para pedidos HTTP.</span><span class="sxs-lookup"><span data-stu-id="e13e2-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="e13e2-125">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="e13e2-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="e13e2-126">**rapidFailsPerMinute** (predefinição = 10.) Número de vezes processo Olá especificado no **processPath** é permitido toocrash por minuto.</span><span class="sxs-lookup"><span data-stu-id="e13e2-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="e13e2-127">Se este limite for excedido, **HttpPlatformHandler** irá parar a iniciar o processo de Olá para o resto Olá minuto Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="e13e2-128">**requestTimeout** (predefinição = "00: 02:00".) Duração para o qual **HttpPlatformHandler** irá aguardar uma resposta do processo de Olá está a escutar `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="e13e2-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="e13e2-129">**startupRetryCount** (predefinição = 10.) Número de vezes que **HttpPlatformHandler** tentará o processo de Olá toolaunch especificado no **processPath**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="e13e2-130">Consulte **startupTimeLimit** para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e13e2-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="e13e2-131">**startupTimeLimit** (predefinição = 10 segundos.) Duração para o qual **HttpPlatformHandler** irá aguardar Olá executável/script toostart um processo a escutar na porta Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="e13e2-132">Se este tempo limite for excedido, **HttpPlatformHandler** irá cancelar o processo de Olá e tente toolaunch-a novamente **startupRetryCount** vezes.</span><span class="sxs-lookup"><span data-stu-id="e13e2-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="e13e2-133">**stdoutLogEnabled** (predefinição = "true".) Se for VERDADEIRO, **stdout** e **stderr** para o processo de Olá especificado no Olá **processPath** definição será redirecionado toohello ficheiro especificado no  **stdoutLogFile** (consulte **stdoutLogFile** secção).</span><span class="sxs-lookup"><span data-stu-id="e13e2-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="e13e2-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Caminho absoluto do ficheiro para o qual **stdout** e **stderr** do processo de Olá especificado no **processPath** serão registados.</span><span class="sxs-lookup"><span data-stu-id="e13e2-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="e13e2-135">`%HTTP_PLATFORM_PORT%`é um marcador de posição especial que tem como parte de toospecified **argumentos** ou como parte de Olá **httpPlatform** **environmentVariables** lista.</span><span class="sxs-lookup"><span data-stu-id="e13e2-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="e13e2-136">Esta será substituída por uma porta gerada internamente pelo **HttpPlatformHandler** para que o processo de Olá especificado pelo **processPath** pode escutar nesta porta.</span><span class="sxs-lookup"><span data-stu-id="e13e2-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="e13e2-137">Implementação</span><span class="sxs-lookup"><span data-stu-id="e13e2-137">Deployment</span></span>
<span data-ttu-id="e13e2-138">As web apps Java com base podem ser implementadas facilmente através da maioria das Olá que mesmo significa que é utilizada com aplicações de web de serviços de informação Internet (IIS) com base Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="e13e2-139">FTP, Git e Kudu é todos suportado como mecanismos de implementação, como é Olá integrada SCM capacidade para aplicações web.</span><span class="sxs-lookup"><span data-stu-id="e13e2-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="e13e2-140">O WebDeploy funciona como um protocolo, no entanto, como Java não está a ser desenvolvida no Visual Studio, o WebDeploy não coincide com casos de utilização de implementação de aplicação web Java.</span><span class="sxs-lookup"><span data-stu-id="e13e2-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="e13e2-141">Exemplos de configuração de aplicação</span><span class="sxs-lookup"><span data-stu-id="e13e2-141">Application configuration Examples</span></span>
<span data-ttu-id="e13e2-142">Para Olá seguintes aplicações, um ficheiro Web. config e Olá configuração da aplicação é fornecida tal como exemplos tooshow como tooenable a aplicação de Java no Web Apps do App Service.</span><span class="sxs-lookup"><span data-stu-id="e13e2-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="e13e2-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="e13e2-143">Tomcat</span></span>
<span data-ttu-id="e13e2-144">Quando existem duas variações no Tomcat que são fornecidas com as Web Apps do App Service, ainda é bastante possíveis tooupload instâncias específicas do cliente.</span><span class="sxs-lookup"><span data-stu-id="e13e2-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="e13e2-145">Abaixo está um exemplo de uma instalação do Tomcat com um diferente Java Máquina Virtual (JVM).</span><span class="sxs-lookup"><span data-stu-id="e13e2-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="e13e2-146">No lado de Tomcat Olá, existem algumas alterações de configuração que necessitam de toobe efetuada.</span><span class="sxs-lookup"><span data-stu-id="e13e2-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="e13e2-147">Olá server.xml precisa tooset toobe editá-lo:</span><span class="sxs-lookup"><span data-stu-id="e13e2-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="e13e2-148">Porta de encerramento = -1</span><span class="sxs-lookup"><span data-stu-id="e13e2-148">Shutdown port = -1</span></span>
* <span data-ttu-id="e13e2-149">Porta do conector HTTP = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="e13e2-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="e13e2-150">Endereço do conector HTTP = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="e13e2-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="e13e2-151">Comente HTTPS e AJP conectores</span><span class="sxs-lookup"><span data-stu-id="e13e2-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="e13e2-152">definição de IPv4 Olá também pode ser definida no ficheiro de catalina.properties olá onde pode adicionar`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="e13e2-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="e13e2-153">Chamadas de Direct3D não são suportadas em Web Apps do App Service.</span><span class="sxs-lookup"><span data-stu-id="e13e2-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="e13e2-154">toodisable das, adicione Olá opção Java a seguir a aplicação, deverá certificar-essas chamadas:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="e13e2-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="e13e2-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="e13e2-155">Jetty</span></span>
<span data-ttu-id="e13e2-156">Como é o caso de Olá para Tomcat, os clientes podem carregar as suas próprias instâncias para Jetty.</span><span class="sxs-lookup"><span data-stu-id="e13e2-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="e13e2-157">No caso de Olá da execução instalação completa de Olá do Jetty, configuração de Olá seria este aspeto:</span><span class="sxs-lookup"><span data-stu-id="e13e2-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="e13e2-158">Olá Jetty configuração necessita de toobe alterado no Olá start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="e13e2-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="e13e2-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="e13e2-159">Springboot</span></span>
<span data-ttu-id="e13e2-160">Na ordem tooget uma aplicação de Springboot com necessário tooupload o ficheiro JAR ou WAR e adicione Olá seguir o ficheiro Web. config.</span><span class="sxs-lookup"><span data-stu-id="e13e2-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="e13e2-161">ficheiro Web. config de Olá passa na pasta de wwwroot Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="e13e2-162">Em Web. config de Olá ajustar o ficheiro JAR do Olá argumentos toopoint tooyour, no Olá seguintes exemplo Olá JAR ficheiro está localizado na pasta de wwwroot de Olá bem.</span><span class="sxs-lookup"><span data-stu-id="e13e2-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="e13e2-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="e13e2-163">Hudson</span></span>
<span data-ttu-id="e13e2-164">Nosso teste utilizado Olá war Hudson 3.1.2 e Olá instância de Tomcat 7.0.50 predefinida, mas sem utilizar as ações de tooset Olá IU cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="e13e2-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="e13e2-165">Uma vez que Hudson é uma ferramenta de compilação de software, é aconselhado tooinstall-lo na dedicado instâncias onde hello **AlwaysOn** sinalizador pode ser definido na aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="e13e2-166">Na sua aplicação web raiz do diretório, ou seja, **d:\home\site\wwwroot**, crie um **webapps** diretório (se não estiver já presente) e coloque Hudson.war no **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="e13e2-167">Transferir o maven apache 3.0.5 (compatível com Hudson) e colocá-lo no **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="e13e2-168">Criar Web. config no **d:\home\site\wwwroot** e colar Olá seguir o conteúdo no mesmo:</span><span class="sxs-lookup"><span data-stu-id="e13e2-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="e13e2-169">Neste momento Olá web aplicação pode ser reiniciadas tootake Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="e13e2-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="e13e2-170">Ligar toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="e13e2-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="e13e2-171">Depois de Hudson configura si próprio, deverá ver Olá ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="e13e2-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="e13e2-173">Olá acesso página de configuração Hudson: clique em **gerir Hudson**e, em seguida, clique em **Configurar sistema**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="e13e2-174">Configure Olá JDK conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="e13e2-174">Configure hello JDK as shown below:</span></span>
   
    ![Configuração de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="e13e2-176">Configure o Maven, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="e13e2-176">Configure Maven as shown below:</span></span>
   
    ![Configuração do maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="e13e2-178">Guarde as definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-178">Save hello settings.</span></span> <span data-ttu-id="e13e2-179">Hudson deve ser configurado e pronto a utilizar.</span><span class="sxs-lookup"><span data-stu-id="e13e2-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="e13e2-180">Para obter informações adicionais sobre Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="e13e2-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="e13e2-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="e13e2-181">Liferay</span></span>
<span data-ttu-id="e13e2-182">Liferay é suportado nas Web Apps do App Service.</span><span class="sxs-lookup"><span data-stu-id="e13e2-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="e13e2-183">Uma vez que o Liferay pode exigir memória significativa, aplicação web de Olá tem toorun num médio ou grande dedicado worker, que pode fornecer memória suficiente.</span><span class="sxs-lookup"><span data-stu-id="e13e2-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="e13e2-184">Liferay também demora vários minutos toostart cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="e13e2-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="e13e2-185">Por esse motivo, é recomendável que defina a aplicação web de Olá demasiado**Always On**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="e13e2-186">Utilizar Liferay 6.1.2 que Comunidade edição GA3 incluídas com Tomcat, hello ficheiros seguintes foram editados depois de transferir Liferay:</span><span class="sxs-lookup"><span data-stu-id="e13e2-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="e13e2-187">**Server.XML**</span><span class="sxs-lookup"><span data-stu-id="e13e2-187">**Server.xml**</span></span>

* <span data-ttu-id="e13e2-188">Altere o encerramento porta demasiado-1.</span><span class="sxs-lookup"><span data-stu-id="e13e2-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="e13e2-189">Alterar o conetor HTTP demasiado`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="e13e2-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="e13e2-190">Comente conector AJP Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="e13e2-191">No Olá **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** pasta, crie um ficheiro denominado **portal ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="e13e2-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="e13e2-192">Este ficheiro necessita de uma linha toocontain, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="e13e2-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="e13e2-193">Em Olá mesmo nível de diretório como pasta do tomcat 7.0.40 Olá, crie um ficheiro denominado **Web. config** com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="e13e2-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="e13e2-194">Em Olá **httpPlatform** bloquear, hello **requestTimeout** estiver definido demasiado "00: 10:00".</span><span class="sxs-lookup"><span data-stu-id="e13e2-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="e13e2-195">Este pode ser reduzido mas, em seguida, é provável que toosee alguns erros de tempo limite ao Liferay é bootstrapping.</span><span class="sxs-lookup"><span data-stu-id="e13e2-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="e13e2-196">Se este valor for alterado, em seguida, Olá **connectionTimeout** no tomcat Olá server.xml também deverá ser modificado.</span><span class="sxs-lookup"><span data-stu-id="e13e2-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="e13e2-197">É importante salientar que varariable de ambiente JRE_HOME Olá é especificada em Olá acima Web. config toopoint toohello, JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="e13e2-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="e13e2-198">predefinição de Olá é de 32 bits, mas uma vez que Liferay podem requerer níveis elevadas de memória, é recomendado toouse Olá JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="e13e2-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="e13e2-199">Depois de efetuar estas alterações, reinicie a aplicação web em execução Liferay, em seguida, abra http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="e13e2-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="e13e2-200">portal de Liferay Olá está disponível a partir da raiz de aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="e13e2-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e13e2-201">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e13e2-201">Next steps</span></span>
<span data-ttu-id="e13e2-202">Para mais informações sobre Liferay, consulte [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="e13e2-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="e13e2-203">Para obter mais informações sobre o Java, visite [do Azure para programadores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="e13e2-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[App Service do Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
