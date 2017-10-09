---
title: aaaAzure AD B2C | Microsoft Docs
description: "Como toobuild uma API Web do .NET utilizando o Azure Active Directory B2C, protegida utilizando os tokens de acesso de OAuth 2.0 para autenticação."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: criar uma API Web do .NET

Com o Azure Active Directory (Azure AD) B2C, pode proteger uma API web utilizando tokens de acesso de OAuth 2.0. Estes tokens permitem que o cliente aplicações tooauthenticate toohello API. Este artigo mostra como toocreate uma API de "lista de tarefas" do MVC do .NET que permite que os utilizadores do seu cliente tarefas tooCRUD de aplicações. Olá web API está protegida com o Azure AD B2C e só permite que os utilizadores autenticados toomanage respetiva lista de tarefas.

## <a name="create-an-azure-ad-b2c-directory"></a>Criar um diretório do Azure AD B2C

Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino. Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc. Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.

> [!NOTE]
> web API e uma aplicação de cliente Olá tem de utilizar diretório do B2C Olá mesmo Azure AD.
>

## <a name="create-a-web-api"></a>Criar uma API Web

Em seguida, terá de toocreate uma aplicação de API web no diretório do B2C. Isto dá-informações do Azure AD que necessidades toosecurely comunicar com a sua aplicação. toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário:

* Incluir um **aplicação web** ou **web API** na aplicação Olá.
* Olá utilize **URI de redirecionamento** `https://localhost:44332/` da aplicação web de Olá. Esta é a localização predefinida de hello do cliente da aplicação web Olá para este exemplo de código.
* Olá cópia **ID da aplicação** que é atribuído tooyour aplicação. Precisará dela mais tarde.
* Introduza um identificador de aplicação em **URI de ID de Aplicação**.
* Adicionar permissões através de Olá **publicados âmbitos** menu.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar as políticas

No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md). Terá de toocreate toocommunicate uma política com o Azure AD B2C. É recomendável utilizar Olá combinado sessão-up/início de sessão de política, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md). Quando criar a política, certifique-se de que:

* Escolhe o **Nome a apresentar** e outros atributos de inscrição na política.
* Escolher as afirmações **Nome a apresentar** e **ID de objeto** como afirmações de aplicação em cada política. Também pode escolher outras afirmações.
* Olá cópia **nome** de cada política depois de a criar. Terá de nome da política hello mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de ter criado com êxito a política de Olá, está pronto toobuild a aplicação.

## <a name="download-hello-code"></a>Transferir o código de Olá

código Olá deste tutorial é mantido no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Pode clonar o exemplo de Olá executando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Depois de transferir o código de exemplo de Olá, abra Olá Visual Studio. sln ficheiro tooget foi iniciado. ficheiro de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`. `TaskWebApp`é uma aplicação de web MVC Olá utilizador interage com. `TaskService`é API de web de back-end da aplicação Olá que armazena a lista de tarefas de cada utilizador. Este artigo apenas abordar Olá `TaskService` aplicação. toolearn como toobuild `TaskWebApp` utilizando o Azure AD B2C, consulte [nosso tutorial da aplicação web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Atualizar a configuração de Olá, Azure AD B2C

Nosso exemplo é configurado toouse Olá políticas e cliente ID do inquilino a nossa demonstração. Se quiser toouse o seu inquilino, terá de Olá toodo seguintes:

1. Abra `web.config` no Olá `TaskService` projeto e substitua os valores de Olá para
    * `ida:Tenant` pelo nome do seu inquilino
    * `ida:ClientId` pelo ID da sua aplicação da API Web
    * `ida:SignUpSignInPolicyId` pelo nome da sua política de “Inscrição ou Início de Sessão”

2. Abra `web.config` no Olá `TaskWebApp` projeto e substitua os valores de Olá para
    * `ida:Tenant` pelo nome do seu inquilino
    * `ida:ClientId` pelo ID da sua aplicação Web
    * `ida:ClientSecret` pela chave de segredo da sua aplicação Web
    * `ida:SignUpSignInPolicyId` pelo nome da sua política de “Inscrição ou Início de Sessão”
    * `ida:EditProfilePolicyId` pelo nome da sua política de “Editar Perfil”
    * `ida:ResetPasswordPolicyId` pelo nome da sua política de “Repor Palavras-Passe”


## <a name="secure-hello-api"></a>Proteger Olá API

Quando tiver um cliente que chama a API, pode utilizar tokens de portador do OAuth 2.0 para proteger a sua API (por exemplo, `TaskService`). Isto assegura que cada API do pedido tooyour só será válida se o pedido de Olá tem um token de portador. A sua API pode aceitar e validar os tokens de portador através da biblioteca OWIN (Open Web Interface para .NET) da Microsoft.

### <a name="install-owin"></a>Instalar OWIN

Comece por instalar o pipeline de autenticação OAuth da OWIN Olá utilizando Olá consola do Gestor de pacotes do Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Esta ação instalará Olá OWIN middleware que irá aceitar e validar os tokens de portador.

### <a name="add-an-owin-startup-class"></a>Adicionar uma classe de startup da OWIN

Adicionar um toohello de classe de arranque da OWIN API chamado `Startup.cs`.  Clique com o botão direito no projeto Olá, selecione **adicionar** e **Novo Item**e, em seguida, pesquise OWIN. Olá OWIN middleware serão invocados Olá `Configuration(…)` método quando a aplicação for iniciada.

No nosso exemplo, Alterámos declaração de classe de Olá demasiado`public partial class Startup` e implementados Olá outro parte da classe de Olá na `App_Start\Startup.Auth.cs`. Olá interior `Configuration` método, adicionámos uma chamada demasiado`ConfigureAuth`, que está definido no `Startup.Auth.cs`. Após a modificação de Olá, `Startup.cs` se parece com Olá seguinte:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a>Configurar a autenticação OAuth 2.0

Ficheiro aberto Olá `App_Start\Startup.Auth.cs`e implementar Olá `ConfigureAuth(...)` método. Por exemplo, se foi aspeto Olá seguinte:

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Proteger o controlador de tarefa Olá

Após a conclusão da aplicação Olá autenticação toouse configurado OAuth 2.0, pode proteger a API web adicionando um `[Authorize]` controlador de tarefa toohello etiquetas. Este é o controlador de olá onde manipulação de lista de todas as tarefas ocorre, pelo que deve proteger controlador na totalidade Olá ao nível de classe de Olá. Também pode adicionar Olá `[Authorize]` tag tooindividual ações para um controlo mais detalhado.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Obter informações de utilizador de Olá token

`TasksController`armazena as tarefas numa base de dados onde cada tarefa tem um utilizador associado que é "proprietário" tarefa Olá. proprietário de Olá é identificado por utilizador Olá **ID de objeto**. (Esta é a razão pela qual é necessário o ID de objeto de Olá tooadd como uma aplicação afirmação em todas as suas políticas.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Validar permissões de Olá no token de Olá

Um requisito comum para as APIs web é toovalidate Olá "âmbitos" presentes no token de Olá. Isto garante que o utilizador Olá consentiu serviço de lista de tarefas necessária tooaccess Olá toohello permissões.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Executar a aplicação de exemplo de Olá

Por último, crie e execute `TaskWebApp` e `TaskService`. Crie algumas tarefas na lista de tarefas do utilizador Olá e repare como persistem na Olá API mesmo depois de parar e reiniciar Olá cliente.

## <a name="edit-your-policies"></a>Editar as suas políticas

Depois de proteger uma API utilizando o Azure AD B2C, pode experimentar com a política de início de sessão-na/sessão-up e vista Olá efeitos (ou ambos falta) na Olá API. Pode manipular afirmações de aplicação Olá nas políticas de Olá e alterar as informações de utilizador de Olá que estão disponíveis na API web do Olá. Qualquer afirmações que adicionar estarão disponíveis tooyour API de web de MVC do .NET no Olá `ClaimsPrincipal` objeto, como descrito anteriormente neste artigo.
