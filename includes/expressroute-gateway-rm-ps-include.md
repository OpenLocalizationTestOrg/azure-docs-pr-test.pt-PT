Olá os passos para utilizar esta tarefa uma VNet com base nos valores de Olá no Olá seguinte lista de referência de configuração. Nomes e outras definições também são descritos nesta lista. Iremos não utilize esta lista diretamente em nenhum dos passos de Olá, embora adicionamos variáveis com base nos valores de Olá nesta lista. Pode copiar Olá lista toouse como uma referência, substituindo os valores de Olá com os seus próprios.

**Lista de referência de configuração**

* Nome da rede virtual = "TestVNet"
* Espaço de endereços de rede virtuais = 192.168.0.0/16
* Grupo de recursos = "TestRG"
* Subnet1 Name = "FrontEnd" 
* Espaço de endereços Subnet1 = "192.168.1.0/24"
* Nome de sub-rede de gateway: "GatewaySubnet" tem de nome sempre uma sub-rede de gateway *GatewaySubnet*.
* Espaço de endereços de sub-rede de gateway = "192.168.200.0/26"
* Região = "EUA Leste"
* O nome do gateway = "GW"
* O nome IP do gateway = "GWIP"
* Configuração de IP do gateway Name = "gwipconf"
* Tipo = "ExpressRoute" deste tipo é necessário para uma configuração do ExpressRoute.
* Nome de IP público do gateway = "gwpip"

## <a name="add-a-gateway"></a>Adicionar um gateway
1. Ligar tooyour subscrição do Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Declare as variáveis para este exercício. Ser tooedit se Olá tooreflect Olá as definições de exemplo que pretende que o toouse.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Armazene o objeto de rede virtual Olá como uma variável.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Adicione um tooyour de sub-rede de gateway rede Virtual. sub-rede do gateway Olá deve ter o nome "GatewaySubnet". Deve criar uma sub-rede de gateway é/27 ou superior (/ 26, / 25, etc.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Definir a configuração de Olá.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Armazenar a sub-rede do gateway Olá como uma variável.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Solicitar um endereço IP público. o endereço IP de Olá é solicitado antes de criar Olá gateway. Não é possível especificar o endereço IP Olá que pretende que o toouse; é dinamicamente atribuído. Utilizará este endereço IP na secção de configuração seguinte Olá. Olá AllocationMethod tem de ser dinâmico.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Crie Olá configuração para o seu gateway. configuração do gateway de Olá define uma sub-rede de Olá e Olá toouse de endereço IP público. Neste passo, são especificar a configuração de Olá que será utilizada ao criar o gateway de Olá. Este passo não criar objeto do gateway Olá efetivamente. Utilize o exemplo de Olá abaixo toocreate a configuração do gateway.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Crie gateway de Olá. Neste passo, Olá **- GatewayType** é especialmente importante. Tem de utilizar o valor de Olá **ExpressRoute**. Depois de executar estes cmdlets, gateway Olá pode demorar 45 minutos ou mais toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Certifique-se de que foi criado o gateway de Olá
Utilize Olá os seguintes comandos tooverify Olá gateway tiver sido criada:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Redimensionar um gateway
Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Pode utilizar Olá seguir Olá toochange do comando SKU de Gateway em qualquer altura.

> [!IMPORTANT]
> Este comando não funciona para UltraPerformance gateway. toochange o gateway de UltraPerformance tooan do gateway, primeiro remova Olá existente ExpressRoute gateway e, em seguida, criar um novo gateway de UltraPerformance. toodowngrade o gateway de um gateway de UltraPerformance, remova primeiro Olá UltraPerformance gateway e, em seguida, crie um novo gateway.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Remover um gateway
Utilize os seguintes comandos tooremove um gateway de Olá:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```