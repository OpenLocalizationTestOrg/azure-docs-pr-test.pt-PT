## <a name="obtain-an-azure-resource-manager-token"></a>Obter um token do Azure Resource Manager
Azure Active Directory tem de autenticar todas as tarefas de Olá efetuar recursos através de Olá do Azure Resource Manager. Olá exemplo apresentado aqui utiliza a autenticação de palavra-passe, para ver outras abordagens [pedidos de autenticação do Azure Resource Manager][lnk-authenticate-arm].

1. Adicionar Olá seguinte código toohello **Main** método Program.cs tooretrieve um token do Azure AD com o id da aplicação Olá e a palavra-passe.
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. Criar um **o ResourceManagementClient** objeto que utiliza Olá token adicionando Olá seguir final toohello código Olá **Main** método:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Cria ou obtém uma referência ao grupo de recursos de Olá que estiver a utilizar:
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx