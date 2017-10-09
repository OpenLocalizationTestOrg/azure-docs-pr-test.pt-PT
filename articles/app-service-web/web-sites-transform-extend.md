---
title: "extensões e configuração avançada aaaAzure aplicação web do app Service"
description: "Utilize Transformation(XDT) de documento XML declarações tootransform Olá ficheiro applicationHost. config no seu App Service do Azure web app e tooadd extensões privadas tooenable personalizado ações de administração."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Aplicação web do Azure App Service, extensões e configuração avançada
Ao utilizar [transformação do documento XML](http://msdn.microsoft.com/library/dd465326.aspx) declarações (XDT), pode transformar Olá [applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) ficheiro na sua aplicação web no App Service do Azure. Também pode utilizar XDT declarações tooadd extensões privadas tooenable web personalizado aplicação ações de administração. Este artigo inclui uma extensão de aplicação de web de PHP Gestor de exemplo que permita a gestão de definições do PHP através de uma interface web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Configuração avançada através de no applicationHost. config
Olá plataforma do App Service proporciona flexibilidade e controlo de configuração de aplicação web. Apesar do ficheiro de configuração de no applicationHost. config de IIS Olá padrão não está disponível para edição direta no App Service, a plataforma de Olá suporta um modelo declarativo de transformação de no applicationHost. config com base na transformação de documento XML (XDT).

tooleverage esta funcionalidade de transformação, crie um ficheiro de ApplicationHost.xdt com XDT conteúdo e colocar sob a raiz do site (d:\home\site) Olá no Olá [consola Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console). Poderá ser necessário toorestart Olá aplicação Web para o efeito de tootake de alterações.

Olá applicationHost.xdt exemplo a seguir mostra como tooadd um novo tooa de variável de ambiente personalizadas web de aplicação que utiliza 5.4 do PHP.

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

Está disponível a partir da raiz FTP de Olá em LogFiles\Transform um ficheiro de registo com o estado de transformação e os detalhes.

Para obter exemplos adicionais, consulte [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Nota**<br />
Elementos da lista de Olá de módulos em `system.webServer` não pode ser removidos ou reordenados, mas a lista de toohello adições são possíveis.

## <a id="extend"></a>Expandir a sua aplicação web
### <a id="overview"></a>Descrição geral das extensões de aplicações web privada
Serviço de aplicações suporta as extensões de aplicação web como um ponto de extensibilidade para ações administrativas. Na verdade, algumas funcionalidades da plataforma de serviço de aplicações são implementadas como extensões pré-instaladas. Enquanto não não possível modificar as extensões de plataforma pré-instaladas Olá, pode criar e configurar extensões privadas para a sua própria aplicação web. Esta funcionalidade baseia-se também em declarações de XDT. passos de Olá fundamentais para a criação de uma extensão de aplicação web privada são seguinte Olá:

1. Extensão de aplicação de Web **conteúdo**: criar qualquer aplicação web suportada pelo App Service
2. Extensão de aplicação de Web **declaração**: criar um ficheiro de ApplicationHost.xdt
3. Extensão de aplicação de Web **implementação**: colocar o conteúdo na pasta de SiteExtensions Olá em`root`

Ligações internas para a aplicação web de Olá devem apontar tooa caminho relativo toohello caminho da aplicação especificado no ficheiro de ApplicationHost.xdt Olá. Qualquer ficheiro de ApplicationHost.xdt toohello alteração requer uma reciclagem de aplicações web.

**Tenha em atenção**: estão disponíveis informações adicionais para estes elementos chaves no [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Um exemplo de detalhado é incluído tooillustrate Olá passos para criar e ativar uma extensão de aplicação web privada. Olá, código de origem, por exemplo, o Gestor de PHP Olá que forma pode ser transferida a partir do [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a>Exemplo de extensão de aplicação Web: o Gestor de PHP
O Gestor de PHP é uma extensão de aplicação web que permite aos administradores de aplicação web tooeasily ver e configurar as definições do PHP utilizando uma interface web em vez de ter ficheiros. ini PHP toomodify diretamente. Ficheiros de configuração comuns para PHP incluem o ficheiro php.ini de Olá localizado em programas e Olá. ficheiro user.ini localizado na pasta raiz de Olá da sua aplicação web. Uma vez que o ficheiro php.ini de Olá não é diretamente editável no Olá plataforma do App Service, Olá extensão PHP Manager utiliza Olá. user.ini ficheiro tooapply alterações de definição.

#### <a id="PHPwebapp"></a>Olá aplicação web Gestor de PHP
Olá que se segue Olá home page do Olá PHP Gestor de implementação:

![TransformSitePHPUI][TransformSitePHPUI]

Como pode ver, uma extensão de aplicação web é semelhante uma aplicação web normal, mas com um ficheiro ApplicationHost.xdt adicional colocado na pasta raiz de Olá da aplicação web de Olá (obter mais detalhes sobre o ficheiro de ApplicationHost.xdt Olá estão disponíveis na secção seguinte, Olá deste artigo).

Olá extensão PHP Manager foi criado utilizando o modelo de Visual Studio ASP.NET 4 aplicação Web MVC Olá. Olá seguinte vista do Explorador de soluções mostra estrutura Olá de Olá extensão PHP Manager.

![TransformSiteSolEx][TransformSiteSolEx]

Olá apenas especial lógica necessária para o ficheiro e/s é tooindicate onde hello diretório wwwroot da aplicação web de Olá está localizado. Como hello seguinte mostra de exemplo de código, Olá ambiente variável "HOME" indica Olá caminho da raiz da aplicação web e o caminho de wwwroot Olá pode ser construído, acrescentando "site\wwwroot":

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


Depois de ter o caminho do diretório Olá, pode utilizar tooread de operações de e/s de ficheiro regular e escrever toofiles.

Um ponto de advertência com extensões de aplicações web regards processamento Olá das ligações internos.  Se tiver quaisquer ligações nos seus ficheiros HTML que atribua caminhos absolutos toointernal ligações na sua aplicação web, tem de garantir que essas ligações são prepended com o nome da extensão como a raiz. Isto é necessário porque Olá de raiz para a extensão é agora "/`[your-extension-name]`/" em vez de ser apenas "/", internas, por isso, quaisquer ligações devem ser atualizadas em conformidade. Por exemplo, suponha que o seu código inclui um seguinte de toohello de ligação:

`"<a href="/Home/Settings">PHP Settings</a>"`

Quando a ligação de Olá faz parte de uma extensão de aplicação web, tem de estar Olá ligação no Olá seguinte formato:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

Pode contornar este requisito utilizando apenas caminhos relativos a sua aplicação web, ou num Olá caso de aplicações do ASP.NET, utilizando Olá `@Html.ActionLink` método que cria ligações adequadas Olá por si.

#### <a id="XDT"></a>ficheiro de applicationHost.xdt Olá
código de Olá para a extensão de aplicação web passa em %HOME%\SiteExtensions\[nome da extensão]. Receberá um telefonema nosso este Olá extensão de raiz.  

tooregister a extensão de aplicação web com o ficheiro applicationHost. config de Olá, terá de tooplace um ficheiro chamado ApplicationHost.xdt na raiz da extensão de Olá. o conteúdo do ficheiro de ApplicationHost.xdt Olá Olá pode da seguinte forma:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

Selecione como o nome de extensão de nome de Olá deve ter Olá mesmo nome como a pasta de raiz de extensão.

Isto não tem efeito Olá de adicionar um novo caminho toohello da aplicação `system.applicationHost` lista de sites no site SCM Olá. site SCM Olá é um ponto de final de administração de sites com as credenciais de acesso específicas. Tem Olá URL `https://[your-site-name].scm.azurewebsites.net`.  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <a id="deploy"></a>Implementação de extensão de aplicação Web
tooinstall a extensão de aplicação web, pode utilizar o FTP toocopy todos os ficheiros de Olá do seu toohello de aplicação web `\SiteExtensions\[your-extension-name]` pasta da aplicação web de Olá no qual pretende que a extensão de Olá tooinstall.  Ser se toocopy Olá ApplicationHost.xdt toothis localização do ficheiro, bem como. Reinicie a aplicação tooenable Olá da extensão web.

Deve ser capaz de toosee a extensão de aplicação web em:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Tenha em atenção que Olá que URL aspeto apenas Olá URL para a sua aplicação web, exceto que utiliza HTTPS e contém "SCM".

É possível toodisable todos os privada (não previamente instalado) extensões para a sua aplicação web durante a programação e as investigações, adicionando as definições de uma aplicação com a chave de Olá `WEBSITE_PRIVATE_EXTENSIONS` e um valor de `0`.

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

