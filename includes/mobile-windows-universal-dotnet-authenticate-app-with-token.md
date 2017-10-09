
1. No ficheiro de projeto do Olá MainPage.xaml.cs, adicione o seguinte de Olá **utilizando** instruções:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Substitua Olá **AuthenticateAsync** método com Olá seguinte código:
   
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
   
    Nesta versão do **AuthenticateAsync**, aplicação Olá tenta credenciais de toouse armazenadas no Olá **PasswordVault** tooaccess Olá serviço. Um regular início de sessão é também efetuado quando não existe nenhuma credencial armazenada.
   
   > [!NOTE]
   > Um token em cache pode estar expirado e expiração do token também pode ocorrer após a autenticação quando a aplicação Olá está a ser utilizado. toolearn como toodetermine se um token tiver expirado, consulte o artigo [Verifique a existência de tokens de autenticação expirada](http://aka.ms/jww5vp). Erros de autorização de toohandling uma solução de tokens de tooexpiring relacionadas, consulte Olá publique [colocação em cache e tokens expirados em Mobile Services do Azure de processamento gerido SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Reinicie a aplicação de Olá duas vezes.
   
    Tenha em atenção que no arranque primeiro de Olá, início de sessão com o fornecedor de Olá novamente é necessária. No entanto, no momento do reinício segundo Olá credenciais Olá em cache são utilizadas e início de sessão é ignorada. 

