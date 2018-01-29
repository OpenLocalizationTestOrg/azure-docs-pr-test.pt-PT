
## <a name="set-up-your-project"></a>Configurar o projeto

Esta secção mostra os passos para instalar e configurar o pipeline de autenticação através da OWIN middleware num projeto ASP.NET com OpenID Connect. 

> Prefere transferir o projeto do Visual Studio este exemplo em vez disso? [Transferir um projeto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e avance para o [passo da configuração](#create-an-application-express) para configurar o exemplo de código antes de executar.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Criar o projeto ASP.NET

> 1. No Visual Studio:`File` > `New` > `Project`<br/>
> 2. Em *Visual C# \Web*, selecione `ASP.NET Web Application (.NET Framework)`.
> 3. Nome da aplicação e clique em *OK*
> 4. Selecione `Empty` e selecione a caixa de verificação para adicionar `MVC` referências
<!--end-collapse-->

## <a name="add-authentication-components"></a>Adicionar componentes de autenticação

1. No Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Adicionar *pacotes de NuGet OWIN middleware* , escrevendo o seguinte na janela da consola do Gestor de pacotes:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Sobre estas bibliotecas

>Ative as bibliotecas acima-início de sessão único (SSO) utilizando o OpenID Connect através da autenticação baseada no cookie. Após a autenticação é concluída e o token que representa o utilizador é enviado para a sua aplicação, o OWIN middleware cria um cookie de sessão. O browser, em seguida, utiliza este cookie nos pedidos subsequentes para que o utilizador não tem de introduzir a palavra-passe e não é necessária nenhuma verificação adicional.
<!--end-collapse-->

## <a name="configure-the-authentication-pipeline"></a>Configurar o pipeline de autenticação
Os passos abaixo são utilizados para criar uma classe de Startup para configurar a autenticação OpenID Connect de middleware OWIN. Esta classe será executada automaticamente quando inicia o processo IIS.

> Se o seu projeto não tem um `Startup.cs` ficheiro na pasta raiz:<br/>
> 1. Botão direito do rato clique na pasta de raiz do projeto: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Nome`Startup.cs`

> Certifique-se a classe selecionada uma classe de Startup da OWIN e não uma padrão c# classe. Confirmar isto, verificando se vir `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` acima o espaço de nomes.


1. Adicionar *OWIN* e *IdentityModel* referências a `Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Substitua a classe de Startup com o código abaixo:
</li>
</ol>

```csharp
public class Startup
{        
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is the URL where the user will be redirected to after they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is the tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is the URL for authority, composed by Azure Active Directory v2 endpoint and the tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN to use OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets the ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set to request the id_token - which contains basic information about the signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
                // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
                // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting the user to the home page with an error in the query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Mais Informações

> Os parâmetros que fornece *OpenIDConnectAuthenticationOptions* servir como coordenadas para a aplicação comunicar com o Azure AD. Uma vez que o middleware OpenID Connect utiliza cookies em segundo plano, terá também de configurar a autenticação de cookie como o código acima mostra. O *ValidateIssuer* valor indica OpenIdConnect não restringir o acesso a uma organização específica.
<!--end-collapse-->

