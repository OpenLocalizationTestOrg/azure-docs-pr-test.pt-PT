## <a name="prepare-for-akv-integration"></a>Preparar a integração AKV
toouse tooconfigure de integração do Cofre de chaves do Azure a VM do SQL Server, existem vários pré-requisitos: 

1. [Instalar o Azure Powershell](#install-azure-powershell)
2. [Criar um Azure Active Directory](#create-an-azure-active-directory)
3. [Criar um cofre de chaves](#create-a-key-vault)

Olá secções seguintes descrevem estas pré-requisitos e informações de Olá, terá de cmdlets do PowerShell toocollect toolater executar Olá.

### <a name="install-azure-powershell"></a>Instalar o Azure PowerShell
Certifique-se de que instalou Olá, Azure PowerShell SDK mais recente. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Criar um Azure Active Directory
Em primeiro lugar, precisa de toohave um [do Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) na sua subscrição. Entre muitas vantagens, isto permite-lhe toogrant permissão tooyour Cofre de chaves para determinados utilizadores e aplicações.

Em seguida, registe uma aplicação com o AAD. Isto irá dar-lhe uma conta do Principal de serviço que tenha acesso tooyour Cofre de chaves que terá da VM. Artigo do Cofre de chaves do Azure Olá, pode encontrar estes passos no Olá [registar uma aplicação no Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) secção, ou pode ver os passos de Olá com capturas de ecrã Olá **obter uma identidade da aplicação Olá secção** de [esta mensagem de blogue](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Antes de concluir estes passos, tenha em atenção que tem de Olá toocollect seguir informações durante este registo que é necessária mais tarde, quando ativar a integração do Cofre de chaves do Azure na sua VM do SQL Server.

* Depois de é adicionada a aplicação Olá, determinar Olá **ID de cliente** no Olá **configurar** separador.   ![ID de cliente do Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    ID de cliente Olá é atribuído toohello posterior **$spName** parâmetro tooenable de script de PowerShell Olá integração do Cofre de chaves do Azure (nome Principal de serviço). 
* Além disso, durante estes passos ao criar a chave, copie segredo de Olá para a sua chave conforme é mostrado na seguinte captura de ecrã de Olá. Esta chave secreta é atribuída toohello posterior **$spSecret** parâmetro (segredo Principal de serviço) no script de PowerShell Olá.  
    ![Segredo do Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* Tem de autorizar este hello de toohave do ID cliente novo as seguintes permissões de acesso: **encriptar**, **desencriptar**, **wrapKey**, **unwrapKey**, **sessão**, e **verificar**. Isto é feito com Olá [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet. Para obter mais informações consulte [autorizar Olá aplicação toouse Olá chave ou segredo](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Criar um cofre de chaves
Ordem toouse Cofre de chaves do Azure toostore Olá chaves que irá utilizar para encriptação na sua VM, terá de Cofre de chaves de tooa de acesso. Se já não configurar o seu Cofre de chaves, crie um seguindo os passos de Olá em Olá [introdução ao Cofre de chaves do Azure](../articles/key-vault/key-vault-get-started.md) tópico. Antes de concluir estes passos, tenha em atenção que não há algumas informações necessárias toocollect durante este conjunto de cópias de segurança que é necessária mais tarde, quando ativar a integração do Cofre de chaves do Azure na sua VM do SQL Server.

Quando chegar toohello passo da criação de um cofre de chaves, Olá nota devolvido **vaultUri** propriedade, o que é o URL do Cofre de chaves de Olá. Exemplo de Olá fornecido esse passo, abaixo, nome do Cofre de chaves de Olá ContosoKeyVault, por conseguinte, o URL do Cofre de chaves de Olá seria https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

URL do Cofre de chaves de Olá é atribuído toohello posterior **$akvURL** parâmetro tooenable de script de PowerShell Olá integração do Cofre de chaves do Azure.

