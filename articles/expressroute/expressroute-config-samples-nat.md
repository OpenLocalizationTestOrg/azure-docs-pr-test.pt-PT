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
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="652cc-103">Configuração de router amostras tooset configurar e gerir o NAT</span><span class="sxs-lookup"><span data-stu-id="652cc-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="652cc-104">Esta página fornece exemplos de configuração de NAT para ASA da Cisco e Juniper SRX routers da série.</span><span class="sxs-lookup"><span data-stu-id="652cc-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="652cc-105">Estes exemplos toobe pretendido para obter orientações sobre apenas e não pode ser utilizados tal como está.</span><span class="sxs-lookup"><span data-stu-id="652cc-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="652cc-106">Pode trabalhar com o toocome fornecedor cópias de segurança com configurações adequadas para a sua rede.</span><span class="sxs-lookup"><span data-stu-id="652cc-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="652cc-107">Os exemplos nesta página são toobe pretendido puramente para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="652cc-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="652cc-108">Tem de trabalhar com a equipa de vendas / técnica do fornecedor e o toocome equipa rede cópias de segurança com toomeet configurações adequado às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="652cc-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="652cc-109">Microsoft não irá suportar problemas relacionados com tooconfigurations listado nesta página.</span><span class="sxs-lookup"><span data-stu-id="652cc-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="652cc-110">Tem de contactar o fornecedor do dispositivo para problemas de suporte.</span><span class="sxs-lookup"><span data-stu-id="652cc-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="652cc-111">Exemplos de configuração de router abaixo aplicam-se tooAzure público e Microsoft peerings.</span><span class="sxs-lookup"><span data-stu-id="652cc-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="652cc-112">Não é necessário configurar NAT para peering privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="652cc-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="652cc-113">Reveja [ExpressRoute peerings](expressroute-circuit-peerings.md) e [requisitos do NAT do ExpressRoute](expressroute-nat.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="652cc-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="652cc-114">TEM de utilizar separado conjuntos IP do NAT para toohello conectividade à internet e ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="652cc-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="652cc-115">Utilizar Olá mesmo IP do NAT agrupamento em Olá internet e ExpressRoute irá resultar no encaminhamento assimétrico e a perda de conectividade.</span><span class="sxs-lookup"><span data-stu-id="652cc-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="652cc-116">Firewalls do Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="652cc-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="652cc-117">Configuração de TERESA para tráfego de tooMicrosoft de rede do cliente</span><span class="sxs-lookup"><span data-stu-id="652cc-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="652cc-118">Configuração de TERESA para tráfego de rede da Microsoft toocustomer</span><span class="sxs-lookup"><span data-stu-id="652cc-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="652cc-119">**Interfaces e direção:**</span><span class="sxs-lookup"><span data-stu-id="652cc-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="652cc-120">**Configuração:**</span><span class="sxs-lookup"><span data-stu-id="652cc-120">**Configuration:**</span></span>

<span data-ttu-id="652cc-121">Conjunto NAT:</span><span class="sxs-lookup"><span data-stu-id="652cc-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="652cc-122">Servidor de destino:</span><span class="sxs-lookup"><span data-stu-id="652cc-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="652cc-123">Objeto de grupo para endereços IP do cliente</span><span class="sxs-lookup"><span data-stu-id="652cc-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="652cc-124">Comandos NAT:</span><span class="sxs-lookup"><span data-stu-id="652cc-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="652cc-125">Routers de série do Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="652cc-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="652cc-126">1. Criar redundantes Ethernet interfaces para cluster Olá</span><span class="sxs-lookup"><span data-stu-id="652cc-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
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


### <a name="2-create-two-security-zones"></a><span data-ttu-id="652cc-127">2. Criar duas zonas de segurança</span><span class="sxs-lookup"><span data-stu-id="652cc-127">2. Create two security zones</span></span>
* <span data-ttu-id="652cc-128">Zona de confiança para a rede interna e zona de Untrust externas com acesso Routers de limite de rede</span><span class="sxs-lookup"><span data-stu-id="652cc-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="652cc-129">Atribuir interfaces adequadas toohello zonas</span><span class="sxs-lookup"><span data-stu-id="652cc-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="652cc-130">Permitir que os serviços em interfaces de Olá</span><span class="sxs-lookup"><span data-stu-id="652cc-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="652cc-131">segurança {zonas {confiança de zona de segurança {anfitriões de entrada-tráfego {-serviços do sistema {ping;                   } protocolos {bgp;                   interfaces de}} {reth0.100;               }} Untrust de zona de segurança {anfitriões de entrada-tráfego {-serviços do sistema {ping;                   } protocolos {bgp;                   interfaces de}} {reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="652cc-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="652cc-132">3. Criar políticas de segurança entre zonas</span><span class="sxs-lookup"><span data-stu-id="652cc-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="652cc-133">4. Configurar políticas NAT</span><span class="sxs-lookup"><span data-stu-id="652cc-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="652cc-134">Crie dois conjuntos de NAT.</span><span class="sxs-lookup"><span data-stu-id="652cc-134">Create two NAT pools.</span></span> <span data-ttu-id="652cc-135">Um será tooMicrosoft saída do tráfego utilizado tooNAT e outros do cliente de toohello da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="652cc-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="652cc-136">Criar regras de tráfego de respetivos tooNAT Olá</span><span class="sxs-lookup"><span data-stu-id="652cc-136">Create rules tooNAT hello respective traffic</span></span>
  
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="652cc-137">5. Configurar prefixos seletivos do BGP tooadvertise em cada direção</span><span class="sxs-lookup"><span data-stu-id="652cc-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="652cc-138">Consulte toosamples no [amostras de configuração de encaminhamento ](expressroute-config-samples-routing.md) página.</span><span class="sxs-lookup"><span data-stu-id="652cc-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="652cc-139">6. Criar políticas</span><span class="sxs-lookup"><span data-stu-id="652cc-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="652cc-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="652cc-140">Next steps</span></span>
<span data-ttu-id="652cc-141">Consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="652cc-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

