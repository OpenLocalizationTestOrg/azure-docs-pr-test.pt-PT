## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="f210b-101">Configurar o PowerShell para modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f210b-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="f210b-102">Antes de poder utilizar o Azure PowerShell com o Resource Manager, terá de toohave Olá corretas do Windows PowerShell e o Azure PowerShell versões.</span><span class="sxs-lookup"><span data-stu-id="f210b-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="f210b-103">Verificar se versões do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f210b-103">Verify PowerShell versions</span></span>
<span data-ttu-id="f210b-104">Certifique-se de que tem o Windows PowerShell versão 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="f210b-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="f210b-105">versão de Olá toofind do Windows PowerShell, escreva este comando numa linha de comandos do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f210b-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="f210b-106">Receberá Olá seguinte tipo de informações:</span><span class="sxs-lookup"><span data-stu-id="f210b-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="f210b-107">Certifique-se de que o valor de Olá **PSVersion** é 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="f210b-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="f210b-108">Caso contrário, veja [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="f210b-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="f210b-109">Definir a conta e a subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="f210b-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="f210b-110">Se ainda não tiver uma subscrição do Azure, pode ativar o [benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se um [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f210b-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="f210b-111">Abra uma linha de comandos do Azure PowerShell e inicie sessão tooAzure com este comando.</span><span class="sxs-lookup"><span data-stu-id="f210b-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="f210b-112">Se tiver várias subscrições do Azure, pode listar as subscrições do Azure com este comando.</span><span class="sxs-lookup"><span data-stu-id="f210b-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="f210b-113">Receberá Olá seguinte tipo de informações:</span><span class="sxs-lookup"><span data-stu-id="f210b-113">You will receive hello following type of information:</span></span>

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

<span data-ttu-id="f210b-114">Pode definir a subscrição do Azure atual de Olá executando estes comandos na linha de comandos do Azure PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="f210b-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="f210b-115">Substitua tudo dentro de aspas Olá, incluindo Olá < e > carateres, com o nome correto Olá.</span><span class="sxs-lookup"><span data-stu-id="f210b-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="f210b-116">Para obter mais informações sobre as subscrições do Azure e as contas, consulte [como: ligar tooyour subscrição](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="f210b-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

