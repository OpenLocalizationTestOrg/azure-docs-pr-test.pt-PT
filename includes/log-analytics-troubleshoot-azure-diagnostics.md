### <a name="troubleshoot-azure-diagnostics"></a>Resolver Problemas do Diagnóstico do Azure

Se receber Olá seguir a mensagem de erro, o fornecedor de recursos do Olá insights não está registado:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

fornecedor de recursos do tooregister Olá, efetuar Olá os seguintes passos no portal do Azure de Olá:

1.  No painel de navegação de Olá Olá esquerda, clique em *subscrições*
2.  Selecione a subscrição de Olá identificada na mensagem de erro Olá
3.  Clique em *Fornecedores de Recursos*
4.  Determinar Olá *insights* fornecedor
5.  Clique em Olá *registar* ligação

![Registe o fornecedor de recursos do microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Uma vez Olá *insights* é registado o fornecedor de recursos, repita a configuração de diagnósticos.


No PowerShell, se receber Olá seguir a mensagem de erro, terá de tooupdate a versão do PowerShell:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Atualizar a versão do PowerShell toohello Novembro de 2016 (v2.3.0) ou versão posterior, utilizando instruções Olá no Olá [introdução aos cmdlets do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artigo.
