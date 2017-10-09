
## <a name="start-your-powershell-session"></a>Iniciar a sessão do PowerShell
Em primeiro lugar, deve ter hello mais recente do Azure PowerShell, instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Muitas funcionalidades novas da base de dados SQL só são suportadas quando estiver a utilizar Olá [modelo de implementação Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md)assim, os exemplos utilizam Olá [cmdlets do PowerShell de base de dados do SQL Azure](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) para o Resource Manager . modelo de implementação de gestão (clássica) de serviço Olá [cmdlets de gestão do serviço de base de dados do Azure SQL](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) são suportados para compatibilidade com versões anteriores, mas recomendamos que utilize Olá cmdlets do Resource Manager.
> 
> 

Executar Olá [ **Add-AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) e o cmdlet será apresentada com um ecrã de início de sessão tooenter as suas credenciais. Utilize Olá mesmo credenciais que utilizam toosign no toohello portal do Azure.

```PowerShell
Add-AzureRmAccount
```

Se tiver várias subscrições, utilize Olá [ **Set-AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect cmdlet que subscrição a sessão do PowerShell deve utilizar. toosee que subscrição Olá PowerShell atual sessão está a utilizar, execute [ **Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). a execução de todas as subscrições, toosee [ **Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
