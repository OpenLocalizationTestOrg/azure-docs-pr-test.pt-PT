<span data-ttu-id="4f56a-101">Antes de iniciar esta configuração, tem de iniciar sessão tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56a-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="4f56a-102">Olá pede-lhe as credenciais de início de sessão de Olá para a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56a-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="4f56a-103">Após iniciar sessão, transfere as definições de conta para que estejam disponível tooAzure do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f56a-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="4f56a-104">Para obter mais informações, veja [Utilizar o Windows PowerShell com o Resource Manager](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4f56a-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="4f56a-105">toolog, abra a consola do PowerShell com privilégios elevados e ligar tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="4f56a-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="4f56a-106">Utilize Olá toohelp de exemplo, ligar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4f56a-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4f56a-107">Se tiver várias subscrições do Azure, verifique subscrições Olá conta Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56a-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="4f56a-108">Especifique que pretende que o toouse de subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f56a-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```