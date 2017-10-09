---
title: "utilizar o início de sessão tooa API web de MVC do .NET aaaAdd Olá ponto final de v 2.0 do Azure AD | Microsoft Docs"
description: Como toobuild uma Api de Web de MVC do .NET que aceita tokens a partir de ambos os Account Microsoft pessoal e contas profissionais ou escolares.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Proteger uma API web MVC
Com o ponto final v 2.0 do Azure Active Directory Olá, pode proteger uma Web API utilizando [OAuth 2.0](active-directory-v2-protocols.md) tokens de acesso, os utilizadores com ambos os conta pessoal da Microsoft e contas profissionais ou escolares toosecurely aceder à sua API Web.

> [!NOTE]
> Nem todos os cenários do Azure Active Directory e funcionalidades são suportadas pelo ponto final de v 2.0 Olá.  toodetermine se deve utilizar o ponto final de v 2.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).
>
>

Nas ASP.NET web APIs, isto é possível utilizar o middleware OWIN da Microsoft incluído no .NET Framework 4.5.  Aqui iremos utilizar OWIN toobuild uma API de Web MVC "tooDo lista" que permite aos clientes toocreate e ler tarefas da lista de tarefas de um utilizador.  API web do Olá irá validar que os pedidos recebidos contém um token de acesso válido e rejeitar quaisquer pedidos que não são transmitidas validação numa rota protegida.  Este exemplo foi criado com o Visual Studio 2015.

## <a name="download"></a>Transferência
código Olá deste tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow ao longo, pode [transferir a estrutura da aplicação Olá como um. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou estrutura de Olá do clone:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

aplicação de estrutura de Olá inclui todo o código automático Olá para uma API simple, mas está em falta todas as partes de relacionadas com identidade Olá. Se não quiser toofollow ao longo, em vez disso, pode clonar ou [transferir exemplo Olá concluída](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Registar uma aplicação
Criar uma nova aplicação em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga estas [detalhadas passos](active-directory-v2-app-registration.md).  Certifique-se de que:

* Copie Olá **Id da aplicação** atribuído tooyour aplicação, irá precisar das mesmas em breve.

Esta solução do visual studio também contém um "TodoListClient", que é uma simple aplicação WPF.  Olá TodoListClient é toodemonstrate utilizado como um utilizador inicia sessão e como um cliente pode emitir pedidos tooyour Web API.  Neste caso, Olá TodoListClient e Olá TodoListService são representados por Olá mesma aplicação.  tooconfigure Olá TodoListClient, deve também:

* Adicionar Olá **Mobile** plataforma para a sua aplicação.

## <a name="install-owin"></a>Instalar OWIN
Agora que já registou uma aplicação, terá de tooset cópias de segurança sua toocommunicate de aplicação com o ponto final de v 2.0 Olá na ordem toovalidate os pedidos recebidos & tokens.

* toobegin, abra a solução Olá e adicione Olá OWIN middleware NuGet pacotes toohello TodoListService projeto Olá consola do Gestor de pacotes a utilizar.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Configurar a autenticação do OAuth
* Adicionar um projeto de toohello classe do arranque de OWIN TodoListService chamado `Startup.cs`.  Clique direito no projeto Olá--> **adicionar** --> **Novo Item** --> procure "OWIN".  Olá OWIN middleware serão invocados Olá `Configuration(…)` método quando a aplicação for iniciada.
* Alterar a declaração de classe de Olá demasiado`public partial class Startup` -iremos já tiver implementado parte desta classe para si no outro ficheiro.  No Olá `Configuration(…)` método, certifique-tooset de tooConfgureAuth(...) uma chamada de configurar a autenticação para a sua aplicação web.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Ficheiro aberto Olá `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(…)` método, o que irá configurar tokens de tooaccept Olá Web API a partir do ponto final de v 2.0 Olá.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Agora, pode utilizar `[Authorize]` tooprotect de atributos, os controladores e ações com autenticação de portador do OAuth 2.0.  OptionalFieldAttribute Olá `Controllers\TodoListController.cs` classe com uma etiqueta de autorizar.  Isto irá forçar Olá utilizador toosign no antes de aceder a essa página.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Quando um autor da chamada autorizado com êxito invoca um Olá `TodoListController` APIs, ação Olá pode precisar de aceder a tooinformation sobre chamador Olá.  OWIN fornece acesso toohello afirmações dentro de token de portador Olá através de Olá `ClaimsPrincpal` objeto.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Por fim, abra Olá `web.config` ficheiro na raiz de Olá do projeto de TodoListService Olá e introduza os valores de configuração no Olá `<appSettings>` secção.
  * O `ida:Audience` é Olá **Id da aplicação** da aplicação Olá que introduziu no portal de Olá.

## <a name="configure-hello-client-app"></a>Configure a aplicação de cliente Olá
Antes de poder ver Olá serviço de lista de tarefas em ação, terá tooconfigure Olá cliente de lista de tarefas para que possa obter os tokens a partir do ponto final de v 2.0 Olá e efetuar chamadas toohello serviço.

* No projeto de TodoListClient Olá, abra `App.config` e introduza os valores de configuração no Olá `<appSettings>` secção.
  * O `ida:ClientId` Id da aplicação que copiou a partir do portal de Olá.

Por fim, apagar, criar e executar cada projeto!  Tem agora uma API de Web de MVC do .NET que aceita tokens a partir de ambas as contas pessoais da Microsoft e contas profissionais ou escolares.  Inicie sessão no Olá TodoListClient e chamar a lista de tarefas web api tooadd tarefas toohello dos seus utilizadores.

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou pode cloná-la a partir do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Passos seguintes
Agora pode mover para tópicos adicionais.  Poderá ser útil tootry:

[Chamar uma API Web a partir de uma aplicação Web >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Para obter recursos adicionais, consulte:

* [Guia para programadores do Olá v 2.0 >>](active-directory-appmodel-v2-overview.md)
* [Etiqueta de StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança dos nossos produtos
Aconselhamo-lo tooget notificações de quando os incidentes de segurança ocorrem, visitando [nesta página](https://technet.microsoft.com/security/dd252948) e subscrever tooSecurity SUBSCREVENDO os alertas.
