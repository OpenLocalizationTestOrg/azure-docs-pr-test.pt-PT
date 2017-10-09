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
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="c04e7-103">Recuperação após desastre para uma base de dados de 12c de base de dados Oracle num ambiente do Azure</span><span class="sxs-lookup"><span data-stu-id="c04e7-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="c04e7-104">Pressupostos</span><span class="sxs-lookup"><span data-stu-id="c04e7-104">Assumptions</span></span>

- <span data-ttu-id="c04e7-105">Ter uma compreensão dos ambientes do Azure e de design de Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="c04e7-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="c04e7-106">Objetivos</span><span class="sxs-lookup"><span data-stu-id="c04e7-106">Goals</span></span>
- <span data-ttu-id="c04e7-107">Conceber a topologia de Olá e a configuração que satisfazem os requisitos de (DR) de recuperação após desastre.</span><span class="sxs-lookup"><span data-stu-id="c04e7-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="c04e7-108">Cenário 1: Primário e de DR sites do Azure</span><span class="sxs-lookup"><span data-stu-id="c04e7-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="c04e7-109">Um cliente tiver um Oracle da base de dados conjunto de cópias de segurança no site primário Olá.</span><span class="sxs-lookup"><span data-stu-id="c04e7-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="c04e7-110">Site de A DR está numa região diferente.</span><span class="sxs-lookup"><span data-stu-id="c04e7-110">A DR site is in a different region.</span></span> <span data-ttu-id="c04e7-111">cliente de Olá utiliza Oracle Data Guard para recuperação rápida entre estes sites.</span><span class="sxs-lookup"><span data-stu-id="c04e7-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="c04e7-112">site primário Olá também tem uma base de dados secundária para relatórios e outras utilizações.</span><span class="sxs-lookup"><span data-stu-id="c04e7-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="c04e7-113">Topologia</span><span class="sxs-lookup"><span data-stu-id="c04e7-113">Topology</span></span>

<span data-ttu-id="c04e7-114">Eis um resumo das Olá a configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="c04e7-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="c04e7-115">Dois sites (um site primário e um site de DR)</span><span class="sxs-lookup"><span data-stu-id="c04e7-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="c04e7-116">Duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="c04e7-116">Two virtual networks</span></span>
- <span data-ttu-id="c04e7-117">Duas bases de dados Oracle com a proteção de dados (servidor primário e o modo de espera)</span><span class="sxs-lookup"><span data-stu-id="c04e7-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="c04e7-118">Duas bases de dados Oracle com Golden porta ou proteção de dados (apenas no site primário)</span><span class="sxs-lookup"><span data-stu-id="c04e7-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="c04e7-119">Dois serviços de aplicação, um site primário e um no site de Olá DR</span><span class="sxs-lookup"><span data-stu-id="c04e7-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="c04e7-120">Um *conjunto de disponibilidade,* que é utilizada para o serviço de base de dados e aplicações num site primário Olá</span><span class="sxs-lookup"><span data-stu-id="c04e7-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="c04e7-121">Um jumpbox em cada site, que restringe a rede privada do acesso toohello e só permite início de sessão por um administrador</span><span class="sxs-lookup"><span data-stu-id="c04e7-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="c04e7-122">Um jumpbox, o serviço de aplicações, a base de dados e o gateway VPN nas sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="c04e7-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="c04e7-123">NSG imposto na aplicação e sub-redes de base de dados</span><span class="sxs-lookup"><span data-stu-id="c04e7-123">NSG enforced on application and database subnets</span></span>

![Captura de ecrã da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="c04e7-125">Cenário 2: Site primário no local e o site de DR no Azure</span><span class="sxs-lookup"><span data-stu-id="c04e7-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="c04e7-126">Um cliente tiver uma configuração de base de dados Oracle no local (site primário).</span><span class="sxs-lookup"><span data-stu-id="c04e7-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="c04e7-127">Site de DR uma está no Azure.</span><span class="sxs-lookup"><span data-stu-id="c04e7-127">A DR site is on Azure.</span></span> <span data-ttu-id="c04e7-128">Oracle Data Guard é utilizado para recuperação rápida entre estes sites.</span><span class="sxs-lookup"><span data-stu-id="c04e7-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="c04e7-129">site primário Olá também tem uma base de dados secundária para relatórios e outras utilizações.</span><span class="sxs-lookup"><span data-stu-id="c04e7-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="c04e7-130">Existem duas abordagens para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="c04e7-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="c04e7-131">Abordagem 1: Ligações diretas entre no local e o Azure, a necessidade de portas TCP abertas na firewall de Olá</span><span class="sxs-lookup"><span data-stu-id="c04e7-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="c04e7-132">Não recomendamos ligações diretas porque estes expõem toohello de portas TCP Olá fora do mundo.</span><span class="sxs-lookup"><span data-stu-id="c04e7-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="c04e7-133">Topologia</span><span class="sxs-lookup"><span data-stu-id="c04e7-133">Topology</span></span>

<span data-ttu-id="c04e7-134">Segue-se um resumo das Olá a configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="c04e7-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="c04e7-135">Site de DR um</span><span class="sxs-lookup"><span data-stu-id="c04e7-135">One DR site</span></span> 
- <span data-ttu-id="c04e7-136">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="c04e7-136">One virtual network</span></span>
- <span data-ttu-id="c04e7-137">Uma base de dados Oracle com a proteção de dados (Active Directory)</span><span class="sxs-lookup"><span data-stu-id="c04e7-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="c04e7-138">Serviço de uma aplicação no site de Olá DR</span><span class="sxs-lookup"><span data-stu-id="c04e7-138">One application service on hello DR site</span></span>
- <span data-ttu-id="c04e7-139">Um jumpbox, que restringe a rede privada do acesso toohello e só permite início de sessão por um administrador</span><span class="sxs-lookup"><span data-stu-id="c04e7-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="c04e7-140">Um jumpbox, o serviço de aplicações, a base de dados e o gateway VPN nas sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="c04e7-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="c04e7-141">NSG imposto na aplicação e sub-redes de base de dados</span><span class="sxs-lookup"><span data-stu-id="c04e7-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="c04e7-142">Entrada de tooallow de regra de política/um NSG a porta TCP 1521 (ou uma porta definida pelo utilizador)</span><span class="sxs-lookup"><span data-stu-id="c04e7-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="c04e7-143">Uma NSG/regra de política toorestrict apenas Olá IP endereço/endereços no local (DB ou aplicação) tooaccess Olá rede virtual</span><span class="sxs-lookup"><span data-stu-id="c04e7-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Captura de ecrã da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="c04e7-145">Abordagem 2: VPN de Site para site</span><span class="sxs-lookup"><span data-stu-id="c04e7-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="c04e7-146">VPN de site a site é uma abordagem de melhor.</span><span class="sxs-lookup"><span data-stu-id="c04e7-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="c04e7-147">Para obter mais informações sobre como configurar uma VPN, consulte [criar uma rede virtual com uma ligação de VPN de Site para Site com a CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="c04e7-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="c04e7-148">Topologia</span><span class="sxs-lookup"><span data-stu-id="c04e7-148">Topology</span></span>

<span data-ttu-id="c04e7-149">Segue-se um resumo das Olá a configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="c04e7-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="c04e7-150">Site de DR um</span><span class="sxs-lookup"><span data-stu-id="c04e7-150">One DR site</span></span> 
- <span data-ttu-id="c04e7-151">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="c04e7-151">One virtual network</span></span> 
- <span data-ttu-id="c04e7-152">Uma base de dados Oracle com a proteção de dados (Active Directory)</span><span class="sxs-lookup"><span data-stu-id="c04e7-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="c04e7-153">Serviço de uma aplicação no site de Olá DR</span><span class="sxs-lookup"><span data-stu-id="c04e7-153">One application service on hello DR site</span></span>
- <span data-ttu-id="c04e7-154">Um jumpbox, que restringe a rede privada do acesso toohello e só permite início de sessão por um administrador</span><span class="sxs-lookup"><span data-stu-id="c04e7-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="c04e7-155">Um jumpbox, o serviço de aplicações, a base de dados e o gateway de VPN são em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="c04e7-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="c04e7-156">NSG imposto na aplicação e sub-redes de base de dados</span><span class="sxs-lookup"><span data-stu-id="c04e7-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="c04e7-157">Ligação de VPN de site a site entre no local e o Azure</span><span class="sxs-lookup"><span data-stu-id="c04e7-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Captura de ecrã da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="c04e7-159">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="c04e7-159">Additional reading</span></span>

- [<span data-ttu-id="c04e7-160">Conceber e implementar uma base de dados Oracle no Azure</span><span class="sxs-lookup"><span data-stu-id="c04e7-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="c04e7-161">Configurar a proteção de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="c04e7-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="c04e7-162">Configurar a porta de Golden Oracle</span><span class="sxs-lookup"><span data-stu-id="c04e7-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="c04e7-163">Cópia de segurança do Oracle e recuperação</span><span class="sxs-lookup"><span data-stu-id="c04e7-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="c04e7-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c04e7-164">Next steps</span></span>

- [<span data-ttu-id="c04e7-165">Tutorial: Criar as VMs de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04e7-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="c04e7-166">Explorar amostras de CLI do Azure de implementação de VM</span><span class="sxs-lookup"><span data-stu-id="c04e7-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
