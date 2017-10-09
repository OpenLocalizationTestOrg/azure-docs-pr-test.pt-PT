Tem de criar uma VNet e uma sub-rede de gateway em primeiro lugar, antes de trabalhar Olá seguintes tarefas. Consulte o artigo Olá [configurar uma rede Virtual com o portal clássico Olá](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) para obter mais informações.   

## <a name="add-a-gateway"></a>Adicionar um gateway
Utilize o comando de Olá abaixo toocreate um gateway. Ser toosubstitute se os valores pelos seus.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Certifique-se de que foi criado o gateway de Olá
Utilize o comando de Olá abaixo tooverify Olá gateway foi criado. Este comando também obtém o ID de gateway Olá, o que precisa para outras operações.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Redimensionar um gateway
Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Pode utilizar Olá seguir Olá toochange do comando SKU de Gateway em qualquer altura.

> [!IMPORTANT]
> Este comando não funciona para UltraPerformance gateway. toochange o gateway de UltraPerformance tooan do gateway, primeiro remova Olá existente ExpressRoute gateway e, em seguida, criar um novo gateway de UltraPerformance. toodowngrade o gateway de um gateway de UltraPerformance, remova primeiro Olá UltraPerformance gateway e, em seguida, crie um novo gateway. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Remover um gateway
Utilize o comando de Olá abaixo tooremove um gateway

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>