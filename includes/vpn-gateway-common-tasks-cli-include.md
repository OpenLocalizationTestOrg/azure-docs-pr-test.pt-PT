### <a name="tooview-local-network-gateways"></a><span data-ttu-id="6f830-101">tooview gateways de rede local</span><span class="sxs-lookup"><span data-stu-id="6f830-101">tooview local network gateways</span></span>

<span data-ttu-id="6f830-102">tooview uma lista de gateways de rede local Olá, utilize Olá [lista de gateway do local de rede de az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.</span><span class="sxs-lookup"><span data-stu-id="6f830-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="6f830-103">valores de chave tooverify Olá partilhado</span><span class="sxs-lookup"><span data-stu-id="6f830-103">tooverify hello shared key values</span></span>

<span data-ttu-id="6f830-104">Certifique-se de que o valor da chave Olá partilhado é Olá mesmo valor que utilizou para a configuração do dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="6f830-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="6f830-105">Se não for, execute ligação Olá novamente utilizando o valor de Olá de dispositivo Olá ou atualizar o dispositivo de Olá com valor Olá Olá retorno.</span><span class="sxs-lookup"><span data-stu-id="6f830-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="6f830-106">valores de Olá têm de corresponder.</span><span class="sxs-lookup"><span data-stu-id="6f830-106">hello values must match.</span></span> <span data-ttu-id="6f830-107">Olá tooview partilhado chave, utilize Olá [lista de ligações vpn de rede az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="6f830-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="6f830-108">gateway de VPN do tooview Olá endereço IP público</span><span class="sxs-lookup"><span data-stu-id="6f830-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="6f830-109">endereço IP de público de Olá do toofind do gateway da rede virtual, utilize Olá [lista de ip público de rede az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="6f830-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="6f830-110">Para ler mais fácil, o resultado da Olá para este exemplo é a lista de Olá toodisplay formatado de IPs públicos no formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="6f830-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
