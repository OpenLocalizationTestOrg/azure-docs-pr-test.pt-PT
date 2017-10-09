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
# <a name="use-azure-key-vault-from-a-web-application"></a>Utilizar o Cofre de chaves do Azure de uma aplicação Web
## <a name="introduction"></a>Introdução
Utilize este tutorial toohelp que aprender como toouse chave do Azure do Cofre de uma aplicação web no Azure. -O orienta através do processo de Olá de aceder a um segredo a partir de um cofre de chaves do Azure para que possa ser utilizado na sua aplicação web.

**Estimado tempo toocomplete:** 15 minutos

Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte o artigo [O que é o Cofre de Chaves do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, tem de ter Olá seguintes:

* Um segredo de tooa URI num cofre de chaves do Azure
* Um ID de cliente e um segredo de cliente para uma aplicação web registado no Azure Active Directory que tem acesso tooyour Cofre de chaves
* Uma aplicação web. Iremos irá ser mostrar Olá os passos para uma aplicação ASP.NET MVC implementado no Azure como uma aplicação Web.

> [!NOTE]
> É essencial que concluiu os passos de Olá apresentados na [introdução ao Cofre de chaves do Azure](key-vault-get-started.md) para este tutorial para que tenha hello segredo do URI tooa e Olá ID de cliente e segredo do cliente para uma aplicação web.
> 
> 

aplicação web Olá que irão aceder aos Olá Cofre de chaves é Olá um que está registado no Azure Active Directory e foi indicado acesso tooyour Cofre de chaves. Se não for este caso de Olá, volte atrás tooRegister uma aplicação no tutorial de introdução Olá e repita os passos de Olá apresentados.

Este tutorial foi concebido para programadores de web que compreender as noções básicas de Olá de criação de aplicações web no Azure. Para obter mais informações sobre as aplicações Web do Azure, consulte [descrição geral das aplicações Web](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Adicionar pacotes Nuget
Existem dois pacotes que a aplicação web precisa de toohave instalado.

* Biblioteca de autenticação do Active Directory - contém métodos para interagir com o Azure Active Directory e gerir a identidade do utilizador
* Biblioteca de Cofre de chaves do Azure - contém métodos para interagir com o Cofre de chaves do Azure

Ambos estes pacotes podem ser instalados utilizando Olá a consola do Gestor de pacotes utilizando o comando de Olá Install-Package.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Modificar Web. config
Existem três definições de aplicações que precisam de ficheiro de Web. config toobe toohello adicionado da seguinte forma.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Se não pretender toohost a aplicação como uma aplicação Web do Azure, deve adicionar Olá real ClientId, o segredo do cliente e o segredo do URI valores toohello Web. config. Caso contrário, deixe estes valores fictícias porque iremos adicionar valores reais Olá no Olá Portal do Azure para um nível adicional de segurança.

## <a id="gettoken"></a>Adicionar método tooGet um Token de acesso
Olá de toouse ordem API Cofre de chaves precisa de um token de acesso. Olá chave de cofre cliente processa chamadas toohello API Cofre de chaves, mas é necessário toosupply-o com uma função que obtém o token de acesso de Olá.  

Segue-se Olá código tooget um token de acesso do Azure Active Directory. Este código pode aceder em qualquer lugar na sua aplicação. Posso como tooadd um Utils ou EncryptionHelper classe.  

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
> A utilização de um ID de cliente e o segredo do cliente é Olá tooauthenticate da forma mais fácil uma aplicação do Azure AD. E utilizá-lo na sua aplicação web permite uma separação de deveres e mais controlo sobre a gestão de chaves. Mas dependem de colocar Olá segredo do cliente nas suas definições de configuração que, para algumas, podem ser como arriscadas como colocar segredo Olá que pretende que tooprotect nas suas definições de configuração. Consulte abaixo para ver um debate sobre como toouse um ID de cliente e certificado em vez de ID de cliente e o segredo de cliente tooauthenticate Olá aplicação do Azure AD.
> 
> 

## <a id="appstart"></a>Obter o segredo de Olá no início da aplicação
Agora vamos precisar de código toocall Olá API Cofre de chaves e obter segredo Olá. Olá seguinte código pode ser colocado em qualquer lugar, desde que é denominado antes que seja necessário toouse-lo. Ter coloque este código Olá pré-carregamento da aplicação durante o evento na Olá global. asax para que é executada uma vez no início e torna Olá segredo disponível para a aplicação Olá.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Adicionar as definições de aplicação Olá Portal do Azure (opcional)
Se tiver uma aplicação Web do Azure agora pode adicionar os valores reais Olá para Olá AppSettings no Olá Portal do Azure. Ao fazê-lo, os valores reais Olá não estarão disponíveis na Web. config de Olá mas protegido através de Olá Portal em que tenha as capacidades de controlo de acesso separado. Estes valores serão substituídos pelos valores de Olá que introduziu no seu Web. config. Certifique-se de que os nomes de Olá são Olá mesmo.

![Definições da aplicação apresentadas no Portal do Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Autenticar com um certificado em vez de um segredo do cliente
Outra forma tooauthenticate uma aplicação do Azure AD é através de um ID de cliente e um certificado em vez de um ID de cliente e o segredo do cliente. Seguintes são Olá passos toouse um certificado numa aplicação Web do Azure:

1. Obter ou criar um certificado
2. Associar Olá certificado uma aplicação do Azure AD
3. Adicionar Olá de toouse de aplicação Web do código tooyour certificado
4. Adicionar uma aplicação Web de tooyour do certificado

**Obter ou criar um certificado** para fins de nosso iremos um certificado de teste. Eis alguns comandos que pode utilizar uma linha de comandos do programador toocreate um certificado. Alterar toowhere de diretório que pretende que os ficheiros de certificado de Olá criados.  Além disso, para Olá início e fim de data do certificado de Olá, utilize Olá data atual mais 1 ano.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Tome nota da data de fim de Olá e Olá palavra-passe para Olá PFX (neste exemplo: 31/07/2016 e test123). Vai precisar deles abaixo.

Para obter mais informações sobre como criar um certificado de teste, consulte [como: criar seu próprio teste certificado](https://msdn.microsoft.com/library/ff699202.aspx)

**Associar Olá certificado com uma aplicação do Azure AD** agora que tem um certificado, tem de tooassociate-o com uma aplicação do Azure AD. Atualmente, Olá Portal do Azure não suporta este fluxo de trabalho; Isto pode ser efetuado através do PowerShell. Execute Olá seguir o certificado de Olá tooassoicate comandos com a aplicação Olá do Azure AD:

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

Depois de executar estes comandos, pode ver a aplicação Olá no Azure AD. Quando pesquisar, certifique-se que selecionar "Aplicações minha empresa detém" em vez de "Aplicações minha empresa utiliza" na caixa de diálogo de pesquisa de Olá.

toolearn mais informações sobre objetos de aplicação do Azure AD e objetos de ServicePrincipal, consulte [objectos da aplicação e objetos de principais de serviço](../active-directory/active-directory-application-objects.md)

**Adicionar Olá de toouse de aplicação Web do código tooyour certificado** agora iremos adicionar código tooyour aplicação Web tooaccess Olá cert e utilizá-lo para autenticação.

Pela primeira vez há cert de Olá tooaccess de código.

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


Tenha em atenção que Olá StoreLocation CurrentUser em vez de LocalMachine. E estão a fornecer toohello 'false' Localizar o método porque está a utilizar um certificado de teste.

Em seguida, é código utiliza Olá CertificateHelper, que cria um ClientAssertionCertificate, necessária para a autenticação.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Eis Olá novo código tooget Olá token de acesso. Esta ação substitui o método de GetToken Olá acima. Posso atribuiu-um nome diferente para sua comodidade.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

Ter colocar todos os este código na classe de Utils meu projeto de aplicação Web para facilidade de utilização.

última alteração de código Olá está a ser Olá Application_Start método. Primeiro é preciso toocall Olá GetCert()-Olá método tooload ClientAssertionCertificate. E, em seguida, vamos alterar método de chamada de retorno de Olá que podemos fornecer ao criar um novo KeyVaultClient. Tenha em atenção que isto substitui o código de Olá tivemos acima.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Adicionar um certificado tooyour aplicação Web através do Portal do Azure de Olá** a adição de uma aplicação Web de tooyour do certificado é um processo de dois passos simples. Em primeiro lugar, aceda a toohello Portal do Azure e navegue tooyour aplicação Web. No painel de definições de Olá para a sua aplicação Web, clique na entrada de Olá para "domínios personalizados e SSL". Olá painel que abre-se de irá ser Olá tooupload capaz de certificado que criou acima, KVWebApp.pfx, certifique-se de que não se esqueça Olá palavra-passe para Olá pfx.

![A adição de uma aplicação Web de tooa certificado Olá Portal do Azure][2]

Olá última coisa que precisa de toodo é tooadd tooyour uma definição de aplicação Web App, que tem o Web site do nome de Olá\_carga\_certificados e um valor de *. Isto irá garantir que todos os certificados estão carregados. Se pretendesse Olá apenas tooload certificados que carregou, em seguida, pode introduzir uma lista separada por vírgulas de thumbprints do respetivos.

toolearn mais informações sobre a adição de um certificado tooa aplicação Web, consulte [utilizando certificados em aplicações de Web sites do Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Adicionar um certificado tooKey cofre como um segredo** em vez de carregar diretamente a toohello de certificado do serviço de aplicações Web, pode armazenar no Cofre de chaves como um segredo e implementá-la a partir daí. Este é um processo de dois passos que está descrito em Olá a seguinte mensagem de blogue, [implementar Azure certificado da aplicação Web através do Cofre de chaves](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Passos seguintes
Para as referências de programação, consulte [Azure chave de cofre c# cliente referência da API](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
