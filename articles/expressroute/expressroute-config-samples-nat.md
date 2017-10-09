---
title: "Exemplos de configuração de router de cliente aaaExpressRoute | Microsoft Docs"
description: "Esta página fornece exemplos de configuração de router para os routers Cisco e Juniper."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a>Configuração de router amostras tooset configurar e gerir o NAT
Esta página fornece exemplos de configuração de NAT para ASA da Cisco e Juniper SRX routers da série. Estes exemplos toobe pretendido para obter orientações sobre apenas e não pode ser utilizados tal como está. Pode trabalhar com o toocome fornecedor cópias de segurança com configurações adequadas para a sua rede. 

> [!IMPORTANT]
> Os exemplos nesta página são toobe pretendido puramente para obter orientações. Tem de trabalhar com a equipa de vendas / técnica do fornecedor e o toocome equipa rede cópias de segurança com toomeet configurações adequado às suas necessidades. Microsoft não irá suportar problemas relacionados com tooconfigurations listado nesta página. Tem de contactar o fornecedor do dispositivo para problemas de suporte.
> 
> 

* Exemplos de configuração de router abaixo aplicam-se tooAzure público e Microsoft peerings. Não é necessário configurar NAT para peering privado do Azure. Reveja [ExpressRoute peerings](expressroute-circuit-peerings.md) e [requisitos do NAT do ExpressRoute](expressroute-nat.md) para obter mais detalhes.

* TEM de utilizar separado conjuntos IP do NAT para toohello conectividade à internet e ExpressRoute. Utilizar Olá mesmo IP do NAT agrupamento em Olá internet e ExpressRoute irá resultar no encaminhamento assimétrico e a perda de conectividade.


## <a name="cisco-asa-firewalls"></a>Firewalls do Cisco ASA
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a>Configuração de TERESA para tráfego de tooMicrosoft de rede do cliente
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a>Configuração de TERESA para tráfego de rede da Microsoft toocustomer

**Interfaces e direção:**

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

**Configuração:**

Conjunto NAT:

    object network outbound-PAT
        host <NAT-IP>

Servidor de destino:

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

Objeto de grupo para endereços IP do cliente

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

Comandos NAT:

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a>Routers de série do Juniper SRX
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a>1. Criar redundantes Ethernet interfaces para cluster Olá
    interfaces {
        reth0 {
            description "tooInternal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a>2. Criar duas zonas de segurança
* Zona de confiança para a rede interna e zona de Untrust externas com acesso Routers de limite de rede
* Atribuir interfaces adequadas toohello zonas
* Permitir que os serviços em interfaces de Olá

    segurança {zonas {confiança de zona de segurança {anfitriões de entrada-tráfego {-serviços do sistema {ping;                   } protocolos {bgp;                   interfaces de}} {reth0.100;               }} Untrust de zona de segurança {anfitriões de entrada-tráfego {-serviços do sistema {ping;                   } protocolos {bgp;                   interfaces de}} {reth1.100;               }           }       }   }


### <a name="3-create-security-policies-between-zones"></a>3. Criar políticas de segurança entre zonas
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a>4. Configurar políticas NAT
* Crie dois conjuntos de NAT. Um será tooMicrosoft saída do tráfego utilizado tooNAT e outros do cliente de toohello da Microsoft.
* Criar regras de tráfego de respetivos tooNAT Olá
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       toorouting-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       toorouting-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a>5. Configurar prefixos seletivos do BGP tooadvertise em cada direção
Consulte toosamples no [amostras de configuração de encaminhamento ](expressroute-config-samples-routing.md) página.

### <a name="6-create-policies"></a>6. Criar políticas
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a>Passos seguintes
Consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md) para obter mais detalhes.

