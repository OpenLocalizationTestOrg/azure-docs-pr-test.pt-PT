---
title: "a configuração do aaaSample – ligar os gateways de VPN tooAzure de dispositivo de Cisco ASA | Microsoft Docs"
description: "Este artigo fornece uma configuração de exemplo para o dispositivo de Cisco ASA tooAzure gateways de VPN a ligar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Configuração de exemplo: Cisco ASA dispositivo (IKEv2/não BGP)
Este artigo fornece configurações de exemplo para dispositivos de Cisco ASA tooAzure gateways de VPN a ligar.

## <a name="device-at-a-glance"></a>Dispositivo de forma rápida

|                        |                                   |
| ---                    | ---                               |
| Fabricante do dispositivo          | Cisco                             |
| Modelo do dispositivo           | ASA (aplicação de segurança adaptável) |
| Versão de destino         | 8.4+                              |
| Modelo testado           | ASA 5505                          |
| Versão testada         | 9.2                               |
| Versão do IKE            | **IKEv2**                         |
| BGP                    | **Não**                            |
| Tipo de gateway VPN do Azure | **Baseado na rota** gateway de VPN       |
|                        |                                   |

> [!NOTE]
> 1. configuração de Olá abaixo liga um tooan de dispositivo de Cisco ASA Azure **baseado na rota** VPN gateway com a política personalizada do IPsec/IKE com a opção "UserPolicyBasedTrafficSelectors", conforme descrito em [neste artigo](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. Requer ASA dispositivos toouse **IKEv2** com configurações de lista-baseada no acesso, não VTI com base em.
> 3. Consulte com as especificações de fornecedor de dispositivo VPN política de Olá tooensure é suportada nos seus dispositivos VPN no local.

## <a name="vpn-device-requirements"></a>Requisitos de dispositivos VPN
Gateways de VPN do Azure utilizam padrão IPsec/IKE protocolo conjuntos tooestablish túneis S2S VPN. Consulte demasiado[acerca dos dispositivos VPN](vpn-gateway-about-vpn-devices.md) para Olá detalhadas os parâmetros de protocolo de IPsec/IKE e algoritmos de criptografia predefinido para gateways de VPN do Azure. Opcionalmente, pode especificar combinação exato de Olá de algoritmos criptográficos e força da codificação chave para uma ligação específica, tal como descrito no [sobre os requisitos de criptografia](vpn-gateway-about-compliance-crypto.md). Se selecionar uma combinação específica de algoritmos criptográficos e chave força da codificação, certifique-se que utilizar especificações correspondente Olá nos seus dispositivos VPN.

## <a name="single-vpn-tunnel"></a>Túnel VPN único
Esta topologia é composta por um único túnel de S2S VPN entre um gateway de VPN do Azure e o dispositivo VPN no local. Opcionalmente, pode configurar o BGP em túnel do Olá VPN.

![túnel único](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Consulte demasiado[configuração de túnel único](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) para detalhadas, instruções passo a passo toobuild Olá configurações do Azure.

### <a name="network-and-vpn-gateway-information"></a>Informações do gateway de rede e da VPN
Esta secção lista os parâmetros de Olá para Olá este exemplo.

| **Parâmetro**                | **Valor**                    |
| ---                          | ---                          |
| Prefixos de endereço VNet        | 10.11.0.0/16<br>10.12.0.0/16 |
| IP do gateway VPN do Azure         | Azure_Gateway_Public_IP      |
| Prefixos de endereço no local | 10.51.0.0/16<br>10.52.0.0/16 |
| IP do dispositivo VPN no local    | OnPrem_Device_Public_IP     |
| * VNet ASN de BGP                | 65010                        |
| * IP do elemento BGP do azure           | 10.12.255.30                 |
| * No local ASN de BGP         | 65050                        |
| * IP do elemento BGP no local     | 10.52.255.254                |
|                              |                              |

* (*) Parâmetros opcionais para BGP apenas.

### <a name="ipsecike-policy--parameters"></a>Política do IPsec/IKE & parâmetros

tabela de Olá abaixo apresenta uma lista de algoritmos de IPsec/IKE Olá e parâmetros utilizados no exemplo de Olá. Consulte o toomake de especificações de dispositivo VPN se de que todos os algoritmos listados acima são suportados pelo seu modelos de dispositivos VPN e as versões de firmware.

| **IPsec/IKEv2**  | **Valor**                            |
| ---              | ---                                  |
| Encriptação IKEv2 | AES256                               |
| Integridade do IKEv2  | SHA384                               |
| Grupo DH         | DHGroup24                            |
| Encriptação do IPsec | AES256                               |
| Integridade do IPsec  | SHA1                                 |
| Grupo PFS        | PFS24                                |
| Duração de SA QM   | segundos de 7200                         |
| Seletor de tráfego | UsePolicyBasedTrafficSelectors $True |
| Chave Pré-partilhada   | PreSharedKey                         |
|                  |                                      |

- (*) Em alguns dispositivos, IPsec integridade tem de ser "null" se GCM AES é utilizado como o algoritmo de encriptação de IPsec.

### <a name="device-notes"></a>Notas de dispositivo

>[!NOTE]
>
> 1. Suporte do IKEv2 requer ASA versão 8.4 e superior.
> 2. Suporte de grupo DH superior e PFS (além do grupo de 5) requer a versão do ASA 9.x.
> 3. Encriptação de IPsec com AES-GCM e IPsec integridade com o SHA-256, SHA-384, suporte de SHA-512 requer a versão do ASA 9.x no hardware mais recente do ASA; 5505 ASA, 5510, 5520, 5540, 5550, são 5580 **não** suportado. (Verifique Olá fornecedor especificações tooconfirm.)
>


### <a name="sample-device-configurations"></a>Configurações de dispositivos de exemplo
script de Olá abaixo fornece uma configuração de exemplo com base na topologia de Olá e os parâmetros indicados acima. configuração de túnel S2S VPN Olá consiste Olá seguintes partes:

1. Interfaces & rotas
2. Apresenta uma lista de acesso
3. Política de IKE e parâmetros (a fase 1 ou modo principal)
4. Política de IPsec e parâmetros (a fase 2 ou modo rápido)
5. Outros parâmetros (TCP MSS clamping, etc.)

>[!IMPORTANT] 
>Certifique-se que conclua a configuração adicional Olá listada abaixo e substitui os marcadores de Olá com valores reais Olá:
> 
> - Configuração para dentro e fora de interfaces de interface
> - Rotas para as redes privadas/dentro e fora/público
> - Certifique-se de que todos os nomes e números de política são exclusivos num dispositivo Olá
> - Certifique-se de que são suportados os algoritmos de criptografia Olá no seu dispositivo
> - Substitua Olá seguir proprietários do local com os valores reais Olá
>   - Fora do nome de interface: "fora"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - Pre_Shared_Key do IKE
>   - VNet e nomes de gateway de rede local (VNetName, LNGName)
>   - Os prefixos de endereços de rede de VNet e no local
>   - Netmasks adequada

#### <a name="sample-configuration"></a>Configuração de exemplo

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Comandos de depuração simples

Eis alguns comandos do ASA para fins de depuração:

1. Mostrar Olá IPsec e do IKE SA
    - "Mostrar ipsec criptografia sa"
    - "Mostrar crypto ikev2 sa"
2. Modo de depuração entrar - Isto pode obter muito desnecessárias, na consola de Olá
    - "depuração ikev2 criptografia plataforma <level>"
    - "protocolo ikev2 criptografia de depuração <level>"
3. Lista de configurações atuais
    - "Mostrar execução" - mostra Olá configurações atuais num dispositivo Olá; Pode utilizar Olá vários comandos secundárias toolist partes específicas da configuração de Olá. Por exemplo, "Mostrar executar criptografia", "Mostrar executar a lista de acesso", "Mostrar executar o grupo de túnel", etc.


## <a name="next-steps"></a>Passos seguintes
Consulte [configurar Gateways de VPN de ativo-ativo em vários locais e ligações VNet a VNet](vpn-gateway-activeactive-rm-powershell.md) para passos tooconfigure ativo-ativo em vários locais e ligações VNet a VNet.

