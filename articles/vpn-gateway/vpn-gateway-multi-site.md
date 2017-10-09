---
title: "Ligar a sites de toomultiple uma rede virtual com Gateway de VPN e o PowerShell: clássico | Microsoft Docs"
description: "Este artigo irá guiá-lo através de vários locais no local sites tooa rede virtual com um Gateway de VPN para o modelo de implementação clássica Olá a ligar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="78490-103">Adicionar um tooa de ligação de Site para Site VNet com uma ligação de gateway VPN existente (clássica)</span><span class="sxs-lookup"><span data-stu-id="78490-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78490-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="78490-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="78490-105">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="78490-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="78490-106">Este artigo orienta-o através do PowerShell tooadd Site a Site (S2S) ligações tooa gateway de VPN que tenha uma ligação existente a utilizar.</span><span class="sxs-lookup"><span data-stu-id="78490-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="78490-107">Este tipo de ligação é frequentemente referido tooas uma configuração de "multilocal".</span><span class="sxs-lookup"><span data-stu-id="78490-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="78490-108">Olá passos neste artigo aplicam-se redes toovirtual criadas utilizando o modelo de implementação clássica Olá (também conhecido como a gestão de serviço).</span><span class="sxs-lookup"><span data-stu-id="78490-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="78490-109">Estes passos não aplicar as configurações de ligação coexistentes tooExpressRoute/Site a Site.</span><span class="sxs-lookup"><span data-stu-id="78490-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="78490-110">Métodos e modelos de implementação</span><span class="sxs-lookup"><span data-stu-id="78490-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="78490-111">Atualizamos esta tabela medida que novos artigos e ferramentas adicionais ficam disponíveis para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="78490-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="78490-112">Quando estiver disponível um artigo, criamos uma ligação diretamente tooit desta tabela.</span><span class="sxs-lookup"><span data-stu-id="78490-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="78490-113">Sobre a ligação</span><span class="sxs-lookup"><span data-stu-id="78490-113">About connecting</span></span>

<span data-ttu-id="78490-114">Pode ligar vários locais sites tooa única rede virtual.</span><span class="sxs-lookup"><span data-stu-id="78490-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="78490-115">Isto é especialmente apelativo para a criação de soluções de nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="78490-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="78490-116">Criar um gateway de rede virtual do Azure de tooyour ligação multilocal é semelhante toocreating outras ligações Site a Site.</span><span class="sxs-lookup"><span data-stu-id="78490-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="78490-117">Na verdade, pode utilizar um gateway de VPN do Azure existente, desde que o gateway de Olá for dinâmico (baseado na rota).</span><span class="sxs-lookup"><span data-stu-id="78490-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="78490-118">Se já tiver uma rede virtual do gateway estático tooyour ligado, pode alterar toodynamic de tipo de gateway Olá sem necessitar de rede virtual do toorebuild Olá em vários sites do ordem tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="78490-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="78490-119">Antes de alterar o tipo de encaminhamento Olá, certifique-se de que o gateway de VPN no local suporta configurações de VPN baseado na rota.</span><span class="sxs-lookup"><span data-stu-id="78490-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="78490-120">![diagrama multilocal](./media/vpn-gateway-multi-site/multisite.png "multilocal")</span><span class="sxs-lookup"><span data-stu-id="78490-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="78490-121">Tooconsider pontos</span><span class="sxs-lookup"><span data-stu-id="78490-121">Points tooconsider</span></span>

<span data-ttu-id="78490-122">**Não será capaz de toouse Olá portal toomake alterações toothis rede virtual.**</span><span class="sxs-lookup"><span data-stu-id="78490-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="78490-123">Terá de ficheiro de configuração do toomake alterações toohello rede em vez de utilizar o portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="78490-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="78490-124">Se efetuar alterações no portal de Olá, estes irá substituir as definições de referência de vários sites para esta rede virtual.</span><span class="sxs-lookup"><span data-stu-id="78490-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="78490-125">Devem sentir-se confortáveis ao utilizar o ficheiro de configuração de rede de Olá dentro do tempo Olá concluiu procedimento de vários sites Olá.</span><span class="sxs-lookup"><span data-stu-id="78490-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="78490-126">No entanto, se tiver várias pessoas na sua configuração de rede, terá de toomake certificar-se de que todas as pessoas conhece esta limitação.</span><span class="sxs-lookup"><span data-stu-id="78490-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="78490-127">Isto não significa que não é possível utilizar o portal de Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="78490-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="78490-128">Pode utilizá-lo para tudo o resto, exceto efetuar configuração alterações toothis rede virtual específico.</span><span class="sxs-lookup"><span data-stu-id="78490-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="78490-129">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="78490-129">Before you begin</span></span>

<span data-ttu-id="78490-130">Antes de iniciar a configuração, certifique-se de que dispõe Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="78490-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="78490-131">Hardware VPN compatíveis para cada localização no local.</span><span class="sxs-lookup"><span data-stu-id="78490-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="78490-132">Verifique [sobre dispositivos VPN para conectividade de rede Virtual](vpn-gateway-about-vpn-devices.md) tooverify se o dispositivo de Olá que pretende que o toouse é algo que é conhecido toobe compatível.</span><span class="sxs-lookup"><span data-stu-id="78490-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="78490-133">Um com acesso exterior IPv4 endereço IP público para cada dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="78490-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="78490-134">endereço IP Olá não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="78490-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="78490-135">Este é o requisito.</span><span class="sxs-lookup"><span data-stu-id="78490-135">This is requirement.</span></span>
* <span data-ttu-id="78490-136">Terá a versão mais recente de Olá tooinstall de Olá cmdlets Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78490-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="78490-137">Certifique-se que instalar a versão de gestão de serviço (SM) Olá na versão de Gestor de recursos de toohello de adição.</span><span class="sxs-lookup"><span data-stu-id="78490-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="78490-138">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="78490-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="78490-139">Alguém que proficient em configurar o hardware VPN.</span><span class="sxs-lookup"><span data-stu-id="78490-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="78490-140">Terá de toohave uma forte compreender como tooconfigure o dispositivo VPN ou trabalhar com alguém que does.</span><span class="sxs-lookup"><span data-stu-id="78490-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="78490-141">intervalos de endereços do IP de Olá que pretende que toouse na sua rede virtual (se não tiver já criado uma).</span><span class="sxs-lookup"><span data-stu-id="78490-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="78490-142">intervalos de endereços IP de Olá para cada um dos sites de rede local de Olá que irá ser ligar.</span><span class="sxs-lookup"><span data-stu-id="78490-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="78490-143">Terá de certificar-se de que os intervalos de endereços IP de Olá para cada um dos sites de rede local Olá que pretende que o tooconnect toodo sobreposição não toomake.</span><span class="sxs-lookup"><span data-stu-id="78490-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="78490-144">Caso contrário, o portal de Olá ou Olá REST API irão rejeitar configuração Olá que está a ser carregada.</span><span class="sxs-lookup"><span data-stu-id="78490-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="78490-145">Por exemplo, se tiver dois sites de rede local que ambos contêm Olá IP endereço intervalo 10.2.3.0/24 e tiver um pacote com um endereço de destino 10.2.3.3, Azure não sabe que site pretende toosend Olá pacote toobecause Olá intervalos de endereços são sobreposição.</span><span class="sxs-lookup"><span data-stu-id="78490-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="78490-146">problemas de encaminhamento tooprevent, Azure não permite-lhe tooupload um ficheiro de configuração que tenha intervalos sobrepostos.</span><span class="sxs-lookup"><span data-stu-id="78490-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="78490-147">1. Criar uma Rede de VPNs</span><span class="sxs-lookup"><span data-stu-id="78490-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="78490-148">Se já tiver uma VPN de Site para Site com um gateway de encaminhamento dinâmico, great!</span><span class="sxs-lookup"><span data-stu-id="78490-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="78490-149">Para poder continuar demasiado[exportar definições de configuração de rede virtual Olá](#export).</span><span class="sxs-lookup"><span data-stu-id="78490-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="78490-150">Se não estiver, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="78490-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="78490-151">Se já tiver uma rede virtual Site a Site, mas tem um gateway de encaminhamento estático (baseado em políticas):</span><span class="sxs-lookup"><span data-stu-id="78490-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="78490-152">Altere o encaminhamento de toodynamic de tipo do gateway.</span><span class="sxs-lookup"><span data-stu-id="78490-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="78490-153">Uma VPN multilocal requer um gateway de encaminhamento dinâmico (também conhecido como baseado na rota).</span><span class="sxs-lookup"><span data-stu-id="78490-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="78490-154">Escreva o seu gateway de toochange, irá precisar de gateway do toofirst eliminar Olá existente, em seguida, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="78490-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="78490-155">Para obter instruções, consulte [como toochange Olá o tipo de encaminhamento de VPN para o seu gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="78490-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="78490-156">Configure o novo gateway e crie o túnel VPN.</span><span class="sxs-lookup"><span data-stu-id="78490-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="78490-157">Para obter instruções, consulte [configurar um Gateway de VPN no Portal clássico do Azure de Olá](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="78490-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="78490-158">Em primeiro lugar, altere o encaminhamento de toodynamic de tipo do gateway.</span><span class="sxs-lookup"><span data-stu-id="78490-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="78490-159">Se não tiver uma rede virtual do Site para Site:</span><span class="sxs-lookup"><span data-stu-id="78490-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="78490-160">Criar a rede virtual do Site para Site a utilizar estas instruções: [criar uma rede Virtual com uma ligação de VPN de Site a Site no Portal clássico do Azure de Olá](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="78490-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="78490-161">Configurar um gateway de encaminhamento dinâmico a utilizar estas instruções: [configurar um Gateway de VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="78490-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="78490-162">Ser tooselect se **encaminhamento dinâmico** para o seu tipo de gateway.</span><span class="sxs-lookup"><span data-stu-id="78490-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="78490-163"><a name="export"></a>2. Exportar ficheiro de configuração de rede Olá</span><span class="sxs-lookup"><span data-stu-id="78490-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="78490-164">Exporte o ficheiro de configuração de rede do Azure executando Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="78490-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="78490-165">Pode alterar a localização de Olá de Olá ficheiro tooexport tooa localização diferente se for necessário.</span><span class="sxs-lookup"><span data-stu-id="78490-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="78490-166">3. Ficheiro de configuração de rede Olá aberta</span><span class="sxs-lookup"><span data-stu-id="78490-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="78490-167">Abra o ficheiro de configuração de rede Olá que transferiu no último passo de Olá.</span><span class="sxs-lookup"><span data-stu-id="78490-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="78490-168">Utilize qualquer editor de xml que pretender.</span><span class="sxs-lookup"><span data-stu-id="78490-168">Use any xml editor that you like.</span></span> <span data-ttu-id="78490-169">ficheiro de Olá deverá ter um aspeto semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="78490-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="78490-170">4. Adicionar várias referências de site</span><span class="sxs-lookup"><span data-stu-id="78490-170">4. Add multiple site references</span></span>
<span data-ttu-id="78490-171">Quando adicionar ou remover informações de referência de site, terá de efetuar alterações de configuração toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="78490-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="78490-172">Adicionar uma nova referência de local site aciona Azure toocreate um túnel de novo.</span><span class="sxs-lookup"><span data-stu-id="78490-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="78490-173">No exemplo de Olá abaixo, a configuração de rede Olá é para uma ligação de site único.</span><span class="sxs-lookup"><span data-stu-id="78490-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="78490-174">Guarde o ficheiro de Olá depois de terminar de efetuar as alterações.</span><span class="sxs-lookup"><span data-stu-id="78490-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="78490-175">referências a sites adicionais tooadd (criar uma configuração de vários site), adicione simplesmente linhas adicionais "LocalNetworkSiteRef", conforme mostrado no exemplo Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="78490-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="78490-176">5. Ficheiro de configuração de rede de Olá de importação</span><span class="sxs-lookup"><span data-stu-id="78490-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="78490-177">Importar ficheiro de configuração de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="78490-177">Import hello network configuration file.</span></span> <span data-ttu-id="78490-178">Quando importar este ficheiro com alterações de Olá, serão adicionados túneis Olá de novo.</span><span class="sxs-lookup"><span data-stu-id="78490-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="78490-179">túneis Olá irão utilizar o gateway dinâmico Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="78490-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="78490-180">Pode utilizar portal clássico Olá ou ficheiro de Olá tooimport do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78490-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="78490-181">6. Transferir as chaves</span><span class="sxs-lookup"><span data-stu-id="78490-181">6. Download keys</span></span>
<span data-ttu-id="78490-182">Assim que foram adicionados os túneis novo, utilize Olá PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Olá IPsec/IKE chaves pré-partilhadas para cada túnel.</span><span class="sxs-lookup"><span data-stu-id="78490-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="78490-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="78490-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="78490-184">Se preferir, pode também utilizar Olá *obter Virtual rede Gateway chave partilhada* tooget de REST API Olá chaves pré-partilhadas.</span><span class="sxs-lookup"><span data-stu-id="78490-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="78490-185">7. Verifique as suas ligações</span><span class="sxs-lookup"><span data-stu-id="78490-185">7. Verify your connections</span></span>
<span data-ttu-id="78490-186">Verifique o estado de vários sites túnel Olá.</span><span class="sxs-lookup"><span data-stu-id="78490-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="78490-187">Depois de transferir as chaves de Olá para cada túnel, poderá ser útil tooverify ligações.</span><span class="sxs-lookup"><span data-stu-id="78490-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="78490-188">Utilize tooget 'Get-AzureVnetConnection' túneis uma lista de rede virtual, conforme mostrado no exemplo Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="78490-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="78490-189">VNet1 é o nome de Olá do Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="78490-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="78490-190">Exemplo de retorno:</span><span class="sxs-lookup"><span data-stu-id="78490-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="78490-191">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="78490-191">Next steps</span></span>

<span data-ttu-id="78490-192">toolearn mais informações sobre Gateways de VPN, consulte [acerca dos VPN Gateways](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="78490-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
