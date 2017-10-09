## <a name="set-up-azure-cli-for-azure-dns"></a>Configurar CLI do Azure para o Azure DNS

### <a name="before-you-begin"></a>Antes de começar

Certifique-se de que tem Olá seguintes itens antes de iniciar a configuração.

* Uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instale a versão mais recente do Olá do Olá CLI do Azure, disponível para Windows, Linux ou Mac. Estão disponíveis mais informações no [instalação Olá CLI do Azure](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Inicie sessão no tooyour a conta do Azure

Abra uma janela de consola e autentique com as suas credenciais. Para obter mais informações, consulte [tooAzure de Olá CLI do Azure de início de sessão](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Alternar o modo da CLI

O DNS do Azure utiliza o Azure Resource Manager. Certifique-se de que alterna comandos da CLI modo toouse do Azure Resource Manager.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Selecione a subscrição de Olá

Verifique Olá subscrições para a conta de Olá.

```azurecli
azure account list
```

Escolha qual das suas toouse de subscrições do Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização, Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos. No entanto, uma vez que todos os recursos DNS são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no DNS do Azure.

Pode ignorar este passo se estiver a utilizar um grupo de recursos existente.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Registar o fornecedor de recursos

Olá serviço DNS do Azure é gerida pelo fornecedor de recursos do Olá Network. A subscrição do Azure tem de ser registado toouse este fornecedor de recursos antes de poder utilizar o DNS do Azure. Esta é uma operação única para cada subscrição.

```azurecli
azure provider register --namespace Microsoft.Network
```

