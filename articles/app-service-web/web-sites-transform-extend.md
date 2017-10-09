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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="e4fa2-103">Aplicação web do Azure App Service, extensões e configuração avançada</span><span class="sxs-lookup"><span data-stu-id="e4fa2-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="e4fa2-104">Ao utilizar [transformação do documento XML](http://msdn.microsoft.com/library/dd465326.aspx) declarações (XDT), pode transformar Olá [applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) ficheiro na sua aplicação web no App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="e4fa2-105">Também pode utilizar XDT declarações tooadd extensões privadas tooenable web personalizado aplicação ações de administração.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="e4fa2-106">Este artigo inclui uma extensão de aplicação de web de PHP Gestor de exemplo que permita a gestão de definições do PHP através de uma interface web.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="e4fa2-107"><a id="transform"></a>Configuração avançada através de no applicationHost. config</span><span class="sxs-lookup"><span data-stu-id="e4fa2-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="e4fa2-108">Olá plataforma do App Service proporciona flexibilidade e controlo de configuração de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="e4fa2-109">Apesar do ficheiro de configuração de no applicationHost. config de IIS Olá padrão não está disponível para edição direta no App Service, a plataforma de Olá suporta um modelo declarativo de transformação de no applicationHost. config com base na transformação de documento XML (XDT).</span><span class="sxs-lookup"><span data-stu-id="e4fa2-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="e4fa2-110">tooleverage esta funcionalidade de transformação, crie um ficheiro de ApplicationHost.xdt com XDT conteúdo e colocar sob a raiz do site (d:\home\site) Olá no Olá [consola Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="e4fa2-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="e4fa2-111">Poderá ser necessário toorestart Olá aplicação Web para o efeito de tootake de alterações.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="e4fa2-112">Olá applicationHost.xdt exemplo a seguir mostra como tooadd um novo tooa de variável de ambiente personalizadas web de aplicação que utiliza 5.4 do PHP.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="e4fa2-113">Está disponível a partir da raiz FTP de Olá em LogFiles\Transform um ficheiro de registo com o estado de transformação e os detalhes.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="e4fa2-114">Para obter exemplos adicionais, consulte [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="e4fa2-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="e4fa2-115">**Nota**</span><span class="sxs-lookup"><span data-stu-id="e4fa2-115">**Note**</span></span><br />
<span data-ttu-id="e4fa2-116">Elementos da lista de Olá de módulos em `system.webServer` não pode ser removidos ou reordenados, mas a lista de toohello adições são possíveis.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="e4fa2-117"><a id="extend"></a>Expandir a sua aplicação web</span><span class="sxs-lookup"><span data-stu-id="e4fa2-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="e4fa2-118"><a id="overview"></a>Descrição geral das extensões de aplicações web privada</span><span class="sxs-lookup"><span data-stu-id="e4fa2-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="e4fa2-119">Serviço de aplicações suporta as extensões de aplicação web como um ponto de extensibilidade para ações administrativas.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="e4fa2-120">Na verdade, algumas funcionalidades da plataforma de serviço de aplicações são implementadas como extensões pré-instaladas.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="e4fa2-121">Enquanto não não possível modificar as extensões de plataforma pré-instaladas Olá, pode criar e configurar extensões privadas para a sua própria aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="e4fa2-122">Esta funcionalidade baseia-se também em declarações de XDT.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="e4fa2-123">passos de Olá fundamentais para a criação de uma extensão de aplicação web privada são seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="e4fa2-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="e4fa2-124">Extensão de aplicação de Web **conteúdo**: criar qualquer aplicação web suportada pelo App Service</span><span class="sxs-lookup"><span data-stu-id="e4fa2-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="e4fa2-125">Extensão de aplicação de Web **declaração**: criar um ficheiro de ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="e4fa2-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="e4fa2-126">Extensão de aplicação de Web **implementação**: colocar o conteúdo na pasta de SiteExtensions Olá em`root`</span><span class="sxs-lookup"><span data-stu-id="e4fa2-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="e4fa2-127">Ligações internas para a aplicação web de Olá devem apontar tooa caminho relativo toohello caminho da aplicação especificado no ficheiro de ApplicationHost.xdt Olá.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="e4fa2-128">Qualquer ficheiro de ApplicationHost.xdt toohello alteração requer uma reciclagem de aplicações web.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="e4fa2-129">**Tenha em atenção**: estão disponíveis informações adicionais para estes elementos chaves no [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="e4fa2-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="e4fa2-130">Um exemplo de detalhado é incluído tooillustrate Olá passos para criar e ativar uma extensão de aplicação web privada.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="e4fa2-131">Olá, código de origem, por exemplo, o Gestor de PHP Olá que forma pode ser transferida a partir do [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="e4fa2-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="e4fa2-132"><a id="SiteSample"></a>Exemplo de extensão de aplicação Web: o Gestor de PHP</span><span class="sxs-lookup"><span data-stu-id="e4fa2-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="e4fa2-133">O Gestor de PHP é uma extensão de aplicação web que permite aos administradores de aplicação web tooeasily ver e configurar as definições do PHP utilizando uma interface web em vez de ter ficheiros. ini PHP toomodify diretamente.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="e4fa2-134">Ficheiros de configuração comuns para PHP incluem o ficheiro php.ini de Olá localizado em programas e Olá. ficheiro user.ini localizado na pasta raiz de Olá da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="e4fa2-135">Uma vez que o ficheiro php.ini de Olá não é diretamente editável no Olá plataforma do App Service, Olá extensão PHP Manager utiliza Olá. user.ini ficheiro tooapply alterações de definição.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="e4fa2-136"><a id="PHPwebapp"></a>Olá aplicação web Gestor de PHP</span><span class="sxs-lookup"><span data-stu-id="e4fa2-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="e4fa2-137">Olá que se segue Olá home page do Olá PHP Gestor de implementação:</span><span class="sxs-lookup"><span data-stu-id="e4fa2-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="e4fa2-139">Como pode ver, uma extensão de aplicação web é semelhante uma aplicação web normal, mas com um ficheiro ApplicationHost.xdt adicional colocado na pasta raiz de Olá da aplicação web de Olá (obter mais detalhes sobre o ficheiro de ApplicationHost.xdt Olá estão disponíveis na secção seguinte, Olá deste artigo).</span><span class="sxs-lookup"><span data-stu-id="e4fa2-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="e4fa2-140">Olá extensão PHP Manager foi criado utilizando o modelo de Visual Studio ASP.NET 4 aplicação Web MVC Olá.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="e4fa2-141">Olá seguinte vista do Explorador de soluções mostra estrutura Olá de Olá extensão PHP Manager.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="e4fa2-143">Olá apenas especial lógica necessária para o ficheiro e/s é tooindicate onde hello diretório wwwroot da aplicação web de Olá está localizado.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="e4fa2-144">Como hello seguinte mostra de exemplo de código, Olá ambiente variável "HOME" indica Olá caminho da raiz da aplicação web e o caminho de wwwroot Olá pode ser construído, acrescentando "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="e4fa2-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

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


<span data-ttu-id="e4fa2-145">Depois de ter o caminho do diretório Olá, pode utilizar tooread de operações de e/s de ficheiro regular e escrever toofiles.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="e4fa2-146">Um ponto de advertência com extensões de aplicações web regards processamento Olá das ligações internos.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="e4fa2-147">Se tiver quaisquer ligações nos seus ficheiros HTML que atribua caminhos absolutos toointernal ligações na sua aplicação web, tem de garantir que essas ligações são prepended com o nome da extensão como a raiz.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="e4fa2-148">Isto é necessário porque Olá de raiz para a extensão é agora "/`[your-extension-name]`/" em vez de ser apenas "/", internas, por isso, quaisquer ligações devem ser atualizadas em conformidade.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="e4fa2-149">Por exemplo, suponha que o seu código inclui um seguinte de toohello de ligação:</span><span class="sxs-lookup"><span data-stu-id="e4fa2-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="e4fa2-150">Quando a ligação de Olá faz parte de uma extensão de aplicação web, tem de estar Olá ligação no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="e4fa2-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="e4fa2-151">Pode contornar este requisito utilizando apenas caminhos relativos a sua aplicação web, ou num Olá caso de aplicações do ASP.NET, utilizando Olá `@Html.ActionLink` método que cria ligações adequadas Olá por si.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="e4fa2-152"><a id="XDT"></a>ficheiro de applicationHost.xdt Olá</span><span class="sxs-lookup"><span data-stu-id="e4fa2-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="e4fa2-153">código de Olá para a extensão de aplicação web passa em %HOME%\SiteExtensions\[nome da extensão].</span><span class="sxs-lookup"><span data-stu-id="e4fa2-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="e4fa2-154">Receberá um telefonema nosso este Olá extensão de raiz.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="e4fa2-155">tooregister a extensão de aplicação web com o ficheiro applicationHost. config de Olá, terá de tooplace um ficheiro chamado ApplicationHost.xdt na raiz da extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="e4fa2-156">o conteúdo do ficheiro de ApplicationHost.xdt Olá Olá pode da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e4fa2-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

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

<span data-ttu-id="e4fa2-157">Selecione como o nome de extensão de nome de Olá deve ter Olá mesmo nome como a pasta de raiz de extensão.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="e4fa2-158">Isto não tem efeito Olá de adicionar um novo caminho toohello da aplicação `system.applicationHost` lista de sites no site SCM Olá.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="e4fa2-159">site SCM Olá é um ponto de final de administração de sites com as credenciais de acesso específicas.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="e4fa2-160">Tem Olá URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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

### <span data-ttu-id="e4fa2-161"><a id="deploy"></a>Implementação de extensão de aplicação Web</span><span class="sxs-lookup"><span data-stu-id="e4fa2-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="e4fa2-162">tooinstall a extensão de aplicação web, pode utilizar o FTP toocopy todos os ficheiros de Olá do seu toohello de aplicação web `\SiteExtensions\[your-extension-name]` pasta da aplicação web de Olá no qual pretende que a extensão de Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="e4fa2-163">Ser se toocopy Olá ApplicationHost.xdt toothis localização do ficheiro, bem como.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="e4fa2-164">Reinicie a aplicação tooenable Olá da extensão web.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="e4fa2-165">Deve ser capaz de toosee a extensão de aplicação web em:</span><span class="sxs-lookup"><span data-stu-id="e4fa2-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="e4fa2-166">Tenha em atenção que Olá que URL aspeto apenas Olá URL para a sua aplicação web, exceto que utiliza HTTPS e contém "SCM".</span><span class="sxs-lookup"><span data-stu-id="e4fa2-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="e4fa2-167">É possível toodisable todos os privada (não previamente instalado) extensões para a sua aplicação web durante a programação e as investigações, adicionando as definições de uma aplicação com a chave de Olá `WEBSITE_PRIVATE_EXTENSIONS` e um valor de `0`.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="e4fa2-168">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e4fa2-169">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="e4fa2-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e4fa2-170">O que mudou</span><span class="sxs-lookup"><span data-stu-id="e4fa2-170">What's changed</span></span>
* <span data-ttu-id="e4fa2-171">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e4fa2-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

