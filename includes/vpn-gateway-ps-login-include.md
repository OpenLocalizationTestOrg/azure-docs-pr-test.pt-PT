Antes de iniciar esta configuração, tem de iniciar sessão tooyour conta do Azure. Olá pede-lhe as credenciais de início de sessão de Olá para a sua conta do Azure. Após iniciar sessão, transfere as definições de conta para que estejam disponível tooAzure do PowerShell. Para obter mais informações, veja [Utilizar o Windows PowerShell com o Resource Manager](../articles/powershell-azure-resource-manager.md).

toolog, abra a consola do PowerShell com privilégios elevados e ligar tooyour conta. Utilize Olá toohelp de exemplo, ligar os seguintes:

```powershell
Login-AzureRmAccount
```

Se tiver várias subscrições do Azure, verifique subscrições Olá conta Olá.

```powershell
Get-AzureRmSubscription
```

Especifique que pretende que o toouse de subscrição de Olá.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```