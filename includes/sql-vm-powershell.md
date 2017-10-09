
## <a name="start-your-powershell-session"></a>Iniciar a sessão do PowerShell
Primeiro terá de toohave Olá mais recente [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Olá, exemplos de utilização deste tópico [modelo de implementação Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md)assim, os exemplos utilizam Olá [cmdlets do Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Executar Olá [ **Add-AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet e será apresentada com um início de sessão no ecrã tooenter as suas credenciais. Utilize Olá mesmo credenciais que utilizam toosign no toohello portal do Azure.

    Add-AzureRmAccount

Se tiver várias subscrições, utilize Olá [ **Set-AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect cmdlet que subscrição a sessão do PowerShell deve utilizar. toosee que subscrição Olá PowerShell atual sessão está a utilizar, execute [ **Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). a execução de todas as subscrições, toosee [ **Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

