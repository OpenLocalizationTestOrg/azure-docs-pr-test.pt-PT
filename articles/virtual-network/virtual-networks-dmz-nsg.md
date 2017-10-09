---
title: "aaaAzure DMZ exemplo – criar uma rede de Perímetro simples com NSGs | Microsoft Docs"
description: "Criar uma rede de Perímetro com grupos de segurança de rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="c2a92-103">Exemplo 1 – criar uma rede de Perímetro simple utilizando NSGs com um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c2a92-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="c2a92-104">[Devolver toohello segurança limites melhores práticas de página][HOME]</span><span class="sxs-lookup"><span data-stu-id="c2a92-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2a92-105">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c2a92-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="c2a92-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2a92-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="c2a92-107">Este exemplo cria uma rede de Perímetro primitivo com quatro servidores do Windows e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="c2a92-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="c2a92-108">Este exemplo descreve cada um dos Olá modelo relevantes secções tooprovide uma compreensão mais aprofundada de cada passo.</span><span class="sxs-lookup"><span data-stu-id="c2a92-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="c2a92-109">Há também um tooprovide da secção de cenário de tráfego uma visão passo a passo detalhada das como procede de tráfego através de camadas de Olá de defesa nas Olá DMZ.</span><span class="sxs-lookup"><span data-stu-id="c2a92-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="c2a92-110">Por fim, na secção de referências de Olá é toobuild de código e as instruções do modelo completo de Olá este ambiente tootest e experiência com vários cenários.</span><span class="sxs-lookup"><span data-stu-id="c2a92-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="c2a92-111">![Rede de Perímetro entrada com o NSG][1]</span><span class="sxs-lookup"><span data-stu-id="c2a92-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="c2a92-112">Descrição de ambiente</span><span class="sxs-lookup"><span data-stu-id="c2a92-112">Environment description</span></span>
<span data-ttu-id="c2a92-113">Neste exemplo, uma subscrição contém Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c2a92-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="c2a92-114">Um grupo de recursos única</span><span class="sxs-lookup"><span data-stu-id="c2a92-114">A single resource group</span></span>
* <span data-ttu-id="c2a92-115">Uma rede Virtual com duas sub-redes; "FrontEnd" e "BackEnd"</span><span class="sxs-lookup"><span data-stu-id="c2a92-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="c2a92-116">Um grupo de segurança de rede que é aplicado tooboth sub-redes</span><span class="sxs-lookup"><span data-stu-id="c2a92-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="c2a92-117">Um servidor do Windows que representa um servidor de web de aplicação ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="c2a92-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="c2a92-118">Servidores de dois windows que representam servidores de back-end de aplicação ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="c2a92-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="c2a92-119">Um servidor do Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="c2a92-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="c2a92-120">Um endereço IP público associado ao servidor de web de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="c2a92-121">Na secção de referências de Olá, há um modelo Azure Resource Manager tooan de ligação que cria o ambiente de Olá descrito neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c2a92-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="c2a92-122">Edifício Olá VMs e as redes virtuais, embora efetuada pelo modelo de exemplo de Olá, não são descritas em detalhe neste documento.</span><span class="sxs-lookup"><span data-stu-id="c2a92-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="c2a92-123">**toobuild neste ambiente** (instruções detalhadas são Olá referências secção deste documento);</span><span class="sxs-lookup"><span data-stu-id="c2a92-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="c2a92-124">Implementar Olá modelo de Gestor de recursos do Azure em: [modelos de início rápido do Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="c2a92-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="c2a92-125">Instalar a aplicação de exemplo de Olá em: [Script de aplicação de exemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="c2a92-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="c2a92-126">servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir".</span><span class="sxs-lookup"><span data-stu-id="c2a92-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c2a92-127">Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="c2a92-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="c2a92-128">Em alternativa um IP público pode ser associado a cada servidor NIC para RDP mais fácil.</span><span class="sxs-lookup"><span data-stu-id="c2a92-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="c2a92-129">Olá secções seguintes fornecem uma descrição detalhada do Olá grupo de segurança de rede e como funciona para este exemplo orientando através de chaves linhas de Olá modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c2a92-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="c2a92-130">Grupos de Segurança de Rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="c2a92-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="c2a92-131">Para este exemplo, um grupo NSG está criado e, em seguida, carregar com regras de seis.</span><span class="sxs-lookup"><span data-stu-id="c2a92-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="c2a92-132">Um modo geral, deve primeiro criar as regras de "Permitir" específicas e, em seguida, hello mais genéricas "Deny" regras pela última vez.</span><span class="sxs-lookup"><span data-stu-id="c2a92-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="c2a92-133">Olá prioridade atribuída determinam as regras são avaliadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="c2a92-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="c2a92-134">Assim que o tráfego for encontrado regras específicas de tooa tooapply, não existem regras adicionais são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="c2a92-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="c2a92-135">Podem aplicar regras do NSG no Olá direção de entrada ou de saída (perspetiva Olá da sub-rede Olá).</span><span class="sxs-lookup"><span data-stu-id="c2a92-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="c2a92-136">Forma declarativa, Olá seguintes regras está a ser criado para o tráfego de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="c2a92-137">O tráfego DNS interno (porta 53) é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="c2a92-138">O tráfego RDP (porta 3389) do Olá Internet tooany VM é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="c2a92-139">Tráfego HTTP (porta 80) do servidor de tooweb Olá Internet (IIS01) é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="c2a92-140">Qualquer tráfego (todas as portas) de IIS01 tooAppVM1 é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="c2a92-141">Qualquer tráfego (todas as portas) de Olá Internet toohello VNet completo (ambas as sub-redes) é negado</span><span class="sxs-lookup"><span data-stu-id="c2a92-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="c2a92-142">Qualquer tráfego (todas as portas) da sub-rede de back-end do Olá front-end sub-rede toohello é negado</span><span class="sxs-lookup"><span data-stu-id="c2a92-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="c2a92-143">Com a sub-rede de tooeach vinculada estas regras, se um pedido de HTTP foi recebido do servidor web do Olá Internet toohello, ambas as regras 3 (permitir) e 5 (negar) seria aplicada, mas uma vez que a regra 3 tem uma prioridade mais alta apenas seria aplicada e regra 5 não seria entrem em play.</span><span class="sxs-lookup"><span data-stu-id="c2a92-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="c2a92-144">Deste modo, pedidos de HTTP Olá seriam permitido toohello servidor de web.</span><span class="sxs-lookup"><span data-stu-id="c2a92-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="c2a92-145">Se esse mesmo tráfego estava a tentar servidor de DNS01 tooreach Olá, regra 5 (negar) seria Olá primeiro tooapply e Olá o tráfego seria não ser permitido toopass toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="c2a92-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="c2a92-146">Regra 6 (negar) blocos de sub-rede de front-end de Olá de falar com a sub-rede de back-end toohello (exceto para o tráfego permitido nas regras de 1 e 4), este conjunto de regras protege a rede de back-end Olá no caso de uma atacante compromissos Olá aplicação web no Olá front-end, atacante Olá seria limitada toohello acesso back-end "protegido" rede (apenas tooresources exposto no servidor de AppVM01 Olá).</span><span class="sxs-lookup"><span data-stu-id="c2a92-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="c2a92-147">Há uma regra de saída predefinida que lhe permite tráfego de saída toohello internet.</span><span class="sxs-lookup"><span data-stu-id="c2a92-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="c2a92-148">Neste exemplo, vamos está a permitir o tráfego de saída e não modificar quaisquer regras de saída.</span><span class="sxs-lookup"><span data-stu-id="c2a92-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="c2a92-149">tooapply tootraffic de política de segurança em ambas as direções, o utilizador definidas encaminhamento é necessário e é explorou "Exemplo 3" no Olá [segurança limites melhores práticas página][HOME].</span><span class="sxs-lookup"><span data-stu-id="c2a92-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="c2a92-150">Cada regra é abordada mais detalhadamente:</span><span class="sxs-lookup"><span data-stu-id="c2a92-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="c2a92-151">Um recurso do grupo de segurança de rede tem de ser toohold instanciadas Olá regras:</span><span class="sxs-lookup"><span data-stu-id="c2a92-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="c2a92-152">primeira regra de Olá neste exemplo permite o tráfego DNS entre todas as redes internas toohello DNS o servidor na sub-rede de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="c2a92-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="c2a92-153">regra de Olá tem alguns parâmetros importantes:</span><span class="sxs-lookup"><span data-stu-id="c2a92-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="c2a92-154">"destinationAddressPrefix" - regras podem utilizar um tipo especial de prefixo de endereço denominado um "etiqueta predefinida", estas etiquetas são identificadores fornecidos pelo sistema que permitem uma forma fácil tooaddress uma categoria superior dos prefixos de endereço.</span><span class="sxs-lookup"><span data-stu-id="c2a92-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="c2a92-155">Esta regra utiliza Olá etiqueta predefinida "Internet" toosignify qualquer endereço fora Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="c2a92-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="c2a92-156">Outras etiquetas de prefixo são VirtualNetwork e AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="c2a92-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="c2a92-157">"Direção" significa na direção do fluxo de tráfego esta regra entra em vigor.</span><span class="sxs-lookup"><span data-stu-id="c2a92-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="c2a92-158">direção de Olá é a partir da perspetiva de Olá de Olá sub-redes ou máquinas virtuais (dependendo de onde está vinculado esta NSG).</span><span class="sxs-lookup"><span data-stu-id="c2a92-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="c2a92-159">Deste modo, se direção "Entrada" e o tráfego está a entrar sub-rede Olá, seria aplicada a regra de Olá e tráfego que sai Olá sub-rede não seria afetado por esta regra.</span><span class="sxs-lookup"><span data-stu-id="c2a92-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="c2a92-160">"Prioridade" define a ordem de Olá avaliação de um fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="c2a92-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="c2a92-161">Olá Olá número Olá superior Olá prioridade inferior.</span><span class="sxs-lookup"><span data-stu-id="c2a92-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="c2a92-162">Quando uma regra aplica-se o fluxo de tráfego específico tooa, não existem regras adicionais são processadas.</span><span class="sxs-lookup"><span data-stu-id="c2a92-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="c2a92-163">Deste modo, se uma regra com prioridade 1 permite que o tráfego e uma regra com prioridade 2 nega tráfego e ambas as regras aplicam-se tootraffic, em seguida, o tráfego de Olá seria permitido tooflow (uma vez que a regra 1 tinha uma prioridade mais alta demorou em vigor e não existem regras adicionais foram aplicadas).</span><span class="sxs-lookup"><span data-stu-id="c2a92-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="c2a92-164">"Acesso" significa tráfego afetado por esta regra estiver bloqueado ("Deny") ou permitido ("Permitir").</span><span class="sxs-lookup"><span data-stu-id="c2a92-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="c2a92-165">Esta regra permite tooflow de tráfego RDP de porta RDP do Olá internet toohello em qualquer servidor na Olá vinculado sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c2a92-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="c2a92-166">Esta regra permite entrada internet tráfego toohit Olá servidor web.</span><span class="sxs-lookup"><span data-stu-id="c2a92-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="c2a92-167">Esta regra não altera o comportamento de encaminhamento Olá.</span><span class="sxs-lookup"><span data-stu-id="c2a92-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="c2a92-168">regra de Olá permite apenas tráfego destinado IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="c2a92-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="c2a92-169">Deste modo, se o tráfego de Internet de Olá tinha o servidor de web de Olá como respectivo destino desta regra seria permitir que e param de processar mais regras.</span><span class="sxs-lookup"><span data-stu-id="c2a92-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="c2a92-170">(Regra de Olá com a prioridade é bloqueado 140 todos os outro internet tráfego de entrada).</span><span class="sxs-lookup"><span data-stu-id="c2a92-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="c2a92-171">Se apenas estiver a processar tráfego HTTP, esta regra pode ser mais restrito tooonly Permitir destino porta 80.</span><span class="sxs-lookup"><span data-stu-id="c2a92-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="c2a92-172">Esta regra permite tráfego toopass do servidor de IIS01 Olá toohello AppVM01 servidor, uma regra posterior bloqueia todo o restante front-end tooBackend tráfego.</span><span class="sxs-lookup"><span data-stu-id="c2a92-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="c2a92-173">tooimprove esta regra, se a porta de Olá é conhecida que deve ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="c2a92-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="c2a92-174">Por exemplo, se o servidor IIS Olá é atingir apenas SQL Server em AppVM01, Olá intervalo de portas de destino deve ser alterado de "*" (Any) too1433 (Olá porta do SQL Server), permitindo assim que uma superfície de ataque de entrada inferior em AppVM01 aplicação web de Olá alguma vez comprometida.</span><span class="sxs-lookup"><span data-stu-id="c2a92-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="c2a92-175">Esta regra negar o tráfego de servidores de tooany Olá internet numa rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="c2a92-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="c2a92-176">Com regras de Olá em prioridade 110 e 120, o efeito de Olá é tooallow apenas internet tráfego toohello firewall de entrada e de portas RDP nos servidores e bloqueia tudo o resto.</span><span class="sxs-lookup"><span data-stu-id="c2a92-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="c2a92-177">Esta regra é um "isento" regra tooblock todos os fluxos inesperados.</span><span class="sxs-lookup"><span data-stu-id="c2a92-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="c2a92-178">regra final Olá nega o tráfego de sub-rede de back-end do Olá front-end sub-rede toohello.</span><span class="sxs-lookup"><span data-stu-id="c2a92-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="c2a92-179">Uma vez que esta regra é uma regra de só de entrada, o tráfego inverso é permitido (a partir de Olá back-end toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="c2a92-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="c2a92-180">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="c2a92-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="c2a92-181">(*Permitidos*) servidor da Internet tooweb</span><span class="sxs-lookup"><span data-stu-id="c2a92-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="c2a92-182">Um utilizador de internet solicita uma página HTTP de endereço IP público de Olá do Olá que NIC associada Olá IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="c2a92-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="c2a92-183">Olá endereço IP público transmite tráfego toohello VNet para IIS01 (servidor de web de Olá)</span><span class="sxs-lookup"><span data-stu-id="c2a92-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="c2a92-184">Sub-rede de front-end inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-185">Não aplicar regras de NSG 1 (DNS), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c2a92-186">Regras de NSG 2 (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c2a92-187">Aplicar regras de NSG 3 (Internet tooIIS01), o tráfego é o processamento da regra permitido, parar</span><span class="sxs-lookup"><span data-stu-id="c2a92-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c2a92-188">O tráfego chega a um endereço IP do servidor de web de Olá IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="c2a92-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="c2a92-189">IIS01 está à escuta para o tráfego web, este pedido de recebe e inicia o processamento de pedido de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="c2a92-190">IIS01 pede-lhe Olá do SQL Server no AppVM01 informações</span><span class="sxs-lookup"><span data-stu-id="c2a92-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="c2a92-191">Não existem regras de saída na sub-rede do front-end, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="c2a92-192">sub-rede de back-end de Olá inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-193">Não aplicar regras de NSG 1 (DNS), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c2a92-194">Regras de NSG 2 (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c2a92-195">NSG regra 3 (Internet tooFirewall) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="c2a92-196">Aplicar regras de NSG 4 (IIS01 tooAppVM01), o tráfego é o processamento da regra permitido, parar</span><span class="sxs-lookup"><span data-stu-id="c2a92-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="c2a92-197">AppVM01 recebe Olá consulta SQL e responde</span><span class="sxs-lookup"><span data-stu-id="c2a92-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="c2a92-198">Uma vez que não existem quaisquer regras de saída na sub-rede de back-end Olá, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="c2a92-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="c2a92-199">Sub-rede de front-end inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-200">Não há nenhuma regra NSG aplica-se tooInbound tráfego de Olá back-end sub-rede toohello front-end sub-rede, pelo que nenhuma das regras do NSG Olá são aplicáveis</span><span class="sxs-lookup"><span data-stu-id="c2a92-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="c2a92-201">regra do sistema predefinido de Olá a permitir o tráfego entre sub-redes permitiria que este tráfego para que o tráfego de Olá é permitido.</span><span class="sxs-lookup"><span data-stu-id="c2a92-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="c2a92-202">servidor IIS Olá recebe a resposta SQL Olá conclui a resposta HTTP Olá e envia toohello autor do pedido</span><span class="sxs-lookup"><span data-stu-id="c2a92-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="c2a92-203">Uma vez que não existem quaisquer regras de saída na sub-rede do front-end de Olá, resposta Olá é permitida e Olá utilizador Internet recebe Olá web página pedida.</span><span class="sxs-lookup"><span data-stu-id="c2a92-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="c2a92-204">(*Permitidos*) servidor de tooIIS RDP</span><span class="sxs-lookup"><span data-stu-id="c2a92-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="c2a92-205">Um administrador do servidor na internet solicita um tooIIS01 de sessão do RDP no endereço IP público de Olá do Olá que NIC associada Olá NIC IIS01 (este endereço IP público pode ser encontrado através de Olá Portal ou o PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c2a92-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="c2a92-206">Olá endereço IP público transmite tráfego toohello VNet para IIS01 (servidor de web de Olá)</span><span class="sxs-lookup"><span data-stu-id="c2a92-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="c2a92-207">Sub-rede de front-end inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-208">Não aplicar regras de NSG 1 (DNS), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c2a92-209">Aplicar regras de NSG 2 (RDP), o tráfego é o processamento da regra permitido, parar</span><span class="sxs-lookup"><span data-stu-id="c2a92-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c2a92-210">Não existem regras de saída, aplicam regras predefinidas e retorno tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="c2a92-211">Sessão do RDP está ativado</span><span class="sxs-lookup"><span data-stu-id="c2a92-211">RDP session is enabled</span></span>
6. <span data-ttu-id="c2a92-212">Pedidos de IIS01 Olá nome de utilizador e palavra-passe</span><span class="sxs-lookup"><span data-stu-id="c2a92-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="c2a92-213">servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir".</span><span class="sxs-lookup"><span data-stu-id="c2a92-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c2a92-214">Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="c2a92-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="c2a92-215">(*Permitidos*) pesquisar DNS de servidor Web num servidor DNS</span><span class="sxs-lookup"><span data-stu-id="c2a92-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="c2a92-216">Web necessidades de servidor, IIS01, dados de um feed em www.data.gov, mas tem de tooresolve Olá endereço.</span><span class="sxs-lookup"><span data-stu-id="c2a92-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="c2a92-217">Olá configuração de rede para as listas de VNet Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como servidor DNS primário do Olá, IIS01 envia Olá DNS pedido tooDNS01</span><span class="sxs-lookup"><span data-stu-id="c2a92-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="c2a92-218">Não existem regras de saída na sub-rede do front-end, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="c2a92-219">Sub-rede de back-end inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="c2a92-220">Aplicar regras de NSG 1 (DNS), o tráfego é o processamento da regra permitido, parar</span><span class="sxs-lookup"><span data-stu-id="c2a92-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="c2a92-221">Servidor DNS recebe o pedido de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="c2a92-222">Servidor DNS não tem endereços Olá em cache e pede-lhe um servidor DNS de raiz no Olá internet</span><span class="sxs-lookup"><span data-stu-id="c2a92-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="c2a92-223">Não existem regras de saída na sub-rede de back-end, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="c2a92-224">Servidor DNS de Internet responde, uma vez que esta sessão foi iniciada internamente, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="c2a92-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="c2a92-225">Servidor DNS coloca Olá resposta em cache e responde toohello pedido inicial back tooIIS01</span><span class="sxs-lookup"><span data-stu-id="c2a92-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="c2a92-226">Não existem regras de saída na sub-rede de back-end, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="c2a92-227">Sub-rede de front-end inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-228">Não há nenhuma regra NSG aplica-se tooInbound tráfego de Olá back-end sub-rede toohello front-end sub-rede, pelo que nenhuma das regras do NSG Olá são aplicáveis</span><span class="sxs-lookup"><span data-stu-id="c2a92-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="c2a92-229">regra do sistema predefinido de Olá a permitir o tráfego entre sub-redes permitiria que este tráfego para que o tráfego de Olá é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="c2a92-230">IIS01 recebe resposta Olá de DNS01</span><span class="sxs-lookup"><span data-stu-id="c2a92-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="c2a92-231">(*Permitidos*) ficheiro de acesso do servidor Web no AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2a92-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="c2a92-232">IIS01 pede-lhe um ficheiro num AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2a92-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="c2a92-233">Não existem regras de saída na sub-rede do front-end, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="c2a92-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="c2a92-234">sub-rede de back-end de Olá inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-235">Não aplicar regras de NSG 1 (DNS), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c2a92-236">Regras de NSG 2 (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c2a92-237">NSG regra 3 (Internet tooIIS01) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="c2a92-238">Aplicar regras de NSG 4 (IIS01 tooAppVM01), o tráfego é o processamento da regra permitido, parar</span><span class="sxs-lookup"><span data-stu-id="c2a92-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c2a92-239">AppVM01 recebe o pedido de Olá e responde com o ficheiro (partindo do princípio de acesso é autorizado)</span><span class="sxs-lookup"><span data-stu-id="c2a92-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="c2a92-240">Uma vez que não existem quaisquer regras de saída na sub-rede de back-end Olá, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="c2a92-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="c2a92-241">Sub-rede de front-end inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-242">Não há nenhuma regra NSG aplica-se tooInbound tráfego de Olá back-end sub-rede toohello front-end sub-rede, pelo que nenhuma das regras do NSG Olá são aplicáveis</span><span class="sxs-lookup"><span data-stu-id="c2a92-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="c2a92-243">regra do sistema predefinido de Olá a permitir o tráfego entre sub-redes permitiria que este tráfego para que o tráfego de Olá é permitido.</span><span class="sxs-lookup"><span data-stu-id="c2a92-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="c2a92-244">servidor IIS Olá recebe um ficheiro de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="c2a92-245">(*Negado*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="c2a92-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="c2a92-246">Um utilizador de internet tenta tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2a92-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="c2a92-247">Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c2a92-248">No entanto se foi ativado um endereço IP público por algum motivo, a regra NSG 2 (RDP) permitiria que este tráfego</span><span class="sxs-lookup"><span data-stu-id="c2a92-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="c2a92-249">servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir".</span><span class="sxs-lookup"><span data-stu-id="c2a92-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c2a92-250">Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="c2a92-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="c2a92-251">(*Negado*) servidor de toobackend Web</span><span class="sxs-lookup"><span data-stu-id="c2a92-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="c2a92-252">Um utilizador de internet tenta tooaccess um ficheiro num AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2a92-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="c2a92-253">Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c2a92-254">Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueariam este tráfego</span><span class="sxs-lookup"><span data-stu-id="c2a92-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="c2a92-255">(*Negado*) pesquisar Web DNS num servidor DNS</span><span class="sxs-lookup"><span data-stu-id="c2a92-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="c2a92-256">Um utilizador de internet tenta toolook se um registo DNS interno no DNS01</span><span class="sxs-lookup"><span data-stu-id="c2a92-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="c2a92-257">Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c2a92-258">Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueariam este tráfego (Nota: se regra 1 (DNS) não seriam aplicadas porque Olá pede o endereço de origem são Olá internet e a regra 1 aplica-se apenas toohello VNet local como origem Olá)</span><span class="sxs-lookup"><span data-stu-id="c2a92-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="c2a92-259">(*Negado*) acesso do SQL Server no servidor de web de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="c2a92-260">Um utilizador de internet solicita dados SQL IIS01</span><span class="sxs-lookup"><span data-stu-id="c2a92-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="c2a92-261">Uma vez que existem não existem endereços IP públicos associados a esta NIC de servidores, este tráfego nunca introduziria Olá VNet e não a alcançar o servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c2a92-262">Se um endereço IP público foi ativado por algum motivo, a sub-rede do front-end de Olá começa processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="c2a92-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c2a92-263">Não aplicar regras de NSG 1 (DNS), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c2a92-264">Regras de NSG 2 (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="c2a92-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c2a92-265">Aplicar regras de NSG 3 (Internet tooIIS01), o tráfego é o processamento da regra permitido, parar</span><span class="sxs-lookup"><span data-stu-id="c2a92-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c2a92-266">O tráfego chega a um endereço IP de Olá IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="c2a92-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="c2a92-267">IIS01 não está a escutar na porta 1433, por isso, não toohello um pedido de resposta</span><span class="sxs-lookup"><span data-stu-id="c2a92-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="c2a92-268">Conclusão</span><span class="sxs-lookup"><span data-stu-id="c2a92-268">Conclusion</span></span>
<span data-ttu-id="c2a92-269">Neste exemplo é uma forma avançar diretamente e relativamente simple de isolar a sub-rede de back-end Olá do tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="c2a92-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="c2a92-270">Obter mais exemplos e uma descrição geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].</span><span class="sxs-lookup"><span data-stu-id="c2a92-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="c2a92-271">Referências</span><span class="sxs-lookup"><span data-stu-id="c2a92-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="c2a92-272">Modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c2a92-272">Azure Resource Manager template</span></span>
<span data-ttu-id="c2a92-273">Este exemplo utiliza um modelo Azure Resource Manager predefinidos num repositório GitHub mantido pela Microsoft e abrir toohello Comunidade.</span><span class="sxs-lookup"><span data-stu-id="c2a92-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="c2a92-274">Este modelo pode ser implementado diretamente do GitHub ou transferiu e alterou toofit às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="c2a92-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="c2a92-275">modelo de principais de Olá esteja num ficheiro Olá com o nome "azuredeploy. JSON".</span><span class="sxs-lookup"><span data-stu-id="c2a92-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="c2a92-276">Este modelo pode ser submetido através do PowerShell ou o CLI (com o ficheiro de associado "azuredeploy.parameters.json" Olá) toodeploy este modelo.</span><span class="sxs-lookup"><span data-stu-id="c2a92-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="c2a92-277">Posso encontrar Olá mais fácil é forma toouse Olá "Implementar tooAzure" botão na página de README.md Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="c2a92-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="c2a92-278">modelo de Olá toodeploy que cria este exemplo a partir do GitHub e Olá portal do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="c2a92-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="c2a92-279">Num browser, navegue toohello [modelo][Template]</span><span class="sxs-lookup"><span data-stu-id="c2a92-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="c2a92-280">Clique no botão de "Implementar tooAzure" hello (ou Olá "Visualizar" botão toosee uma representação gráfica deste modelo)</span><span class="sxs-lookup"><span data-stu-id="c2a92-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="c2a92-281">Introduza Olá conta de armazenamento, nome de utilizador e palavra-passe no painel de parâmetros de Olá, em seguida, clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="c2a92-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="c2a92-282">Criar um grupo de recursos para esta implementação (pode utilizar um existente, mas recomendada a um novo para obter os melhores resultados)</span><span class="sxs-lookup"><span data-stu-id="c2a92-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="c2a92-283">Se necessário, altere as definições de subscrição e localização Olá para a sua VNet.</span><span class="sxs-lookup"><span data-stu-id="c2a92-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="c2a92-284">Clique em **consultar termos legais**, Olá termos de licenciamento e clique em **Compra** tooagree.</span><span class="sxs-lookup"><span data-stu-id="c2a92-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="c2a92-285">Clique em **criar** toobegin implementação Olá deste modelo.</span><span class="sxs-lookup"><span data-stu-id="c2a92-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="c2a92-286">Após a conclusão com êxito da implementação de Olá, navegue toohello criado para esta implementação toosee Olá os recursos configurados no interior do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2a92-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="c2a92-287">Este modelo permite RDP toohello IIS01 apenas servidor (Olá localizar um IP público para IIS01 no Olá Portal).</span><span class="sxs-lookup"><span data-stu-id="c2a92-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="c2a92-288">servidores de back-end tooany tooRDP nesta instância, o servidor IIS Olá é utilizado como uma "caixa ir".</span><span class="sxs-lookup"><span data-stu-id="c2a92-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c2a92-289">Servidor IIS de toohello RDP primeiro e, em seguida, a partir do servidor de Olá RDP de servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="c2a92-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="c2a92-290">tooremove esta implementação, Olá eliminar grupo de recursos e todos os recursos subordinados também serão eliminados.</span><span class="sxs-lookup"><span data-stu-id="c2a92-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="c2a92-291">Scripts de aplicação de exemplo</span><span class="sxs-lookup"><span data-stu-id="c2a92-291">Sample application scripts</span></span>
<span data-ttu-id="c2a92-292">Assim que o modelo de Olá é executada com êxito, pode configurar Olá servidor web e servidor de aplicações com um tooallow de aplicação web simples testar com esta configuração de rede de Perímetro.</span><span class="sxs-lookup"><span data-stu-id="c2a92-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="c2a92-293">tooinstall uma aplicação de exemplo para isto e outros exemplos de rede de Perímetro, um tiver sido fornecido no Olá seguinte hiperligação: [Script de aplicação de exemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="c2a92-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2a92-294">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c2a92-294">Next steps</span></span>

* <span data-ttu-id="c2a92-295">Implementar neste exemplo</span><span class="sxs-lookup"><span data-stu-id="c2a92-295">Deploy this example</span></span>
* <span data-ttu-id="c2a92-296">Criar aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="c2a92-296">Build hello sample application</span></span>
* <span data-ttu-id="c2a92-297">Testar os fluxos de tráfego diferentes através desta rede de Perímetro</span><span class="sxs-lookup"><span data-stu-id="c2a92-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Rede de Perímetro entrada com o NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md