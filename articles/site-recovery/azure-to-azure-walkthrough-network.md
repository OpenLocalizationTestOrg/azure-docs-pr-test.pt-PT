---
title: "aaaPlan para replicação de tooAzure do VMware com a recuperação de Site de rede | Microsoft Docs"
description: "Este artigo descreve o planeamento de rede necessários ao replicar as VMs do Azure com o Azure Site Recovery"
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Passo 3: Planear o funcionamento em rede para a replicação de VM do Azure

Depois de verificar que a Olá [os pré-requisitos de implementação](azure-to-azure-walkthrough-prerequisites.md), leia esta Olá de toounderstand artigo redes considerações quando replicar e recuperar máquinas de virtuais (VMs) do Azure a partir de uma região do Azure tooanother, utilizando Olá Serviço de recuperação de sites do Azure. 

- Quando acabar de artigo Olá, deve ter um eliminar compreensão sobre como tooset saída segurança acesso para as VMs do Azure pretende tooreplicate e como tooconnect do seu local de site toothose VMs.
- Publique quaisquer comentários na parte inferior deste artigo hello, ou colocar questões no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> Replicação de VM do Azure com a recuperação de Site está atualmente em pré-visualização.



## <a name="network-overview"></a>Descrição geral da rede

Normalmente, as suas VMs do Azure estão localizados numa rede/sub-rede virtual do Azure e existe uma ligação a partir do seu tooAzure de site no local utilizando uma ligação de VPN ou Azure ExpressRoute.

Redes são, normalmente, protegidas através de firewalls e/ou grupos de segurança (NSGs) de rede. As firewalls podem utilizar com base no URL listas baseada em IP, toocontrol conectividade de rede. Os NSGs utilizam regras com base no intervalo IP. 


Para a recuperação de sites toowork esperado, terá de toomake algumas alterações na conectividade de rede de saída, de VMs que pretende que o tooreplicate. Recuperação de sites não suporta a utilização de uma conectividade de rede de toocontrol de proxy de autenticação. Se tiver um proxy de autenticação, não é possível ativar a replicação. 


Olá diagrama seguinte ilustra um ambiente típico para uma aplicação em execução em VMs do Azure.

![ambiente de cliente](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Ambiente de VM do Azure**

Também poderá ter um tooAzure de ligação de multimédia do seu site no local, utilizando uma ligação de VPN ou Azure ExpressRoute. 

![ambiente de cliente](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**TooAzure de ligação no local**



## <a name="outbound-connectivity-for-urls"></a>Conectividade de saída para os URLs

Se estiver a utilizar uma conectividade de saída de toocontrol de proxy firewall baseada no URL, certifique-se a permitir que estes URLs utilizados pela recuperação de sites

**URL** | **Detalhes**  
--- | ---
*.blob.core.windows.net | Permite toobe dados escrito a partir do Olá VM, a conta de armazenamento de cache toohello na região de origem Olá.
login.microsoftonline.com | Fornece autorização e autenticação tooSite URLs do serviço de recuperação.
*.hypervrecoverymanager.windowsazure.com | Permite a comunicação com Olá serviço de recuperação de sites do Olá VM.
*. servicebus.windows.net | Necessário para que os dados de monitorização e diagnóstico da recuperação de Site Olá podem ser escritos a partir do Olá VM.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Conectividade de saída para intervalos de endereços IP

- Pode criar automaticamente regras de Olá necessário no Olá NSG ao descarregar e executar [este script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- Recomendamos que crie regras do NSG Olá necessário num NSG de teste e, certifique-se de que existem não existem problemas, antes de criar regras de Olá sobre um NSG de produção.
- número de Olá necessário toocreate de regras do NSG, certifique-se de que a sua subscrição está na lista de permissões. Contacte o suporte tooincrease Olá NSG regra limite na sua subscrição.
Se estiver a utilizar qualquer proxy firewall baseada em IP ou conectividade de saída do toocontrol de regras do NSG, hello seguintes intervalos de IP necessário na lista de permissões de toobe, consoante as localizações de origem e destino Olá das máquinas de virtuais Olá:

    - Todos os intervalos de endereços IP que correspondem toohello localização de origem. Transferência Olá [intervalos](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Adicionar à lista branca é necessário, para que os dados podem ser escritos a conta de armazenamento de cache toohello de Olá VM.
    - Todos os intervalos IP que correspondem tooOffice 365 [pontos finais de endereço IP V4 de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Se o novo IPs adicionadas tooOffice 365 intervalos IP, terá de toocreate novas regras de NSG.
-     Endereços de IP de ponto final de serviço de recuperação de sites ([disponíveis num ficheiro XML](https://aka.ms/site-recovery-public-ips)), que dependem da sua localização de destino: 

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

## <a name="example-nsg-configuration"></a>Exemplo de configuração de NSG

Esta secção mostra como as regras tooconfigure NSG, para que replicações funciona para uma VM. Se estiver a utilizar a conectividade de saída do toocontrol de regras do NSG, utilize "Permitir HTTPS saída" regras para todos os intervalos IP Olá necessário.

Neste exemplo, Olá localização de origem da VM é "EUA Leste". localização de destino de replicação de Olá está EUA Central.


### <a name="example"></a>Exemplo

#### <a name="east-us"></a>EUA Leste

1. Criar regras que correspondem demasiado[intervalos de IP do Leste E.U.A.](https://www.microsoft.com/download/confirmation.aspx?id=41653). Isto é necessário para que os dados podem ser escritos a conta de armazenamento de cache toohello de Olá VM.
2. Criar regras para todos os intervalos IP que correspondem tooOffice 365 [pontos finais de endereço IP V4 de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Crie regras que correspondem a localização de destino toohello:

   **Localização** | **Serviço de recuperação de sites IPs** |  **Recuperação de site do IP de monitorização**
    --- | --- | ---
   EUA Central | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>EUA Central

Estas regras são necessárias para que a replicação pode ser ativada a região de origem do Olá destino região toohello, após a ativação pós-falha.

1. Criar regras que correspondem demasiado[intervalos de IP de E.U.A. Central](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Criar regras para todos os intervalos IP que correspondem tooOffice 365 [pontos finais de endereço IP V4 de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Crie regras que correspondem a localização de origem toohello:

   **Localização** | **Serviço de recuperação de sites IPs** |  **Recuperação de site do IP de monitorização**
    --- | --- | ---
   EUA Leste | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Existente no local ligação

Se tiver uma ligação ExpressRoute ou VPN entre o site no local e a localização de origem Olá no Azure, siga estas diretrizes:

**Configuração** | **Detalhes**
--- | ---
**Imposição do túnel** | Normalmente, uma rota predefinida (0.0.0.0/0) força tooflow saída do tráfego de internet através de localização do Olá no local. Não é recomendável. Tráfego de replicação e comunicações de recuperação de Site devem permanecer no Azure.<br/><br/> Como uma solução, adicione as rotas definidas pelo utilizador (UDRs) para [estes intervalos IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges), para que o tráfego de Olá não passa no local.
**Conetividade** | Se as aplicações necessitam de máquinas de tooon local tooconnect ou clientes no local ligam toohello aplicação através de no local através do VPN/ExpressRoute, certifique-se de que tem, pelo menos, um [ligação site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), entre destino Olá região do Azure e site do Olá no local.<br/><br/> Se os volumes de tráfego elevados entre destino Olá região do Azure e o site no local de Olá, crie outro [ligação do ExpressRoute](../expressroute/expressroute-introduction.md), entre a região de destino Olá e no local.<br/><br/> Se quiser tooretain IPs para as VMs após a ativação pós-falha, mantenha a ligação de site para site/ExpressRoute da região de destino Olá no estado desligado. Isto garante que não existem nenhum intervalo entra em conflito entre Olá origem e destino intervalos de endereços IP.
**ExpressRoute** | Crie um circuito ExpressRoute Olá regiões de origem e de destino.<br/><br/> Crie uma ligação entre a rede de origem de Olá e o circuito de ExpressRoute Olá e entre a rede de destino Olá e circuito Olá.<br/><br/> Recomendamos que utilize diferentes intervalos IP em regiões de origem e de destino. Olá circuito não será capaz de tooconnect toomore que um Azure redes com Olá mesmo intervalos de IP, nos Olá mesmo tempo.<br/><br/> Pode criar redes virtuais com Olá mesmo IP intervalos em ambas as regiões e, em seguida, criar circuito do ExpressRoute em ambas as regiões. Para ativação pós-falha, desligue circuito Olá a rede virtual de origem Olá e ligar circuito Olá na rede virtual de destino Olá.<br/><br/> Se a região primária Olá está completamente baixo, Olá desligar a operação poderá falhar. Neste caso, a rede virtual de destino Olá não obter conectividade do ExpressRoute.
**Premium do ExpressRoute** | Pode criar circuitos em Olá mesma região geopolítica.<br/><br/> circuitos toocreate em diferentes regiões geopolíticas, precisa do Azure ExpressRoute Premium.<br/><br/> Com o Premium, o custo de Olá é incremental. Se já estiver a utilizá-lo, há sem custos adicionais.<br/><br/> Saiba mais sobre [localizações](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) e [preços](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 4: criar um cofre](azure-to-azure-walkthrough-vault.md)

