---
title: 'Ligar o seu tooan de rede no local rede virtual do Azure: VPN Site a Site: PowerShell | Microsoft Docs'
description: "Uma ligação de IPsec do seu local de rede tooan rede virtual do Azure através de toocreate de passos Olá Internet pública. Estes passos ajudam-no a criar uma ligação de Gateway de Rede de VPNs em vários sites com o PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="426e5-104">Criar uma VNet com uma ligação de Rede de VPNs com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="426e5-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="426e5-105">Este artigo mostra como toouse PowerShell ligação de gateway VPN toocreate um Site para Site do seu local de rede toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="426e5-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="426e5-106">passos de Olá neste artigo aplicam-se o modelo de implementação do Resource Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="426e5-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="426e5-107">Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="426e5-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="426e5-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="426e5-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="426e5-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="426e5-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="426e5-110">CLI</span><span class="sxs-lookup"><span data-stu-id="426e5-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="426e5-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="426e5-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="426e5-112">Portal clássico (clássico)</span><span class="sxs-lookup"><span data-stu-id="426e5-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="426e5-113">Uma ligação de gateway VPN de Site a Site é utilizado tooconnect tooan rede virtual do Azure de rede no local através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="426e5-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="426e5-114">Este tipo de ligação requer uma VPN dispositivos localizado no local que tenha um tooit de atribuída de endereço IP público com acesso exterior.</span><span class="sxs-lookup"><span data-stu-id="426e5-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="426e5-115">Para obter mais informações sobre o gateways de VPN, veja [About VPN gateway (Acerca do gateway de VPN)](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="426e5-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama da ligação de Gateway de Rede de VPNs em vários sites](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="426e5-117"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="426e5-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="426e5-118">Certifique-se de que cumpriu Olá os seguintes critérios antes de iniciar a configuração:</span><span class="sxs-lookup"><span data-stu-id="426e5-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="426e5-119">Certifique-se de um dispositivo VPN compatível e alguém que seja capaz de tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="426e5-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="426e5-120">Para obter mais informações sobre os dispositivos VPN compatíveis e a configuração do dispositivo, consulte [About VPN Devices (Acerca dos Dispositivos VPN)](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="426e5-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="426e5-121">Verifique se tem um endereço IP IPv4 público com acesso exterior para o seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="426e5-122">Este endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="426e5-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="426e5-123">Se não estiver familiarizado com intervalos de endereços IP Olá localizados na configuração de rede no local, tem de toocoordinate com alguém que consiga fornecer esses detalhes.</span><span class="sxs-lookup"><span data-stu-id="426e5-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="426e5-124">Ao criar esta configuração, tem de especificar que o Azure irá encaminhar localização no local de tooyour dos prefixos de intervalo de endereços para IP Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="426e5-125">Nenhuma das sub-redes Olá da sua rede no local pode através de lap com sub-redes da rede virtual Olá que pretende que sejam tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="426e5-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="426e5-126">Instale a versão mais recente do Olá do Olá cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="426e5-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="426e5-127">Cmdlets do PowerShell são frequentemente atualizados e, normalmente, terá de tooupdate a PowerShell cmdlets tooget Olá mais recente funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="426e5-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="426e5-128">Se não atualizar os seus cmdlets do PowerShell, os valores de Olá especificados poderão falhar.</span><span class="sxs-lookup"><span data-stu-id="426e5-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="426e5-129">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como transferir e instalar os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="426e5-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="426e5-130"><a name="example"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="426e5-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="426e5-131">Exemplos de Olá neste artigo utilizam Olá os seguintes valores.</span><span class="sxs-lookup"><span data-stu-id="426e5-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="426e5-132">Pode utilizar estes toocreate de valores num ambiente de teste, ou consulte toothem toobetter compreender exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="426e5-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="426e5-133"><a name="Login"></a>1. Ligar tooyour subscrição</span><span class="sxs-lookup"><span data-stu-id="426e5-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="426e5-134"><a name="VNet"></a>2. Criar uma rede virtual e uma sub-rede de gateway</span><span class="sxs-lookup"><span data-stu-id="426e5-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="426e5-135">Se ainda não tiver uma rede virtual, crie uma.</span><span class="sxs-lookup"><span data-stu-id="426e5-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="426e5-136">Ao criar uma rede virtual, certifique-se de que os espaços de endereços Olá que especificou não se sobrepõem a qualquer um dos espaços de endereços de Olá que tem na sua rede no local.</span><span class="sxs-lookup"><span data-stu-id="426e5-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="426e5-137"><a name="vnet"></a>toocreate uma rede virtual e uma sub-rede de gateway</span><span class="sxs-lookup"><span data-stu-id="426e5-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="426e5-138">Este exemplo cria uma rede virtual e uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="426e5-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="426e5-139">Se já tiver uma rede virtual que necessitam de tooadd uma sub-rede de gateway para ver [tooadd uma gateway sub-rede tooa rede virtual que já criou](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="426e5-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="426e5-140">Criar um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="426e5-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="426e5-141">Criar a sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="426e5-141">Create your virtual network.</span></span>

1. <span data-ttu-id="426e5-142">Definir variáveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="426e5-143">Crie Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="426e5-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="426e5-144"><a name="gatewaysubnet"></a>tooadd uma rede virtual do gateway sub-rede tooa que já criou</span><span class="sxs-lookup"><span data-stu-id="426e5-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="426e5-145">Definir variáveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="426e5-146">Crie a sub-rede do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="426e5-147">Definir a configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="426e5-148">3. <a name="localnet"></a>Criar gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="426e5-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="426e5-149">gateway de rede local Olá refere-se normalmente localização do tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="426e5-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="426e5-150">Dê site Olá um nome pelo qual Azure pode consulte tooit, em seguida, especifique o endereço IP Olá de toowhich de dispositivo VPN do Olá no local, irá criar uma ligação.</span><span class="sxs-lookup"><span data-stu-id="426e5-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="426e5-151">Também especificar prefixos de endereços IP Olá serão encaminhados através de um dispositivo VPN do Olá VPN gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="426e5-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="426e5-152">especificar prefixos de endereços de Olá são prefixos Olá localizados na sua rede no local.</span><span class="sxs-lookup"><span data-stu-id="426e5-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="426e5-153">Se alterar a sua rede no local, pode facilmente atualizar prefixos Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="426e5-154">Utilize Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="426e5-154">Use hello following values:</span></span>

* <span data-ttu-id="426e5-155">Olá *GatewayIPAddress* é Olá endereço IP do seu dispositivo VPN no local.</span><span class="sxs-lookup"><span data-stu-id="426e5-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="426e5-156">O dispositivo VPN não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="426e5-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="426e5-157">Olá *AddressPrefix* está no local espaço de endereços.</span><span class="sxs-lookup"><span data-stu-id="426e5-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="426e5-158">tooadd um gateway de rede local com um prefixo de endereço único:</span><span class="sxs-lookup"><span data-stu-id="426e5-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="426e5-159">tooadd um gateway de rede local com vários prefixos de endereço:</span><span class="sxs-lookup"><span data-stu-id="426e5-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="426e5-160">toomodify os prefixos de endereço IP para o gateway de rede local:</span><span class="sxs-lookup"><span data-stu-id="426e5-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="426e5-161">Às vezes, os prefixos de gateway da sua rede local mudam.</span><span class="sxs-lookup"><span data-stu-id="426e5-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="426e5-162">passos de Olá tomar toomodify seu endereço IP prefixos dependem se tiver criado uma ligação de gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="426e5-163">Consulte Olá [prefixos de endereços IP modificar para um gateway de rede local](#modify) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="426e5-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="426e5-164"><a name="PublicIP"></a>4. Solicitar um endereço IP Público</span><span class="sxs-lookup"><span data-stu-id="426e5-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="426e5-165">Um gateway de VPN deve ter um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="426e5-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="426e5-166">Primeiro pedido de recurso de endereço IP de Olá e, em seguida, consulte tooit ao criar o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="426e5-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="426e5-167">Olá está atribuído endereço IP dinamicamente recursos toohello quando Olá gateway de VPN criado.</span><span class="sxs-lookup"><span data-stu-id="426e5-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="426e5-168">O Gateway de VPN, atualmente, apenas suporta a alocação de endereços IP públicos *dinâmicos*.</span><span class="sxs-lookup"><span data-stu-id="426e5-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="426e5-169">Não é possível pedir uma atribuição de endereço IP Público Estático.</span><span class="sxs-lookup"><span data-stu-id="426e5-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="426e5-170">No entanto, isto não significa que o endereço IP Olá alterado depois de lhe ser atribuído tooyour gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="426e5-171">tempo apenas Olá alterações do endereço de IP público de Olá quando é Olá gateway é eliminado e recriado.</span><span class="sxs-lookup"><span data-stu-id="426e5-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="426e5-172">Não é alterado ao redimensionar, repor ou ao realizar qualquer outra manutenção/atualização interna do gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="426e5-173">Solicitar um endereço de IP público que será atribuído tooyour de rede virtual gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="426e5-174"><a name="GatewayIPConfig"></a>5. Criar a configuração de endereçamento de IP do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="426e5-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="426e5-175">configuração do gateway de Olá define uma sub-rede de Olá e Olá toouse de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="426e5-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="426e5-176">Utilize a configuração do gateway de Olá toocreate de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="426e5-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="426e5-177"><a name="CreateGateway"></a>6. Criar gateway de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="426e5-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="426e5-178">Crie gateway de VPN de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="426e5-179">Criar um gateway VPN pode demorar até too45 minutos ou mais toocomplete.</span><span class="sxs-lookup"><span data-stu-id="426e5-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="426e5-180">Utilize Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="426e5-180">Use hello following values:</span></span>

* <span data-ttu-id="426e5-181">Olá *- GatewayType* para uma Site a Site é configuração *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="426e5-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="426e5-182">tipo de gateway Olá é sempre configuração toohello específico que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="426e5-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="426e5-183">Por exemplo, outras configurações de gateway poderão exigir o ExpressRoute -GatewayType.</span><span class="sxs-lookup"><span data-stu-id="426e5-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="426e5-184">Olá *- VpnType* pode ser *RouteBased* (referido tooas um Gateway dinâmico em alguma documentação), ou *PolicyBased* (referido tooas Gateway estático em alguma documentação ).</span><span class="sxs-lookup"><span data-stu-id="426e5-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="426e5-185">Para obter mais informações sobre os tipos de gateways de VPN, veja [Acerca dos Gateways de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="426e5-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="426e5-186">Selecione Olá SKU de Gateway que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="426e5-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="426e5-187">Existem limitações de configuração para determinados SKUs.</span><span class="sxs-lookup"><span data-stu-id="426e5-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="426e5-188">Para obter mais informações, veja [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="426e5-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="426e5-189">Se obtiver um erro ao criar o gateway de VPN Olá sobre Olá - GatewaySku, certifique-se de que instalou a versão mais recente do Olá Olá de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="426e5-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="426e5-190"><a name="ConfigureVPNDevice"></a>7. Configurar o dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="426e5-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="426e5-191">Rede do ligações site a Site tooan no local requer um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="426e5-192">Neste passo, configure o seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="426e5-193">Quando configurar o seu dispositivo VPN, terá de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="426e5-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="426e5-194">Uma chave partilhada.</span><span class="sxs-lookup"><span data-stu-id="426e5-194">A shared key.</span></span> <span data-ttu-id="426e5-195">Isto é Olá mesmo partilhado chave que especificar ao criar a ligação de VPN de Site para Site.</span><span class="sxs-lookup"><span data-stu-id="426e5-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="426e5-196">Nos nossos exemplos, iremos utilizar uma chave partilhada básica.</span><span class="sxs-lookup"><span data-stu-id="426e5-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="426e5-197">Recomendamos que geram um toouse chave mais complexa.</span><span class="sxs-lookup"><span data-stu-id="426e5-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="426e5-198">Olá endereço IP público do gateway da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="426e5-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="426e5-199">Pode ver o endereço IP público Olá utilizando Olá portal do Azure, PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="426e5-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="426e5-200">Olá toofind endereço IP público do seu gateway de rede virtual com o PowerShell, o seguinte exemplo de Olá de utilização:</span><span class="sxs-lookup"><span data-stu-id="426e5-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="426e5-201"><a name="CreateConnection"></a>8. Criar a ligação de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="426e5-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="426e5-202">Em seguida, crie a ligação de VPN de Site para Site Olá entre o gateway de rede virtual e o seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="426e5-203">Ser se valores de Olá tooreplace com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="426e5-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="426e5-204">chave partilhada Olá tem de corresponder ao valor de Olá utilizado para a configuração do dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="426e5-205">Tenha em atenção que Olá '-ConnectionType' para o Site a Site é *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="426e5-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="426e5-206">Definir variáveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="426e5-207">Crie ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="426e5-208">Após um curto período ao hello será estabelecida ligação.</span><span class="sxs-lookup"><span data-stu-id="426e5-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="426e5-209"><a name="toverify"></a>9. Certifique-se a ligação de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="426e5-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="426e5-210">Existem algumas formas diferentes tooverify a ligação VPN.</span><span class="sxs-lookup"><span data-stu-id="426e5-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="426e5-211"><a name="connectVM"></a>tooconnect tooa máquina</span><span class="sxs-lookup"><span data-stu-id="426e5-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="426e5-212"><a name="modify"></a>Modificar os prefixos de endereços IP de um gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="426e5-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="426e5-213">Se alterar prefixos de endereços IP Olá que pretende que sejam encaminhados localização do tooyour no local, pode modificar o gateway de rede local Olá.</span><span class="sxs-lookup"><span data-stu-id="426e5-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="426e5-214">São fornecidos dois conjuntos de instruções.</span><span class="sxs-lookup"><span data-stu-id="426e5-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="426e5-215">instruções de Olá que escolher dependem se já tiver criado a ligação de gateway.</span><span class="sxs-lookup"><span data-stu-id="426e5-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="426e5-216"><a name="modifygwipaddress"></a>Modificar o endereço IP do gateway Olá para um gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="426e5-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="426e5-217">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="426e5-217">Next steps</span></span>

*  <span data-ttu-id="426e5-218">Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="426e5-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="426e5-219">Para obter mais informações, veja [Máquinas Virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="426e5-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="426e5-220">Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="426e5-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
