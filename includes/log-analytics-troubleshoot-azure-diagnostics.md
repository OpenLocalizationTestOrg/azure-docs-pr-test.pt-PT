### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="ce8b4-101">Resolver Problemas do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ce8b4-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="ce8b4-102">Se receber Olá seguir a mensagem de erro, o fornecedor de recursos do Olá insights não está registado:</span><span class="sxs-lookup"><span data-stu-id="ce8b4-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="ce8b4-103">fornecedor de recursos do tooregister Olá, efetuar Olá os seguintes passos no portal do Azure de Olá:</span><span class="sxs-lookup"><span data-stu-id="ce8b4-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="ce8b4-104">No painel de navegação de Olá Olá esquerda, clique em *subscrições*</span><span class="sxs-lookup"><span data-stu-id="ce8b4-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="ce8b4-105">Selecione a subscrição de Olá identificada na mensagem de erro Olá</span><span class="sxs-lookup"><span data-stu-id="ce8b4-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="ce8b4-106">Clique em *Fornecedores de Recursos*</span><span class="sxs-lookup"><span data-stu-id="ce8b4-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="ce8b4-107">Determinar Olá *insights* fornecedor</span><span class="sxs-lookup"><span data-stu-id="ce8b4-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="ce8b4-108">Clique em Olá *registar* ligação</span><span class="sxs-lookup"><span data-stu-id="ce8b4-108">Click hello *Register* link</span></span>

![Registe o fornecedor de recursos do microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="ce8b4-110">Uma vez Olá *insights* é registado o fornecedor de recursos, repita a configuração de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="ce8b4-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="ce8b4-111">No PowerShell, se receber Olá seguir a mensagem de erro, terá de tooupdate a versão do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ce8b4-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="ce8b4-112">Atualizar a versão do PowerShell toohello Novembro de 2016 (v2.3.0) ou versão posterior, utilizando instruções Olá no Olá [introdução aos cmdlets do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artigo.</span><span class="sxs-lookup"><span data-stu-id="ce8b4-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
