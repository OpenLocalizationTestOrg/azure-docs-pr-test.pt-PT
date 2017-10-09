### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="73b85-101">gateway de rede local toomodify Olá 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="73b85-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="73b85-102">Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="73b85-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="73b85-103">o endereço IP do gateway Olá pode ser alterado sem remover uma ligação de gateway VPN existente (se tiver uma).</span><span class="sxs-lookup"><span data-stu-id="73b85-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="73b85-104">endereço IP do gateway toomodify Olá, substituir valores de Olá 'Site2' e 'TestRG1' com a suas próprias utilizando Olá [atualização de gateway do local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.</span><span class="sxs-lookup"><span data-stu-id="73b85-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="73b85-105">Certifique-se de que o endereço IP Olá está correto no resultado de Olá:</span><span class="sxs-lookup"><span data-stu-id="73b85-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```