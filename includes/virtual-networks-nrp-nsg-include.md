## <a name="network-security-group"></a><span data-ttu-id="21848-101">Grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="21848-101">Network Security Group</span></span>
<span data-ttu-id="21848-102">Um recurso NSG permite a criação de Olá de limite de segurança para cargas de trabalho, através da implementação de permissão e negação regras.</span><span class="sxs-lookup"><span data-stu-id="21848-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="21848-103">Estas regras podem ser aplicadas tooa VM, um NIC ou uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="21848-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="21848-104">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21848-104">Property</span></span> | <span data-ttu-id="21848-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="21848-105">Description</span></span> | <span data-ttu-id="21848-106">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="21848-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21848-107">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="21848-107">**subnets**</span></span> |<span data-ttu-id="21848-108">Lista de ids de sub-rede Olá NSG é aplicada a.</span><span class="sxs-lookup"><span data-stu-id="21848-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="21848-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/Providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="21848-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="21848-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="21848-110">**securityRules**</span></span> |<span data-ttu-id="21848-111">Lista de regras de segurança que compõem Olá NSG</span><span class="sxs-lookup"><span data-stu-id="21848-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="21848-112">Consulte [regra de segurança](#Security-rule) abaixo</span><span class="sxs-lookup"><span data-stu-id="21848-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="21848-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="21848-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="21848-114">Lista de regras de segurança predefinidas presentes em cada NSG</span><span class="sxs-lookup"><span data-stu-id="21848-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="21848-115">Consulte [predefinido regras de segurança](#Default-security-rules) abaixo</span><span class="sxs-lookup"><span data-stu-id="21848-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="21848-116">**Regra de segurança** -um NSG pode ter várias regras de segurança definidas.</span><span class="sxs-lookup"><span data-stu-id="21848-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="21848-117">Cada regra pode permitir ou negar os diferentes tipos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="21848-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="21848-118">Regra de segurança</span><span class="sxs-lookup"><span data-stu-id="21848-118">Security rule</span></span>
<span data-ttu-id="21848-119">Uma regra de segurança é um recurso de subordinados de um NSG que contém as propriedades de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="21848-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="21848-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21848-120">Property</span></span> | <span data-ttu-id="21848-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="21848-121">Description</span></span> | <span data-ttu-id="21848-122">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="21848-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21848-123">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="21848-123">**description**</span></span> |<span data-ttu-id="21848-124">Descrição da regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-124">Description for hello rule</span></span> |<span data-ttu-id="21848-125">Permitir o tráfego de entrada para todas as VMs numa sub-rede X</span><span class="sxs-lookup"><span data-stu-id="21848-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="21848-126">**protocolo**</span><span class="sxs-lookup"><span data-stu-id="21848-126">**protocol**</span></span> |<span data-ttu-id="21848-127">Protocolo toomatch para a regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="21848-128">TCP, UDP ou *</span><span class="sxs-lookup"><span data-stu-id="21848-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="21848-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="21848-129">**sourcePortRange**</span></span> |<span data-ttu-id="21848-130">Toomatch de intervalo de portas de origem para a regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="21848-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="21848-131">80, 100-200, *</span></span> |
| <span data-ttu-id="21848-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="21848-132">**destinationPortRange**</span></span> |<span data-ttu-id="21848-133">Toomatch de intervalo de portas de destino para a regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="21848-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="21848-134">80, 100-200, *</span></span> |
| <span data-ttu-id="21848-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="21848-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="21848-136">Toomatch de prefixo de endereço de origem para a regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="21848-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="21848-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="21848-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="21848-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="21848-139">Toomatch de prefixo de endereço de destino para a regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="21848-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="21848-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="21848-141">**direção**</span><span class="sxs-lookup"><span data-stu-id="21848-141">**direction**</span></span> |<span data-ttu-id="21848-142">Direção do tráfego toomatch para a regra de Olá</span><span class="sxs-lookup"><span data-stu-id="21848-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="21848-143">De entrada ou de saída</span><span class="sxs-lookup"><span data-stu-id="21848-143">inbound or outbound</span></span> |
| <span data-ttu-id="21848-144">**prioridade**</span><span class="sxs-lookup"><span data-stu-id="21848-144">**priority**</span></span> |<span data-ttu-id="21848-145">Prioridade da regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="21848-145">Priority for hello rule.</span></span> <span data-ttu-id="21848-146">As regras são verificados por ordem de prioridade, depois de uma regra se aplica, são testadas não mais regras para correspondência.</span><span class="sxs-lookup"><span data-stu-id="21848-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="21848-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="21848-147">10, 100, 65000</span></span> |
| <span data-ttu-id="21848-148">**acesso**</span><span class="sxs-lookup"><span data-stu-id="21848-148">**access**</span></span> |<span data-ttu-id="21848-149">Tipo de acesso tooapply se Olá regra corresponder</span><span class="sxs-lookup"><span data-stu-id="21848-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="21848-150">Permitir ou negar</span><span class="sxs-lookup"><span data-stu-id="21848-150">allow or deny</span></span> |

<span data-ttu-id="21848-151">Exemplo NSG no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="21848-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="21848-152">Regras de segurança predefinidas</span><span class="sxs-lookup"><span data-stu-id="21848-152">Default security rules</span></span>

<span data-ttu-id="21848-153">Regras de segurança predefinidas têm Olá mesmas propriedades disponíveis nas regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="21848-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="21848-154">Elas existem tooprovide conectividade básica entre os recursos que tenham toothem NSGs aplicados.</span><span class="sxs-lookup"><span data-stu-id="21848-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="21848-155">Certifique-se de que sabe que [predefinido regras de segurança](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existe.</span><span class="sxs-lookup"><span data-stu-id="21848-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="21848-156">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="21848-156">Additional resources</span></span>
* <span data-ttu-id="21848-157">Obter mais informações [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="21848-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="21848-158">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163615.aspx) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="21848-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="21848-159">Olá leitura [documentação de referência da REST API](https://msdn.microsoft.com/library/azure/mt163580.aspx) para regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="21848-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
