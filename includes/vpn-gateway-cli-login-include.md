<span data-ttu-id="25298-101">Inicie sessão no tooyour subscrição do Azure com Olá [início de sessão az](/cli/azure/#login) de comandos e siga Olá no ecrã de instruções.</span><span class="sxs-lookup"><span data-stu-id="25298-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="25298-102">Para obter mais informações sobre o início de sessão, veja [Introdução à CLI 2.0 do Azure](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="25298-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="25298-103">Se tiver mais do que uma subscrição do Azure, liste as subscrições de Olá para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="25298-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="25298-104">Especifique que pretende que o toouse de subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="25298-104">Specify hello subscription that you want toouse.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```