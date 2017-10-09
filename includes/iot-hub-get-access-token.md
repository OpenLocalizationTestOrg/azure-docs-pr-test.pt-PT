## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="0bc01-101">Obter um token do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0bc01-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="0bc01-102">Azure Active Directory tem de autenticar todas as tarefas de Olá efetuar recursos através de Olá do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0bc01-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="0bc01-103">Olá exemplo apresentado aqui utiliza a autenticação de palavra-passe, para ver outras abordagens [pedidos de autenticação do Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="0bc01-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="0bc01-104">Adicionar Olá seguinte código toohello **Main** método Program.cs tooretrieve um token do Azure AD com o id da aplicação Olá e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="0bc01-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
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
2. <span data-ttu-id="0bc01-105">Criar um **o ResourceManagementClient** objeto que utiliza Olá token adicionando Olá seguir final toohello código Olá **Main** método:</span><span class="sxs-lookup"><span data-stu-id="0bc01-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="0bc01-106">Cria ou obtém uma referência ao grupo de recursos de Olá que estiver a utilizar:</span><span class="sxs-lookup"><span data-stu-id="0bc01-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
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