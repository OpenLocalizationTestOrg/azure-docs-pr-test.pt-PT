---
title: "aaaHow tooSet computador cópias de segurança para o desenvolvimento de serviços de suporte de dados com o .NET"
description: "Saiba mais sobre Olá pré-requisitos para os Media Services utilizando Olá SDK de Media Services para .NET. Também saber como toocreate uma aplicação do Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="e60fb-104">Desenvolvimento de Media Services com .NET</span><span class="sxs-lookup"><span data-stu-id="e60fb-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="e60fb-105">Este tópico descreve como serviços de multimédia de desenvolvimento de toostart aplicações através do .NET.</span><span class="sxs-lookup"><span data-stu-id="e60fb-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="e60fb-106">Olá **SDK .NET do Azure Media Services** biblioteca permite-lhe tooprogram nos serviços de suporte de dados através do .NET.</span><span class="sxs-lookup"><span data-stu-id="e60fb-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="e60fb-107">toomake-mesmo toodevelop mais fácil com o .NET, hello **extensões do SDK .NET do Azure suporte de dados de serviços** biblioteca é fornecida.</span><span class="sxs-lookup"><span data-stu-id="e60fb-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="e60fb-108">Esta biblioteca contém um conjunto de métodos de extensão e funções de programa auxiliar que simplificam o código de .NET.</span><span class="sxs-lookup"><span data-stu-id="e60fb-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="e60fb-109">Ambas as bibliotecas estão disponíveis através de **NuGet** e **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="e60fb-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e60fb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e60fb-110">Prerequisites</span></span>
* <span data-ttu-id="e60fb-111">Uma conta dos Media Services numa subscrição Azure nova ou existente.</span><span class="sxs-lookup"><span data-stu-id="e60fb-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="e60fb-112">Consulte o tópico Olá [como tooCreate uma conta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e60fb-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e60fb-113">Sistemas operativos: Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.</span><span class="sxs-lookup"><span data-stu-id="e60fb-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="e60fb-114">.NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e60fb-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="e60fb-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e60fb-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e60fb-116">Criar e configurar um projeto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e60fb-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="e60fb-117">Esta secção mostra-lhe como toocreate um projeto no Visual Studio e defina-o para o desenvolvimento de Media Services.</span><span class="sxs-lookup"><span data-stu-id="e60fb-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="e60fb-118">Neste caso, projeto Olá é uma aplicação de consola c# Windows, mas hello mesmos passos de configuração mostrados aqui aplicam tooother tipos de projetos, que pode criar para aplicações de serviços de suporte de dados (por exemplo, uma aplicação do Windows Forms ou uma aplicação Web de ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="e60fb-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="e60fb-119">Esta secção mostra como toouse **NuGet** tooadd SDK .NET dos Media Services extensões e outras bibliotecas dependentes.</span><span class="sxs-lookup"><span data-stu-id="e60fb-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="e60fb-120">Em alternativa, pode obter bits SDK .NET dos Media Services mais recentes do Olá a partir do GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), construir solução Olá e adicionar as referências de Olá toohello projeto de cliente.</span><span class="sxs-lookup"><span data-stu-id="e60fb-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="e60fb-121">Todas as dependências necessárias de Olá obterem transferiu e extraiu automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e60fb-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="e60fb-122">Crie uma nova Aplicação de Consola C# no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e60fb-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="e60fb-123">Introduza Olá **nome**, **localização**, e **nome da solução**e, em seguida, clique em OK.</span><span class="sxs-lookup"><span data-stu-id="e60fb-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="e60fb-124">Compilar a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="e60fb-124">Build hello solution.</span></span>
3. <span data-ttu-id="e60fb-125">Utilize **NuGet** tooinstall e adicione **extensões do SDK .NET do Azure suporte de dados de serviços** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="e60fb-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="e60fb-126">Ao instalar este pacote, também é instalado o **SDK do .NET dos Media Services** e são adicionadas todas as outras dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="e60fb-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="e60fb-127">Certifique-se de que tem a versão mais recente do Olá do NuGet instalado.</span><span class="sxs-lookup"><span data-stu-id="e60fb-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="e60fb-128">Para obter mais instruções de instalação e informações, consulte [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="e60fb-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="e60fb-129">No Explorador de soluções, clique no nome de Olá do projeto de Olá e escolha pacotes NuGet gerir.</span><span class="sxs-lookup"><span data-stu-id="e60fb-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="e60fb-130">é apresentada a caixa de diálogo Olá gerir pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="e60fb-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="e60fb-131">Na Galeria de Olá Online, procure as extensões de MediaServices do Azure, escolha extensões do SDK .NET do Azure suporte de dados de serviços e, em seguida, clique no botão de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="e60fb-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="e60fb-132">projeto de Olá é modificado e referencia toohello extensões do SDK do .NET dos serviços de suporte de dados, SDK .NET dos Media Services, e são adicionadas outras assemblagens dependentes.</span><span class="sxs-lookup"><span data-stu-id="e60fb-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="e60fb-133">toopromote limpeza ambiente de desenvolvimento, considere ativar restauro do pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="e60fb-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="e60fb-134">Para obter mais informações, consulte [restauro do pacote NuGet "](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="e60fb-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="e60fb-135">Adicione uma referência demasiado**System** assemblagem.</span><span class="sxs-lookup"><span data-stu-id="e60fb-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="e60fb-136">Esta assemblagem contém Olá System. **ConfigurationManager** classe, ou seja, ficheiros de configuração tooaccess utilizados (por exemplo, App. config).</span><span class="sxs-lookup"><span data-stu-id="e60fb-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="e60fb-137">referências de tooadd utilizando Olá a caixa de diálogo de referências de gerir, clique no nome do projeto Olá no Olá Explorador de soluções.</span><span class="sxs-lookup"><span data-stu-id="e60fb-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="e60fb-138">Em seguida, selecione Adicionar e referências.</span><span class="sxs-lookup"><span data-stu-id="e60fb-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="e60fb-139">é apresentada a caixa de diálogo do Olá referências de gerir.</span><span class="sxs-lookup"><span data-stu-id="e60fb-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="e60fb-140">Em assemblagens do .NET framework, localize e selecione a assemblagem de System Olá e prima OK.</span><span class="sxs-lookup"><span data-stu-id="e60fb-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="e60fb-141">Abra o ficheiro de App. config Olá e adicione um *appSettings* ficheiro toohello de secção.</span><span class="sxs-lookup"><span data-stu-id="e60fb-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="e60fb-142">Definir valores de Olá que são necessários tooconnect toohello API dos serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="e60fb-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="e60fb-143">Para obter mais informações, consulte [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e60fb-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="e60fb-144">Se estiver a utilizar [autenticação de utilizador](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) o ficheiro de configuração irá provavelmente têm valores para o seu domínio de inquilino do Azure AD e Olá ponto final de API de REST de AMS.</span><span class="sxs-lookup"><span data-stu-id="e60fb-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="e60fb-145">A maioria dos exemplos de código no Olá documentação de Media Services do Azure definir, utilize um tipo (interativo) de utilizador da autenticação tooconnect toohello API de AMS.</span><span class="sxs-lookup"><span data-stu-id="e60fb-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="e60fb-146">Este método de autenticação irá funcionar bem para gestão ou de monitorização de aplicações nativas: as aplicações móveis, as aplicações do Windows e aplicações de consola.</span><span class="sxs-lookup"><span data-stu-id="e60fb-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="e60fb-147">Este método de autenticação não é adequado para o servidor, serviços web, tipo APIs de aplicações.</span><span class="sxs-lookup"><span data-stu-id="e60fb-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="e60fb-148">Para obter mais informações, consulte [Olá de acesso AMS API com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e60fb-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="e60fb-149">Substituir a existente Olá **utilizando** instruções início Olá Olá Program.cs do ficheiro de com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="e60fb-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="e60fb-150">Neste momento, está pronto toostart desenvolver uma aplicação dos Media Services.</span><span class="sxs-lookup"><span data-stu-id="e60fb-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="e60fb-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e60fb-151">Example</span></span>

<span data-ttu-id="e60fb-152">Eis um exemplo de pequeno que se liga toohello AMS API e apresenta uma lista de todos os processadores de suporte de dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e60fb-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="e60fb-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e60fb-153">Next steps</span></span>

<span data-ttu-id="e60fb-154">Agora [pode ligar toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) e iniciar [desenvolver](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e60fb-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="e60fb-155">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="e60fb-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e60fb-156">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="e60fb-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

