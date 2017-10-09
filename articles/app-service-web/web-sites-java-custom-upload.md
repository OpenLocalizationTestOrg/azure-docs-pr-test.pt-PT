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
# <a name="upload-a-custom-java-web-app-tooazure"></a>Carregar um tooAzure de aplicação web de Java personalizada
Este tópico explica como tooupload um Java personalizada aplicação web demasiado[App Service do Azure] Web Apps. Incluído é informações que se aplicam tooany site em Java ou aplicação web e também alguns exemplos de aplicações específicas.

Tenha em atenção que o Azure fornece um meio para criar as web apps Java utilizando a IU de configuração do Portal do Azure Olá e Olá Azure Marketplace, conforme documentado no [criar uma aplicação web Java no App Service do Azure](web-sites-java-get-started.md). Este tutorial é para cenários nos quais não pretende IU de configuração toouse Olá Portal do Azure ou Olá Azure Marketplace.  

## <a name="configuration-guidelines"></a>Diretrizes de configuração
seguinte Olá descreve definições de Olá esperadas para aplicações web em Java personalizadas no Azure.

* porta HTTP de Olá utilizada pelo Olá processo Java é atribuída dinamicamente.  processo de Olá tem de utilizar a porta Olá da variável de ambiente de Olá `HTTP_PLATFORM_PORT`.
* Todos os escutam as portas diferentes de escuta HTTP único Olá deve ser desativada.  No Tomcat, que inclui o encerramento de Olá, HTTPS e AJP portas.
* contentor de Olá tem toobe configurado para apenas o tráfego IPv4.
* Olá **arranque** comando para a aplicação de Olá tem toobe definido na configuração de Olá.
* As aplicações que necessitam da permissão de escrita de diretórios com precisam toobe localizado no diretório conteúdo da aplicação web do Azure Olá, que é **D:\home**.  variável de ambiente de Olá `HOME` refere-se tooD:\home.  

Pode definir variáveis de ambiente, conforme necessário, no ficheiro Web. config de Olá.

## <a name="webconfig-httpplatform-configuration"></a>configuração do Web. config httpPlatform
Olá informações seguintes descrevem Olá **httpPlatform** formato na Web. config.

**argumentos** (predefinição = ""). Argumentos toohello executável ou script especificado no Olá **processPath** definição.

Exemplos (mostrada com **processPath** incluídos):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello caminho executável ou script que irá iniciar um processo a escutar para pedidos HTTP.

Exemplos:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (predefinição = 10.) Número de vezes processo Olá especificado no **processPath** é permitido toocrash por minuto. Se este limite for excedido, **HttpPlatformHandler** irá parar a iniciar o processo de Olá para o resto Olá minuto Olá.

**requestTimeout** (predefinição = "00: 02:00".) Duração para o qual **HttpPlatformHandler** irá aguardar uma resposta do processo de Olá está a escutar `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (predefinição = 10.) Número de vezes que **HttpPlatformHandler** tentará o processo de Olá toolaunch especificado no **processPath**. Consulte **startupTimeLimit** para obter mais detalhes.

**startupTimeLimit** (predefinição = 10 segundos.) Duração para o qual **HttpPlatformHandler** irá aguardar Olá executável/script toostart um processo a escutar na porta Olá.  Se este tempo limite for excedido, **HttpPlatformHandler** irá cancelar o processo de Olá e tente toolaunch-a novamente **startupRetryCount** vezes.

**stdoutLogEnabled** (predefinição = "true".) Se for VERDADEIRO, **stdout** e **stderr** para o processo de Olá especificado no Olá **processPath** definição será redirecionado toohello ficheiro especificado no  **stdoutLogFile** (consulte **stdoutLogFile** secção).

**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Caminho absoluto do ficheiro para o qual **stdout** e **stderr** do processo de Olá especificado no **processPath** serão registados.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`é um marcador de posição especial que tem como parte de toospecified **argumentos** ou como parte de Olá **httpPlatform** **environmentVariables** lista. Esta será substituída por uma porta gerada internamente pelo **HttpPlatformHandler** para que o processo de Olá especificado pelo **processPath** pode escutar nesta porta.
> 
> 

## <a name="deployment"></a>Implementação
As web apps Java com base podem ser implementadas facilmente através da maioria das Olá que mesmo significa que é utilizada com aplicações de web de serviços de informação Internet (IIS) com base Olá.  FTP, Git e Kudu é todos suportado como mecanismos de implementação, como é Olá integrada SCM capacidade para aplicações web. O WebDeploy funciona como um protocolo, no entanto, como Java não está a ser desenvolvida no Visual Studio, o WebDeploy não coincide com casos de utilização de implementação de aplicação web Java.

## <a name="application-configuration-examples"></a>Exemplos de configuração de aplicação
Para Olá seguintes aplicações, um ficheiro Web. config e Olá configuração da aplicação é fornecida tal como exemplos tooshow como tooenable a aplicação de Java no Web Apps do App Service.

### <a name="tomcat"></a>Tomcat
Quando existem duas variações no Tomcat que são fornecidas com as Web Apps do App Service, ainda é bastante possíveis tooupload instâncias específicas do cliente. Abaixo está um exemplo de uma instalação do Tomcat com um diferente Java Máquina Virtual (JVM).

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

No lado de Tomcat Olá, existem algumas alterações de configuração que necessitam de toobe efetuada. Olá server.xml precisa tooset toobe editá-lo:

* Porta de encerramento = -1
* Porta do conector HTTP = ${port.http}
* Endereço do conector HTTP = "127.0.0.1"
* Comente HTTPS e AJP conectores
* definição de IPv4 Olá também pode ser definida no ficheiro de catalina.properties olá onde pode adicionar`java.net.preferIPv4Stack=true`

Chamadas de Direct3D não são suportadas em Web Apps do App Service. toodisable das, adicione Olá opção Java a seguir a aplicação, deverá certificar-essas chamadas:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Como é o caso de Olá para Tomcat, os clientes podem carregar as suas próprias instâncias para Jetty. No caso de Olá da execução instalação completa de Olá do Jetty, configuração de Olá seria este aspeto:

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

Olá Jetty configuração necessita de toobe alterado no Olá start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
Na ordem tooget uma aplicação de Springboot com necessário tooupload o ficheiro JAR ou WAR e adicione Olá seguir o ficheiro Web. config. ficheiro Web. config de Olá passa na pasta de wwwroot Olá. Em Web. config de Olá ajustar o ficheiro JAR do Olá argumentos toopoint tooyour, no Olá seguintes exemplo Olá JAR ficheiro está localizado na pasta de wwwroot de Olá bem.  

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


### <a name="hudson"></a>Hudson
Nosso teste utilizado Olá war Hudson 3.1.2 e Olá instância de Tomcat 7.0.50 predefinida, mas sem utilizar as ações de tooset Olá IU cópias de segurança.  Uma vez que Hudson é uma ferramenta de compilação de software, é aconselhado tooinstall-lo na dedicado instâncias onde hello **AlwaysOn** sinalizador pode ser definido na aplicação web de Olá.

1. Na sua aplicação web raiz do diretório, ou seja, **d:\home\site\wwwroot**, crie um **webapps** diretório (se não estiver já presente) e coloque Hudson.war no **d:\home\site\wwwroot\webapps**.
2. Transferir o maven apache 3.0.5 (compatível com Hudson) e colocá-lo no **d:\home\site\wwwroot**.
3. Criar Web. config no **d:\home\site\wwwroot** e colar Olá seguir o conteúdo no mesmo:
   
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
   
    Neste momento Olá web aplicação pode ser reiniciadas tootake Olá alterações.  Ligar toohttp://yourwebapp/hudson toostart Hudson.
4. Depois de Hudson configura si próprio, deverá ver Olá ecrã a seguir:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Olá acesso página de configuração Hudson: clique em **gerir Hudson**e, em seguida, clique em **Configurar sistema**.
6. Configure Olá JDK conforme mostrado abaixo:
   
    ![Configuração de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Configure o Maven, como mostrado abaixo:
   
    ![Configuração do maven](./media/web-sites-java-custom-upload/maven.png)
8. Guarde as definições de Olá. Hudson deve ser configurado e pronto a utilizar.

Para obter informações adicionais sobre Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay é suportado nas Web Apps do App Service. Uma vez que o Liferay pode exigir memória significativa, aplicação web de Olá tem toorun num médio ou grande dedicado worker, que pode fornecer memória suficiente. Liferay também demora vários minutos toostart cópias de segurança. Por esse motivo, é recomendável que defina a aplicação web de Olá demasiado**Always On**.  

Utilizar Liferay 6.1.2 que Comunidade edição GA3 incluídas com Tomcat, hello ficheiros seguintes foram editados depois de transferir Liferay:

**Server.XML**

* Altere o encerramento porta demasiado-1.
* Alterar o conetor HTTP demasiado`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Comente conector AJP Olá.

No Olá **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** pasta, crie um ficheiro denominado **portal ext.properties**. Este ficheiro necessita de uma linha toocontain, conforme mostrado aqui:

    liferay.home=%HOME%/site/wwwroot/liferay

Em Olá mesmo nível de diretório como pasta do tomcat 7.0.40 Olá, crie um ficheiro denominado **Web. config** com Olá seguinte conteúdo:

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

Em Olá **httpPlatform** bloquear, hello **requestTimeout** estiver definido demasiado "00: 10:00".  Este pode ser reduzido mas, em seguida, é provável que toosee alguns erros de tempo limite ao Liferay é bootstrapping.  Se este valor for alterado, em seguida, Olá **connectionTimeout** no tomcat Olá server.xml também deverá ser modificado.  

É importante salientar que varariable de ambiente JRE_HOME Olá é especificada em Olá acima Web. config toopoint toohello, JDK de 64 bits. predefinição de Olá é de 32 bits, mas uma vez que Liferay podem requerer níveis elevadas de memória, é recomendado toouse Olá JDK de 64 bits.

Depois de efetuar estas alterações, reinicie a aplicação web em execução Liferay, em seguida, abra http://yourwebapp. portal de Liferay Olá está disponível a partir da raiz de aplicação web de Olá. 

## <a name="next-steps"></a>Passos seguintes
Para mais informações sobre Liferay, consulte [http://www.liferay.com](http://www.liferay.com).

Para obter mais informações sobre o Java, visite [do Azure para programadores de Java](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[App Service do Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
