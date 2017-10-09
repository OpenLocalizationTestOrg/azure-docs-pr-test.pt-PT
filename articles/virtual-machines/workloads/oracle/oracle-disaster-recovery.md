---
title: "aaaOverview de um cenário de recuperação de desastre Oracle no seu ambiente do Azure | Microsoft Docs"
description: "Um cenário de recuperação de desastres para uma base de dados de 12c de base de dados Oracle no seu ambiente do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Recuperação após desastre para uma base de dados de 12c de base de dados Oracle num ambiente do Azure

## <a name="assumptions"></a>Pressupostos

- Ter uma compreensão dos ambientes do Azure e de design de Oracle Data Guard.


## <a name="goals"></a>Objetivos
- Conceber a topologia de Olá e a configuração que satisfazem os requisitos de (DR) de recuperação após desastre.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Cenário 1: Primário e de DR sites do Azure

Um cliente tiver um Oracle da base de dados conjunto de cópias de segurança no site primário Olá. Site de A DR está numa região diferente. cliente de Olá utiliza Oracle Data Guard para recuperação rápida entre estes sites. site primário Olá também tem uma base de dados secundária para relatórios e outras utilizações. 

### <a name="topology"></a>Topologia

Eis um resumo das Olá a configuração do Azure:

- Dois sites (um site primário e um site de DR)
- Duas redes virtuais
- Duas bases de dados Oracle com a proteção de dados (servidor primário e o modo de espera)
- Duas bases de dados Oracle com Golden porta ou proteção de dados (apenas no site primário)
- Dois serviços de aplicação, um site primário e um no site de Olá DR
- Um *conjunto de disponibilidade,* que é utilizada para o serviço de base de dados e aplicações num site primário Olá
- Um jumpbox em cada site, que restringe a rede privada do acesso toohello e só permite início de sessão por um administrador
- Um jumpbox, o serviço de aplicações, a base de dados e o gateway VPN nas sub-redes separadas
- NSG imposto na aplicação e sub-redes de base de dados

![Captura de ecrã da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Cenário 2: Site primário no local e o site de DR no Azure

Um cliente tiver uma configuração de base de dados Oracle no local (site primário). Site de DR uma está no Azure. Oracle Data Guard é utilizado para recuperação rápida entre estes sites. site primário Olá também tem uma base de dados secundária para relatórios e outras utilizações. 

Existem duas abordagens para esta configuração.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Abordagem 1: Ligações diretas entre no local e o Azure, a necessidade de portas TCP abertas na firewall de Olá 

Não recomendamos ligações diretas porque estes expõem toohello de portas TCP Olá fora do mundo.

#### <a name="topology"></a>Topologia

Segue-se um resumo das Olá a configuração do Azure:

- Site de DR um 
- Uma rede virtual
- Uma base de dados Oracle com a proteção de dados (Active Directory)
- Serviço de uma aplicação no site de Olá DR
- Um jumpbox, que restringe a rede privada do acesso toohello e só permite início de sessão por um administrador
- Um jumpbox, o serviço de aplicações, a base de dados e o gateway VPN nas sub-redes separadas
- NSG imposto na aplicação e sub-redes de base de dados
- Entrada de tooallow de regra de política/um NSG a porta TCP 1521 (ou uma porta definida pelo utilizador)
- Uma NSG/regra de política toorestrict apenas Olá IP endereço/endereços no local (DB ou aplicação) tooaccess Olá rede virtual

![Captura de ecrã da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Abordagem 2: VPN de Site para site
VPN de site a site é uma abordagem de melhor. Para obter mais informações sobre como configurar uma VPN, consulte [criar uma rede virtual com uma ligação de VPN de Site para Site com a CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Topologia

Segue-se um resumo das Olá a configuração do Azure:

- Site de DR um 
- Uma rede virtual 
- Uma base de dados Oracle com a proteção de dados (Active Directory)
- Serviço de uma aplicação no site de Olá DR
- Um jumpbox, que restringe a rede privada do acesso toohello e só permite início de sessão por um administrador
- Um jumpbox, o serviço de aplicações, a base de dados e o gateway de VPN são em sub-redes separadas
- NSG imposto na aplicação e sub-redes de base de dados
- Ligação de VPN de site a site entre no local e o Azure

![Captura de ecrã da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Leitura adicional

- [Conceber e implementar uma base de dados Oracle no Azure](oracle-design.md)
- [Configurar a proteção de dados Oracle](configure-oracle-dataguard.md)
- [Configurar a porta de Golden Oracle](configure-oracle-golden-gate.md)
- [Cópia de segurança do Oracle e recuperação](oracle-backup-recovery.md)


## <a name="next-steps"></a>Passos seguintes

- [Tutorial: Criar as VMs de elevada disponibilidade](../../linux/create-cli-complete.md)
- [Explorar amostras de CLI do Azure de implementação de VM](../../linux/cli-samples.md)
