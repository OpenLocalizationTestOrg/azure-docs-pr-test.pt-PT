---
title: "aaaAzure orientações de rede de recuperação de sites para replicar máquinas virtuais do Azure tooAzure | Microsoft Docs"
description: "Rede orientações para replicar máquinas virtuais do Azure"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Rede orientações para replicar máquinas virtuais do Azure

>[!NOTE]
> Replicação de recuperação de site para máquinas virtuais do Azure está atualmente em pré-visualização.

Olá de detalhes deste artigo orientações para o Azure Site Recovery de rede quando estiver a replicar e recuperar máquinas virtuais do Azure a partir de região de tooanother uma região. Para obter mais informações sobre os requisitos do Azure Site Recovery, consulte Olá [pré-requisitos](site-recovery-prereq.md) artigo.

## <a name="site-recovery-architecture"></a>Arquitetura de recuperação de site

Recuperação de sites fornece uma forma simples e fácil tooreplicate aplicações executadas em máquinas virtuais do Azure tooanother região do Azure para que podem ser recuperados se houver uma interrupção na região primária Olá. Saiba mais sobre [este cenário e a arquitetura da recuperação de Site](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>A infraestrutura de rede

Olá diagrama seguinte ilustra Olá típico ambiente do Azure para uma aplicação em execução em máquinas virtuais do Azure:

![ambiente de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Se estiver a utilizar o Azure ExpressRoute ou de uma ligação VPN um tooAzure de rede no local, ambiente de Olá este aspeto:

![ambiente de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

Normalmente, os clientes protegem as respetivas redes através de firewalls e/ou grupos de segurança de rede (NSGs). firewalls Olá podem utilizar a listas brancas baseado no URL ou baseada em IP para controlar a conectividade de rede. Os NSGs permitem regras para a utilização de intervalos IP toocontrol conectividade de rede.

>[!IMPORTANT]
> Se estiver a utilizar uma conectividade de rede de toocontrol proxy autenticado, não é suportada e não é possível ativar a replicação do Site Recovery. 

Olá secções seguintes abordam Olá conectividade de saída as alterações da rede que são necessárias de máquinas virtuais do Azure para toowork de replicação do Site Recovery.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Conectividade de saída para os URLs de recuperação de Site do Azure

Se estiver a utilizar qualquer conectividade de saída de toocontrol de proxy firewall baseada no URL, ser toowhitelist se estes necessários URLs do serviço Azure Site Recovery:


**URL** | **Objetivo**  
--- | ---
*.blob.core.windows.net | Necessário para que os dados podem ser escritos a conta de armazenamento de cache toohello na região de origem Olá de Olá VM.
login.microsoftonline.com | Necessário para autenticação e autorização URLs do serviço de recuperação de Site toohello.
*.hypervrecoverymanager.windowsazure.com | Necessário para que a comunicação do serviço de recuperação de Site Olá pode ocorrer do Olá VM.
*. servicebus.windows.net | Necessário para que os dados de monitorização e diagnóstico da recuperação de Site Olá podem ser escritos a partir do Olá VM.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Conectividade de saída para intervalos de IP do Azure Site Recovery

>[!NOTE]
> tooautomatically criar regras do NSG Olá necessário, no grupo de segurança de rede Olá, pode [transferir e utilizar este script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * Recomendamos que crie regras do NSG Olá necessário num grupo de segurança de rede de teste e certifique-se de que existem não existem problemas antes de criar regras de Olá num grupo de segurança de rede de produção.
> * número de Olá necessário toocreate de regras do NSG, certifique-se de que a sua subscrição está na lista de permissões. Contacte o suporte tooincrease Olá NSG regra limite na sua subscrição.

Se estiver a utilizar qualquer proxy firewall baseada em IP ou conectividade de saída do toocontrol de regras do NSG, hello seguintes intervalos de IP necessário na lista de permissões de toobe, consoante as localizações de origem e destino Olá das máquinas de virtuais Olá:

- Todos os intervalos IP que correspondem toohello localização de origem. (Pode transferir Olá [intervalos IP](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Adicionar à lista branca é necessário para que os dados podem ser escritos a conta de armazenamento de cache toohello de Olá VM.

- Todos os intervalos IP que correspondem tooOffice 365 [pontos finais de endereço IP V4 de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Se IPs novo adicionadas tooOffice 365 intervalos IP no Olá futura, é necessário toocreate novas regras de NSG.
    
- Sites de ponto final do serviço de recuperação IPs ([disponíveis num ficheiro XML](https://aka.ms/site-recovery-public-ips)), que dependem da sua localização de destino: 

   **Localização de destino** | **Serviço de recuperação de sites IPs** |  **Recuperação de site do IP de monitorização**
   --- | --- | ---
   Ásia Oriental | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Sudeste Asiático | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   Índia Central | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Sul da Índia | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   EUA Centro-Norte | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Europa do Norte | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Europa Ocidental | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   EUA Leste | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   EUA Oeste | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   EUA Centro-Sul | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   EUA Central | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   EUA Leste 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Leste do Japão | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Oeste do Japão | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Sul do Brasil | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Leste da Austrália | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Sudeste da Austrália | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Canadá Central | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Leste do Canadá | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   EUA Centro-Oeste | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   EUA Oeste 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Reino Unido Oeste | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Reino Unido Sul | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>Exemplo de configuração de NSG
Esta secção explica as regras do NSG Olá passos tooconfigure para que possam funcionar a replicação do Site Recovery numa máquina virtual. Se estiver a utilizar conectividade de saída do toocontrol de regras do NSG, utilize "Permitir HTTPS saída" regras para todos os intervalos IP Olá necessário.

>[!Note]
> tooautomatically criar regras do NSG Olá necessário, no grupo de segurança de rede Olá, pode [transferir e utilizar este script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Por exemplo, se a localização de origem da VM é "EUA Leste" e a localização de destino de replicação é "Central EUA", siga os passos de Olá Olá junto duas secções.

>[!IMPORTANT]
> * Recomendamos que crie regras do NSG Olá necessário num grupo de segurança de rede de teste e certifique-se de que existem não existem problemas antes de criar regras de Olá num grupo de segurança de rede de produção.
> * número de Olá necessário toocreate de regras do NSG, certifique-se de que a sua subscrição está na lista de permissões. Contacte o suporte tooincrease Olá NSG regra limite na sua subscrição. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>Regras do NSG no grupo de segurança de rede do Olá EUA leste

* Criar regras que correspondem demasiado[intervalos de IP do Leste E.U.A.](https://www.microsoft.com/download/confirmation.aspx?id=41653). Isto é necessário para que os dados podem ser escritos a conta de armazenamento de cache toohello de Olá VM.

* Criar regras para todos os intervalos IP que correspondem tooOffice 365 [pontos finais de endereço IP V4 de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Crie regras que correspondem a localização de destino toohello:

   **Localização** | **Serviço de recuperação de sites IPs** |  **Recuperação de site do IP de monitorização**
    --- | --- | ---
   EUA Central | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Regras do NSG no grupo de segurança de rede do Olá e.u. a Central

Estas regras são necessárias para que a replicação pode ser ativada a partir Olá destino região toohello origem região pós-falha:

* As regras que correspondem demasiado[intervalos de IP de E.U.A. Central](https://www.microsoft.com/download/confirmation.aspx?id=41653). Estes são necessários para que os dados podem ser escritos a conta de armazenamento de cache toohello de Olá VM.

* Regras para todos os intervalos IP que correspondem tooOffice 365 [pontos finais de endereço IP V4 de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Regras que correspondem a localização de origem toohello:

   **Localização** | **Serviço de recuperação de sites IPs** |  **Recuperação de site do IP de monitorização**
    --- | --- | ---
   EUA Leste | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Diretrizes para a configuração do Azure-para-no local. o ExpressRoute/VPN existente

Se tiver uma ligação ExpressRoute ou VPN entre no local e Olá da origem de localização no Azure, siga as diretrizes de Olá nesta secção.

### <a name="forced-tunneling-configuration"></a>Forçado a configuração de túnel

Uma configuração de cliente comum é toodefine uma rota predefinida (0.0.0.0/0) que força tooflow saída do tráfego de Internet através de localização do Olá no local. Não recomendamos esta. tráfego de replicação de Olá e comunicação de serviço de recuperação de Site não devem deixar Olá limites do Azure. Olá solução é tooadd definido pelo utilizador rotas (UDRs) para [estes intervalos IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges) para que o tráfego de replicação de Olá não passa no local.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Conectividade entre a localização de destino e no local Olá

Siga estas diretrizes para ligações entre a localização de destino de Olá e localização no local de Olá:
- Se a sua aplicação precisar de máquinas do tooconnect toohello no local, ou se não existirem clientes que ligam toohello aplicações no local através de VPN/ExpressRoute, certifique-se de que tem, pelo menos, um [ligação site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) entre o seu centro de dados de destino do Azure região e Olá no local.

- Se espera que uma grande quantidade de tráfego tooflow entre a sua região do Azure de destino e o Centro de dados do Olá no local, deve criar outro [ligação do ExpressRoute](../expressroute/expressroute-introduction.md) entre o Centro de dados do Olá destino do Azure região e Olá no local.

- Se quiser tooretain IPs para máquinas de virtuais Olá depois de efetuar a ativação pós-falha, mantenha a ligação de site para site/ExpressRoute da região de destino Olá no estado desligado. Este é toomake se de que não haja nenhum conflito de intervalo entre os intervalos IP da região de origem Olá e intervalos IP da região de destino.

### <a name="best-practices-for-expressroute-configuration"></a>Melhores práticas para a configuração do ExpressRoute
Siga estas práticas recomendadas para a configuração do ExpressRoute:

- É necessário toocreate um circuito de ExpressRoute em ambas as regiões de origem e destino Olá. Em seguida, terá de toocreate uma ligação entre:
  - rede virtual de origem Olá e o circuito de ExpressRoute Olá.
  - rede virtual de destino Olá e o circuito de ExpressRoute Olá.

- Como parte do ExpressRoute standard, pode criar circuitos em Olá mesma região geopolítica. circuitos do ExpressRoute toocreate em diferentes regiões geopolíticas, Azure ExpressRoute Premium é necessário, que envolve um custo incremental. (Se já estiver a utilizar o ExpressRoute Premium, existe um custo extra.) Para obter mais detalhes, consulte Olá [documento de localizações do ExpressRoute](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) e [ExpressRoute preços](https://azure.microsoft.com/pricing/details/expressroute/).

- Recomendamos que utilize diferentes intervalos IP em regiões de origem e de destino. Olá circuito do ExpressRoute não conseguirá intervalos de IP mesmo tooconnect com duas redes virtuais do Azure de Olá em Olá mesmo tempo.

- Pode criar redes virtuais com Olá mesmo IP intervalos em ambas as regiões e, em seguida, criar circuito do ExpressRoute em ambas as regiões. No caso de Olá de um evento de ativação pós-falha, desligue circuito Olá a rede virtual de origem Olá e ligar circuito Olá na rede virtual de destino Olá.

 >[!IMPORTANT]
 > Se a região primária Olá está completamente baixo, Olá desligar a operação pode falhar. Que irá impedir que a rede virtual de destino Olá obtenham a conectividade do ExpressRoute.

## <a name="next-steps"></a>Passos seguintes
Começar a proteger as cargas de trabalho por [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).
