### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>gateway de rede local toomodify Olá 'gatewayIpAddress'

Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram. o endereço IP do gateway Olá pode ser alterado sem remover uma ligação de gateway VPN existente (se tiver uma). endereço IP do gateway toomodify Olá, substituir valores de Olá 'Site2' e 'TestRG1' com a suas próprias utilizando Olá [atualização de gateway do local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Certifique-se de que o endereço IP Olá está correto no resultado de Olá:

```
"gatewayIpAddress": "23.99.222.170",
```