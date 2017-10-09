---
title: as rotas aaaTroubleshoot - Portal | Microsoft Docs
description: "Saiba como tootroubleshoot rotas Olá do Azure Resource Manager implementação modelo utilizando Olá Portal do Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Resolver problemas de rotas com Olá Portal do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
>
>

Se ocorrerem tooor de problemas de conectividade de rede da sua máquina Virtual do Azure (VM), as rotas podem estar a afetar os fluxos de tráfego da VM. Este artigo fornece uma descrição geral das funcionalidades de diagnóstico para rotas toohelp profundidade.

As tabelas de rotas estão associadas a sub-redes e são eficazes em todas as interfaces de rede (NIC) nessa sub-rede. Olá tipos de rotas seguintes pode ser aplicados tooeach interface de rede:

* **Rotas de sistema:** por predefinição, cada sub-rede criada numa rede Virtual do Azure (VNet) tem as tabelas de rotas de sistema permitem tráfego de VNet local, o tráfego através de gateways de VPN no local e o tráfego de Internet. Também existem rotas de sistema para VNets em modo de peering.
* **Rotas BGP:** propagadas toonetwork interfaces através do ExpressRoute ou ligações de VPN de site para site. Saiba mais sobre o encaminhamento de BGP através da leitura Olá [BGP com gateways de VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) e [descrição geral do ExpressRoute](../expressroute/expressroute-introduction.md) artigos.
* **As rotas definidas pelo utilizador (UDR):** se estiver a utilizar dispositivos de rede virtual ou são forçado túnel tráfego tooan no local rede através de uma VPN de site a site podem ter definido pelo utilizador rotas (UDRs) associadas à sua tabela de rota de sub-rede. Se não estiver familiarizado com UDRs, leia Olá [rotas definidas pelo utilizador](virtual-networks-udr-overview.md#user-defined-routes) artigo.

Com Olá várias rotas que podem ser aplicados tooa interface de rede, pode ser difícil toodetermine que rotas agregadas são eficazes. toohelp resolver problemas de conectividade de rede VM, pode ver todas as rotas efetivas Olá para uma interface de rede no modelo de implementação Azure Resource Manager Olá.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Utilizando o fluxo de tráfego do rotas efetivas tootroubleshoot VM
Este artigo utiliza Olá seguir o cenário como uma tooillustrate de exemplo como tootroubleshoot Olá eficaz encaminha para uma interface de rede:

Uma VM (*VM1*) ligado toohello VNet (*VNet1*, prefixo: 10.9.0.0/16) falha tooconnect tooa VM(VM3) numa VNet em modo de peering recentemente (*VNet3*, prefixo 10.10.0.0/16). Existem não UDRs ou BGP encaminha aplicados tooVM1-NIC1 rede interface ligada toohello VM, apenas as rotas de sistema são aplicadas.

Este artigo explica como toodetermine Olá causa da falha de ligação de Olá, utilizar a capacidade de rotas efetivas no modelo de implementação de gestão de recursos do Azure.
Exemplo de Olá utiliza apenas as rotas de sistema, Olá mesmos passos pode ser falhas de ligação de entrada e saída de toodetermine utilizado por qualquer tipo de rota.

> [!NOTE]
> Se a VM tem mais do que um NIC anexado, verifique as rotas efetivas para cada um dos Olá NICs tooand de problemas da conectividade de rede de toodiagnose de uma VM.
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a>Vista rotas eficazes para uma máquina virtual
toosee Olá agregado rotas que são aplicado tooa VM, Olá concluir os seguintes passos:

1. Toohello de início de sessão do portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **máquinas virtuais** na lista de Olá que aparece.
3. Selecione um tootroubleshoot VM Olá lista que é apresentado e é apresentado o painel uma VM com as opções.
4. Clique em **diagnosticar & resolver problemas** e, em seguida, selecione um problema comum. Neste exemplo, **não consigo ligar toomy VM do Windows** está selecionada.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Os passos apresentados em problema Olá, como mostrado na Olá seguinte imagem:

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Clique em *rotas efetivas* na lista de Olá de passos recomendados.
6. Olá **rotas efetivas** é apresentado o painel, conforme mostrado no Olá seguinte imagem:

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Se a VM tem apenas um NIC, está selecionado por predefinição. Se tiver mais do que um NIC, selecione NIC Olá para o qual pretende rotas efetivas do tooview Olá.

   > [!NOTE]
   > Se hello VM associado hello NIC não está num Estado de execução, rotas efetivas não serão apresentadas. Apenas hello primeiros 200 rotas efetivas são apresentadas no portal de Olá. Para a lista completa de Olá, clique em **transferir**. Pode continuar a filtrar resultados Olá de Olá transferido. csv.
   >
   >

    Tenha em atenção o seguinte Olá na saída de Olá:

   * **Origem**: indica o tipo de Olá da rota. Rotas de sistema são apresentadas como *predefinido*, UDRs são apresentadas como *utilizador* e rotas de gateway (estático ou BGP) são apresentadas como *o VPNGateway*.
   * **Estado**: indica o estado de rotas efetivas Olá. Os valores possíveis são *Active Directory* ou *inválido*.
   * **AddressPrefixes**: Especifica o prefixo de endereço Olá de rotas efetivas Olá em notação CIDR.
   * **nextHopType**: indica o salto seguinte do Olá para Olá fornecido rota. Os valores possíveis são *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, ou *nulo*. Um valor de *nulo* para **nextHopType** num UDR pode indicar uma rota inválida. Por exemplo, se **nextHopType** é *VirtualAppliance* e Olá rede aplicação virtual, de VM não se encontra num Estado aprovisionado/em execução. Se **nextHopType** é *o VPNGateway* e nenhum gateway aprovisionado/em execução no Olá fornecido VNet, existe rota Olá pode tornar-se inválida.
7. Não há nenhuma rota listada toohello *WestUS VNET3* VNet (prefixo 10.10.0.0/16) a partir de Olá *WestUS VNet1* (prefixo 10.9.0.0/16) na imagem de Olá no passo anterior Olá. Nas Olá seguinte imagem, ligação peering Olá está a ser Olá *desligado* Estado:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    ligação de bidirecional Olá para peering Olá é interrompida, o qual explica por que motivo VM1 não conseguiu estabelecer ligação tooVM3 no Olá *WestUS VNet3* VNet.
8. Olá imagem seguinte mostra as rotas de Olá depois de estabelecer a ligação de peering Olá bidirecional:

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Para cenários de resolução de problemas mais para avaliação forçada de túnel e route, leia o artigo Olá [considerações](virtual-network-routes-troubleshoot-portal.md#considerations) secção deste artigo.

### <a name="view-effective-routes-for-a-network-interface"></a>Vista rotas eficazes para uma interface de rede
Se o fluxo de tráfego de rede é afetado para uma determinada interface de rede (NIC), pode ver uma lista completa das rotas efetivas de um NIC diretamente. toosee Olá agregado rotas que são aplicado tooa NIC, Olá concluir os seguintes passos:

1. Toohello de início de sessão do portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **interfaces de rede**
3. Procurar lista Olá para o nome de Olá de uma NIC ou selecione-o na lista de Olá que aparece. Neste exemplo, **VM1 NIC1** está selecionada.
4. Selecione **rotas efetivas** no Olá **interface de rede** painel, conforme mostrado no Olá seguinte imagem:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Olá **âmbito** interface de rede predefinições toohello selecionado.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Ver as rotas eficazes para uma tabela de rota
Quando modificar as rotas definidas pelo utilizador (UDRs) na tabela de rotas, poderá pretender impacto de Olá tooreview das rotas Olá a serem adicionados numa VM específica. Uma tabela de rota pode ser associada a qualquer número de sub-redes. Agora, pode ver todas as rotas de Efetivo Olá para Olá todos os NICs que uma tabela de rota indicado é aplicada, sem ter tooswitch contexto de Olá dado o painel de tabela de rota.

Neste exemplo, um UDR (*UDRoute*) é especificada na tabela de rotas (*UDRouteTable*). Esta rota envia todo o tráfego de Internet de *Subnet1* no Olá *WestUS VNet1* VNet, através de uma aplicação virtual de rede (NVA) na *Subnet2* de Olá mesma VNet. rota de Olá é apresentada nos Olá seguinte imagem:

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee Olá agregado as rotas para uma tabela de rota, Olá concluir os seguintes passos:

1. Toohello de início de sessão do portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **tabelas de rotas**
3. Lista de pesquisa de Olá para a tabela de rota Olá que pretende toosee rotas agregado para e selecione-o. Neste exemplo, **UDRouteTable** está selecionada. Um painel para a tabela de rota Olá selecionada for apresentada, conforme mostrado no Olá seguinte imagem:

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Selecione **rotas efetivas** no Olá **tabela de rotas** painel. Olá **âmbito** está definida a tabela de rotas toohello que selecionou.
5. Uma tabela de rota pode ser aplicados toomultiple sub-redes. Selecione Olá **sub-rede** pretende tooreview da lista de Olá. Neste exemplo, **Subnet1** está selecionada.
6. Selecione um **Interface de rede**. Sub-rede toohello ligado selecionado do todos os NICs são listados. Neste exemplo, **VM1 NIC1** está selecionada.

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Se Olá NIC não estiver associado uma VM em execução, não rotas efetivas são apresentadas.
   >
   >

## <a name="considerations"></a>Considerações
Alguns aspetos tookeep em mente quando rever a lista de Olá das rotas devolvido:

* Encaminhamento baseia-se em mais longo do prefixo da correspondência (LPM) entre UDRs, as rotas BGP e sistema. Se existir mais do que uma rota com Olá mesmo LPM corresponderem, em seguida, uma rota é selecionada com base na respetiva origem em Olá seguinte ordem:

  * Rota definida pelo utilizador
  * Rota BGP
  * Rota de sistema (predefinição)

    Com rotas efetivas, pode vê apenas rotas efetivas que estão a correspondência LPM com base em todas as rotas de disponíveis Olá. Para mostrar como rotas Olá, na verdade, são avaliadas para um determinado NIC, isto torna muito mais fácil rotas específicas tootroubleshoot podem estar a afetar a conectividade de/para a VM.
* Se tiver UDRs e está a enviar aplicação virtual do tráfego tooa rede (NVA), com *VirtualAppliance* como **nextHopType**, certifique-se de que o reencaminhamento IP está ativado no tráfego de Olá recetor NVA Olá ou pacotes serem largados.
* Se forçar o túnel estiver ativado, todo o tráfego de saída da Internet será encaminhado tooon local. RDP/SSH de tooyour Internet que VM poderão não funcionar com esta definição, dependendo de como Olá no local processa este tráfego.
  Túnel forçado pode ser ativado:
  * Se utilizar VPN de site a site, definindo uma rota definida pelo utilizador (UDR) com o nextHopType como Gateway de VPN
  * Se uma rota predefinida é anunciada através do BGP
* Vnet peering tráfego toowork corretamente, uma rota de sistema com **nextHopType** *VNetPeering* tem de existir para o intervalo de prefixo da VNet em modo de peering de Olá. Se esses uma rota não existir e Olá o VNet peering ligação resultados parecem estar OK:
  * Aguarde alguns segundos e repita o se se tratar de uma ligação de peering recentemente estabelecida. Ocasionalmente, demora mais toopropagate rotas interfaces de rede de Olá tooall numa sub-rede.
  * Regras do grupo de segurança de rede (NSG) podem estar a afetar Olá fluxos de tráfego. Para obter mais informações, consulte Olá [resolver problemas relacionados com grupos de segurança de rede](virtual-network-nsg-troubleshoot-portal.md) artigo.
