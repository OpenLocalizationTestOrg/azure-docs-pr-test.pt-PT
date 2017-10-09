## <a name="set-up-azure-powershell-for-azure-dns"></a>Configurar o Azure PowerShell para o DNS do Azure

### <a name="before-you-begin"></a>Antes de começar

Certifique-se de que tem Olá seguintes itens antes de iniciar a configuração.

* Uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Tem a versão mais recente de Olá tooinstall de Olá cmdlets do PowerShell do Azure Resource Manager. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Inicie sessão no tooyour a conta do Azure

Abra a consola do PowerShell e ligue tooyour conta. Para obter mais informações, consulte [utilizando o PowerShell com o Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Selecione a subscrição de Olá
 
Verifique Olá subscrições para a conta de Olá.

```powershell
Get-AzureRmSubscription
```

Escolha qual das suas toouse de subscrições do Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização, Esta localização é utilizada como localização predefinida de Olá para recursos nesse grupo de recursos. No entanto, uma vez que todos os recursos DNS são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no DNS do Azure.

Pode ignorar este passo se estiver a utilizar um grupo de recursos existente.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Registar o fornecedor de recursos

Olá serviço DNS do Azure é gerida pelo fornecedor de recursos do Olá Network. A subscrição do Azure tem de ser registado toouse este fornecedor de recursos antes de poder utilizar o DNS do Azure. Esta é uma operação única para cada subscrição.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```