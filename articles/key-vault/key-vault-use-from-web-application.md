---
title: "aaaUse Cofre de chaves do Azure de uma aplicação Web | Microsoft Docs"
description: "Utilize este tutorial toohelp que aprender como toouse chave do Azure do Cofre de uma aplicação web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="801d8-103">Utilizar o Cofre de chaves do Azure de uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="801d8-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="801d8-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="801d8-104">Introduction</span></span>
<span data-ttu-id="801d8-105">Utilize este tutorial toohelp que aprender como toouse chave do Azure do Cofre de uma aplicação web no Azure.</span><span class="sxs-lookup"><span data-stu-id="801d8-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="801d8-106">-O orienta através do processo de Olá de aceder a um segredo a partir de um cofre de chaves do Azure para que possa ser utilizado na sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="801d8-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="801d8-107">**Estimado tempo toocomplete:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="801d8-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="801d8-108">Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte o artigo [O que é o Cofre de Chaves do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="801d8-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="801d8-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="801d8-109">Prerequisites</span></span>
<span data-ttu-id="801d8-110">toocomplete neste tutorial, tem de ter Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="801d8-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="801d8-111">Um segredo de tooa URI num cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="801d8-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="801d8-112">Um ID de cliente e um segredo de cliente para uma aplicação web registado no Azure Active Directory que tem acesso tooyour Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="801d8-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="801d8-113">Uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="801d8-113">A web application.</span></span> <span data-ttu-id="801d8-114">Iremos irá ser mostrar Olá os passos para uma aplicação ASP.NET MVC implementado no Azure como uma aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="801d8-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="801d8-115">É essencial que concluiu os passos de Olá apresentados na [introdução ao Cofre de chaves do Azure](key-vault-get-started.md) para este tutorial para que tenha hello segredo do URI tooa e Olá ID de cliente e segredo do cliente para uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="801d8-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="801d8-116">aplicação web Olá que irão aceder aos Olá Cofre de chaves é Olá um que está registado no Azure Active Directory e foi indicado acesso tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="801d8-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="801d8-117">Se não for este caso de Olá, volte atrás tooRegister uma aplicação no tutorial de introdução Olá e repita os passos de Olá apresentados.</span><span class="sxs-lookup"><span data-stu-id="801d8-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="801d8-118">Este tutorial foi concebido para programadores de web que compreender as noções básicas de Olá de criação de aplicações web no Azure.</span><span class="sxs-lookup"><span data-stu-id="801d8-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="801d8-119">Para obter mais informações sobre as aplicações Web do Azure, consulte [descrição geral das aplicações Web](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="801d8-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="801d8-120"><a id="packages"></a>Adicionar pacotes Nuget</span><span class="sxs-lookup"><span data-stu-id="801d8-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="801d8-121">Existem dois pacotes que a aplicação web precisa de toohave instalado.</span><span class="sxs-lookup"><span data-stu-id="801d8-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="801d8-122">Biblioteca de autenticação do Active Directory - contém métodos para interagir com o Azure Active Directory e gerir a identidade do utilizador</span><span class="sxs-lookup"><span data-stu-id="801d8-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="801d8-123">Biblioteca de Cofre de chaves do Azure - contém métodos para interagir com o Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="801d8-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="801d8-124">Ambos estes pacotes podem ser instalados utilizando Olá a consola do Gestor de pacotes utilizando o comando de Olá Install-Package.</span><span class="sxs-lookup"><span data-stu-id="801d8-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="801d8-125"><a id="webconfig"></a>Modificar Web. config</span><span class="sxs-lookup"><span data-stu-id="801d8-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="801d8-126">Existem três definições de aplicações que precisam de ficheiro de Web. config toobe toohello adicionado da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="801d8-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="801d8-127">Se não pretender toohost a aplicação como uma aplicação Web do Azure, deve adicionar Olá real ClientId, o segredo do cliente e o segredo do URI valores toohello Web. config. Caso contrário, deixe estes valores fictícias porque iremos adicionar valores reais Olá no Olá Portal do Azure para um nível adicional de segurança.</span><span class="sxs-lookup"><span data-stu-id="801d8-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="801d8-128"><a id="gettoken"></a>Adicionar método tooGet um Token de acesso</span><span class="sxs-lookup"><span data-stu-id="801d8-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="801d8-129">Olá de toouse ordem API Cofre de chaves precisa de um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="801d8-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="801d8-130">Olá chave de cofre cliente processa chamadas toohello API Cofre de chaves, mas é necessário toosupply-o com uma função que obtém o token de acesso de Olá.</span><span class="sxs-lookup"><span data-stu-id="801d8-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="801d8-131">Segue-se Olá código tooget um token de acesso do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="801d8-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="801d8-132">Este código pode aceder em qualquer lugar na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="801d8-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="801d8-133">Posso como tooadd um Utils ou EncryptionHelper classe.</span><span class="sxs-lookup"><span data-stu-id="801d8-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="801d8-134">A utilização de um ID de cliente e o segredo do cliente é Olá tooauthenticate da forma mais fácil uma aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="801d8-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="801d8-135">E utilizá-lo na sua aplicação web permite uma separação de deveres e mais controlo sobre a gestão de chaves.</span><span class="sxs-lookup"><span data-stu-id="801d8-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="801d8-136">Mas dependem de colocar Olá segredo do cliente nas suas definições de configuração que, para algumas, podem ser como arriscadas como colocar segredo Olá que pretende que tooprotect nas suas definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="801d8-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="801d8-137">Consulte abaixo para ver um debate sobre como toouse um ID de cliente e certificado em vez de ID de cliente e o segredo de cliente tooauthenticate Olá aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="801d8-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="801d8-138"><a id="appstart"></a>Obter o segredo de Olá no início da aplicação</span><span class="sxs-lookup"><span data-stu-id="801d8-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="801d8-139">Agora vamos precisar de código toocall Olá API Cofre de chaves e obter segredo Olá.</span><span class="sxs-lookup"><span data-stu-id="801d8-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="801d8-140">Olá seguinte código pode ser colocado em qualquer lugar, desde que é denominado antes que seja necessário toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="801d8-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="801d8-141">Ter coloque este código Olá pré-carregamento da aplicação durante o evento na Olá global. asax para que é executada uma vez no início e torna Olá segredo disponível para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="801d8-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="801d8-142"><a id="portalsettings"></a>Adicionar as definições de aplicação Olá Portal do Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="801d8-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="801d8-143">Se tiver uma aplicação Web do Azure agora pode adicionar os valores reais Olá para Olá AppSettings no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="801d8-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="801d8-144">Ao fazê-lo, os valores reais Olá não estarão disponíveis na Web. config de Olá mas protegido através de Olá Portal em que tenha as capacidades de controlo de acesso separado.</span><span class="sxs-lookup"><span data-stu-id="801d8-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="801d8-145">Estes valores serão substituídos pelos valores de Olá que introduziu no seu Web. config. Certifique-se de que os nomes de Olá são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="801d8-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Definições da aplicação apresentadas no Portal do Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="801d8-147">Autenticar com um certificado em vez de um segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="801d8-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="801d8-148">Outra forma tooauthenticate uma aplicação do Azure AD é através de um ID de cliente e um certificado em vez de um ID de cliente e o segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="801d8-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="801d8-149">Seguintes são Olá passos toouse um certificado numa aplicação Web do Azure:</span><span class="sxs-lookup"><span data-stu-id="801d8-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="801d8-150">Obter ou criar um certificado</span><span class="sxs-lookup"><span data-stu-id="801d8-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="801d8-151">Associar Olá certificado uma aplicação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="801d8-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="801d8-152">Adicionar Olá de toouse de aplicação Web do código tooyour certificado</span><span class="sxs-lookup"><span data-stu-id="801d8-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="801d8-153">Adicionar uma aplicação Web de tooyour do certificado</span><span class="sxs-lookup"><span data-stu-id="801d8-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="801d8-154">**Obter ou criar um certificado** para fins de nosso iremos um certificado de teste.</span><span class="sxs-lookup"><span data-stu-id="801d8-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="801d8-155">Eis alguns comandos que pode utilizar uma linha de comandos do programador toocreate um certificado.</span><span class="sxs-lookup"><span data-stu-id="801d8-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="801d8-156">Alterar toowhere de diretório que pretende que os ficheiros de certificado de Olá criados.</span><span class="sxs-lookup"><span data-stu-id="801d8-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="801d8-157">Além disso, para Olá início e fim de data do certificado de Olá, utilize Olá data atual mais 1 ano.</span><span class="sxs-lookup"><span data-stu-id="801d8-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="801d8-158">Tome nota da data de fim de Olá e Olá palavra-passe para Olá PFX (neste exemplo: 31/07/2016 e test123).</span><span class="sxs-lookup"><span data-stu-id="801d8-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="801d8-159">Vai precisar deles abaixo.</span><span class="sxs-lookup"><span data-stu-id="801d8-159">You will need them below.</span></span>

<span data-ttu-id="801d8-160">Para obter mais informações sobre como criar um certificado de teste, consulte [como: criar seu próprio teste certificado](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="801d8-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="801d8-161">**Associar Olá certificado com uma aplicação do Azure AD** agora que tem um certificado, tem de tooassociate-o com uma aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="801d8-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="801d8-162">Atualmente, Olá Portal do Azure não suporta este fluxo de trabalho; Isto pode ser efetuado através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="801d8-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="801d8-163">Execute Olá seguir o certificado de Olá tooassoicate comandos com a aplicação Olá do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="801d8-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="801d8-164">Depois de executar estes comandos, pode ver a aplicação Olá no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="801d8-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="801d8-165">Quando pesquisar, certifique-se que selecionar "Aplicações minha empresa detém" em vez de "Aplicações minha empresa utiliza" na caixa de diálogo de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="801d8-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="801d8-166">toolearn mais informações sobre objetos de aplicação do Azure AD e objetos de ServicePrincipal, consulte [objectos da aplicação e objetos de principais de serviço](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="801d8-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="801d8-167">**Adicionar Olá de toouse de aplicação Web do código tooyour certificado** agora iremos adicionar código tooyour aplicação Web tooaccess Olá cert e utilizá-lo para autenticação.</span><span class="sxs-lookup"><span data-stu-id="801d8-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="801d8-168">Pela primeira vez há cert de Olá tooaccess de código.</span><span class="sxs-lookup"><span data-stu-id="801d8-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="801d8-169">Tenha em atenção que Olá StoreLocation CurrentUser em vez de LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="801d8-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="801d8-170">E estão a fornecer toohello 'false' Localizar o método porque está a utilizar um certificado de teste.</span><span class="sxs-lookup"><span data-stu-id="801d8-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="801d8-171">Em seguida, é código utiliza Olá CertificateHelper, que cria um ClientAssertionCertificate, necessária para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="801d8-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="801d8-172">Eis Olá novo código tooget Olá token de acesso.</span><span class="sxs-lookup"><span data-stu-id="801d8-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="801d8-173">Esta ação substitui o método de GetToken Olá acima.</span><span class="sxs-lookup"><span data-stu-id="801d8-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="801d8-174">Posso atribuiu-um nome diferente para sua comodidade.</span><span class="sxs-lookup"><span data-stu-id="801d8-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="801d8-175">Ter colocar todos os este código na classe de Utils meu projeto de aplicação Web para facilidade de utilização.</span><span class="sxs-lookup"><span data-stu-id="801d8-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="801d8-176">última alteração de código Olá está a ser Olá Application_Start método.</span><span class="sxs-lookup"><span data-stu-id="801d8-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="801d8-177">Primeiro é preciso toocall Olá GetCert()-Olá método tooload ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="801d8-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="801d8-178">E, em seguida, vamos alterar método de chamada de retorno de Olá que podemos fornecer ao criar um novo KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="801d8-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="801d8-179">Tenha em atenção que isto substitui o código de Olá tivemos acima.</span><span class="sxs-lookup"><span data-stu-id="801d8-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="801d8-180">**Adicionar um certificado tooyour aplicação Web através do Portal do Azure de Olá** a adição de uma aplicação Web de tooyour do certificado é um processo de dois passos simples.</span><span class="sxs-lookup"><span data-stu-id="801d8-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="801d8-181">Em primeiro lugar, aceda a toohello Portal do Azure e navegue tooyour aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="801d8-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="801d8-182">No painel de definições de Olá para a sua aplicação Web, clique na entrada de Olá para "domínios personalizados e SSL".</span><span class="sxs-lookup"><span data-stu-id="801d8-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="801d8-183">Olá painel que abre-se de irá ser Olá tooupload capaz de certificado que criou acima, KVWebApp.pfx, certifique-se de que não se esqueça Olá palavra-passe para Olá pfx.</span><span class="sxs-lookup"><span data-stu-id="801d8-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![A adição de uma aplicação Web de tooa certificado Olá Portal do Azure][2]

<span data-ttu-id="801d8-185">Olá última coisa que precisa de toodo é tooadd tooyour uma definição de aplicação Web App, que tem o Web site do nome de Olá\_carga\_certificados e um valor de *.</span><span class="sxs-lookup"><span data-stu-id="801d8-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="801d8-186">Isto irá garantir que todos os certificados estão carregados.</span><span class="sxs-lookup"><span data-stu-id="801d8-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="801d8-187">Se pretendesse Olá apenas tooload certificados que carregou, em seguida, pode introduzir uma lista separada por vírgulas de thumbprints do respetivos.</span><span class="sxs-lookup"><span data-stu-id="801d8-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="801d8-188">toolearn mais informações sobre a adição de um certificado tooa aplicação Web, consulte [utilizando certificados em aplicações de Web sites do Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="801d8-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="801d8-189">**Adicionar um certificado tooKey cofre como um segredo** em vez de carregar diretamente a toohello de certificado do serviço de aplicações Web, pode armazenar no Cofre de chaves como um segredo e implementá-la a partir daí.</span><span class="sxs-lookup"><span data-stu-id="801d8-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="801d8-190">Este é um processo de dois passos que está descrito em Olá a seguinte mensagem de blogue, [implementar Azure certificado da aplicação Web através do Cofre de chaves](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="801d8-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="801d8-191"><a id="next"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="801d8-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="801d8-192">Para as referências de programação, consulte [Azure chave de cofre c# cliente referência da API](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="801d8-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
