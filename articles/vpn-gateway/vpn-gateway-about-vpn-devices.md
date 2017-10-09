---
title: "dispositivos VPN aaaAbout para ligações do Azure em vários locais | Microsoft Docs"
description: "Este artigo aborda os dispositivos VPN e os parâmetros IPsec para ligações entre locais do Gateway de VPN S2S. São fornecidas hiperligações tooconfiguration instruções e exemplos."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>Acerca dos dispositivos de VPN e dos parâmetros IPsec/IKE para ligações do Gateway da Rede de VPNs

Um dispositivo VPN é tooconfigure necessária uma ligação de VPN de vários locais Site a Site (S2S) utilizando um gateway de VPN. Ligações site a Site podem ser utilizado toocreate uma solução híbrida ou sempre que pretender ligações seguras entre as redes no local e as redes virtuais. Este artigo fornece uma lista de dispositivos VPN validados e uma lista de parâmetros de IPsec/IKE para gateways de VPN.

> [!IMPORTANT]
> Se está a ter problemas de conectividade entre os dispositivos VPN no local e os gateways de VPN, consulte demasiado[problemas de compatibilidade de dispositivos conhecidos](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Itens toonote quando visualizar as tabelas de Olá:

* A terminologia para os gateways de VPN do Azure foi alterada. Apenas os nomes de Olá foram alteradas. Não há qualquer alteração de funcionalidade.
  * Encaminhamento Estático = PolicyBased
  * Encaminhamento Dinâmico = RouteBased
* Especificações para o gateway de HighPerformance VPN e o gateway de RouteBased VPN são Olá mesmo, exceto indicação em contrário. Por exemplo, dispositivos VPN de Olá validada que são compatíveis com gateways de RouteBased VPN também são compatíveis com Olá gateway de HighPerformance VPN.

## <a name="devicetable"></a>Dispositivos VPN validados e guias de configuração de dispositivo

> [!NOTE]
> Ao configurar uma ligação Site a Site, é preciso um endereço IP IPv4 destinado ao público para o dispositivo VPN.
>

Em parceria com os fornecedores dos dispositivos, validámos uma série de dispositivos VPN padrão. Todos os dispositivos de Olá no famílias de dispositivos de Olá no Olá a seguir lista devem funcionar com gateways de VPN. Consulte [sobre o VPN Gateway definições](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand Olá VPN escreva utilização (PolicyBased ou RouteBased) para Olá solução de Gateway de VPN que pretende tooconfigure.

toohelp configurar o dispositivo VPN, consulte toohello ligações que correspondem tooappropriate família de dispositivos. são fornecidas instruções de tooconfiguration de ligações de Olá numa base de melhor esforço. Para obter suporte para dispositivos VPN, contacte o fabricante do dispositivo.

|**Fornecedor**          |**Família de dispositivos**     |**Versão mínima do SO** |**Instruções de configuração PolicyBased** |**Instruções de configuração RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Não Compatível  |[Guia de configuração](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |Routers VPN Série AR |2.9.2                  |Brevemente     |Não compatível  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall série F |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Guia de configuração](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Guia de configuração](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall série X |Barracuda Firewall 6.5 |[Guia de configuração](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Não compatível |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Guia de configuração](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Não compatível |
| Check Point |Gateway de Segurança |R77.30 |[Guia de configuração](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Guia de configuração](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Não compatível |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Exemplos de configuração*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 e posterior |[Guia de configuração](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Não compatível |
| F5 |Série BIG-IP |12.0 |[Guia de configuração](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Guia de configuração](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Guia de configuração](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Série SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Guia de configuração](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Não compatível |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Série J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Serviço de Encaminhamento e Acesso Remoto |Windows Server 2012 |Não compatível |[Exemplos de configuração](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Gateway de Segurança do Controlo da Missão |N/D |[Guia de configuração](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Não compatível |
| Openswan |Openswan |2.6.32 |(Brevemente) |Não compatível |
| Palo Alto Networks |Todos os dispositivos com o PAN-OS |PAN-OS<br>PolicyBased: 6.1.5 ou posterior<br>RouteBased: 7.1.4 |[Guia de configuração](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Guia de configuração](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |Série TZ, Série NSA<br>Série SuperMassive<br>Série NSA Classe E |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Guia de configuração do SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guia de configuração do SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Guia de configuração do SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guia de configuração do SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Todos |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Guia de configuração](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Guia de configuração](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) Os routers da série ISR 7200 só suportam VPNs PolicyBased.

## <a name="additionaldevices"></a>Dispositivos VPN não validados

Se não vir o seu dispositivo listado na tabela de dispositivos VPN validados Olá, o dispositivo ainda pode funcionar com uma ligação Site a Site. Contacte o fabricante do dispositivo para obter instruções adicionais de suporte e de configuração.

## <a name="editing"></a>Editar os exemplos de configuração do dispositivo

Depois de transferir o exemplo de configuração de dispositivo VPN Olá fornecido, terá de tooreplace algumas das Olá valores de definições de Olá tooreflect para o seu ambiente.

### <a name="tooedit-a-sample"></a>tooedit um exemplo:

1. Abra o exemplo de Olá com o bloco de notas.
2. Procure e substitua todas <*texto*> cadeias com valores de Olá que dizem respeito tooyour ambiente. Ser tooinclude se < e >. Quando é especificado um nome, nome de Olá que selecionar deve ser exclusivo. Se um comando não funcionar, consulte a documentação do fabricante do dispositivo.

| **Texto de exemplo** | **Alterar para** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |O nome que escolheu para este objeto. Exemplo: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |O nome que escolheu para este objeto. Exemplo: myAzureNetwork |
| &lt;RP_AccessList&gt; |O nome que escolheu para este objeto. Exemplo: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |O nome que escolheu para este objeto. Exemplo: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |O nome que escolheu para este objeto. Exemplo: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Especifique o intervalo. Exemplo: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Especifique a máscara de sub-rede. Exemplo: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Especifique o intervalo no local. Exemplo: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Especifique a máscara de sub-rede no local. Exemplo: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Informações específicas tooyour a rede virtual e encontra-se no Portal de gestão de Olá como **endereço IP do Gateway**. |
| &lt;SP_PresharedKey&gt; |Esta informação é tooyour específicos de rede virtual e está localizada na Olá Portal de gestão como gerir chave. |

## <a name="ipsec"></a>Parâmetros de IPsec/IKE

> [!NOTE]
> Embora Olá listados no Olá a tabela seguinte são atualmente suportados valores pelo gateway VPN Olá, existe não é nenhum mecanismo para si toospecify ou selecionar uma combinação específica de algoritmos ou parâmetros de gateway de VPN Olá. Tem de especificar as eventuais restrições no dispositivo VPN do Olá no local. Além disso, tem de fixar **MSS** em **1350**.
> 
>

No Olá seguintes tabelas:

* SA = Associação de Segurança
* IKE Fase 1 também é denominado "Modo Principal"
* IKE Fase 2 também é denominado "Modo Rápido"

### <a name="ike-phase-1-main-mode-parameters"></a>Parâmetros de IKE Fase 1 (Modo Principal)

| **Propriedade**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Versão do IKE           |IKEv1              |IKEv2              |
| Grupo Diffie-Hellman  |Grupo 2 (1024 bits) |Grupo 2 (1024 bits) |
| Método de Autenticação |Chave Pré-partilhada     |Chave Pré-partilhada     |
| Algoritmos de Encriptação e Hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Duração de SA           |28 800 segundos     |28 800 segundos     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Parâmetros de IKE Fase 2 (Modo Rápido)

| **Propriedade**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Versão do IKE                   |IKEv1          |IKEv2                                        |
| Algoritmos de Encriptação e Hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Ofertas de RouteBased QM SA](#RouteBasedOffers) |
| Duração de SA (Tempo)            |3600 segundos  |27,000 segundos                                |
| Duração de SA (Bytes)           |102 400 000 KB | -                                           |
| Perfect Forward Secrecy (PFS) |Não             |[Ofertas de RouteBased QM SA](#RouteBasedOffers) |
| Deteção de Elemento Inutilizado (DPD)     |Não suportado  |Suportado                                    |


### <a name ="RouteBasedOffers"></a>Ofertas de RouteBased VPN IPsec Security Association (SA do Modo Rápido de IKE)

Olá tabela seguinte apresenta uma lista de ofertas de SA de IPsec (IKE de modo rápido). As ofertas estão ordem listada Olá de preferência que oferta Olá é apresentada ou aceite.

#### <a name="azure-gateway-as-initiator"></a>Gateway do Azure como iniciador

|-  |**Encriptação**|**Autenticação**|**Grupo PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |Nenhuma         |
| 2 |AES256        |SHA1              |Nenhuma         |
| 3 |3DES          |SHA1              |Nenhuma         |
| 4 |AES256        |SHA256            |Nenhuma         |
| 5 |AES128        |SHA1              |Nenhuma         |
| 6 |3DES          |SHA256            |Nenhuma         |

#### <a name="azure-gateway-as-responder"></a>Gateway do Azure como dispositivo de resposta

|-  |**Encriptação**|**Autenticação**|**Grupo PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |Nenhuma         |
| 2 |AES256        |SHA1              |Nenhuma         |
| 3 |3DES          |SHA1              |Nenhuma         |
| 4 |AES256        |SHA256            |Nenhuma         |
| 5 |AES128        |SHA1              |Nenhuma         |
| 6 |3DES          |SHA256            |Nenhuma         |
| 7 |DES           |SHA1              |Nenhuma         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |Nenhuma         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* Pode especificar a encriptação IPsec ESP NULL com gateways de VPN RouteBased e HighPerformance. Encriptação baseada em nulo não proporciona proteção toodata em trânsito e só deve ser utilizada quando máximo débito e latência mínima é necessária. Os clientes podem optar toouse isto em cenários de comunicação de VNet a VNet ou quando a encriptação está a ser aplicada noutro local na solução de Olá.
* Conectividade em vários locais através da Internet de Olá, utilize definições do gateway de VPN do Azure do Olá predefinido com a encriptação e algoritmos hash listados nas tabelas de Olá acima tooensure de segurança da sua comunicação crítica.

## <a name="known"></a>Problemas de compatibilidade de dispositivos conhecidos

> [!IMPORTANT]
> Estes são Olá problemas de compatibilidade conhecidos entre dispositivos VPN de terceiros e gateways de VPN do Azure. Olá equipa do Azure ativamente está a trabalhar com fornecedores de Olá tooaddress Olá problemas listados aqui. Depois de problemas de Olá sejam resolvidos, esta página será atualizada com informações mais atualizadas à sua Olá. Volte a verificar periodicamente.
>
>

### <a name="feb-16-2017"></a>16 de fevereiro de 2017

**Dispositivos de redes da Palo Alto com too7.1.4 anterior versão** para VPN baseado na rota do Azure: Se estiver a utilizar dispositivos VPN da Palo Alto redes com o PAN-OS versão anterior too7.1.4 e estão a ter conectividade emite tooAzure gateways de VPN baseado na rota, Execute Olá os seguintes passos:

1. Verifique a versão de firmware Olá do seu dispositivo da Palo Alto redes. Se a sua versão PAN-OS é anterior ao 7.1.4, atualize too7.1.4.
2. No dispositivo de redes da Palo Alto Olá, alterar Olá fase 2 SA (ou SA de modo rápido) duração too28, 800 segundos (8 horas) quando ligar toohello VPN gateway do Azure.
3. Se ainda ocorrerem problemas de conectividade, abra um pedido de suporte de Olá portal do Azure.
