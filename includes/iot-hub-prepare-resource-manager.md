## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Preparar tooauthenticate pedidos do Azure Resource Manager
Tem de autenticar todas as operações de Olá efetuar recursos através de Olá [do Azure Resource Manager] [ lnk-authenticate-arm] com o Azure Active Directory (AD). Olá tooconfigure de forma mais fácil é toouse PowerShell ou a CLI do Azure.

Instalar Olá [cmdlets Azure PowerShell] [ lnk-powershell-install] antes de continuar.

Olá, como os seguintes passos Mostrar tooset configurar a autenticação de palavra-passe para uma aplicação AD utilizando o PowerShell. Pode executar estes comandos numa sessão do PowerShell padrão.

1. Inicie sessão no tooyour subscrição do Azure com Olá os seguintes comandos:

    ```powershell
    Login-AzureRmAccount
    ```

1. Se tiver várias subscrições do Azure, iniciar sessão tooAzure concede acesso tooall Olá subscrições Azure associadas as suas credenciais. Utilize Olá toolist Olá subscrições do Azure disponíveis para si toouse de comando a seguir:

    ```powershell
    Get-AzureRMSubscription
    ```

    Utilize Olá seguir subscrição tooselect de comando que pretende que o toouse toorun Olá comandos toomanage seu IoT hub. Pode utilizar o nome da subscrição Olá ou o ID da saída de Olá do comando anterior Olá:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Tome nota do seu **TenantId** e **SubscriptionId**. Poderá precisa deles mais tarde.
3. Crie uma nova aplicação do Azure Active Directory utilizando Olá comando a seguir, substituindo os proprietários de local da Olá:
   
   * **{Nome a apresentar}:** um nome a apresentar para a sua aplicação, tais como **MySampleApp**
   * **{URL da página inicial}:** Olá, tais como o URL da Olá home page da sua aplicação **http://mysampleapp/home**. Este URL não precisa de toopoint tooa real aplicação.
   * **{Identificador da aplicação}:** um identificador exclusivo, tais como **http://mysampleapp**. Este URL não precisa de toopoint tooa real aplicação.
   * **{Palavra-passe}:** uma palavra-passe que utiliza tooauthenticate com a sua aplicação.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Tome nota do Olá **ApplicationId** da aplicação Olá que criou. Poderá precisa deste mais tarde.
5. Criar um novo principal de serviço com Olá comando a seguir, substituindo **{MyApplicationId}** com Olá **ApplicationId** do passo anterior Olá:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Configurar uma atribuição de função utilizando Olá comando a seguir, substituindo **{MyApplicationId}** com seu **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Terminar agora de criar a aplicação do Azure AD Olá que lhe permite tooauthenticate da sua aplicação c# personalizada. É necessário Olá os seguintes valores mais tarde no tutorial:

* TenantId
* SubscriptionId
* ApplicationId
* Palavra-passe

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
