
1. <span data-ttu-id="6e8ea-101">No ficheiro de projeto do Olá MainPage.xaml.cs, adicione o seguinte de Olá **utilizando** instruções:</span><span class="sxs-lookup"><span data-stu-id="6e8ea-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="6e8ea-102">Substitua Olá **AuthenticateAsync** método com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6e8ea-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    <span data-ttu-id="6e8ea-103">Nesta versão do **AuthenticateAsync**, aplicação Olá tenta credenciais de toouse armazenadas no Olá **PasswordVault** tooaccess Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="6e8ea-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="6e8ea-104">Um regular início de sessão é também efetuado quando não existe nenhuma credencial armazenada.</span><span class="sxs-lookup"><span data-stu-id="6e8ea-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6e8ea-105">Um token em cache pode estar expirado e expiração do token também pode ocorrer após a autenticação quando a aplicação Olá está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="6e8ea-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="6e8ea-106">toolearn como toodetermine se um token tiver expirado, consulte o artigo [Verifique a existência de tokens de autenticação expirada](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="6e8ea-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="6e8ea-107">Erros de autorização de toohandling uma solução de tokens de tooexpiring relacionadas, consulte Olá publique [colocação em cache e tokens expirados em Mobile Services do Azure de processamento gerido SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e8ea-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="6e8ea-108">Reinicie a aplicação de Olá duas vezes.</span><span class="sxs-lookup"><span data-stu-id="6e8ea-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="6e8ea-109">Tenha em atenção que no arranque primeiro de Olá, início de sessão com o fornecedor de Olá novamente é necessária.</span><span class="sxs-lookup"><span data-stu-id="6e8ea-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="6e8ea-110">No entanto, no momento do reinício segundo Olá credenciais Olá em cache são utilizadas e início de sessão é ignorada.</span><span class="sxs-lookup"><span data-stu-id="6e8ea-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

