## <a name="setting-up-powershell-for-resource-manager-templates"></a>Configurar o PowerShell para modelos do Resource Manager
Antes de poder utilizar o Azure PowerShell com o Resource Manager, terá de toohave Olá corretas do Windows PowerShell e o Azure PowerShell versões.

### <a name="verify-powershell-versions"></a>Verificar se versões do PowerShell
Certifique-se de que tem o Windows PowerShell versão 3.0 ou 4.0. versão de Olá toofind do Windows PowerShell, escreva este comando numa linha de comandos do Windows PowerShell.

    $PSVersionTable

Receberá Olá seguinte tipo de informações:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Certifique-se de que o valor de Olá **PSVersion** é 3.0 ou 4.0. Caso contrário, veja [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Definir a conta e a subscrição do Azure
Se ainda não tiver uma subscrição do Azure, pode ativar o [benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se um [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

Abra uma linha de comandos do Azure PowerShell e inicie sessão tooAzure com este comando.

    Login-AzureRmAccount

Se tiver várias subscrições do Azure, pode listar as subscrições do Azure com este comando.

    Get-AzureRmSubscription

Receberá Olá seguinte tipo de informações:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Pode definir a subscrição do Azure atual de Olá executando estes comandos na linha de comandos do Azure PowerShell Olá. Substitua tudo dentro de aspas Olá, incluindo Olá < e > carateres, com o nome correto Olá.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Para obter mais informações sobre as subscrições do Azure e as contas, consulte [como: ligar tooyour subscrição](/powershell/azureps-cmdlets-docs#step-3-connect).

