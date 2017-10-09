### <a name="gwipnoconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - nenhuma ligação de gateway

Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram. Utilize o exemplo de Olá toomodify um gateway de rede local que não tem uma ligação de gateway.

Quando modificar este valor, também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo. Na ordem toooverwrite Olá as definições atuais de ser se toouse Olá nome existente do gateway de rede local. Se utilizar um nome diferente, criar um novo gateway de rede local, em vez de substituir Olá já existente.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - ligação de gateway existente

Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram. Se gateway já existe uma ligação, terá primeiro de ligação de Olá tooremove. Depois de remover a ligação de Olá, pode modificar o endereço IP do gateway Olá e recriá-lo de uma nova ligação. Também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo. Este procedimento resulta num período de indisponibilidade da ligação VPN. Quando modificar o endereço IP do gateway Olá, não precisa de gateway de VPN de Olá toodelete. Só precisa de ligação de Olá tooremove.
 

1. Remova ligação Olá. Pode encontrar o nome Olá da sua ligação utilizando o cmdlet Olá 'Get-AzureRmVirtualNetworkGatewayConnection'.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Modifique o valor de 'GatewayIpAddress' Olá. Também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo. Ser se toouse Olá existente nome da sua rede local gateway toooverwrite Olá definições atuais. Caso contrário, crie um novo gateway de rede local, em vez de substituir Olá já existente.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Crie ligação Olá. Neste exemplo, configuramos uma ligação do tipo IPsec. Ao recriar a ligação, utilize o tipo de ligação de Olá especificado para a sua configuração. Para tipos de ligação adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.  nome do tooobtain Olá VirtualNetworkGateway, pode executar Olá 'Get-AzureRmVirtualNetworkGateway' cmdlet.
   
    Definir variáveis de Olá.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Crie ligação Olá.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```