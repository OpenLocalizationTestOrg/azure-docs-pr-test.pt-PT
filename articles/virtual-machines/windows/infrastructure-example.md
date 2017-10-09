---
title: "aaaExample instruções de infraestrutura do Azure | Microsoft Docs"
description: "Saiba mais sobre Olá chaves design e implementação diretrizes para implementar uma infraestrutura de exemplo no Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="5836b-103">Instruções de infraestrutura do Azure de exemplo para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="5836b-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="5836b-104">Este artigo explica de conceção de uma infraestrutura de aplicação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5836b-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="5836b-105">Iremos detalhe conceber uma infraestrutura para uma loja online simple que reúne todas as diretrizes de Olá e decisões à volta de convenções de nomenclatura, conjuntos de disponibilidade, redes virtuais e Balanceadores de carga e a implementação, na verdade, as máquinas virtuais (VMs).</span><span class="sxs-lookup"><span data-stu-id="5836b-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="5836b-106">Carga de trabalho de exemplo</span><span class="sxs-lookup"><span data-stu-id="5836b-106">Example workload</span></span>
<span data-ttu-id="5836b-107">Adventure Works Cycles pretende toobuild uma aplicação da loja online no Azure que é composta por:</span><span class="sxs-lookup"><span data-stu-id="5836b-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="5836b-108">Dois servidores IIS que executem cliente Olá front-end numa camada web</span><span class="sxs-lookup"><span data-stu-id="5836b-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="5836b-109">Dois servidores IIS processar dados e as ordens de uma camada de aplicação</span><span class="sxs-lookup"><span data-stu-id="5836b-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="5836b-110">Duas instâncias do Microsoft SQL Server com grupos de Disponibilidade AlwaysOn (dois servidores do SQL Server e um testemunho de nó maioria) para armazenar dados de produto e as ordens numa camada de base de dados</span><span class="sxs-lookup"><span data-stu-id="5836b-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="5836b-111">Dois controladores de domínio do Active Directory para contas de cliente e fornecedores uma camada de autenticação</span><span class="sxs-lookup"><span data-stu-id="5836b-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="5836b-112">Todos os servidores de Olá estão localizados em duas sub-redes:</span><span class="sxs-lookup"><span data-stu-id="5836b-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="5836b-113">uma sub-rede para servidores de web de Olá front-end</span><span class="sxs-lookup"><span data-stu-id="5836b-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="5836b-114">uma sub-rede de back-end para servidores de aplicação Olá, cluster do SQL Server e os controladores de domínio</span><span class="sxs-lookup"><span data-stu-id="5836b-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagrama de diferentes camadas para a infraestrutura de aplicação](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="5836b-116">Entrada segura tráfego web tem de ser com balanceamento de carga entre servidores de web de Olá clientes procurar loja online Olá.</span><span class="sxs-lookup"><span data-stu-id="5836b-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="5836b-117">Ordem de processamento de tráfego num formulário de Olá de pedidos de HTTP da web de Olá servidores devem ser balanceados entre servidores de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5836b-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="5836b-118">Além disso, a infraestrutura de Olá têm de ser concebida para elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5836b-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="5836b-119">design resultante Olá tem de incorporar:</span><span class="sxs-lookup"><span data-stu-id="5836b-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="5836b-120">Uma conta e subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="5836b-120">An Azure subscription and account</span></span>
* <span data-ttu-id="5836b-121">Um grupo de recursos única</span><span class="sxs-lookup"><span data-stu-id="5836b-121">A single resource group</span></span>
* <span data-ttu-id="5836b-122">Managed Disks do Azure</span><span class="sxs-lookup"><span data-stu-id="5836b-122">Azure Managed Disks</span></span>
* <span data-ttu-id="5836b-123">Uma rede virtual com duas sub-redes</span><span class="sxs-lookup"><span data-stu-id="5836b-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="5836b-124">Conjuntos de disponibilidade para Olá VMs com uma função semelhante</span><span class="sxs-lookup"><span data-stu-id="5836b-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="5836b-125">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5836b-125">Virtual machines</span></span>

<span data-ttu-id="5836b-126">Todos os Olá acima siga estas convenções de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="5836b-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="5836b-127">Adventure Works Cycles utiliza **[carga de trabalho IT]-[localização]-[recursos do Azure]** como prefixo</span><span class="sxs-lookup"><span data-stu-id="5836b-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="5836b-128">Neste exemplo, "**azos**" (Azure on-line loja) é Olá nome de carga de trabalho de TI e "**utilizar**" (EUA Leste 2) é a localização de Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="5836b-129">Redes virtuais utilizam AZOS-utilização-VN**[número]**</span><span class="sxs-lookup"><span data-stu-id="5836b-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="5836b-130">Conjuntos de disponibilidade utilizam azos-utilizar-como-**[função]**</span><span class="sxs-lookup"><span data-stu-id="5836b-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="5836b-131">Nomes de máquina virtual utilizar azos-utilizar-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="5836b-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="5836b-132">Contas e as subscrições do Azure</span><span class="sxs-lookup"><span data-stu-id="5836b-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="5836b-133">Adventure Works Cycles está a utilizar a subscrição do Enterprise, com o nome de subscrição no Adventure Works Enterprise, tooprovide faturação para esta carga de trabalho IT.</span><span class="sxs-lookup"><span data-stu-id="5836b-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="5836b-134">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="5836b-134">Storage</span></span>
<span data-ttu-id="5836b-135">Adventure Works Cycles determinar que utilizam discos gerida do Azure.</span><span class="sxs-lookup"><span data-stu-id="5836b-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="5836b-136">Durante a criação de VMs, ambas as camadas de armazenamento disponível armazenamento são utilizadas:</span><span class="sxs-lookup"><span data-stu-id="5836b-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="5836b-137">**Armazenamento Standard** para servidores de web de Olá, servidores de aplicações e controladores de domínio e os respetivos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="5836b-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="5836b-138">**Armazenamento Premium** para Olá VMs do SQL Server e os respetivos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="5836b-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="5836b-139">Rede virtual e sub-redes</span><span class="sxs-lookup"><span data-stu-id="5836b-139">Virtual network and subnets</span></span>
<span data-ttu-id="5836b-140">Porque a rede virtual Olá não precisa de rede no local do conectividade em curso toohello Adventure ciclos de trabalho, estes decidiu numa rede virtual apenas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5836b-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="5836b-141">Estes criaram uma rede virtual apenas na nuvem com Olá definições Olá portal do Azure a utilizar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5836b-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="5836b-142">Nome: AZOS-utilização-VN01</span><span class="sxs-lookup"><span data-stu-id="5836b-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="5836b-143">Localização: EUA Leste 2</span><span class="sxs-lookup"><span data-stu-id="5836b-143">Location: East US 2</span></span>
* <span data-ttu-id="5836b-144">Espaço de endereços de rede virtual: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="5836b-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="5836b-145">Primeira sub-rede:</span><span class="sxs-lookup"><span data-stu-id="5836b-145">First subnet:</span></span>
  * <span data-ttu-id="5836b-146">Nome: front-end</span><span class="sxs-lookup"><span data-stu-id="5836b-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="5836b-147">Espaço de endereços: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="5836b-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="5836b-148">Segunda sub-rede:</span><span class="sxs-lookup"><span data-stu-id="5836b-148">Second subnet:</span></span>
  * <span data-ttu-id="5836b-149">Nome: back-end</span><span class="sxs-lookup"><span data-stu-id="5836b-149">Name: BackEnd</span></span>
  * <span data-ttu-id="5836b-150">Espaço de endereços: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="5836b-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="5836b-151">Conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5836b-151">Availability sets</span></span>
<span data-ttu-id="5836b-152">toomaintain elevada disponibilidade de todos os escalões de quatro da respetiva loja online, Adventure Works Cycles assim sendo, optou em quatro conjuntos de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="5836b-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="5836b-153">**azos utilize como web** para servidores de web de Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="5836b-154">**azos utilize como aplicação** Olá para servidores de aplicações</span><span class="sxs-lookup"><span data-stu-id="5836b-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="5836b-155">**azos utilize como sql** para Olá servidores SQL</span><span class="sxs-lookup"><span data-stu-id="5836b-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="5836b-156">**azos utilize como dc** Olá para controladores de domínio</span><span class="sxs-lookup"><span data-stu-id="5836b-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="5836b-157">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5836b-157">Virtual machines</span></span>
<span data-ttu-id="5836b-158">Adventure Works Cycles decidir Olá os seguintes nomes para as respetivas VMs do Azure:</span><span class="sxs-lookup"><span data-stu-id="5836b-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="5836b-159">**azos-utilização-vm-web01** para o primeiro servidor de web Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="5836b-160">**azos-utilização-vm-web02** para o segundo servidor de web Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="5836b-161">**azos-utilização-vm-app01** para o primeiro servidor de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="5836b-162">**azos-utilização-vm-app02** para o segundo servidor de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="5836b-163">**azos-utilização-vm-sql01** para o servidor do SQL Server primeiro Olá num cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="5836b-164">**azos-utilização-vm-sql02** para o servidor do SQL Server segundo Olá num cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="5836b-165">**azos-utilização-vm-dc01** Olá primeiro controlador de domínio</span><span class="sxs-lookup"><span data-stu-id="5836b-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="5836b-166">**azos-utilização-vm-dc02** Olá segundo controlador de domínio</span><span class="sxs-lookup"><span data-stu-id="5836b-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="5836b-167">Segue-se a configuração resultante Olá.</span><span class="sxs-lookup"><span data-stu-id="5836b-167">Here is hello resulting configuration.</span></span>

![Infraestrutura de aplicação final implementada no Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="5836b-169">Incorpora esta configuração:</span><span class="sxs-lookup"><span data-stu-id="5836b-169">This configuration incorporates:</span></span>

* <span data-ttu-id="5836b-170">Uma rede virtual apenas na nuvem com duas sub-redes (front-end e back-end)</span><span class="sxs-lookup"><span data-stu-id="5836b-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="5836b-171">Discos do Azure gerida com discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="5836b-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="5836b-172">Quatro conjuntos de disponibilidade, um para cada camada do loja online Olá</span><span class="sxs-lookup"><span data-stu-id="5836b-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="5836b-173">máquinas virtuais Olá de camadas de Olá quatro</span><span class="sxs-lookup"><span data-stu-id="5836b-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="5836b-174">Um conjunto com balanceamento de carga externo para o tráfego de web baseado em HTTPS de servidores web do Olá Internet toohello</span><span class="sxs-lookup"><span data-stu-id="5836b-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="5836b-175">Conjunto para o tráfego de web não encriptada de servidores de aplicações de toohello de servidores web Olá com balanceamento de uma carga interno</span><span class="sxs-lookup"><span data-stu-id="5836b-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="5836b-176">Um grupo de recursos única</span><span class="sxs-lookup"><span data-stu-id="5836b-176">A single resource group</span></span>