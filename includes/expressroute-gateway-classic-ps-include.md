<span data-ttu-id="eaf1d-101">Tem de criar uma VNet e uma sub-rede de gateway em primeiro lugar, antes de trabalhar Olá seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="eaf1d-102">Consulte o artigo Olá [configurar uma rede Virtual com o portal clássico Olá](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="eaf1d-103">Adicionar um gateway</span><span class="sxs-lookup"><span data-stu-id="eaf1d-103">Add a gateway</span></span>
<span data-ttu-id="eaf1d-104">Utilize o comando de Olá abaixo toocreate um gateway.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="eaf1d-105">Ser toosubstitute se os valores pelos seus.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="eaf1d-106">Certifique-se de que foi criado o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="eaf1d-106">Verify hello gateway was created</span></span>
<span data-ttu-id="eaf1d-107">Utilize o comando de Olá abaixo tooverify Olá gateway foi criado.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="eaf1d-108">Este comando também obtém o ID de gateway Olá, o que precisa para outras operações.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="eaf1d-109">Redimensionar um gateway</span><span class="sxs-lookup"><span data-stu-id="eaf1d-109">Resize a gateway</span></span>
<span data-ttu-id="eaf1d-110">Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="eaf1d-111">Pode utilizar Olá seguir Olá toochange do comando SKU de Gateway em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eaf1d-112">Este comando não funciona para UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="eaf1d-113">toochange o gateway de UltraPerformance tooan do gateway, primeiro remova Olá existente ExpressRoute gateway e, em seguida, criar um novo gateway de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="eaf1d-114">toodowngrade o gateway de um gateway de UltraPerformance, remova primeiro Olá UltraPerformance gateway e, em seguida, crie um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="eaf1d-115">Remover um gateway</span><span class="sxs-lookup"><span data-stu-id="eaf1d-115">Remove a gateway</span></span>
<span data-ttu-id="eaf1d-116">Utilize o comando de Olá abaixo tooremove um gateway</span><span class="sxs-lookup"><span data-stu-id="eaf1d-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>