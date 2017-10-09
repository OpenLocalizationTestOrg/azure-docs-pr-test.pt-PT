Inicie sessão no tooyour subscrição do Azure com Olá [início de sessão az](/cli/azure/#login) de comandos e siga Olá no ecrã de instruções. Para obter mais informações sobre o início de sessão, veja [Introdução à CLI 2.0 do Azure](/cli/azure/get-started-with-azure-cli).

```azurecli
az login
```

Se tiver mais do que uma subscrição do Azure, liste as subscrições de Olá para a conta de Olá.

```azurecli
az account list --all
```

Especifique que pretende que o toouse de subscrição de Olá.

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```