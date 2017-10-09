### <a name="noconnection"></a>prefixos de endereços IP de gateway de rede local toomodify - nenhuma ligação de gateway

tooadd prefixos de endereços adicionais:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

prefixos de endereço tooremove:<br>
Deixe os prefixos de Olá que já não necessita. Neste exemplo, vamos já não precisamos do prefixo 20.0.0.0/24 (do exemplo anterior Olá), pelo que iremos atualizar o gateway de rede local Olá, excluir esse prefixo.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify rede local gateway prefixos de endereços IP - existente a ligação de gateway

Se tiver uma ligação de gateway e pretender tooadd ou remover prefixos de endereço IP do Olá contidos no gateway de rede local, terá de Olá toodo os seguintes passos, por ordem. Este procedimento resulta num período de indisponibilidade da ligação VPN. Ao modificar os prefixos de endereços IP, não precisa de gateway de VPN de Olá toodelete. Só precisa de ligação de Olá tooremove.


1. Remova ligação Olá.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Modificar os prefixos de endereço de Olá para gateway de rede local.
   
  Definir variável Olá para Olá LocalNetworkGateway.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Modificar os prefixos de Olá.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Crie ligação Olá. Neste exemplo, configuramos uma ligação do tipo IPsec. Ao recriar a ligação, utilize o tipo de ligação de Olá especificado para a sua configuração. Para tipos de ligação adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.
   
  Definir variável Olá para Olá VirtualNetworkGateway.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Crie ligação Olá. Este exemplo utiliza a variável de Olá $local que configurou no passo 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```