### <a name="tooview-local-network-gateways"></a>tooview gateways de rede local

tooview uma lista de gateways de rede local Olá, utilize Olá [lista de gateway do local de rede de az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>valores de chave tooverify Olá partilhado

Certifique-se de que o valor da chave Olá partilhado é Olá mesmo valor que utilizou para a configuração do dispositivo VPN. Se não for, execute ligação Olá novamente utilizando o valor de Olá de dispositivo Olá ou atualizar o dispositivo de Olá com valor Olá Olá retorno. valores de Olá têm de corresponder. Olá tooview partilhado chave, utilize Olá [lista de ligações vpn de rede az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>gateway de VPN do tooview Olá endereço IP público

endereço IP de público de Olá do toofind do gateway da rede virtual, utilize Olá [lista de ip público de rede az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando. Para ler mais fácil, o resultado da Olá para este exemplo é a lista de Olá toodisplay formatado de IPs públicos no formato de tabela.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
